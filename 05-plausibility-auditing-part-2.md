# Chapter 5 — Plausibility Auditing (Part 2: Audit First)

Here are five AI outputs. Audit them.

That is the assignment, and it arrives before the instruction — deliberately, and against the grain of how courses usually work. You have not yet been taught a protocol. You are not going to be handed a checklist first and then asked to apply it. You are going to do the thing, badly and uncomfortably, and then we are going to look at what happened in your own audit and name it. The discomfort is not an accident of sequencing. It is the instrument.

The reason is that the capacity you are building runs on knowledge you mostly cannot articulate. If we taught you the protocol first, you would apply the protocol and learn nothing about the tacit model underneath it. By forcing the audit before the framework, we surface two things at once: what your domain knowledge already lets you catch without being told how, and — just as important — the precise edge where your knowledge runs out and you are auditing blind. Both are findings. The second one is the seed of everything the rest of this book builds toward.

So before you read another word of method, do the audit. Read each of the five outputs below. For each, decide *before consulting any source*: does this need verification, and if so, what exactly should the verification look for? Write your verdicts. Then come back.

**Output A (clinical).** A discharge summary for an elderly patient with documented chronic kidney disease. It is complete, well-organized, clinically fluent — and it includes a standard adult dose of a renally-cleared medication.

**Output B (legal).** A brief that cites a real, locatable case as authority for a particular holding. The citation format is impeccable. The case exists.

**Output C (analyst).** A regression output predicting customer churn. The model summary reports an R² of 0.97.

**Output D (logistics).** A routing plan that minimizes total miles across a delivery network. Mathematically optimal. The plan assigns a 53-foot trailer to a delivery stop.

**Output E (engineering).** A structural load calculation, internally consistent, every unit carried correctly through every line, arriving at a clean final number.

Write your five verdicts now. Then continue.

## The Audit-First Protocol

You have just done the thing the protocol describes; now we can name what you did. The protocol has exactly one inviolable rule, and it is the one most likely to be broken: **render the verdict and name the mechanism before any lookup is permitted.** The moment you open a database, a reference, or a second tool, you have left the audit and entered verification — and you can no longer claim the audit caught anything, because you no longer know whether your grounded model fired or whether the source did the work.

A complete audit of a single output produces three things, in this order:

1. **A verdict** — does this require verification, yes or no?
2. **A target** — if yes, what specifically should the verification hunt for? "Check the whole thing" is not a target; it is an abdication.
3. **A mechanism** — *why* did this output draw your attention, or fail to? Domain-grounded pattern recognition, or anomaly detection against a held model?

The third item is the one that separates auditing from lucky guessing, and it is where the grading bites hardest. A correct verdict with no named mechanism earns no credit in this course. That is not pedantry. A verdict you cannot explain is one you cannot teach, cannot defend to a skeptic, and — most damning — cannot trust yourself, because you have no way to know whether you reasoned or merely reacted.

## Reading the Five Outputs

Walk back through the five with the mechanisms named, and watch how the audit fires differently in each.

**Output A, the discharge summary, fires anomaly detection against a mental model.** Nothing about the dose is wrong in general — it is a perfectly standard adult dose, which is exactly why a fluency check sails past it. The audit fires because you hold, tacitly, a constraint: renal clearance governs the safe dose of this drug, and this patient's documented kidney disease means the standard dose assumes a clearance the patient does not have. The output is in distribution. It violates a held boundary of the specific case. Verdict: verify. Target: confirm the dose against the patient's renal function, not against the drug's general dosing table.

**Output B, the legal brief, fires domain-grounded pattern recognition.** The trap here is subtle and worse than a fabricated citation, because the case is real. The failure is that the case is cited for a holding it does not contain — it is about jurisdiction, say, and it is being offered for a point about the merits. A fluency check passes it instantly: real case, correct format, confident sentence. The audit fires because the *shape* is wrong — "I know roughly what that line of cases stands for, and it isn't this." Verdict: verify. Target: read the holding, not the citation.

**Output C, the churn regression, fires anomaly detection — on the implausibly good fit.** An R² of 0.97 in a messy behavioral domain like churn is not a triumph; it is a tell. Real human behavior does not predict that cleanly, and an analyst with a grounded model of the domain feels the number as *too good* — the classic signature of data leakage or a target that has been contaminated with information from the future. The naïve reader celebrates. The auditor's stomach drops. Verdict: verify. Target: hunt for leakage; check what's in the feature set that wouldn't be available at prediction time.

**Output D, the routing plan, fires anomaly detection against an operational constraint.** The plan is optimal on the math and violates a fact about the physical world: a stop that cannot physically receive a 53-foot trailer. This is the most purely tacit of the five — the constraint lives in operational experience, not in any document the model had access to. Verdict: verify. Target: confirm trailer-length feasibility at every assigned stop.

**Output E, the load calculation, is the one designed to teach humility.** It may be entirely correct. Internal consistency and correct unit propagation are real, if weak, evidence. But they are evidence of *coherence*, not of *groundedness in the actual structure* — the calculation can be flawless and built on a span length or a material property that doesn't match the thing being built. The honest audit here may be: "I cannot fully audit this without the as-built drawings; what I can confirm is internal consistency, and that is not enough." That is a legitimate, gradeable verdict. Knowing the limit of your audit is part of the audit.

| Output | Verdict | Mechanism | What it surfaced | Verify? |
|---|---|---|---|---|
| A — discharge summary | Suspect | Anomaly vs. model (renal clearance) | Dose assumes normal clearance | Yes — against patient's renal function |
| B — legal brief | Suspect | Pattern recognition (doctrine shape) | Real case, wrong holding | Yes — read the holding |
| C — churn regression | Suspect | Anomaly vs. model (too-clean fit) | R² implausible for domain | Yes — hunt for leakage |
| D — routing plan | Suspect | Anomaly vs. operational constraint | Trailer can't reach stop | Yes — confirm feasibility |
| E — load calc | Indeterminate | Limit of audit reached | Coherence ≠ groundedness | Partial — need as-builts |

## The Fluency Trap Under Live Conditions, and the Literature Behind It

At least one of those five outputs was engineered to be maximally fluent and subtly, domain-specifically wrong — so that if you waved it through, you would feel the fluency trap from the inside rather than merely reading about it. That is the most valuable thing that can happen in this exercise, because it is not a personal failing. It is a documented and robust feature of how humans interact with automation.

The construct is **automation bias**: the tendency to over-trust automated output, to treat it as a heuristic shortcut, and to reduce one's own vigilance accordingly. It was first characterized in aviation in the 1990s and 2000s — Mosier, Skitka, and colleagues showed that operators following automated cues commit both *omission* errors (missing a problem the automation didn't flag) and *commission* errors (acting on an automated recommendation against contrary evidence). [High] Parasuraman and Manzey's 2010 integrative review in *Human Factors* is the standard synthesis of the mechanism: humans ascribe high authority to automation and lean on it as a substitute for their own monitoring. [High] That is the fluency trap, named and measured decades before large language models existed, and the 2024–2026 literature confirms the construct transfers cleanly to AI outputs.

It is worth being precise about what good auditing produces, because the goal is not maximal suspicion. Lee and See's 2004 paper, also in *Human Factors*, frames the target as **calibrated trust**: reliance should match actual trustworthiness. [High] Both failure directions are real. Over-reliance — using output you should have checked — is *misuse*. Under-reliance — refusing to use output that is in fact sound — is *disuse*, and it wastes the genuine capability you are supervising. Picture a graph with your trust on one axis and the output's actual trustworthiness on the other. The diagonal is calibration. Automation bias lives above the diagonal; reflexive distrust lives below it. The audit is the mechanism that moves a professional toward the diagonal.

![Two-axis plot with the output's actual trustworthiness on the horizontal axis and the auditor's trust on the vertical axis; a red diagonal marks calibration, the region above it is labeled MISUSE (over-reliance / automation bias) and the region below DISUSE (under-reliance), with an arrow showing the audit pulling an over-trusting point down toward the diagonal.](images/05-plausibility-auditing-part-2-fig-01.png)

*Figure 5.1 — Calibrated trust is the diagonal where trust matches trustworthiness; over-reliance (misuse) lives above it and reflexive distrust (disuse) below, and the audit's job is to move you toward the line.*

Two cautions the evidence specifically supports. First, the model telling you it is "95% confident" is not a substitute for your audit — and may make your calibration *worse*. At least one controlled study found that transparency about the system's reasoning improved appropriate reliance while confidence displays did *not*. [Medium — single-study, cite carefully] In this course's labs, you will generally audit without seeing the model's self-reported confidence, on purpose. Second, and this is the frame to carry forward: the audit-first protocol is not a novel invention of this book. It is a **trained debiasing intervention** against automation bias — a deliberate procedure that interrupts the heuristic substitution the human-factors literature has documented for thirty years. That is a strength, not a weakness. You are not being asked to trust a clever new trick; you are being trained out of a well-mapped cognitive failure.

## Documenting the Mechanism, Not Just the Finding

The grading rubric in this course rewards the *mechanism*, not the catch. This is the single design decision that makes the labs teach the capacity rather than reward intuition. Consider two students who both flag Output A's dose. The first writes: "The dose looks wrong." The second writes: "This is a renally-cleared drug; the patient has documented CKD; the dose assumes normal clearance — anomaly detection against the clearance constraint, not pattern-matching, because the dose is normal *in general* and only wrong *for this patient*."

The first student may have caught it by luck, by vague unease, or by having seen the answer key. The second has demonstrated a transferable, defensible capacity — and, critically, has located the audit's dependency. They now know that this finding required knowing the drug's clearance route and the patient's renal status. Strip either piece of knowledge away and the audit goes silent. That is the boundary the next deliverable forces you to map.

## The Honest Limit: Polanyi and the Edge of the Audit

Why can't the model just be told all of this? Why is the audit irreducibly yours?

The answer is the philosophical spine of this entire book, and its cleanest statement is Michael Polanyi's, from *The Tacit Dimension* (1966): **"we can know more than we can tell."** [High] Note the auxiliary verb — *can* — and do not drop it, as many quotations do. Polanyi's claim is not that we happen to know some things we haven't gotten around to saying. It is stronger: there is knowledge we *cannot fully tell*, even in principle, because it lives in our capacity to recognize and to act rather than in any set of explicit propositions. You know a face in a crowd without being able to specify the features that identify it. The logistics manager knows the dock cannot take the trailer without ever having written that constraint down.

The grounded model your audit runs against is largely this kind of knowledge. And that is exactly why no prompt can transfer it to the model. You cannot prompt into a system the knowledge you cannot fully articulate to yourself. The asymmetry between solving and verifying does not close as models improve, because the verification draws on a kind of knowing that is, by Polanyi's argument, non-transferable by construction. (Donald Schön's *The Reflective Practitioner* (1983) is the natural companion here: his "knowing-in-action" is Polanyi's tacit knowledge made professional and observable — the practitioner reading a situation in real time. We will draw on Schön directly when we reach problem formulation.)

This is also why the audit has an *edge*, and why naming that edge is a graded act rather than an admission of weakness. Your tacit model is rich in your home domain and thin or absent outside it. The honest auditor does not pretend otherwise. On Output E, the most defensible verdict named the limit: coherence confirmed, groundedness not auditable without the as-builts. Marking where your audit cannot reach is not a failure of the audit. It is the most supervisorily mature thing the audit produces — and it is where, in the final chapter of this book, the Gap Account begins.

---

> ### AI Wayback Machine: Polanyi and the Tacit Dimension (1966)
>
> **Michael Polanyi, *The Tacit Dimension.* University of Chicago Press (1966).** The line is "we can know more than we can tell," and the *can* is load-bearing. Polanyi, a chemist turned philosopher, argued that the foundation of skilled knowing is tacit — a capacity to recognize and to act that cannot be exhaustively reduced to explicit rules. We recognize a face, ride a bicycle, and read a situation by drawing on knowledge we hold but cannot fully state.
>
> The Wayback lesson is the keystone of plausibility auditing. The grounded domain model your audit runs against is precisely this tacit kind of knowledge — which is why it cannot be prompted into a model that lacks it, and why the audit remains irreducibly human as capability scales. The solve-verify asymmetry is not a temporary gap awaiting a better model. It rests on a structural fact about knowledge that Polanyi named sixty years before the systems you supervise existed. (His earlier *Personal Knowledge*, 1958, develops the tacit/explicit distinction at length.)

---

## Exercises

These constitute the basis of **Supervision Lab Exercise #2 (25 pts)** and **Supervision Lab Exercise #3 (25 pts)**. Each names a judgment call the Assessment Spine requires you to surface.

**Exercise 5.1 — Audit five outputs, mechanism required (Apply).** For five provided outputs, render for each: the necessity-of-verification verdict, the named target, and the mechanism (pattern recognition vs. anomaly-against-model). No lookups before the verdict. Deliverable: the five-row audit table on the model shown above. *Grading note: a correct verdict with no named mechanism earns zero credit.* *The judgment call to name: for each finding, what specific knowledge made it possible — and would a competent generalist in an adjacent field have caught it?*

**Exercise 5.2 — Audit a capstone-domain output and document the model (Apply).** Take a real AI output from your capstone domain. Audit it before any verification, then document — in prose — the grounded model you audited *against*: the patterns, constraints, and tacit facts your audit drew on. Deliverable: the output, the audit verdict and target, and a paragraph reconstructing the model behind it. *The judgment call to name: which parts of that model could you actually write down, and which are tacit in Polanyi's sense — knowable but not fully tellable?*

**Exercise 5.3 — Name what your audit could not reach (Evaluate). [Track 2]** For the same capstone output, name explicitly: one finding your domain knowledge made possible, and one thing your audit *could not reach* — a place where you lacked the grounded model to fire, and where an expert in a neighboring specialty would have caught something you could not. Deliverable: two named items with reasoning. *The judgment call to name: this is your first Gap Account in embryo — take responsibility, in writing, for the limit of your own audit rather than concealing it.*

## Chapter Closing / Bridge

You can now audit what is in front of you. You can render a verdict before reaching for a source, name the mechanism that fired, recognize the fluency trap as a documented cognitive bias rather than a personal lapse, and — hardest and most valuable — mark the edge where your tacit model runs out.

But there is a deeper failure mode that no amount of auditing skill defends against, because it operates one level up. You can audit an output flawlessly and still be auditing the *wrong problem* with perfect rigor — verifying, with great care, an answer to a question that was never the one that mattered. A perfect audit of a well-solved but wrongly-framed problem is still a wasted audit. That is where the next capacity lives. Before you audit the answer, someone has to have chosen the question — and that choice, it turns out, is the one an AI can fluently produce and cannot originate.

## Sources

- Polanyi, Michael. *The Tacit Dimension.* University of Chicago Press (1966). [Canonical line: "we can know more than we can tell."]
- Polanyi, Michael. *Personal Knowledge: Towards a Post-Critical Philosophy.* University of Chicago Press (1958).
- Parasuraman, Raja, and Dietrich Manzey. "Complacency and Bias in Human Use of Automation: An Attentional Integration." *Human Factors* 52(3), 381–410 (2010).
- Lee, John D., and Katrina A. See. "Trust in Automation: Designing for Appropriate Reliance." *Human Factors* 46(1), 50–80 (2004).
- Mosier, Kathleen L., and Linda J. Skitka. Work on automation bias in aviation (1990s–2000s). [Origin of the "automation bias" construct.]
- Goddard, K., et al. "Automation Bias: A Systematic Review." *JAMIA* (2012). PMC3240751. [For quantified frequency/mitigator claims.]
- Schön, Donald A. *The Reflective Practitioner: How Professionals Think in Action.* Basic Books (1983). [Companion source: "knowing-in-action."]
- Klein, Gary. *Sources of Power: How People Make Decisions.* MIT Press (1998). [Optional companion: recognition-primed decision (RPD) making — experts acting by pattern recognition rather than formal option comparison.]
