# Hierarchical Consensus Pseudo-Code

Goal: we need to express the complicated bits of our paper with pseudo-code. This document is a preliminary to the LaTeX writeup, expressing the pseudo- code in plain english as a draft.

Includes codes for:

- root consensus and delegation
- the nuclear option and delegation safety
- worst case scenario: assassination
- epoch changes
- fuzzy epochs, showing handshakes

Still to do/explore:

- Raft version showing changes we've made: leases?
- Anti-entropy: helps with durability, assists with handshakes

> Failure is handled from the bottom up, we attempt to handle it as low as possible.

## Definitions

**epoch**: a monotonically increasing logical time element that defines subquorums and their assigned tags. We've further optimized the root quorum to also consider the epoch as the term of the root leader (**PJK: this implies we need to elect a new leader for every command!**). The epoch is equivalent to a _configuration_ in VP.

**command**: In Vertical Paxos (VP) a command is identified by three dimensions: the configuration id, the the ballot number, and the log index. In HC, a command is identified by: epoch, subquorum term, and log index.

## Root Consensus and Delegation

At the root leader:

1. Root quorum broadcasts proposed command to all replicas (we also have a "thrifty" mode where we only send messages to replicas who voted last time, usually subquorum leaders, timeout causes a full broadcast).
2. Root quorum receives votes from replicas as (e, q, t, v)
    e = the epoch number
    q = the subquorum id
    t = the subquorum term
    v = the number of yes votes (1 for self, >1 is delegations)
3. If there is a (q,t) conflict - e.g. the root receives two batches of delegated votes from the same subquorum, it resolves the number of votes by selecting the delegation with the highest subquorum term in case a failure in the subquorum caused a new leader election. (**PJK: What happens when these two distinct SQ leaders send delegated votes to distinct candidates of a RQ election? If the SQ leader failed before telling it's people what it was about to do, new SQ leader (of same SQ) doesn't know that the vote has happened. The two RQ leaders are unaware of each other, and the one contested SQ might be enough to tilt the election one way or another. I don't know a straightforward way of fixing this other than requiring candidates to use undelegated votes only, i.e. it's a nuclear timeout w/o waiting for the nuclear timeout**)(**PJK: example: 3 SQ of three each. Root election in progress w/ two candidates. SQ 1 votes for candidate A, SQ 2 votes for B. SQ 3 votes for A, fails, and then votes for B.**)
4. If sum(v) > n/2+1 where n is the number of replicas, the command is committed. The root quorum broadcasts the commit to all replicas (**PJK: thrifty**).

At root followers:

- if epoch of command < current epoch: send no votes; report current root leader
- if hot spare: send one vote
- if vote delegated for this epoch: dismiss message
- if candidate in subquorum: send one vote with current term (this may be wrong: here we're trying to handle failures of a leader in the subquorum)
- if has votes, either self or delegated to: send delegated votes

### The Nuclear Option

Delegations are only valid for the given epoch. If enough replicas with delegated votes have failed such that the root quorum cannot make progress, then the nuclear option is required to reset delegations and establish a new, stable root quorum.

The nuclear option is triggered by the nuclear timeout. This timeout is reset either when a heartbeat is received from the leader, but is much longer than the timeout for the root leader election. This must mean two things:

1. That the root leader has failed AND
2. That a new root leader cannot be elected from the subquorum leaders

The nuclear options starts by incrementing the epoch by the vote delegation limit, this cancels all current delegations because all delegations will be in the epoch before and therefore ignored. An election takes place then that involves all replicas including hot spares. Once the new root leader is established the following synchronizations must occur:

- perform a new epoch change with all online replicas (those that voted in the root election)
- update the health of all failed nodes who are not participating
- perform a safety check to ensure that all subquorums have moved into the new epoch correctly.

**NOTE**: The "safety check" is currently a hacked together experimental evaluation that tests to see if the logs are correct. I was thinking that perhaps we could implement something more formal but haven't fully thought it out.

### Delegation Safety

We have implemented two mechanisms for delegation safety: the first is timeout based, and the second is a simple book-keeping mechanism.

In the timeout-based delegation, a replica delegates it's vote for a term limited logical period, usually at least two epochs. This means that the delegated vote lasts through at most 1 root leader election. The nuclear timeout option is longer than the root election timeout, therefore in order for the nuclear option to occur at least one failed root leader election also must have occurred. Because the nuclear option is triggered after a root leader election the delegation is reset on the nuclear option, and every replica must vote for themselves (ensuring that the nuclear option contains no delegations at all).

See the assassination scenario for the worst case scenario for this.

(**PJK: Again, I think this fails if delegation can be used for root votes.**) In the book-keeping mechanism, replicas can delegate their votes to anyone. All root votes must be accompanied by the term, epoch, and ID of the delegation. The root leader tracks votes as follows:

- If the delegated vote is not in the current epoch, it is discarded
- Otherwise the leader accepts only the vote with the highest term (e.g. the
  current subquorum leader).
- If the leader receives a vote from the replica, then it accepts that vote
  no matter what.

In this way, it is possible for duplicate votes to be received by the leader, but only a single vote per replica will be counted.

### Assassination

Scenario:

System size of 18, HC 5x3 (5 subquourms of size three, 3 hot spares) in 3 regions - 6 replicas per region. In epoch e there is a configuration such that all 5 subquorum leaders and the root leader are in a single region, which loses it's connectivity to the rest of the world. All followers have delegated their votes to their subquorum leaders, except the hot spares which haven't delegated to anyone.

Just a note here, we've been calling it "assassination" but it's actually very difficult to create a scenario where this occurs if replicas are evenly distributed over all regions without violating the principle of localization. In the above example, every single subquourm is geo-replicated.

6 replicas with 16 votes can communicate and 12 replicas with 2 votes cannot.

Step one: all subquorums elect a leader for the next term; they continue to handle requests.

Step two: group of 6 attempts an epoch change to repair the poor progress, they assign all work to two subquorums of 3 (best scenario if there is total failure).

Step three: group of 12 attempts a root leader election, it fails because they only have 2 votes.

Step four: group of 12 initiates nuclear option, taking back delegations, moves into an epoch after the group of 6.

We now have the scenario where we have concurrent writes to objects in two partitioned regions, however because of the epoch ordering, we know that all writes that happen in the group of 6 happen before the writes that happen in the group of 12.

The group of 6 cannot make another epoch change because their delegations have expired and they cannot re-acquire them.

## Epoch Changes

Epoch changes are initiated by:

- request from subquorum leader or client
- reconfiguration (joining replicas or terminating failed replicas)
- localization of objects (via heuristics)
- quiescence procedures

In any of these cases an epoch change request is sent to the root leader;
normal RPC rules apply for timeouts, detecting leader failure, retries, etc.

On receipt of an epoch change request the _root leader_:

1. Creates an epoch-change command by monotonically increasing the epoch
   number, defining the subquorum configuration, and assigning initial
   leaders.
2. Initiates root quorum consensus on the epoch-change command
3. On commit: announce epoch change (broadcast commit)

On receipt of epoch change commit at _root followers_:

1. Write a tombstone into the current log.
2. Accept any commands whose index < less than tombstone and meets consensus
   rules (validating term, commit, etc.)
3. Once log is entirely committed, truncate and archive log
4. Join new subquorum configuration

**NOTE**: root followers means any system replica that is involved in the epoch change. In practice, this is all system replicas, but the only replicas that do anything special are the designated subquorum leaders for the next epoch and the subquorum leaders for the previous epoch who are engaging in the handoff.

On receipt of epoch change commit at _e-1 leaders_:

1. Begin handshake procedure
2. Finalize consensus and commits for any outstanding commands
3. Report epoch concluded to root leader and e leader
4. Forward any new requests to the epoch e leader

On receipt of epoch change commit at _e leaders_:

1. Send immediate heartbeats to followers to assert leadership
   (initialize consensus)
2. Buffer incoming requests in new epoch
3. On handshake-complete begin consensus

## Handshake Procedure

- **Initiating replica**: leader of subquorum in e-1
- **Remote replica**: leader of subquorum in e

1. Initiating replica sends last committed command for every object required
   by the new leader (may be sending to multiple leaders). If the object does
   not have a log entry, sends a null command for it. The initiating replica
   also reports the number of outstanding entries per object.
2. Remote replica appends the last entries in the log and performs batch     
   consensus with followers so that they're at the same state
3. Once the remote replica has committed all entries, it reports complete and
   begins consensus on new accesses.

Note: background anti-entropy is supposed to make this easier, potentially by replicating large amounts of data and only allowing the commands to be committed.

### Failure during Handshakes

The possible failure scenarios during handshake are:

1. The subquorums are partitioned and cannot communicate at all.
2. The initiating replica fails
3. The remote replica fails

Case #1 is the reason for fuzzy epochs -- inability for two subqourums to resolve the handshake should only result in an outage for the specified keys, not the entire system. Another epoch change by the root leader can break a deadlock when the handshake does not repair within a reasonable amount of time.

In both cases #2 and #3, the subquorum will re-elect a new leader. In case #2, the newly elected leader will retry the handshake with the remote leader. Because of the tombstone commit, it is guaranteed to be a duplicate request to the remote, therefore the remote can simply respond with the status of the handshake to allow the initiating subquorum to dissolve.

If the remote replica fails, one of two scenarios can occur:

1. The new remote leader commits a command received by append entries but
   without a commit message.
2. The new leader receives a retry request from the initiating replica and
   attempts to commit the handshake.

Again, because of the tombstone command, it is not possible to truncate the handshake command because no new commands are permitted until the handshake has been committed.
