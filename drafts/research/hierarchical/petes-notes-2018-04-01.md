
# Big things

1. Base protocol (w/o delegations) to be described first. (I know this is the opposite of what I've been saying)
3. Base protocol description and correctness should cast in terms of individual sq guarantees together with handshakes.
2. Delegations do not apply to leader elections (for simplicity)

## Issues

- Handshakes still necessary for non-delegation case, as network means old tag owners might not know of new RQ
- Delegations mean that old RQ might be changing tag mapping even though new epoch (new leader already elected).
  - This is okay, but we need to specify the procedure for the new RQ
    finding out the last tagset that the old RQ defined, so that the
    handshake for a given tag between the new and old RQ is between
    the correct sets.
