Benjamin,

Thanks again for you submission to the ACS-15 Goal Reasoning workshop, titled Interactive Knowledge-Goal Reasoning. I'm pleased to notify you that it is accepted. (In fact, the majority of the reviewers concurred that all the submissions are relevant to the workshop's topic; all 14 have been accepted.) Decisions for oral vs. poster presentation will soon be announced.

Please see the attached reviews, and in particular suggestions for modifying/improving the submission. Please revise your submission accordingly and upload a final camera-ready version by Sunday, May 24. This will leave only a few days before we meet in Atlanta on Thursday, May 28, so please upload your final version on time.

We plan to make the camera-ready versions of the papers available from the workshop's web site (www.cc.gatech.edu/~svattam/goal-reasoning) and publish the workshop proceedings as a Georgia Tech technical report. First authors: Please notify me whether we have your permission to do this.

I plan to provide a draft agenda by Monday night (18 May). Questions welcome at any time.

Thanks again,
David Aha (GR Workshop Chair)


## REVIEW 1

- PAPER: 6
- TITLE: Interactive Knowledge-Goal Reasoning
- AUTHORS: Benjamin Bengfort and Michael T. Cox

- OVERALL EVALUATION: 2 (accept)
- REVIEWER'S CONFIDENCE: 4 (high)
- Relevance (to goal reasoning): 3 (High)
- Novelty: 2 (Medium)
- Maturity Level: 1 (Early work (e.g., no implementation))
- Recommendation (if accepted): 2 (Either)

### REVIEW

This paper is fairly careful to qualify the work as more of a proposal than a report on finished work, and that's fine.  As such, it wouldn't be fair to expect a whole lot more detail, but there are a few places where it wouldn't hurt.

So the basic idea is that complex knowledge goals can involve an arbitrary amount of inferential chaining and rather than automate the entire process, an interactive environment offloads some of the control problem to the human who can pursue the investigation by asking natural language questions to drive problem decomposition, and provide a goal trajectory which can be retained as cases and reused in the future.

The notion of knowledge goals and "solving" a knowledge goal are not defined in a terribly clear manner.  Is there a difference between a knowledge goal and a knowledge acquisition goal?  Are they always purely inferential problems or can they be experimentally addressed?  The concept/task/context representation would seem to be insufficient to handle knowledge goals pertaining to a more general notion of knowledge - e.g., bounding ignorance by extending the scope of knowledge about a concept, increasing the precision of a measurement or property, or reducing uncertainty or ambiguity.  This doesn't mean that the proposed system must handle these things, just that it would help to clarify the definitions used here with respect to the more general concepts.

Goal trajectory is an interesting concept, but Figure 1 doesn't get it across.  Is the sequence of questions the trajectory? How do we know there's a change?  Is the apparent branching the trajectory change?  What do the dashed lines mean?  The speaker is not labeled, but the conversation appears to be interleaved.  Are both speakers' questions part of the trajectory?

Section 2.4.2 leaves the nature of the planning that will be required completely vague, and mentions that "some learning framework" will be required, but leaves it unspecified as well.   An example of context is presented in Fig1, but how is it delimited?  Is it necessarily domain/task specific?  Natural language is assumed, but no mention of a parser, or where linguistic knowledge will come from.  Given the role it will play, that's kind of a big omission.

Related work: I would take a strong look at James Allen's PLOW system as an example of an interactive system that takes natural language annotations of a demonstration task (looking information up on a website) and learns the inferential task.  The tasks they address are very much like complex knowledge goals, even if they're not presented that way.


## REVIEW 2

- PAPER: 6
- TITLE: Interactive Knowledge-Goal Reasoning
- AUTHORS: Benjamin Bengfort and Michael T. Cox

- OVERALL EVALUATION: 0 (borderline paper (eh))
- REVIEWER'S CONFIDENCE: 3 (medium)
- Relevance (to goal reasoning): 3 (High)
- Novelty: 2 (Medium)
- Maturity Level: 1 (Early work (e.g., no implementation))
- Recommendation (if accepted): 1 (Poster presentation)

### REVIEW

The topic of this paper is quite relevant and could lead to very interesting
results.  The paper is a very early step.  Although there's a bit of
implementation, it's mostly for knowledge capture, so with respect to the key
ideas the submission is a proposal.  The proposal is highly ambitious.

Comments

This paper proposes an interactive process for satisfying knowledge goals through knowledge goal decomposition, aided by case-based reuse of prior methods.  I especially like the notion of goal trajectories and the observation that goals may change during a trajectory, requiring a dynamic process.

The work is at quite an early stage, so the paper's primary goal is to lay out
the basic approach and some foundational aspects.  However, tests on knowledge
capture from human users are being done in sample domains.

The paper raises many good issues.  Another issue the authors may wish to consider is the integration of the information resulting from various subgoals.  This seems to be taken for granted, but I think that it could be a hard problem in itself.

Some aspects may need more thought and some of the exposition could be clearer.  There are points in the paper at which definitions don't seem consistent.  I've highlighted them below.

I think this is an exciting direction and am looking forward to seeing how the
project develops.


Specific

p 1: fill-in -> fill in

research ... focus -> research ... focuses

p 2: the aim of which are -> which can be satisfied by

determine look up -> determine

"there is no ... set of relevant documents that might help [to determine where
to go for dinner]": A set of restaurant reviews could certainly help.  I
understand the point, but this passage needs to be sharpened.

restaurant to eat -> restaurant in which to eat

Saying the task is "how the information will be used" makes sense.  However,
the bullet describing the task seems to conflict with this.  It includes "the
task may be search or a database query".  This seems to say the task is the
plan to be executed to get the concepts?  Presumably a knowledge goal could be
satisfied in multiple ways and the system's job is to determine how; it
doesn't seem a knowledge goal would pre-specify this.  Maybe I'm confused on
this, but it would help to specify the task more precisely and to make sure
it's consistent across the paper.

p 4: "the final tasks of such a plan are simple knowledge goals": Saying that
a task can be a knowledge goal seems inconsistent with the earlier definitions.

p 5: "The concept of the question is explicitly": Should that be "implicitly"?

"Goal trajectories can be influenced by other users in the system": I don't
think the multi-user system has been described at this point.

p 6: in to -> into

The formulation of simple knowledge goals seems sometimes to define them by
content (e.g., contextual) and sometimes by how the information that they seek
is found (e.g., retrieval).  It seems these could overlap (contextual
information could be gained by retrieval).  Ideally, this would be a uniform
scheme with orthogonal items.

p 7: incrementally elicit -> incrementally elicits

"maximizing session length rather than minimizing it": What this means needs
further explanation/elaboration/justification.  One could maximize by pursuing
arbitrarily many irrelevant questions but of course that isn't what's intended.

p 8: "similar questions will be adapted with the current context of the user":
This sounds interesting but needs elaboration.  An example would help.

"The task is identified via a taxonomic classifier": It seems this could be
difficult.  Could you elaborate?

p 10: "Since the reasoning system is interactive, the system cannot passively
wait": Wouldn't the same be true in a batch system (that the system has to
come up with an answer)?

Bottom of page: This raises classic case-based maintenance questions.  Pure
frequency-based deletion can cause problems when a rarely used case is still
important.  An alternative is competence based deletion (e.g., Smyth and
Mckenna's work).

p 11: It would be nice to have more details on the experiments.  Who are the
users, how many there are, and what level of testing has
been done?


## REVIEW 3

- PAPER: 6
- TITLE: Interactive Knowledge-Goal Reasoning
- AUTHORS: Benjamin Bengfort and Michael T. Cox

- OVERALL EVALUATION: 2 (accept)
- REVIEWER'S CONFIDENCE: 4 (high)
- Relevance (to goal reasoning): 3 (High)
- Novelty: 3 (High)
- Maturity Level: 1 (Early work (e.g., no implementation))
- Recommendation (if accepted): 2 (Either)

### REVIEW

Thanks for submitting this paper; this is clearly relevant to the workshop and is of high interest.

This paper describes the role of user interaction and planning to solve *complex* knowledge goals (i.e., goals for acquiring additional information, such as for subsequent decision making) that are expressed as NL queries. This certainly integrates several topics and is perhaps AI-complete (or at least AI-complex and a suitable, ambitious topic for the ACS conference). This is a "vision" paper; early work.

Seems that there are a few synonyms for "knowledge" goals (e.g., "information-gathering", "learning").

This is a nice tie-in with plan decomposition, perhaps involving HTN planning.

Given the case-based reasoning (CBR) perspective, I'm reminded of interactive CBR work on planning for information gathering and thought of one paper, namely (Carrick et al., ICCBR-99) titled "Activating CBR systems through autonomous information gathering". While you've already noted several other things (e.g., work on SiN), perhaps this would also interest you, though it did not (as I vaguely recall) involve NL understanding.

On p1, "We claim that humans solve...": Will this later be tested using subject studies?

On p2, "Because this type of system is interactive and adaptive it is subject to goal  changes". This seems to be a disconnect; it would be subject to goal changes if the scenarios in the environment encourage goal changes. If the environment did not encourage them, it wouldn't matter whether the system was interactive or adaptive; there wouldn't be a need for goal change.

Ok, the topic of anticipating knowledge goals to propose better plans is interesting.

In Figure 1, the "S" terms (e.g., STIME, SSUBJECT) were not defined. I suggest also explicitly labeling/highlighting the goal trajectory in this figure.

At the end of 2.2, I like the discussion on how to handle situations when contextual information is missing. There seems to be an expectation, though, that the responses will themselves be unambiguous, which may not always be the case.

In Section 2.4.2, the list raises additional questions, such as how unsatisfactory queries are detected and why should the system mimic how humans solve similar goals?

In Section 3, what's the motivation for maximizing session length?

On p8, "learns over time and can anticipate future knowledge goals": I'd like to see an example.

Figure 2 has some issues: First, there's no human! If it's interactive, show a human/user. Second, where's the input (i.e., NL question)? Third, what are the semantics of a diamond vs. a rectangle?  Fourth, why is the Unstructured Data a sink?  Fifth, why does "Similar Questions" point from the Plan Query task/function to the Case Base, rather than in the opposite direction?  Is it mislabeled?  In general, this needs some attention and would benefit from a more formal discussion. Oh: an ontology is mentioned but not shown. Also missing is an indication where the system "responds with a textual knowledge goal", and a "taxonomic classifier". The text is not consistent with the figure.

The case representation (not "casebase representation", written earlier) in Section 3.1 is helpful but could/should be stated more formally, such as C = <knowledge goal, goal trajectories>, etc. But then a 2nd, distinct informal definition is given that conflicts with this representation, namely C = <topics, context requirements, task>.  I'm confused.

I didn't follow how this could be generalized to "professional" sports. Why would that be "more general"?

On p9, the "supplementary case base" is not shown in Figure 2.

In 3.2, "responds to systems ADVICE", this is the first use of the word "advice", which seems to come out of the blue. (This was not mentioned again until Section 4.1).

Towards the end of Section 3.2, on p10, there's again discussion of system functionality that is not indicated in Figure 2 (e.g., user providing info about their goals). Also, what are "behavior signals"? This wasn't mentioned elsewhere.

Section 3.3 on case management seems of low priority now because it's too early to talk about this; more space would be better devoted to clarifying intended system behavior. (I'm tempted to suggest using pseudocode if you think that would help.) That is, the system doesn't exist yet, so don't worry yet about CBM.

Later in Section 3.3, there's a mention of user feedback and relevance scoring that was not depicted in Figure 2, and it's unclear how adaptation (whether "easy" or not) is performed. Again, I recommend not discussing CBM yet, and suggest instead focusing on clarifying case representation and core system components for now.

Ok, good idea to discuss case studies. I was surprised that you assume "other users" would answer asked questions. Perhaps this could be done if the other users have motivation, such as monetary (i.e., Turkers) or are experts participating in an online forum. Ok, this seems your expectation. But the sheer amount of user annotation mechanisms suggests that you're being optimistic that users will actually provide all this info.

In Section 4.2, "we observed" suggests that a study has already been completed.

In the discussion on Related Work, what's the takeaway from the first paragraph (i.e., how is this related to your work)?  (Perhaps the final sentence of the 2nd paragraph is also intended to apply to the first paragraph?)  Also, SiN didn't focus on goal change, but rather on how to decompose a plan based on info provided by a user. SiN is a plan generator, not a plan executor. Your description of SiN may need to be revised; please check.

In the Conclusion, you mention that CCBR systems solve knowledge goals. I suppose so: they elicit problem descriptions from users in an attempt to point users to a solution to their (elicited) problem. So, yes, they perform an information-gathering activity.

The final mention of "creative investigative processes" seems to come out of the blue (i.e., Why? Is this approach well-suited for such processes?).

Minor

p1: resuse > reuse

p2: case based > case-based

p2: ": questions" reads awkwardly

p3: delete "look up"

p4: only allowing > allowing only

p7: interval, ... > interval. However, the required...

p7: elicit > elicits

p9: other, if > other. If

p10: "deuplication"?

p11: figure 3 > Figure 3

p12: There's some redundant text in Section 4.2.

p13: The final sentence of Section 4.2 has a grammar problem.

p13: "hoped"? Surprised by both the word and its past tense.

p14: have focused > has focused

p14: Need some citations in the final paragraph of Section 5.

p14: "system used": But it doesn't exist yet, so why the past tense?  Same for "indexed" and "relied".

p14: I suggest not using "hope".

References: Some lack capitalization (e.g., "faq finder", "international"), and Ram & Hunter (1991) seems incomplete.
