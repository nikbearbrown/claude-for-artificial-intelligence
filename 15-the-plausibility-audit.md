# Chapter 15 — The Plausibility Audit

You submit before you read anything.

That is the instruction, and it is deliberate. There is no preparatory lecture for this chapter, no warm-up case, no reassuring framework delivered first. You take the Supervisory Analysis you revised in the dress rehearsal — the one you believe is sound, the one a peer has already heard — and you hand it to Claude, instructed to function as an adversarial Plausibility Auditor. Then you watch it go to work on the document you signed your name to.

The auditor applies the five-capacity framework against you, adversarially. It hunts undocumented handoffs where a tool's output acquired authority it never earned. It hunts defaulted formulations where you let the common-and-likely framing stand instead of reframing toward the salient. It hunts interpretive judgment that diagnoses a legitimacy gap and never fills it. And it hunts the thing you were warned about all through Act Two: integration sections that *sequence* rather than integrate — five capacities narrated in a row with no documented re-engagement, a synthesis with a bow on it.

If you did the work in Chapters 13 and 14 — if you killed the three failure modes in your self-audit and survived the dress rehearsal — the auditor will not find the obvious things. It will reach for something more specific. And that reaching is exactly where the final learning of the course happens, because it forces the question this whole book has been building toward: *what can this auditor, by its nature, never find?*

## The Adversarial-Auditor Architecture

Picture the loop. You submit. Claude, prompted as the Plausibility Auditor, returns a numbered set of findings, each naming a capacity, a location, and an alleged failure. You then do something the auditor cannot do to itself: you **evaluate each finding** as a genuine failure or a false positive, with reasoning. You revise where the findings are genuine, defend where they are false positives, and then — the graduation move — you write the **Gap Account.** The human is the final node in the loop. You evaluate the evaluator.

![Diagram with a cyclic submit-findings-evaluate-revise loop on the left, the human marked as the final node, and on the right a target whose outer ring of contingent misses a better auditor could close but whose red center — the structural blind spot of situatedness, stake, and accountability — the Gap Account points to as out of reach.](images/15-the-plausibility-audit-fig-02.png)

*Figure 15.2 — The audit loop lets a better auditor close contingent misses, but the Gap Account names the structural blind spot — situatedness, stake, accountability — that no model removes.*

The whole architecture is newly possible because capable auditor models now exist. That is the "why now" of the entire course. But the same capability that makes the auditor useful makes it dangerous to over-trust, and the chapter insists you hold both at once.

## The Auditor Is a Capable Adversary, Not an Oracle

Three misconceptions will wreck a student here, and the contemporary evidence dismantles all three.

**"A clean audit equals an A."** It does not. Carry Popper forward from Chapter 14: surviving the audit is *corroboration, not proof.* The auditor finding nothing means only that this auditor, this time, did not refute you. The graduation condition of this course is not a clean audit. We will return to this; it is the spine of the chapter.

**"The auditor is the authority; if it finds nothing, I am done."** No — the auditor's silence is not proof, and the auditor is gameable. LLM judges are vulnerable to prompt-injection attacks against the judging architecture itself; reported attack-success rates in 2025 studies vary widely with the setup, spanning roughly the low-double-digits to the seventy-percent range depending on configuration (one study reports a comparative-undermining attack exceeding 30%; another reports success rates up to roughly 74% against some judges) [High that the vulnerability is documented; cited as a range, not a single number]. An impressive auditor is still not an oracle.

**"Every auditor finding is a real failure."** Also no — and *uncritically accepting findings is itself a supervisory failure.* LLM-as-judge systems carry documented, reproducible biases: **self-preference** (favoring outputs that resemble their own style), **position bias** (the order in which options are presented shifts judgments measurably — in pairwise judging, swapping presentation order alone can move accuracy by more than ten percentage points), and **verbosity bias** (longer answers scored higher regardless of quality) [High that these biases are documented; magnitudes stated as ranges]. These biases manufacture *false positives* — findings that are artifacts of the auditor's machinery, not flaws in your work. Catching and rebutting them is the genuine-versus-false-positive evaluation, and it is graded. The same skill you rehearsed against peers in Chapter 14 — revise, defend, acknowledge — you now perform against the machine.

So you approach the auditor exactly as you would approach a brilliant, tireless, slightly self-regarding reviewer who occasionally invents problems and can be tricked: take it seriously, and do not believe it on authority.

## Genuine Failure or False Positive

For each finding, the disciplined output is a row in a table: *the finding / is it located? / genuine failure or false positive / reasoning / action.*

A **genuine failure** is one where the auditor's reading is correct and the evidence is where it says. You revise, and you log it. A **false positive** is one where the auditor misread the evidence — pointed at a handoff and called it undocumented when the trust decision is stated, or flagged §5 as sequencing when the Re-engagement Log contains exactly the trigger it claims is missing, or down-scored a section for brevity in a way that smells of verbosity bias. You defend, with the located evidence the auditor missed, and you log that too. The discipline is symmetric: an unexamined acceptance is as much a failure as an unexamined rejection.

Before you read the audit, close the loop from Chapter 14: take your three predicted findings and mark, for each, whether *you* think it will turn out genuine or false. Then read. The gap between your prediction and the auditor's actual findings — and between your genuine/false guesses and your considered evaluations — is calibration data. It is the dress rehearsal's prediction scorecard, completed.

## The Gap Account — The Whole Point

Now the graduation move. The **Gap Account** is a written account of at least one failure mode the auditor **could not detect** — and a specific explanation of *why* detecting it required human supervisory judgment no prompt can supply.

Everything turns on a distinction, and it is the hardest and most important one in the course: the difference between a **contingent miss** and a **structural blind spot.**

A contingent miss is something the auditor *happened* not to find this time — a flaw it could have caught with a better prompt, a different run, a sharper model. Naming a contingent miss is a weak Gap Account, because the gap is fixable; a better auditor closes it. That is not the irreducibly-human move. That is just a bug the next version patches.

A structural blind spot is something the auditor **cannot reach by its nature** — not this auditor, not a better one, not any auditor — because reaching it would require something the auditor structurally lacks. Naming *that*, from inside your own work, with the *why*, is the Gap Account that graduates you.

So what is structurally out of reach? The contemporary safety literature gives the first layer of the answer, and the philosophy gives the second.

The empirical layer: **correlated failure modes.** When an auditor and the system it audits share architecture and training, their errors correlate — and an auditor cannot catch a blind spot it shares [High; this is the strongest contemporary grounding for the Gap Account]. The clean current example is "the same AI writes the implementation and the tests": the tests pass, the bug ships, because the evaluator and the evaluated are blind in the same place [High]. This is more than a tuning problem. It says that AI-evaluating-AI has a structural ceiling wherever the two share their blind spots — and a fix that makes the auditor more capable in the usual way may make it *more* correlated, not less.

But correlated error is still, in principle, reducible — use a differently-trained auditor and some of the overlap shrinks. The Gap Account needs a limit that does not shrink. That limit is philosophical, and it is where the book's namesake ancestor arrives.

### AI Wayback Machine — Hubert Dreyfus, *What Computers Can't Do* (1972; rev. 1979; *What Computers Still Can't Do*, 1992)

> *Figure 15.1 — The structural blind spot.*
>
> In 1972, the philosopher Hubert Dreyfus published *What Computers Can't Do: A Critique of Artificial Reason.* Drawing on Heidegger, Merleau-Ponty, and Wittgenstein, he argued that human intelligence rests on an informal, largely unconscious, *embodied and situated* background of skilled coping — know-how that cannot be fully captured in explicit rules or symbols. Time vindicated much of the critique [High].
>
> **One mismatch you must not paper over.** Dreyfus's target was *symbolic GOFAI* — the rule-and-representation program of the Newell–Simon–Minsky era. The auditor in this chapter is an *LLM*: a statistical, connectionist system, the very kind of approach Dreyfus's own Heideggerian sympathies treated as *more* promising than symbol manipulation. So "Dreyfus refuted the LLM auditor" is **not** a clean syllogism, and a careful reader will catch you if you imply it. Dreyfus's argument was against *rules*; LLMs are not rule-based [High for his thesis; the GOFAI-vs-LLM mismatch is real and must be named].
>
> Build the Gap Account on Dreyfus's **positive** doctrine instead, not his negative target. The usable claim is not "the auditor follows rules and rules can't capture intelligence." It is: the auditor has **no world to be situated in.** It has no body, no embodied background of coping, and — the addition this book makes its own — **no stake and no accountability.** It will not sign your recommendation. It will not answer for the consequences when the analysis leaves the screen. It has no situated relationship to the specific humans your decision affects. That is the structural limit, and it does not shrink with a better model, because it is not a capability gap. It is an *ontological* one. [High for the thesis; the routing through situatedness/stake/accountability is the chapter's required handling.]

## Where the Gap Lives: Through Chapter 10's Legitimacy Types

To keep the Gap Account rigorous rather than hand-wavy, route it through the apparatus you already built. In Chapter 10 you learned Suchman's three legitimacy types: **pragmatic** (does it work, efficiently), **moral** (is it aligned with human values), and **cognitive** (is it transparent and trustworthy). The auditor can assess pragmatic legitimacy — it can check whether your reasoning hangs together, whether your workflow is documented, whether your claims are internally consistent. What it cannot supply, and cannot fully *verify*, is **moral legitimacy grounded in a specific human context that you inhabit and are accountable for.** The auditor can flag *that* a moral-legitimacy account is missing — that is a contingent, fixable observation. It cannot weigh whether your situated moral judgment is *right*, because rightness here turns on a stake in the specific situation that the auditor does not have.

That is the philosophically cleanest Gap Account, and it does not over-rely on Dreyfus: it routes through the book's own Chapter 10 machinery [Medium-High]. Three archetypes, to give you patterns rather than a fill-in template:

1. **Situated moral legitimacy.** A stakeholder consequence visible and weighable only from inside your accountability relationship — a community you personally answer to, whose harm the equity tool can score but whose *standing* to veto only you can grant. The auditor notes the absence; it cannot weigh the presence.
2. **Tacit domain anomaly.** A "this number is fine but feels wrong for *this* site" judgment grounded in embodied domain experience — the Polanyi tie-in from Chapter 5, *we know more than we can tell.* The auditor lacks the tacit model, so it cannot have the intuition or check it.
3. **Accountability asymmetry.** You will sign and bear the consequences; the auditor will not. A judgment that turns on *who is on the hook* is structurally outside its reach, because having no stake is not a deficiency it can be prompted out of.

A strong Gap Account names one of these *from inside your own analysis* — the specific judgment, in your specific document, on your specific problem — and explains why detecting it required exactly the situated, accountable human capacity the auditor structurally cannot have. A weak Gap Account names a flaw the auditor merely happened to miss. The difference between those two is the difference between passing and graduating.

## Why the Gap Account Is the Proof-of-Concept of the Whole Course

This is the terminal expression of the solve-verify asymmetry. The auditor *solves* — it finds plausible flaws fast, tirelessly, adversarially. You *verify the auditor* — genuine or false positive — and then you name the gap the solver structurally cannot reach. The Gap Account is the asymmetry made personal: proof, from inside your own work, that there was supervisory work only a situated, accountable human could do.

And it is why **a clean audit is explicitly not the graduation condition.** Here the two ancestors of Act Three interlock. Popper (Chapter 14): a clean audit is corroboration, not proof — the absence of refutation is not the presence of truth. Dreyfus (Chapter 15): the auditor has a structural limit, so there are flaws it could never find regardless of how clean its report. Put them together and the conclusion is forced: a clean audit *cannot* be the graduation condition, because a clean audit is both provisional (Popper) and blind in a fixed region (Dreyfus). What graduates you is the Gap Account — the thing the auditor, by its nature, could not have written. The course's whole thesis is compressed into that asymmetry: the human is for the work the machine cannot do, and the Gap Account is you doing it, on the record.

## The Week 1 Inventory Returns

In Week 1 you built a personal AI-usage inventory: your current practice classified by level, the supervisory gap at each stage. It has been waiting for you. Open it now.

The closing reflection asks you to name **three specific judgment calls you now make that you would have delegated, deferred, or missed at the start.** Not "I am more careful now." Not "I think harder about AI outputs." *Specific.* Named. Located in your own practice. *I now reframe before I prompt, because in the Week-1 inventory I see I let the tool's framing stand on the budget analysis that went wrong. I now run a cross-audit with a differently-failing tool, because I see where I once trusted a single chain end to end. I now write a legitimacy account in my own voice, because I see where I once signed the AI's pragmatic case as if it were my judgment.* Three of those. The inventory from Week 1 is the control condition; you are the experiment; the reflection is the measurement.

This is the conductorless orchestra closing. In Chapter 1 you confronted five competent professionals producing plausible, confident, wrong outputs, and you could not yet name what was missing. What was missing was the conductor. You are now the conductor — and the Gap Account is your proof, written from inside your own performance, that the role is real and that you can fill it.

## Where This Leaves You — and the Honest Limit

One last honesty, owed to a course built on honesty. The auditor drifts between model versions; it is gameable; its false-positive rate against real Supervisory Analyses has not yet been measured at scale; the auditor prompt and rubric are still being calibrated. The course does not pretend the auditor is a settled, validated instrument. That, too, is a supervisory lesson: you are learning to use an impressive tool precisely *without* over-trusting it, which is the entire competence this book set out to build. The auditor's imperfections are not a flaw in the assessment. They are the final demonstration of why a human must be the last node in the loop.

## Exercises

**Exercise 15.1 — The full audit (Apply).** Submit your revised Supervisory Analysis to Claude as the adversarial Plausibility Auditor. For every finding, complete the evaluation table — located? / genuine failure or false positive / reasoning / action — and revise or defend accordingly. At least one finding should be defended as a false positive, with the auditor's likely bias (self-preference, position, verbosity) named where it applies. *(Deliverable: the audit transcript, your per-finding evaluation, and the revised analysis. Part of the **250-point Final Submission.**)*

**Exercise 15.2 — The Gap Account (Create).** Write the Gap Account: name at least one failure mode the auditor **structurally** could not detect — not a contingent miss — and explain, with reference to your own specific analysis, why detecting it required situated, accountable human judgment no prompt can supply. Route the explanation through one of the three legitimacy types (Chapter 10) and one of the three archetypes (situated moral legitimacy, tacit domain anomaly, accountability asymmetry). State explicitly why this is a structural blind spot and not a bug a better auditor would fix. *(Deliverable: the Gap Account, ~600–900 words. This is the graduation condition. Part of the 250-point Final Submission.)*

**Exercise 15.3 — Closing reflection: the inventory returns (Evaluate).** Return to your Week 1 AI-usage inventory. Name three specific judgment calls you now make that you would have delegated, deferred, or missed at the start. Each must be concrete, located in your own practice, and tied to a specific line in the original inventory. Then complete the prediction scorecard from Chapter 14: which of your three predicted findings were genuine, which were false positives, and what the gap between prediction and reality taught you about your own calibration. *(Deliverable: the closing reflection plus the completed scorecard. Part of the 250-point Final Submission. This is the Assessment Spine of the entire course, turned on yourself: the proof that the supervision was real and that it changed how you work.)*

## Chapter Closing — The Performance Ends

The course closes where it opened. In Chapter 1 the orchestra had no conductor, and five capable players produced a performance that fell apart at the seams nobody was watching. You now hold all five capacities at once, you can prove it under an adversary that does not tire, and — the part no algorithm can take from you — you can name, from inside your own work, the one judgment the adversary could never reach, because reaching it required a body, a context, and a stake.

The graduation condition was never the clean audit. A clean audit is corroboration, not proof, and it is blind in a region no improvement removes. The graduation condition is the Gap Account: the irreducibly-human move, made operational, signed by you. You came in able to operate the instruments. You leave able to conduct — and to prove the conducting was real to something that was actively looking for the proof to be false.

## Sources

- Dreyfus, Hubert L. *What Computers Can't Do: A Critique of Artificial Reason.* Harper & Row, 1972; rev. 1979. Reissued and expanded as *What Computers Still Can't Do: A Critique of Artificial Reason.* MIT Press, 1992.
- Dreyfus, Hubert L., and Stuart E. Dreyfus. *Mind over Machine.* Free Press, 1986. (The five-stage skill model; tacit expertise; offered as supplement.)
- Polanyi, Michael. *The Tacit Dimension.* Doubleday, 1966. (Carried from Chapter 5 for the tacit-anomaly archetype.)
- Suchman, Mark C. "Managing Legitimacy: Strategic and Institutional Approaches." *Academy of Management Review* 20, no. 3 (1995): 571–610. (Carried from Chapter 10; the rigorous home for the moral/cognitive Gap.)
- Popper, Karl R. *Conjectures and Refutations.* Routledge & Kegan Paul, 1963. (Carried from Chapter 14; corroboration ≠ proof.)
- On LLM-as-judge bias (self-preference, position, verbosity): documented in the 2024–2026 evaluation literature (e.g., arXiv:2410.21819 on self-preference; the IJCNLP 2025 position-bias study across many judges). Cite as ranges.
- On correlated/shared failure modes between evaluator and evaluated: the 2025 AI-safety literature (e.g., arXiv:2510.11235), including the "same AI writes implementation and tests" result.
- On prompt-injection vulnerability of LLM judges: 2025 studies (e.g., arXiv:2504.18333; arXiv:2505.13348). Cite attack-success as a range.

*[Editorial note] Magnitudes from the 2024–2026 LLM-as-judge literature have been verified and are cited as ranges, not single numbers: position-bias accuracy swings exceeding ten points (e.g., the 2025 position-bias study across many judges), and prompt-injection attack-success rates spanning roughly 30% to ~74% depending on configuration (arXiv:2505.13348; arXiv:2504.18333). Self-preference, position, and verbosity biases are documented phenomena (e.g., arXiv:2410.21819). The auditor's false-positive rate against real Supervisory Analyses is unmeasured (TIKTOC V04 / Risk 2); the chapter describes the architecture honestly but claims no calibrated reliability. The Dreyfus GOFAI-vs-LLM mismatch is handled in text: the Gap Account rests on situatedness/stake/accountability and the Chapter 10 legitimacy types, not on "the auditor follows rules."*
