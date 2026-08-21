# Chapter 4 — Plausibility Auditing (Part 1: The Judgment Before Verification)

In March 2023, OpenAI's technical report for GPT-4 announced that the model had scored in roughly the 90th percentile on the Uniform Bar Examination. The number traveled fast. It appeared in keynote slides, regulatory hearings, and the opening paragraphs of think pieces about the end of the legal profession. It was clean, quantified, and exactly the kind of fact that ends an argument. A machine had outscored nine out of ten human test-takers on the gateway exam to the practice of law.

Now hold that claim in your hand for a moment before you reach for a source to check it. Does it sit right?

If you know how the bar exam works — how the percentile cohorts are constructed, who retakes the exam and when, what the essay components measure — something should itch. A legal-education researcher named Eric Martínez felt the itch and pulled the thread. His 2024 paper in *Artificial Intelligence and Law* found that the 90th-percentile figure was an artifact of the comparison group. The percentile had been computed against a sample of February repeat-takers — people who had already failed the exam in July and were sitting it again — rather than against a representative cohort. Against a more representative population, GPT-4's score lands around the 69th percentile of all test-takers (and roughly the 63rd among first-time takers). Against those who actually passed, around the 48th. On the written essay component — the part that most resembles the daily reasoning of a practicing lawyer — around the 15th. [Contested]

The structural point survives the correction. GPT-4 is genuinely capable on a standardized legal exam. But the specific, load-bearing claim — *90th percentile* — turned out to be the very thing this chapter is about: a statement that was fluent, confident, widely repeated, and not grounded in the reality it claimed to describe. Nobody fabricated it. It propagated because it was plausible, and because the people repeating it did not have, or did not deploy, the domain model that would have made it itch.

That itch — the response *before* you go looking for a source — is the capacity this chapter names. We call it **plausibility auditing**, and the first task is to say precisely what it is not.

## What Plausibility Auditing Is Not

The single most common misconception your strongest students will arrive with is that auditing is just careful verification — fact-checking done by a more conscientious person. It is not. Verification, fact-checking, and error detection are all *downstream*, *source-dependent* operations. They consume an external authority: a database, a reference text, a recomputation, a second tool. They confirm or refute a specific claim against something outside the output.

Plausibility auditing is the judgment that comes *before* any of that. It does not consult a source. It decides two things:

1. **Whether** a source needs to be consulted at all.
2. **What** the verification should look for if it happens.

This is not a smaller version of verification. It is a different cognitive operation, and it runs on a different input. Verification runs on external evidence. Auditing runs on your internal, grounded model of how the domain actually works — the model that tells you, before you check anything, that a dimensionless drag coefficient of 47 is wrong, that a holding does not fit the doctrine it is cited for, that a pediatric dose plausible for an adult is lethal for the patient in front of you.

![Flow diagram: an AI output feeds into a plausibility-audit gate that runs on the auditor's tacit domain model rather than an external source; the gate branches to either Proceed (no source needed) or downstream Verification, which is source-dependent — the audit sitting upstream of all source-consulting operations.](images/04-plausibility-auditing-part-1-fig-01.png)

*Figure 4.1 — Plausibility auditing sits upstream of verification: running on your tacit domain model, it decides whether a source is even needed and what the check should hunt for.*

The conductor's phrase for this, used throughout this book, is *hearing the wrong note before the score confirms it*. The conductor does not stop the orchestra to consult the sheet music every time a violin enters. They hear the dissonance against a held model of the piece, and only *then* reach for the score to locate exactly what went wrong. The plausibility audit is that first hearing. Verification is the trip to the score.

Here is the distinction operationalized as a table — the kind of artifact worth keeping at your desk while you learn the capacity:

| Operation | Trigger | Input it consumes | When it happens |
|---|---|---|---|
| **Plausibility auditing** | Any output, before checking | Your tacit domain model | First — decides whether to proceed |
| **Verification** | A specific claim you've decided to check | An external source | After the audit flags something |
| **Fact-checking** | A discrete factual assertion | A reference / database | Downstream, source-dependent |
| **Error detection** | A completed artifact | The artifact's internal logic | Downstream, often automated |

If you find yourself saying "I audited it by checking it against a database," verification has leaked in and the audit has not happened. The audit is the move that decided the database was worth opening.

## The Dividing Case: Statistical Likelihood Is Not a Grounded Model

Why is this a *distinct* capacity rather than a personality trait of careful people? Because the systems we are supervising are built on a foundation that produces fluency without groundedness as a structural matter, not as a temporary bug.

The cleanest demonstration in the field comes from the Abstraction and Reasoning Corpus, introduced by François Chollet in his 2019 paper "On the Measure of Intelligence." [High] Chollet's argument is that we have been confusing two things. There is *skill on a familiar distribution* — competence at tasks that resemble what you have seen a great deal of — and there is the *efficiency with which you make sense of genuinely novel tasks*. The first is what a standardized exam measures. The second is closer to what we mean by intelligence in the demanding sense. ARC is a set of small visual puzzles, each requiring you to infer a transformation rule from two or three examples and apply it to a new case. The puzzles are built on near-innate human priors — objectness, counting, symmetry — so that humans find them easy and a system cannot succeed merely by having memorized a large distribution of similar problems.

For several years ARC was the canonical embarrassment for large models: systems that aced professional exams stumbled on puzzles that ordinary people solve at a glance. The lesson was tidy, and for a while you could state it as "the model fails a puzzle a five-year-old can solve."

You can no longer say that, and the reason you can't is itself the lesson. In December 2024, OpenAI's o3 model cracked ARC-AGI-1, scoring 75.7% at the public compute limit and 87.5% in a high-compute configuration — above the 73–85% human-baseline band, and at very high cost (on the order of thousands of dollars per task at the maximal setting). The benchmark that had made the point so cleanly stopped making it. So the ARC Prize team rebuilt the test to resist exactly that kind of memorization. The relevant exemplars are now **ARC-AGI-2** (launched March 2025) and the interactive **ARC-AGI-3**. The pattern holds: at ARC-AGI-2's launch, pure LLMs scored near 0% and frontier reasoning systems only single digits to ~16%, while non-expert humans solved every task — over 60% on average, with 100% of tasks solved by at least two untrained testers. [High, updated April 2026] The gap narrows as the distribution becomes familiar — by late 2025 the best verified commercial model reached roughly the high-30s percent and a Gemini-3-based refinement solution about 54% — but it does so at steep compute cost and still trails the untrained human rate. The precise leaderboard numbers move monthly; check the current ARC Prize technical report before quoting any single figure.

The deep point is the one that survives every rebuild: **the gap reconstitutes itself.** Each time a benchmark is made resistant to memorization, frontier systems that excel on familiar distributions fall back to a fraction of human performance on the genuinely novel — and then climb again as the new distribution becomes familiar. This is not a story about one weak model. It is a structural feature of statistical pattern matching. A system optimized over a vast distribution of text and images is supremely good at producing what is *common and likely* given that distribution. It has no separate faculty that checks whether the common-and-likely output is *true of the specific situation in front of you.*

That is the whole foundation of plausibility auditing. **Statistical likelihood across a training corpus is not a grounded model of how a domain works.** The output can be the most probable continuation and still be wrong about the one patient, the one jurisdiction, the one load-bearing beam that matters. Fluency is evidence of likelihood. It is not evidence of groundedness. And because the human reader's instinct is to read fluency *as* groundedness, the capacity that corrects this instinct has to be trained deliberately. It does not come for free with competence at producing outputs.

## Two Mechanisms the Audit Runs On

When you audit an output, what is actually firing? Across the cases in this book it helps to name two distinct mechanisms. A caution before we do: this two-part split is a *pedagogical scaffold of this course*, not a named dichotomy you will find labeled this way in the cognitive-science literature. It maps loosely onto recognition-primed and dual-process accounts of expert judgment, but treat it as a teaching instrument, not an established taxonomy.

**Mechanism one: domain-grounded pattern recognition.** This is the audit that fires as *positive* recognition failing. "I have seen thousands of cases in this domain, and this does not match the shape of any of them." The lawyer who reads a citation and feels that the holding does not fit the doctrine is running this mechanism. Nothing is being computed against a rule yet; a familiar pattern simply isn't there where one should be.

**Mechanism two: anomaly detection against a mental model.** This is the audit that fires as a *violated constraint*. You hold, tacitly, a model of what is possible in the domain — conservation laws, dose ranges, the fact that a dock cannot accept a trailer longer than its bay — and the output trips one of those constraints. The engineer who sees an internally coherent forecast and thinks "that assumes a regime that ended two years ago" is running this mechanism. The model isn't matching a known good pattern; it's checking against a held boundary.

The reason this distinction earns its keep is that the two mechanisms surface *different* kinds of error and depend on *different* kinds of knowledge. Pattern recognition catches the output that is subtly out of distribution for your domain. Anomaly detection catches the output that is in distribution but violates a hard constraint of the specific case. A complete audit uses both, and — this is the part the assessment will press on — a defensible audit *names which one produced each finding.* Catching the error is not enough. The discipline is knowing why you caught it, because that is what tells you whether another auditor without your knowledge would have caught it too.

## Why Fluency Disarms the Audit

There is a perverse relationship at the center of this capacity, and it is worth stating bluntly because it runs against intuition: **the better the output reads, the more the audit is disarmed.** This is the fluency trap, and it is not a quirk of the unwary. It is a well-replicated finding from three decades of human-factors research on automation bias — the tendency of humans to grant automated outputs an authority they have not earned and to use them as a heuristic substitute for their own checking. We will give that literature its full weight in the next chapter, where you perform audits under live conditions. For now, hold the shape of it: the polish of an output is produced by the same statistical machinery that produces its likely-but-possibly-ungrounded content. Polish and groundedness are generated by the same process and are therefore *correlated only by accident*. Your reader's brain treats them as the same signal. They are not.

This is why the audit must be trained as a deliberate act rather than trusted as an instinct. Your instinct is calibrated by a lifetime of human communication, in which fluency genuinely did track competence — fluent humans usually did know what they were talking about. That heuristic is now actively wrong in the presence of a system engineered to be fluent independent of whether it is right.

## Worked Example: The Same System, Two Results

Return to where we began, and place the two facts side by side, because together they make the chapter's whole argument visible in a single frame.

A frontier model scores well above a passing standard on a standardized legal exam — that part is real, even after Martínez deflates the headline percentile. The *same* class of system, on ARC-AGI-2, scores a fraction of what untrained adults score on puzzles requiring a transformation rule to be inferred from a few examples. One system. Two results that look like a contradiction.

They are not a contradiction. They are the chapter's thesis stated twice. The exam rewards skill on a familiar distribution — the kind of legal questions that appear, in vast quantity, in the training corpus. ARC-AGI-2 demands sense-making on the genuinely novel, where having seen the distribution buys you nothing. The model is exactly what its construction predicts: excellent at the common and the likely, weak at the grounded and the new.

And the 90th-percentile claim itself completes the lesson. It was the output of human discourse, not a model — but it failed in precisely the way model outputs fail. It was fluent, confident, widely propagated, and ungrounded in the specific reality (the cohort construction) it described. The people who repeated it were not careless about facts in general. They lacked, in that moment, the domain model of bar-exam psychometrics that would have made the number itch — and so they reached for verification too late or not at all. The audit they did not run is the one this capacity teaches you to run by default.

---

> ### AI Wayback Machine: Chollet and the Measure of Intelligence (2019)
>
> **François Chollet, "On the Measure of Intelligence," arXiv:1911.01547 (2019).** Chollet's intervention was to insist on a distinction the field had been blurring: skill on a familiar distribution is not the same as the ability to make sense of the genuinely novel. He grounded the claim in algorithmic information theory and built the Abstraction and Reasoning Corpus to operationalize it — tasks built on innate human priors, solvable from a handful of examples, easy for people and hard for systems that succeed by absorbing distributions.
>
> The Wayback lesson is durable even as the benchmark numbers churn. When o3 cracked ARC-AGI-1 in 2024, the response was not to declare the question settled but to rebuild the test — and the gap reappeared on ARC-AGI-2. That recurrence *is* the structural argument behind plausibility auditing. A system's fluency reflects mastery of what it has seen. It does not, and cannot by construction, certify groundedness in the specific, novel reality you are accountable for. The audit is the human faculty that supplies what the measure of intelligence says the machine lacks.

---

## Exercises

These exercises are diagnostic and formative; together they constitute the basis of **Reading Response #3 (30 pts)**. Each names a judgment call that is yours to make — and that the Assessment Spine requires you to surface explicitly.

**Exercise 4.1 — Define by negation, then defend it (Understand).** In one sentence, state the distinction between plausibility auditing and verification. Then write a short paragraph defending that sentence against a peer who insists they are the same operation done at different levels of care. Your deliverable is the sentence plus the defense (roughly 150 words). *The judgment call to name: what, specifically, in your own domain, can you audit without consulting any source — and how do you know the difference between "I recognize this is wrong" and "I looked it up"?*

**Exercise 4.2 — What a grounded model flags that a fluency check misses (Analyze).** For three AI outputs (provided, or drawn from your own recent use), state for each: what a domain-grounded model would flag, and what a reader checking only for fluency and internal coherence would miss. For each finding, identify which of the two mechanisms produced it — domain-grounded pattern recognition or anomaly detection against a held constraint. Deliverable: a three-row table with the finding, the mechanism, and the missed signal. *The judgment call to name: which findings depended on knowledge you hold that a competent generalist would not?*

**Exercise 4.3 — The audit-or-not decision (Evaluate). [Track 2]** Take a real AI output from your own capstone domain. Before consulting any source, write the audit verdict: does this output require verification, and if so, what specifically should the verification look for? If it does not require verification, defend why your grounded model is sufficient warrant to proceed. Deliverable: the output, the verdict, the named target (or the defense of skipping). *The judgment call to name: the decision to verify or not verify is itself an accountable choice — name what you are taking responsibility for if your audit is wrong.*

## Chapter Closing / Bridge

You can now say what the audit *is* — and, more importantly, what it is not. It is the judgment before verification: the decision about whether a source is even needed and what the check should hunt for. It runs not on external evidence but on a grounded, largely tacit model of how your domain actually works, and it fires through two mechanisms — recognizing what should be there and isn't, and detecting what shouldn't be there and is.

Saying what the audit is, however, is not the same as performing one under pressure. The next chapter inverts the usual order: the assessment instrument arrives *before* the instruction. You will be handed five real AI outputs and asked to audit them first — before you are taught how. The discomfort of that is deliberate. It is the only way to surface what your domain knowledge already lets you catch, and to mark, honestly, the edge of what it cannot reach.

## Sources

- Chollet, François. "On the Measure of Intelligence." arXiv:1911.01547 (2019). https://arxiv.org/abs/1911.01547
- Martínez, Eric. "Re-evaluating GPT-4's Bar Exam Performance." *Artificial Intelligence and Law* (2024). SSRN: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4441311 ; Springer: https://link.springer.com/article/10.1007/s10506-024-09396-9
- OpenAI. "GPT-4 Technical Report" (March 2023). [Cited as the origin of the contested 90th-percentile claim, not as settled fact.]
- ARC Prize. "OpenAI o3 Breakthrough High Score on ARC-AGI-Pub" (Dec. 2024); "Announcing ARC-AGI-2" and ARC-AGI-2 Technical Report (2025); ARC Prize 2025 Results and Analysis. https://arcprize.org (figures current as of April 2026; percentage figures are date-sensitive — verify against the latest report before quoting).
- Polanyi, Michael. *The Tacit Dimension.* University of Chicago Press (1966). [Introduced here, developed in Chapter 5: "we can know more than we can tell."]
