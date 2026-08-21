# Chapter 8 — The Seven Signals: What Genuine Learning Looks Like

*Learning is not a state you arrive at. It is an event that leaves evidence — and the evidence is specific enough to distinguish the real thing from a very good imitation.*

---

In 1997, Wolfram Schultz, Peter Dayan, and Read Montague published a paper in *Science* that changed how neuroscientists thought about dopamine. The common story at the time was that dopamine signals reward — the brain's way of saying *that felt good*. Schultz's recordings of primate dopamine neurons said something more precise. Dopamine does not signal reward. It signals the *gap* between expected reward and actual reward. When something happens exactly as predicted, the dopamine response is muted. When something violates the prediction — better than expected or worse — the signal fires. The brain is running a continuous prediction-error computation, and dopamine is what tells it: *this is worth encoding*.

The implications for learning follow immediately. A student working through a hard problem is running predictions: she expects the drug to behave one way; it behaves differently; the violation is the moment the knowledge gets laid down. A student who asks a language model for the answer and copies it has made no prediction. There is no violation. There is no encoding signal. She has produced an artifact while bypassing the neurobiological event that constitutes learning.

This is not a new observation dressed in new language. It is the old observation — *you learn from mistakes, not from answers* — with a mechanistic account of why. And once you have the mechanism, a question follows: if genuine learning involves prediction errors, and prediction errors leave behavioral traces, what do those traces look like? Can you measure them? Can you distinguish, from the outside, a student who learned from a student who produced?

That is the question this chapter answers. The answer is seven specific traces, which I call signals here. Each has a clean mechanistic account from cognitive psychology. Each has decades of empirical support as an individual measure. The integration — these seven, combined as a deployed measurement architecture — is Medhavy's design choice, and I want to be honest about that distinction throughout: the components have evidence; the composite is a bet.

---

## Why the chapter before this one was not enough

Chapter 7 closed with a distinction between engagement evidence and learning evidence. Canvas measures engagement: clicks, time on page, completion, quiz scores. These are real numbers about real behavior. They are not measures of whether the cognitive event occurred. A student can click for forty-seven minutes without ever generating a prediction error. A student can score eighty-eight percent on a quiz by submitting a second tab's AI output without any of the knowledge landing in retrievable long-term storage.

The distinction matters because of what happens six weeks later. Elizabeth and Robert Bjork, in 1992, separated *storage strength* from *retrieval strength*. Storage strength is how durably a memory trace is encoded. Retrieval strength is how easily the trace surfaces on demand. Retrieval strength decays with time and disuse; storage strength does not. A student who studied through genuine prediction errors — making wrong guesses, being corrected, generating the encoding signal — has built storage strength. A student who offloaded to an AI has retrieval strength on loan, available as long as the AI is in the loop, gone when it isn't.

The engagement metrics are blind to this distinction. The seven signals are designed specifically to see it. What follows is each signal: what it measures, why it works, and what it looks like in a health sciences setting.

<!-- → [INFOGRAPHIC: Two-track diagram of storage strength vs. retrieval strength — left track shows storage strength as a horizontal line that holds flat across weeks 1–12; right track shows retrieval strength as a curve that decays without practice but recovers with each retrieval attempt — annotated with "genuine learning path" vs. "offloaded learning path"; student should see why a delayed retention quiz reveals what a same-day quiz cannot] -->

<!-- → [TABLE: Seven signals quick reference — columns: Signal, One-sentence mechanism, Primary mode(s) that produce it, What strong signal looks like vs. weak — serves as an anchor the reader can return to while reading the detailed explanations below] -->

---

## The seven signals

**Y1 — Temporal Engagement.** Cognitive load theory, developed by John Sweller in the late 1980s, establishes that genuine cognitive processing takes time, and the time scales with the intrinsic difficulty of the material. This is not a subtle finding: it follows from the architecture of working memory, which has limited capacity and requires more processing cycles for harder material. A student who genuinely works through a difficult pharmacology case spends measurably longer on it than on an easy one from the same module. A student who has offloaded the work — to an AI, to a neighbor's answer, to a vague guess — does not show that scaling. The hard problem takes about the same time as the easy one, because the processing is not happening. Y1 is not total time; it is the *shape* of time across problems of varying difficulty. A flat distribution is the warning. A scaling distribution is consistent with genuine engagement.

**Y2 — Error Trajectory Coherence.** In 1978, John Seely Brown and Richard Burton published what became one of the foundational papers in educational technology. Working with elementary arithmetic, they showed that student errors are not random. Students make systematic mistakes that reveal specific procedural misconceptions — Brown and Burton called them *bugs* in the student's mental model. The bugs are coherent: the same pattern shows up across similar problems. And when a student with a genuine misconception receives correct instruction, the bug updates: the student stops making that particular error. A student guessing makes incoherent errors that do not update. The trajectory over time is the signal. In nursing, a student who has not yet integrated vital-signs trends will consistently misread subtle deterioration as stable — same pattern across different cases, and when shown the correct interpretation, the pattern updates. Guessing on the same scenarios produces scatter, not pattern, and scatter does not update under instruction.

**Y3 — Cross-Context Transfer.** Transfer is the oldest question in learning science. Edward Thorndike asked it in 1901 and concluded that transfer is rare: what you learn in one context does not automatically apply in another. The modern refinement, from John Bransford and Daniel Schwartz in 1999, reframes transfer as *preparation for future learning*: the student who genuinely understood the underlying mechanism of a concept is faster to learn the next, related concept. The student who memorized surface features is not. In pharmacy, a student who genuinely learned why one drug class causes QT prolongation can recognize the same risk in a new drug class she has never seen. The student who memorized the warning label cannot. The recognition in a novel context is the signal.

**Y4 — Uncertainty Calibration.** The metacognition literature, summarized in John Dunlosky and Janet Metcalfe's textbook and built on Nelson and Narens's 1990 foundational work, establishes a reliable finding: students who study with external resources — textbooks, AI systems, annotated notes — inflate their judgments of their own learning. They feel more confident than subsequent testing reveals to be warranted. The borrowed certainty feels like knowledge; it is not. A genuine learner who has studied anticoagulation correctly will hesitate on the borderline case — the patient with mild hepatic dysfunction and low body weight — and will say *I'm not sure; I would want to check the current guideline*. An AI-assisted student who absorbed a textbook answer will state the answer with a confidence the situation does not warrant. The hesitation is calibration. The misplaced confidence is its absence.

**Y5 — Social Knowledge Texture.** This signal is less standardized in the research literature than the others, and I want to say that clearly. The mechanism draws on Allyson Hadwin and Sanna Järvelä's work on socially shared regulation of learning, as well as the long tradition of case-discussion pedagogy. The observation is this: a student reasoning through a problem in dialogue — with an AI, a peer, an instructor — leaves a textured trace. Specific confusions are named. Positions change in response to argument. Half-formed ideas are articulated and revised as the student works toward clarity. A student who has not genuinely engaged but is producing dialogue from borrowed text produces smooth, generic statements. No specific confusion. No position change. No visible working-out. Faculty who lead case discussions have been reading this texture for decades without naming it. The student who says *I initially thought this because of X, but then I realized that doesn't hold because of Y* is showing Y5. The student who says *as we know, the mechanism involves...* and then recites fluent text is not.

**Y6 — Retrieval Strength Decay.** This is the Bjork distinction again, made into a measurable signal. Retrieval strength decays with disuse; storage strength does not. Karpicke and Roediger in 2008 demonstrated that students who tested themselves once outperformed students who restudied four times, at a one-week delay. Henry Bahrick's 1984 work extended the finding to the fifty-year scale: what survives decades after a language course is not what performed best immediately — it is what was encoded deeply enough to resist decay. In practice: a student who genuinely learned the differential diagnosis for chest pain in the cardiology block can still produce it three months later in the emergency medicine block, even if slowly and with effort. A student who memorized for the cardiology examination cannot. The delayed retrieval check is the signal. Quiz Me is the mode designed specifically to produce Y6, because its scheduling algorithm structures retrieval at increasing intervals — building storage strength by design.

**Y7 — Scaffolding Response Curve.** Vygotsky, in 1978, described the zone of proximal development: the space where a learner can do, with assistance, what they cannot yet do alone. The zone has a shape. Anders Ericsson formalized it in 1993 as deliberate practice — effortful work at the precise edge of current capability. Koedinger and Aleven, in 2007, named the *assistance dilemma*: too much help produces offloading; too little produces shutdown; the diagnostic information is in how the student responds to *graduated* assistance. A student with genuine partial understanding will, given a small hint, complete the remaining reasoning herself and arrive at the answer. A student without underlying understanding will not move forward from the same hint — the hint lands in a gap with nothing to connect to. The shape of the response to graduated assistance is the signal.

---

## What the mapping looks like

These seven signals are not produced equally by all four modes. The architecture pairs specific signals with specific modes — not because the other modes couldn't produce them, but because each mode is designed around the cognitive operation that generates a particular kind of trace.

<!-- → [TABLE: Mode-to-signal mapping — rows: Ask AI, Quiz Me, Case Study, Glimmer; columns: Y1 through Y7; cells marked Primary, Secondary, or dash — student should see which modes are single-signal vs. multi-signal, and why Case Study is primary on six of seven] -->

| Mode        | Y1 Temporal | Y2 Error | Y3 Transfer | Y4 Calibration | Y5 Social | Y6 Retrieval | Y7 Scaffolding |
|-------------|:-----------:|:--------:|:-----------:|:--------------:|:---------:|:------------:|:--------------:|
| Ask AI      | Primary     | Secondary| —           | Primary        | Secondary | —            | Primary        |
| Quiz Me     | Secondary   | Primary  | Secondary   | Secondary      | —         | Primary      | Secondary      |
| Case Study  | Primary     | Primary  | Primary     | Primary        | Primary   | Secondary    | Primary        |
| Glimmer     | Primary     | Secondary| Primary     | Primary        | Primary   | Secondary    | Secondary      |

Two things in this table are worth pausing on. First, Case Study is primary on six of the seven signals. This is not an accident of enthusiasm. It follows from Case Study's structure: a student running through a scenario with an AI facilitator is simultaneously generating time-on-difficulty data, error trajectories under feedback, transfer demands, calibration judgments, social texture, and scaffolding responses. The mode is expensive to build — scenario authoring, graduated hint design, faculty review — because it is doing the most measurement work. The cost and the signal are related.

Second, Quiz Me is primary on exactly one signal: Y6 retrieval strength decay. This makes Quiz Me look simple in the table. It is simple. That is the design. Quiz Me is the cleanest single-signal mode in the architecture, and its value comes from running reliably and often enough that the single signal becomes very strong. The trade-off is clarity for breadth, and for the specific purpose of building and measuring durable storage, the trade-off is correct.

---

## Two students, one table

Return to the two students from Chapter 7. Canvas analytics: forty-seven minutes on the module, roughly one hundred forty clicks, one hundred percent completion, eighty-eight percent on the quiz, assignments of similar surface quality. Canvas could not distinguish them.

Here is what the seven signals see.

| Signal                       | Student A                      | Student B                        |
|------------------------------|--------------------------------|----------------------------------|
| Y1 Temporal Engagement       | Time scales with difficulty    | Flat across difficulty           |
| Y2 Error Trajectory          | Coherent, updates under feedback | Random, does not update        |
| Y3 Cross-Context Transfer    | Applies in new scenario        | Does not transfer                |
| Y4 Uncertainty Calibration   | Hesitates on edge cases        | Confident on edge cases          |
| Y5 Social Knowledge Texture  | Specific confusions, position shifts | Smooth, generic statements  |
| Y6 Retrieval Strength Decay  | Holds at six weeks             | Collapses at six weeks           |
| Y7 Scaffolding Response      | Small hint unlocks reasoning   | Small hint does not move her     |

<!-- → [INFOGRAPHIC: Side-by-side signal profiles for Student A and Student B — visual representation of each signal as a meter or bar, showing the contrast in pattern — designed to make the abstract table concrete; student should see that the profiles are not close calls but systematic differences across every dimension] -->

Student A's profile reads as someone for whom the neurobiological encoding events occurred: predictions made, errors generated, storage laid down. Student B's profile reads as someone who produced artifacts while bypassing those events. The Canvas dashboard, six weeks earlier, said both students were indistinguishable. The seven-signal profile taken in the moment predicted the difference before it became visible.

I want to be careful about how I state that claim. The example is illustrative. It is drawn from the mechanistic logic of each signal, not from a published validation study of the seven-signal composite as a deployed predictive system. The components — Bjork's storage-retrieval distinction, Brown and Burton's error coherence, Bransford and Schwartz on transfer — are well-validated individually. The *composite* as a deployed measurement architecture with a single GLP score is Medhavy's design, and its predictive validity at scale is the open empirical question you are evaluating when you consider adoption. The components have evidence. The integration is theoretically motivated, not yet empirically validated at the scale the system proposes to operate.

---

## What the GLP score is and isn't

The GLP score is the composite of the seven signals, updated per student and per concept as more interactions accumulate. It is the number the instructor sees on a dashboard. It is not a grade. This distinction is not a technicality — it is load-bearing for the architecture's validity.

If the GLP score were entered in the gradebook, students would optimize against it. And the seven signals are only signals because students are not consciously trying to produce them. Y5 social knowledge texture reads genuine because it is genuine — the student is working something out, not performing working-something-out for an audience. Y4 uncertainty calibration is diagnostic because the student is expressing real confidence, not a performed confidence calibrated to look appropriately humble. Move the score into the gradebook and the signals become targets. Targets get gamed. The measurement validity collapses.

The score also changes over time. Early in the term it is noisy — not enough interactions to distinguish signal from fluctuation. By mid-term the constituent signals have accumulated enough that the composite is interpretable. The cold-start period is real and is one of the honest limitations of any measurement system that learns from behavior: it needs behavior before it can learn from it.

<!-- → [CHART: Line chart showing GLP score confidence interval width over a 15-week term — x-axis is weeks, y-axis is uncertainty band around the composite score; band is wide in weeks 1–4 (cold-start), narrows progressively through weeks 5–10, stabilizes in weeks 11–15 — annotated with "act with caution" zone and "interpretable" zone; reader should see when the score is and isn't actionable] -->

The instructor's role in this architecture is the meta-model. The GLP score adds one input the instructor currently cannot see. It does not replace the inputs the instructor already has — direct observation, assessment quality, clinical performance, everything else that constitutes knowing a student. A high GLP score for a student the instructor has watched struggle in simulation is a data conflict to investigate, not a result to trust over the instructor's own eyes. The system surfaces signal. The instructor decides what to do with it.

---

## What would change my mind

The case for the seven signals rests on a categorical claim: engagement evidence and learning evidence are different categories of measurement, and conflating them produces systematic blind spots. If a published, replicated study showed that a sufficiently rich engagement model — click counts, time on page, quiz performance, completion rates — predicts delayed retention as well as the seven-signal composite, that claim would soften. The categorical distinction would become a resolution distinction: engagement metrics are a coarser measure of the same thing, not a categorically different thing. The individual components of the Frictional Framework would survive that finding. The argument for a *separate measurement category* would need to be rebuilt.

There is also a longer-horizon question the chapter does not answer. The seven signals were designed around current AI limitations — specifically, the fact that language models produce fluent text without the behavioral markers of genuine cognitive engagement. Y5 social texture reads offloading because AI-generated dialogue is smooth and generic in a way that human reasoning-aloud is not. Y4 calibration reads offloading because AI systems express confidence without the metacognitive uncertainty that genuine learners feel. Both of these are features of current systems. If future AI systems produce outputs that mimic genuine social texture and genuine uncertainty calibration, the signals that currently detect offloading will need to be redesigned. How to measure genuine learning when the imitations are indistinguishable from the real thing is the problem the field of educational measurement will be working on for the next decade. This chapter does not solve it.

---

## LLM Exercises

1. **(Understand)** For each of the seven signals (Y1 through Y7), write one sentence describing a specific behavior you have observed in a student — in office hours, in class discussion, in a clinical simulation, in a written assignment — that would register as genuine learning on that signal. Use a different student or a different concept for each signal. The exercise's value is in discovering that you have, in fact, been observing these signals for years without a framework to name them.

2. **(Apply — application to your deployment)** Identify the single highest-risk assessment in your curriculum — the one where AI offloading would cause the most downstream harm, whether to patient safety, professional licensure, or program reputation. Name the two or three signals from the seven that would be most diagnostic for that assessment. For each, write one sentence on why that signal is the right diagnostic for that assessment.

3. **(Evaluate — application to your deployment)** Of the seven signals, which ones could you currently observe — imperfectly, informally, by faculty inspection of Canvas data and direct contact with students — without adding Medhavy? Be honest. Which ones cannot be observed at meaningful scale without a measurement layer like Medhavy's? Write the two lists. The size of the second list is one of the inputs to your adoption decision.
