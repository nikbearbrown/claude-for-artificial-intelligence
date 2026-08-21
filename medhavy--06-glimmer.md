# Chapter 6 — Glimmer: The Mode for Defended Generation

*The thing that makes defended work different from graded work is the same thing that makes a dissertation different from a final exam: you have to know why you did it.*

---

Here is a question that sounds simple and isn't: what does it mean to know how to do something?

Not know *about* it. Know how to *do* it. The distinction matters in professional education because the things we want graduates to be able to do are not the same as the things that are easy to measure. A pharmacist who can recall every drug interaction from a list has learned something real. But the same pharmacist, presented with an elderly patient on eleven medications, a new diagnosis, and a prescription from a hospitalist who won't answer her calls, has to *generate* a plan. She can't recall the plan. No plan exists yet. She has to make one, and then she has to be willing to defend it.

Bloom's revised taxonomy puts that operation — Create — at the top. Not because it is hardest in some abstract sense, but because it is the operation that cannot be performed without everything below it. You cannot generate a defensible clinical plan without remembering, without understanding, without being able to apply and analyze. Generation is the integration test. It is how the system checks whether the lower levels were actually built.

The previous three modes in Medhavy's architecture address the lower levels. Ask AI builds the initial model. Quiz Me makes it durable through retrieval. Case Study trains judgment under ambiguity. Glimmer is the fourth mode, and it addresses the question those three cannot: can the student produce something that did not exist before, and can they explain why it is the right something?

<!-- → [INFOGRAPHIC: Bloom's revised taxonomy pyramid with the four Medhavy modes mapped to their corresponding cognitive levels — Ask AI at Remember/Understand, Quiz Me at Remember, Case Study at Apply/Analyze, Glimmer at Evaluate/Create — student should see how the modes are not redundant but positionally distinct] -->

---

## What Glimmer actually is

A Glimmer assignment has three features that distinguish it from a conventional essay, project, or write-up.

First, the output is open-ended. There is no single correct answer. A deprescribing plan, a clinical surveillance protocol, a public-health intervention design — these have defensible answers and indefensible ones, but the space of defensible answers is wide. The student has to navigate that space and commit to a position, which is different from working toward a known answer.

Second, the grade is on the reasoning, not the artifact. This is the load-bearing claim. A generative assignment graded on the artifact — does this protocol look plausible? does the plan list the right components? — has a structural problem: a general-purpose language model can produce an artifact that looks plausible. The artifact is not the hard part. The reasoning that produced the artifact is the hard part, and the reasoning is what Glimmer grades.

Third, before the faculty member grades the revised work, an AI pre-grading reviewer asks the student one targeted question. Not a comprehensive critique. One question about the weakest point in the student's reasoning. The student revises. The faculty member sees what the student was capable of after being pushed once, not what they produced on the first attempt.

Each of these features is a decision. The open-ended assignment is a decision against convergent tasks. The reasoning-as-grade is a decision against artifact-level assessment. The single targeted question is a decision against comprehensive markup. These decisions have empirical motivations, which is worth making explicit.

---

## The five dimensions

Glimmer evaluates reasoning along five dimensions. They are not arbitrary. Each is designed to require something a current language model produces unevenly — well enough to pass a cursory reading, not well enough to hold up when someone pushes on it.

**WHY** — did the student frame the problem before solving it? A deprescribing plan that opens with "the patient is on too many medications" has not framed the problem. It has named a symptom. A plan that opens with "this patient's primary clinical risk is a fall; the primary contributors to that risk are the combination of Agent A, Agent B, and Agent C; and the deprescribing priority follows from that risk hierarchy" has framed the problem. The framing is domain-specific and clinically current. Ask a language model to write a deprescribing plan for an elderly patient and you will get something that reads as competent. Ask it to frame the specific risk hierarchy for this patient with these comorbidities, and the output weakens noticeably. The WHY dimension is a filter for that weakness.

**Usefulness** — would the output actually be useful to a real practitioner? A theoretically defensible plan that ignores the realities of the outpatient clinic — time constraints, what the patient will reliably do, what the receiving physician will act on — is not useful. Usefulness is a judgment that requires familiarity with the practice context. Generic competence at writing clinical language does not transfer to context-grounded utility.

**Mechanism** — did the student explain the causal steps? Not "we reduced the diuretic dose" but "we reduced the diuretic dose because the patient's volume status had stabilized following the change in antihypertensive, which we expect to reduce the workload on the remaining kidney function via this pathway." The mechanistic sentence is easy to write. The mechanism that actually holds together when an attending asks "why" three times is harder. Current language models are fluent at mechanism language and uneven at mechanistic substance.

**Defensibility** — can the student defend the choice against the reasonable counter-argument? If the obvious objection to a plan is "but this patient was started on warfarin for a reason," does the plan address that reason? Defensibility requires holding both a position and its objection in mind simultaneously. A language model will generate counter-arguments if asked. Predicting which counter-arguments are the relevant ones for this patient, this clinical context, this prescriber — that is the skill.

**Specificity** — did the student commit to particulars? Not "monitor closely" but "obtain CBC and BMP at one week and again at three weeks; the values that would trigger a change are X and Y." Vague outputs from a language model are easy. Concrete, defensible specifics in a clinical context are not. The plan that names the lab, the interval, and the trigger value is the plan that can be executed.

<!-- → [TABLE: Five Glimmer dimensions side-by-side — columns: Dimension, What it asks, Why it resists offloading, Example of a weak response, Example of a strong response — student should see the evaluative standard concretely for each] -->

What these five dimensions share is that they ask for the features of clinical reasoning that a dissertation defense has been testing for a hundred years. They are not new tests. They are the old tests, applied at scale, with an AI layer upstream of the grade.

---

## Why one question

John Hattie and Helen Timperley, in their 2007 synthesis of feedback research, distinguished four levels at which feedback can operate: the task, the process, self-regulation, and the self. The strongest learning effects came from process-level feedback — feedback about the reasoning, not the output. Comprehensive feedback at the task level, which is what most annotated papers provide, produced weaker learning gains than a single well-aimed question at the process level. (*Review of Educational Research*, 77(1), 2007.)

This is a research finding that most faculty members have encountered in some form and forget when they pick up a pen. The urge to mark every weak sentence is strong. It feels thorough. It feels like the work of a good teacher. The empirical literature is unambiguous that it underperforms a targeted question.

The AI pre-grading reviewer does not have the pen-in-hand habit. It asks one question and stops.

The question targets the weakest of the five dimensions. Not all five. Not even two. One. The student revises in response to that one question. The faculty member grades the revision. What the faculty member sees is what the student was capable of after being pushed at the point of greatest weakness — which is more diagnostic than the first draft and more useful to grade.

<!-- → [INFOGRAPHIC: Flow diagram showing Glimmer's submission process — Student submits → AI identifies weakest dimension → AI asks one targeted question → Student revises → Faculty grades revision — annotations at each step explaining why each hand-off happens in that direction] -->

There is a faculty workflow implication here worth naming directly. The pre-grading layer does not replace faculty judgment. It shifts what faculty judgment is applied to. Without the AI layer, the faculty member grades a first draft that may have a simple, correctable weakness. With the AI layer, the faculty member grades a second draft in which that weakness has been addressed. The faculty member's expertise is now engaged at a higher level of the student's reasoning. This is not automation of grading. It is a change in what gets graded.

---

## The emergent term project

The first Glimmer in week three of the course looks like an isolated assignment. The second, in week six, looks like a somewhat larger isolated assignment. In week ten the student is told, plainly, that the work they have been doing builds into a term portfolio, and that the integrated portfolio is the final assessment.

The students did not know this in week three. That is a deliberate pedagogical choice.

The bet is this: announced portfolios produce student-strategic output. When a student knows from week one that their assignments will be assembled into a portfolio reviewed by program directors and hospital partners, they optimize for what the portfolio rubric rewards. The work becomes strategic in a specific way — shaped toward the anticipated audience rather than toward the problem at hand. The emergent design removes that strategic pressure. The student takes the week-three assignment seriously because it is the week-three assignment, not because they have already calculated its place in a portfolio they are building.

The theoretical support for this bet comes from self-determination theory — Ryan and Deci's work on intrinsic motivation and its conditions. Hidden purpose effects on intrinsic motivation are plausible within that framework. Direct empirical evidence on this exact design — students who discover the portfolio in week ten compared to students who knew from week one — does not yet exist. Medhavy is making a bet that has theoretical support but not direct confirmation. The first cohorts of programs deploying Glimmer are part of the evidence on whether the bet is right.

If a study showed that announced-portfolio students produced delayed-transfer performance equal to or better than emergent-design students, the hidden-purpose design would lose its central justification. The five-dimension architecture and the AI reviewer would survive that finding intact. The emergent framing would not.

---

## When Glimmer is wrong

Glimmer is not a universal prescription. It is appropriate when the student has enough domain proficiency that open-ended generation is productive rather than anxiety-inducing. Patricia Alexander's model of domain learning describes three stages — acclimation, competence, proficiency — with different cognitive operations appropriate to each. A student in early acclimation, asked to produce and defend an open-ended clinical protocol, does not learn from the experience. She learns that she doesn't know enough. Which she already knew. The assignment confirms the gap; it does not close it.

Medhavy's response to this is backwards-faded scaffolding, drawing on research by Alexander Renkl and Robert Atkinson on faded worked examples in algebra. Early in the domain, the Glimmer comes with most of the structure provided; the student fills in the final step. As proficiency develops, the scaffold fades. By proficiency stage, the assignment is fully open. The progression from worked example to partially open to fully generative mirrors the empirical findings on how expertise develops — findings from algebra, adapted here to clinical reasoning, which is itself an extrapolation that has theoretical motivation but has not yet been directly measured in this context.

The phase gate before Glimmer deployment is not bureaucratic caution. It is the mechanism that prevents an assignment designed for proficiency-stage learners from landing on acclimation-stage students and doing damage.

<!-- → [INFOGRAPHIC: Backwards-faded scaffolding diagram showing three horizontal bands corresponding to Alexander's stages (Acclimation, Competence, Proficiency) — within each band, a Glimmer assignment structure showing how much scaffold is provided vs. how much the student generates; the scaffold shrinks left-to-right as proficiency increases — student should see that the assignment type is the same but the cognitive demand shifts with the learner's stage] -->

---

## The four-mode arc completed

For the past three chapters I have been following one student — a second-year pharmacy student learning beta blockade. Ask AI built her first working model of the mechanism: why beta-1 selective blockade produces different outcomes in a heart-failure patient than non-selective blockade. Quiz Me made that model durable across three weeks of spaced retrieval. Case Study put her in front of a sixty-four-year-old man with COPD, heart failure with reduced ejection fraction, and a resting heart rate of fifty-two, and asked her to defend a recommendation. She arrived at a defensible position and revised it once when the AI surfaced a consideration she hadn't addressed.

The Glimmer assignment is the fourth step: *Design a clinical protocol for initiating beta blockade in patients with concurrent COPD and reduced ejection fraction, including monitoring parameters, escalation criteria, and de-escalation triggers. Defend every decision against the obvious counter-argument.*

She produces a four-page protocol. It names the patient population, the two beta blockers she chose to include and why, the initiation dose, the monitoring interval, and the conditions under which dose escalates or the drug is discontinued.

The AI pre-grading reviewer reads the protocol and identifies her weakest dimension: Specificity. The monitoring intervals are vague. The trigger values are absent. "Monitor pulmonary function" appears without a named test or threshold. The question the AI asks is: *You wrote that pulmonary function should be monitored, but you did not name the test, the interval, or the threshold that would trigger a change. A pulmonologist reading this would not know what to order. What did you intend?*

She revises. The revised protocol names spirometry at baseline and at one month, with a fifteen percent decline in FEV1 as the trigger for protocol escalation. The faculty member grades the revision.

The protocol joins her term portfolio. In week ten she will learn that the portfolio she has been building without knowing it is her integrated final assessment.

<!-- → [TABLE: Four-mode arc summary table — columns: Mode, Cognitive operation (Bloom's level), What the student does, What the AI does, What it produces — one row per mode showing the full sequence from Acquire through Generate] -->

The four modes cover the full cognitive sequence: acquire, retain, apply, generate. The sequence is not decoration. It is the spine of what professional education is supposed to do. The generate step — Glimmer — is the step that produces the artifact a program director can show a hospital partner when asked what the graduates can actually do.

---

## What would change my mind

If a multi-site study showed that students completing Glimmer assignments performed no better on delayed transfer assessments — clinical reasoning scenarios at six months, scenarios they had not seen before — than students completing conventional essay assignments, the chapter's central claim would require substantial revision. The five-dimension framework's defense is that it targets cognitive operations distinguishable from those a conventional essay rubric targets. Direct empirical confirmation of that distinguishability does not yet exist. A null result on delayed transfer would be the counter-finding that matters.

There is a longer-term pressure on Glimmer's design that is worth naming. The five dimensions resist current language model capabilities because those capabilities are uneven at mechanistic causal explanation, counter-argument anticipation, and context-grounded utility judgment. That unevenness will change. As models improve, the five dimensions will erode as anti-offload defenses. What replaces them when a model can routinely produce domain-grounded framing, context-specific mechanism, and defensible specifics on request? That question is not answered in this book. It is the question the field of professional education will be working on for the next decade.

<!-- → [CHART: Conceptual timeline chart showing estimated LLM capability progression across each of the five Glimmer dimensions (WHY/framing, Usefulness, Mechanism, Defensibility, Specificity) — x-axis is time, y-axis is LLM proficiency at each dimension; lines should show different rates of erosion, with Specificity and Mechanism eroding faster than Defensibility and Usefulness — reader should see that the dimensions do not fail simultaneously, which has implications for how the rubric should evolve] -->

---

## LLM Exercises

1. **(Understand)** For one Glimmer-style assignment in your curriculum — or one you could imagine introducing — write a sample student artifact one paragraph long. Then write the one targeted question an AI pre-grading reviewer would ask about its weakest dimension. Name the dimension. Defend why it is the weakest of the five and not one of the other four.

2. **(Apply — to your own deployment)** Pick a learning objective in your program that currently ends in a written assignment graded on the artifact. Rewrite the assignment so the grade is on the reasoning, using the five dimensions. Identify which dimension is the load-bearing one for that specific objective. Write a one-paragraph note to the faculty member who currently grades that assignment explaining what changes about their grading workflow and what does not.

3. **(Evaluate)** In your deployment, what percentage of your learning objectives require students to produce something original and defend it? Those are Glimmer candidates. Write the percentage and a one-paragraph defense of the estimate. Then write what would change if you committed to the emergent term-project design. Identify one specific risk of the hidden-purpose framing in your program's culture and one specific benefit. If you cannot name one of each, you have not yet thought hard enough about whether the emergent design is the right bet for your institution.
