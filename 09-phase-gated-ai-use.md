# Phase-Gated AI Use

*Keep your judgment in the loop by design, not by willpower.*

In February 2024, Klarna announced that its new AI customer-service assistant had, in its first month, handled 2.3 million conversations — about two-thirds of the company's chat volume — doing "the equivalent work of 700 full-time agents." Resolution time fell from about eleven minutes to under two. The company projected a $40 million profit improvement for the year. The story traveled fast, because it was the cleanest version of the thing everyone feared: a number of jobs, stated precisely, replaced by software almost overnight.

Then, in 2025, the company walked part of it back. CEO Sebastian Siemiatkowski told the press the cost-first approach had gone too far — "We focused too much on efficiency and cost" — and Klarna began rehiring human agents into a flexible remote pool for the work the machine handled badly: cases requiring oversight, empathy, contextual interpretation, and nuanced problem-solving. He did not abandon the AI. He continued to claim it had enabled something like a 40% workforce reduction overall. The honest summary is not "AI failed" and not "AI won." It is "the company found the boundary between automatable work and judgment work the expensive way" — by crossing it, noticing the damage, and rebalancing toward a hybrid.

Two cautions before we build anything on this. First, every Klarna figure here — the 700 agents, the 2.3 million chats, the $40 million, the eleven-to-two minutes — comes from Klarna's own press releases and OpenAI's case page, not from any independent audit. Treat them as self-reported, promotional numbers. Second, the story is still moving. The eventual equilibrium — how many humans, doing exactly what — is not settled, and this paragraph will age. [Medium — self-reported; story still in motion]

But notice what Klarna *had* to do to find the boundary. They ran a live, expensive, public experiment on themselves. They had no checkpoint that would have told them, in advance, which two-thirds was safe to automate and which third was not. They discovered the line by stepping over it.

This chapter is about not having to do that. It is about putting the checkpoint *before* the mistake instead of after it — building the boundary into your own daily workflow by design, so that your judgment stays engaged whether or not you happen to feel diligent on a given Tuesday.

## The evidence: why willpower is the wrong tool

Start with a forty-year-old paper that predicted this entire situation. In 1983, the British cognitive psychologist Lisa Bainbridge published a five-page article called "Ironies of Automation." Her central observation is a paradox, and once you see it you cannot unsee it: when you automate the routine parts of a job, you leave the human responsible only for the rare, hard, abnormal cases — exactly the cases that demand *more* skill — while stripping away the routine practice that built that skill in the first place. In her words, "when manual take-over is needed there is likely to be something wrong in the process, so that unusual actions will be needed to control it, and one can argue that the operator needs to be more rather than less skilled." [High — foundational, directly on point]

Bainbridge was writing about industrial control rooms and autopilots, not large language models. But the structure transfers exactly. The better your AI gets at the routine 80%, the more your value concentrates in the abnormal 20% — and the less routine practice you get at the skills the 20% requires. That is the deskilling trap of the previous chapter, restated as a design problem.

The natural response is "I'll just stay vigilant." The research says you won't — not reliably, and not because you're lazy. The study of human-automation interaction has a name for the failure: *automation complacency*. Raja Parasuraman and Victor Riley, in a 1997 paper that mapped the failure modes of automated systems, distinguished *misuse* (over-trusting and over-accepting automation), *disuse* (rejecting it after it errs once), and *complacency* (ceasing to monitor it at all). Monitoring failures, they found, get worse — not better — as the automation becomes more reliable, as workload rises, and as the cues that something is wrong become less salient. [High]

The finding that should change how you think about your own discipline came in 2010. Parasuraman, now with Dietrich Manzey, reviewed the evidence on complacency and concluded that it "is found in both naive and expert participants and cannot be overcome with simple practice." [High] Read that twice. Expertise does not inoculate you. Practice does not fix it. Telling yourself to be more careful does not work, because the failure is not a failure of character — it is a predictable property of how attention behaves around a system that is usually right and very smooth.

And smoothness is the point. Modern AI is conversational, fluent, and confident by default. Fluency is itself a trust cue — the brain reads "easy to process" as "likely to be true," a bias psychologists call the processing-fluency heuristic. So the generative-AI interface is, almost by design, the condition that maximizes complacency: usually right, very smooth, and delivered in the register of competence. The single most reliable trust signal your mind uses is the one the machine is best at faking.

If vigilance can't be willed, what *can* break passive acceptance? Here the evidence narrows to a single, vivid research program, and the confidence drops accordingly. In a 2019 study published in *PLoS ONE* — informally "the lying calculator" — researchers gave participants an on-screen calculator that had been secretly programmed to inflate its answers (in one study by 15%, in another by 120%, plus some answers that were conceptually nonsensical). The core finding: most participants raised few or no suspicions until the answers were grossly, absurdly wrong. Unguided users almost never independently verified anything. [Medium — single research program, robust within it; treat the exact "+15% / +120%" magnitudes and the four-second figure below as values to confirm against the paper before quoting as precise]

Two conditions *did* increase the rate at which people caught the lie, and both are things you can engineer into a workflow:

1. **High numeracy.** Skilled users kept an unassisted mental estimate as a baseline, and flagged answers that landed outside it.
2. **Concrete problem framing.** Real-world, physical scenarios activated real-world schemas and made absurd answers *feel* absurd, where the same error in abstract numbers slid past. (In the studies, a more flagrant injected error — a 120% lie rather than the original 15% — also pushed end-of-study suspicion up sharply, from a few percent to roughly 40%, but only an error that large.) [Medium]

Notice what is *not* on the list — and one of the absences is instructive. The authors also tested a **passive four-second delay** before the calculator displayed its answer, on the theory that a pause would prompt mental estimation. It did *not* significantly increase suspicion, and they dropped it after the first study. [High] The lesson is not that delay is useless; it is that a *passive* pause is not a gate. What protected people was actually producing their own estimate (condition 1) — an action, not a wait. A gate has to force the action, not merely impose the interval. The same research program also found that financial incentives improved accuracy but did *not* increase suspicion or reduce reliance on the tool. Paying people to be right did not make them more skeptical. The triggers that work are structural — a baseline you compute, a concrete framing — not motivational, and not merely temporal.

There is one more honest finding, and it cuts against naïve enthusiasm for "human oversight." A 2024 study on putting a human in the loop found that adding human oversight *increased* the uptake of the automated decision while *decreasing* the accuracy of the final outcome — people adjusted good recommendations into worse ones. [Medium] A checkpoint that becomes a rubber stamp is worse than no checkpoint, because it launders the machine's output through a human's signature without adding any judgment. This is the failure mode every gate in this chapter has to defend against.

![Two parallel pipelines: a real gate forces an action — write your own answer first — before sign-off, while a rubber stamp inserts only a passive pause and signs off, increasing uptake but decreasing accuracy.](images/09-phase-gated-ai-use-fig-02.png)

*Figure 9.1 — A real gate forces an action before acceptance; a rubber stamp only waits, which raises uptake while lowering accuracy.*

## The mechanism: what a gate actually does

Put the pieces together. Complacency is automatic and resists willpower (Parasuraman & Manzey). The triggers that defeat it are specific and structural, not motivational (the lying-calculator program). Therefore the only honest remedy is to build the triggers *into the workflow* rather than relying on yourself to summon them. A phase gate is a designed checkpoint that forces what psychologists call System-2 engagement — slow, effortful, deliberate reasoning — at a moment when System-1 fluency would otherwise wave the output through.

The mechanism is simple. Left alone, you read the fluent AI output, it feels right, and you accept it; complacency does the rest. A gate inserts a step *before* acceptance that you cannot skip without noticing you're skipping it — and that step recreates one of the lying-calculator triggers. Make your own estimate first, and you've installed the numeracy baseline. State the problem in concrete terms, and you've installed the concrete framing. Wait before accepting, and you've installed the delay. The gate doesn't ask you to be more disciplined. It rearranges the work so that the disciplined behavior is the path of least resistance.

This is why gates must be *designed* and not merely intended. The research on levels of automation (Parasuraman, Sheridan & Wickens, 2000) frames it usefully: automation is not on or off — you choose *where* in a process a human stays in control. The four natural insertion points are information gathering, analysis, deciding among options, and acting. A gate is a deliberate choice to keep yourself in control at one of those points, on purpose, regardless of how the rest is automated. [High, as a design vocabulary]

It helps to see the gate against the three modes of AI use the book has been tracking. *Passive acceptance* — read the output, it sounds right, ship it — is the default, and it is the mode that demonstrably degrades capability. *Supervisory* use — staying alert, checking the output — is better, but it leans on exactly the vigilance the complacency research says you can't sustain; it works right up until the day you're tired or rushed, which is the day it matters. *Phase-gated* use is the third mode: it doesn't ask you to supervise harder, it builds the supervision into the task's structure so it happens whether or not you're feeling sharp. The gate is supervisory use made independent of your mood. That independence is the entire reason it's worth the friction — it converts a capacity that fails under pressure into one that holds under pressure, because the pressure can't reach it.

![Three horizontal flow strips from AI output to ship: passive acceptance has no checkpoint and degrades; supervisory use has a vigilance-dependent check that leaks when tired or rushed; phase-gated use has a hard gate the flow cannot bypass, holding under pressure.](images/09-phase-gated-ai-use-fig-01.png)

*Figure 9.2 — The three modes differ only at the acceptance moment: passive ships unchecked, supervisory leaks under pressure, phase-gated installs a gate that can't be bypassed.*

## What it means for you

The previous chapters argued that supervisory judgment, causal reasoning, problem formulation, and accountability are the durable capacities — and that passive AI use quietly erodes the very judgment a supervisor needs. That is the book's hardest problem: the defense and the thing being eroded are the same faculty. If you wait until you *feel* skeptical to engage your judgment, complacency guarantees you mostly won't. Gates are the resolution. They make engagement non-optional by building it into the shape of the task, so your judgment fires whether or not your skepticism happens to be awake.

The cost is friction, and friction is exactly what productivity pressure routes around. A gate you have to remember to use will decay into nothing; a gate you have to actively skip might survive. So the design target is not "more careful" but "harder to bypass without noticing." The gates below are ordered roughly from cheapest to most demanding; you are not meant to run all seven on every task. You are meant to install one or two where the stakes justify the friction.

**The seven gates** (each maps to a mechanism):

1. **Formulate the question before you generate.** Write what you're actually trying to decide, in your own words, before you open the prompt box. Forces problem ownership — and surfaces the cases where you don't yet know the question, which no prompt can fix for you.
2. **Write your own answer or estimate first.** Before you read the model's output, commit to a rough answer — an order of magnitude, a first draft, a predicted conclusion. This is the numeracy-baseline trigger: you now have something to be surprised against.
3. **List your assumptions before generating.** Name what you're taking for granted. The model will quietly adopt your unstated assumptions and return them to you looking like findings.
4. **Impose a mandatory delay before accepting.** Do not act on the first output. Build in a pause — a walk, an overnight, a five-minute hold — between "the answer arrived" and "I used it." The delay trigger, weaponized.
5. **Frame the task concretely.** Translate the abstract into something physical and checkable — a real client, a real dollar figure, a real fact pattern — so that an absurd answer has a chance to *feel* absurd. The concrete-framing trigger.
6. **Red-team the output.** Ask, adversarially, where this is wrong: what would a hostile reviewer attack, what is the strongest counter-case, what would have to be true for this to fail? Generate the disconfirmation the model won't volunteer.
7. **Sign off on accountability, explicitly.** Before it leaves your hands, state — to yourself or in writing — that you are responsible for this output and you are prepared to defend it. The signature has to mean something, which is the whole defense against the rubber-stamp failure.

Worked across domains, the gates look concrete. In coding: write your own pseudocode and an independent test *before* you generate the implementation, then review the diff against the test you authored. In finance or analysis: estimate the order of magnitude before the model returns a figure, and flag anything outside your pre-stated range. In law: formulate the legal question and list the governing authorities before you retrieve anything, and concrete-frame the fact pattern so a hallucinated citation has a chance to look as wrong as it is. In customer service — Klarna's case — route the routine FAQ to pure automation, but build a *designed escalation gate* to a human the moment a case shows ambiguity, ethical weight, or distress.

## The honest confidence

Here is the claim this chapter most wants to make, stated as plainly as the evidence allows: **that phase gates preserve unassisted capability at scale is Low-to-Medium confidence — mechanism-supported, not scale-tested.** [Low-Medium]

Everything underneath the gates is solid. Bainbridge's irony is foundational. Parasuraman and Manzey's finding that complacency resists practice is robust. The lying-calculator triggers are demonstrated. The logic — that since willpower fails, structure is the remedy — follows cleanly from that evidence. What is *missing* is the top-line proof: there is no large-scale field trial showing that mandated phase gates in real AI-integrated knowledge work preserve people's unassisted capability over months and years. The triggers were demonstrated in a narrow numeric task, not in open-ended professional judgment. We do not know which gates have the best ratio of effort to protection. And we have direct evidence (the human-in-the-loop study) that gates can decay into accuracy-reducing rubber stamps under exactly the productivity pressure your workplace will apply.

This is not hedging for its own sake. It is the book's own rule turned on its own recommendation. A guide that warned you about laundering Medium claims into certainties would be a fraud if it then sold you gates as proven. They are not proven. They are the best-reasoned defense available, built on strong mechanism evidence and an honest gap at the top. Install them as a reasoned bet, monitor whether they're decaying into rubber stamps, and adjust.

## The move

This week, install exactly two gates — not seven. Pick the two with the best fit to your actual work and the stakes you actually carry.

For most knowledge workers, the highest-yield pair is **gate 2 (write your own answer first)** and **gate 6 (red-team the output)** — the first because it gives you a baseline to be surprised against, the second because it manufactures the disconfirmation the model will never offer. Choose one task you do regularly with AI, and make those two steps non-skippable: write your estimate in a file before you prompt; keep a standing "where is this wrong?" pass before you ship. Do it for a week and notice, honestly, how often the gate catches something — and how often you're tempted to skip it under time pressure. That temptation is the data. It tells you whether the gate is doing work or decaying into a stamp.

You are not trying to slow everything down. You are trying to keep your judgment in the loop at the two or three points where being wrong is expensive — by design, so it doesn't depend on you feeling sharp that day.

## Bridge

Gates keep your judgment engaged while you work. But engagement is not the same as *growth*. A gate stops your causal reasoning or your problem formulation from atrophying; it does not, by itself, make those capacities stronger. For that you need deliberate training — and the next chapter shows why the average "AI workshop" trains nothing at all, and what actually does.

## Sources

- Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779.
- Parasuraman, R., & Riley, V. (1997). Humans and automation: Use, misuse, disuse, abuse. *Human Factors*, 39(2), 230–253.
- Parasuraman, R., & Manzey, D. H. (2010). Complacency and bias in human use of automation: An attentional integration. *Human Factors*, 52(3), 381–410.
- Parasuraman, R., Sheridan, T. B., & Wickens, C. D. (2000). A model for types and levels of human interaction with automation. *IEEE Transactions on Systems, Man, and Cybernetics — Part A*, 30(3), 286–297.
- LaCour, M., Cantú, N. G., & Davis, T. (2019). When calculators lie: A demonstration of uncritical calculator usage among college students and factors that improve performance. *PLoS ONE*, 14(10), e0223736. doi:10.1371/journal.pone.0223736. (The "15%" and "120%" are the sizes of the *injected* error, not detection rates; the four-second delay manipulation had no significant effect and was dropped after Study 1.)
- Sele, D., & Chugunova, M. (2024). Putting a human in the loop: Increasing uptake, but decreasing accuracy of automated decision-making. *PLoS ONE*, 19(2), e0298037. doi:10.1371/journal.pone.0298037 (PMC10857587).
- Klarna / OpenAI case page and press releases (Feb 2024); Klarna CEO statements and press coverage (2025), Fortune / PYMNTS. [self-reported; story still moving]
