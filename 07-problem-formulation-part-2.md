# Chapter 7 — Problem Formulation (Part 2: Three Distinct Reframings)

A student hands in three reframings of a customer-support problem. They read:

1. "How do we reduce the number of support tickets?"
2. "How do we decrease the volume of customer support requests?"
3. "How can we lower the rate at which customers contact support?"

Three sentences. One problem. The student has done what the assignment seemed to ask — produced three framings — and has in fact produced one framing, reworded three times. Every one of them would be tested by the *same* solution: anything that reduces ticket count counts as a win for all three. They are synonyms wearing the costume of alternatives.

This is the most common failure in this chapter, and defeating it is the chapter's whole instrument. So we begin with the test that separates a reframing from a rewording, and we apply it ruthlessly.

## The Distinctness Test

Here is the operational test, and it is gradeable precisely because it is not a matter of taste:

> **Would these two formulations require different solutions even to test?** If a single solution could satisfy both, they are not distinct — they are one formulation in two outfits.

Run the test on the three support framings. A solution that suppresses tickets — say, hiding the "contact us" button — satisfies all three simultaneously. One solution, all three "reframings." Verdict: not distinct. They collapse to one.

Now watch genuinely distinct reframings of the same situation:

1. **"How do we reduce support tickets?"** — tested by ticket volume. Solution space: deflection, self-service, friction on contact.
2. **"Why is the product generating this much confusion in the first place?"** — tested by *whether the underlying confusion drops*, which a deflection solution would not move at all. Solution space: redesign, onboarding, documentation. A button-hiding solution that lowered ticket count would *fail* this framing, because confusion would be unchanged. The two framings are tested by different solutions. Distinct.
3. **"Which customers are contacting us, and is the highest-value segment the one we're losing to frustration?"** — tested by retention and value-weighted contact, not raw volume. A solution that cut total tickets while driving away your best customers would *pass* framing 1 and *fail* framing 3. Distinct again.

These three would each require a different solution to test, and — the deeper tell — a solution that triumphs on one can *fail* another. That is the signature of genuine distinctness: the framings are not just worded differently, they *disagree about what would count as success.* When your three reframings can disagree about whether a given solution won, you have three problems. When they all cheer for the same solution, you have one problem and two rewrites.

![Three reframings of a support problem tested against one solution, hide the contact button: framing one passes in red, framings two and three fail; one pass and two fails is the signature of distinctness.](images/07-problem-formulation-part-2-fig-01.png)

*Figure 7.1 — Genuinely distinct reframings disagree about success: a single solution passes one and fails the others, the signature reworded synonyms can never show.*

| | Tested by | A "hide the button" solution would… |
|---|---|---|
| Reduce tickets | Ticket volume | **Pass** |
| Reduce product confusion | Drop in underlying confusion | **Fail** (confusion unchanged) |
| Protect high-value retention | Value-weighted retention | **Fail** (best customers leave) |

If you cannot fill that last column with at least one disagreement across your reframings, return to the drawing board. You have rewordings.

## The Reframe Moves

Distinctness is the test; it is not a method for *generating* candidates. Three moves reliably produce genuinely distinct framings from a single situation. (These are this course's pedagogical scaffolds, not cited constructs — use them as generators, then subject every output to the distinctness test above.)

**Zoom out.** Move up a level of abstraction until the original problem becomes a symptom. "How do we reduce support tickets?" zooms out to "Why is the product generating confusion?" The original metric becomes evidence of something larger, and the solution space relocates entirely.

**Zoom in.** Move down to a specific, load-bearing sub-case. "Improve retention" zooms in to "Why do users churn in week one specifically?" The narrowing is not a loss of ambition; week-one churn may be a different phenomenon with a different cause than month-six churn, and a solution for one may be irrelevant to the other. Zooming in passes the distinctness test when the sub-case genuinely requires its own solution.

**Change the actor or locus.** Ask whose problem this actually is, and where the binding constraint really sits. "How do we get drivers to follow the optimal routes?" — which locates the problem in driver compliance — becomes "Whose constraint is actually binding: dispatch's routing assumptions or the drivers' on-the-ground reality?" The actor shifts, and with it the entire diagnosis. This move is especially powerful because the default framing almost always locates the problem in the most convenient actor, which is rarely the one whose constraint binds.

These three moves are not exhaustive, and a reframe that combines them is often the strongest. But notice what they have in common: each is a deliberate refusal of the modal framing the previous chapter warned about. The AI, asked to "frame the problem," gives you the center of the distribution. The reframe moves are how a human pulls deliberately toward the edges — toward the salient framings the distribution underweights.

## The Type III Error: Being Exactly Right About the Wrong Problem

What, precisely, is the danger these reframings defend against? It has a name, and the name has a tangled and instructive history that is worth telling honestly — because a chapter about getting the problem right should not get its own attribution wrong.

The danger is **solving the wrong problem precisely.** Not a sloppy answer to the right question — a flawless, rigorous, beautifully verified answer to a question that was never the one that mattered. Semmelweis's contemporaries, had they been more rigorous, could have produced an impeccable statistical characterization of the mortality variance and learned nothing that saved a mother. Exactly right. Wrong problem.

The formal label is the **"error of the third kind"** or **Type III error**, and here is the lineage, stated straight:

- **Allyn Kimball (1957)**, a statistician at Oak Ridge, coined "the error of the third kind," defining it as "the error committed by giving the right answer to the wrong problem." This is the earliest attested coinage. [High]
- **Howard Raiffa (1968)**, in *Decision Analysis*, discussed an error of the third kind — and, from imperfect memory, misattributed it to John Tukey. [High] A book on getting the problem right contains, in its own lineage, a documented case of getting the attribution wrong. The detail is too on-theme to omit.
- **Ian Mitroff and Tom Featheringham (1974)**, in *Behavioral Science*, extended the concept and — this is the part that matters for us — tied it explicitly to **problem formulation**: "one of the most important determinants of a problem's solution is how that problem has been represented or formulated in the first place." [High] This is the source closest to our actual subject, and it is where the concept should be anchored.

You will frequently see the Type III error credited to Russell Ackoff. Ackoff did *not* coin it. [High] What Ackoff did — in *Redesigning the Future* (1974) — was give the danger its most memorable formulation: **"We fail more often because we solve the wrong problem than because we get the wrong solution to the right problem."** [High] That line is genuinely his and is perfect for the chapter. Use Ackoff for the *quote*; anchor the *concept* on Mitroff and Featheringham, who connected it to formulation; credit Kimball with the coinage. Stating this lineage honestly is itself an exercise in the chapter's discipline — refusing the modal, convenient attribution in favor of the accurate one.

The connection to AI supervision is the asymmetry's sharpest edge. An AI's flawless optimization of the wrong formulation is *more* dangerous than a human's sloppy solution to the right one — because it is more convincing. A rigorous, well-presented, internally verified answer carries authority. When that authority is attached to the wrong problem, the very polish that the audit of Chapters 4 and 5 might otherwise trust becomes the mechanism by which a Type III error launders itself into a decision. Problem formulation is the only defense, because it operates before the polish exists.

## The Constraint Set as an Evaluation Instrument

Three distinct reframings are necessary but not sufficient. You must choose one, and the choice must survive scrutiny. The instrument for that is an explicit **constraint set** — the criteria against which the reframings are scored, named in advance so the selection cannot be rationalized after the fact.

A serviceable constraint set has both *feasibility* dimensions and *salience* dimensions, and the design of the set is itself a judgment:

| Constraint | What it asks |
|---|---|
| Feasibility | Can this framing's solution actually be built with available resources? |
| Cost | What does pursuing this framing cost in time, money, attention? |
| Time horizon | Does this framing's solution matter on the timescale that matters? |
| Salience / importance | If solved, does this framing address what actually matters here? |
| Values / whose interests | Which stakeholders does this framing center, and which does it decenter? |

The critical design rule: **the constraint set must include salience and values, not only feasibility.** If your constraints are all feasibility constraints — cost, time, buildability — you have built a machine that selects the *most tractable* framing, which is the AI default and the high road to a Type III error. The whole point of the previous chapter was that the tractable framing is often the wrong one. A constraint set that scores only tractability re-introduces, through the back door, exactly the bias formulation is supposed to defend against.

![A scored comparison of three reframes across feasibility, cost, time horizon, salience, and values; reframe B scores low on feasibility but highest on salience and values and is selected in red.](images/07-problem-formulation-part-2-fig-02.png)

*Figure 7.2 — Scored against a set that includes salience and values, the selected reframe is the defended values choice — not the most tractable one.*

## The Values Decision Inside Formulation

Here is the chapter's distinctive and most consequential claim, and it is worth stating without hedging: **every reframing is already a values choice.** Not a values choice that gets added afterward, in an "ethical considerations" section appended to the analysis. A values choice baked into the framing itself, made the moment you chose which difference to treat as signal and whose constraint to treat as binding.

Frame a hospital scheduling problem as "maximize throughput" and you have decentered patient experience and staff burnout — not as a separate ethical lapse, but as a direct consequence of what the framing attends to. Frame the same situation as "minimize staff burnout" and you have decentered throughput. There is no neutral framing that centers everyone; framing is the act of deciding what to center, and to center one thing is to decenter another. The "objective problem statement" that centers no one's interests is a fiction, and a dangerous one, because it conceals the values choice rather than removing it.

This is why an AI cannot make the selection for you, and the reason is structural, not a matter of current capability. The model can *generate* candidate framings — it is fluent at producing variations. But it cannot certify that three framings are genuinely distinct, because the distinctness test requires a grounded model of what "would require a different solution to test" in your actual domain, which is the tacit knowledge of Chapter 5. And it cannot make the *values* selection among the distinct framings, because that selection is an accountable act — someone has to own the decision to center throughput over burnout and answer for it. The model has no values to bring and no accountability to bear. Both the distinctness certification and the values selection require exactly what the model lacks: situated judgment and a name on the decision.

## Worked Example: A Brief Reframed Three Ways

Take a capstone-style brief: *"Our field-service technicians are completing fewer jobs per day than projected. Fix it."*

**Reframe A — Reduce per-job time (zoom in on the metric).** Tested by: average minutes per job. Solution space: better tools, route optimization, paperwork reduction. Centers: operational efficiency. Decenters: technician wellbeing, service quality.

**Reframe B — Are we measuring the right output? (zoom out, change the locus).** Tested by: whether "jobs per day" is even the value-relevant metric, versus first-time-fix rate. A solution that raised jobs-per-day by rushing would *fail* this framing if it lowered first-time-fix and generated repeat visits. Centers: customer outcome and total cost. Decenters: the original throughput target.

**Reframe C — Whose constraint is binding? (change the actor).** Tested by: identifying whether the limit is technician capacity, parts availability, or dispatch's scheduling assumptions. A solution aimed at technician speed would *fail* if the real constraint is parts arriving late. Centers: the actual binding constraint. Decenters: the assumption that technicians are the problem.

Run the distinctness test: a solution that speeds technicians (A) could lower first-time-fix (failing B) and would do nothing if parts are the constraint (failing C). The three disagree about what counts as success. **Distinct.** Now score against the constraint set — and suppose first-time-fix data and a salience judgment that *customer outcome matters more than raw counts* tilt the selection toward B. The defense is both analytical (the data suggest repeat visits are inflating the apparent shortfall) and values-based (we are choosing to center service quality over throughput, which decenters the original target and the managers whose dashboards track it). That decentering must be *named*, not buried. Naming who you chose not to serve is the difference between a defended selection and a laundered one.

---

> ### AI Wayback Machine: Ackoff on Solving the Wrong Problem (1974)
>
> **Russell L. Ackoff, *Redesigning the Future: A Systems Approach to Societal Problems* (Wiley, 1974).** "We fail more often because we solve the wrong problem than because we get the wrong solution to the right problem." Ackoff distinguished tangled "messes" from well-defined "difficulties" and argued that the consequential work is choosing which problem to solve at all.
>
> Honesty about the lineage is part of the lesson. Ackoff supplied the memorable *line*, but he did not coin "the error of the third kind" — Allyn Kimball did, in 1957; Raiffa discussed it in 1968 while misattributing it to Tukey; Mitroff and Featheringham, in 1974, tied it to problem formulation, which is where the concept belongs for us. The Wayback lesson and the meta-lesson coincide: getting the *problem* right includes getting its *history* right. A chapter that championed solving the right problem while carelessly repeating the modal (wrong) attribution would have committed, in miniature, the very error it warns against. Formulation is the defense against being exactly right about the wrong thing — including, recursively, about who said what.

---

## Exercises

These constitute the basis of **Supervision Lab Exercise #4 (25 pts)** and **Supervision Lab Exercise #5 (25 pts)**. Each names a judgment call the Assessment Spine requires you to surface.

**Exercise 7.1 — Three distinct reframings of your capstone problem (Create).** Produce three reframings of your capstone problem and prove their distinctness: for each pair, identify a solution that would pass one and fail the other. If you cannot find such a solution for some pair, that pair is not distinct — revise until all three genuinely disagree about what counts as success. Deliverable: three reframings, each with its test-by metric, plus the pairwise distinctness demonstration. *The judgment call to name: certifying distinctness required your grounded model of what "a different solution" means in your domain — name the knowledge that certification rested on.*

**Exercise 7.2 — Constraint-set evaluation and defended selection (Evaluate).** Build a constraint-set table (including at least one salience constraint and one values/whose-interests constraint, not only feasibility) and score your three reframings against it. Select one. Defend the selection on *both* analytical grounds and values grounds, and explicitly name the interests your selected framing decenters. Deliverable: the scored table plus the dual defense with decentered interests named. *The judgment call to name: the selection centered some interests over others — name whom you chose not to serve and why you are accountable for that choice.*

**Exercise 7.3 — The Assessment Spine for the formulation (Create). [Track 2]** Write the Assessment Spine statement for this formulation: state the one judgment call in selecting your reframe that required *your* values or domain knowledge, and explain specifically why it could not have been delegated to a model. Deliverable: a focused statement (roughly 150–200 words). *The judgment call to name: this is the spine itself — distinguish a genuine values/knowledge judgment from a feasibility call the model could have made, and defend why yours is the former.*

## Chapter Closing / Bridge

You have chosen the problem worth solving — generated three framings that genuinely disagree about success, scored them against a constraint set that refuses to reward mere tractability, selected one, and named the interests you decentered in doing so. You have also seen that the values decision lives *inside* the formulation, not after it, and that this is precisely why the selection cannot be handed to a model: certifying distinctness and choosing whose interests to center are accountable acts requiring situated judgment and a name on the decision.

Now the tools run. With the right problem chosen, the next capacity governs *how the solving actually happens* — which tool, in which order, with which handoff verified. Selecting and sequencing tools is not a clerical step downstream of the real thinking. It is itself a supervisory decision, with its own failure modes, its own discipline, and its own way of laundering an unverified output into a trusted one if you let the handoffs go silent.

## Sources

- Ackoff, Russell L. *Redesigning the Future: A Systems Approach to Societal Problems.* Wiley (1974), p. 8. Source of the "wrong problem" quote (full sentence: "Successful problem solving requires finding the right solution to the right problem. We fail more often because we solve the wrong problem than because we get the wrong solution to the right problem.").
- Kimball, Allyn W. "Errors of the Third Kind in Statistical Consulting." *Journal of the American Statistical Association* 52(278), 133–142 (1957). Coinage of "error of the third kind" ("the error committed by giving the right answer to the wrong problem"). JSTOR 2280840.
- Raiffa, Howard. *Decision Analysis: Introductory Lectures on Choices under Uncertainty.* Addison-Wesley (1968). [Discusses the error; misattributes to Tukey.]
- Mitroff, Ian I., and Tom R. Featheringham. "On Systemic Problem Solving and the Error of the Third Kind." *Behavioral Science* 19(6), 383–393 (1974). [Ties the Type III error to problem formulation — the concept's home for this chapter.]
- Mitroff, Ian I., and Abraham Silvers. *Dirty Rotten Strategies* (2009). [Optional: extends to a "Type IV error"; verify before use.]
- Schön, Donald A. *The Reflective Practitioner.* Basic Books (1983). [Carries from Chapter 6: "naming and framing."]
