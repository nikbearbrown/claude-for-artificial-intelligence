# Chapter 5 — Case Study: The Mode for Judgment Under Ambiguity

There is a particular kind of failure you see on the first day of a clinical rotation. A student walks in who has passed every board-style exam you put in front of her. She knows what beta blockade does — the mechanism at the receptor level, the major indications, the contraindications. She can retrieve all of this under timed conditions. Then you hand her a patient: sixty-four years old, COPD, heart failure with reduced ejection fraction, resting heart rate of fifty-two. Should this patient be on a beta blocker?

She freezes.

This is not a knowledge gap. If you ask her what beta blockers do, she can tell you. The mechanism is intact. What is not intact — what has never been built — is the capacity to *decide* when the situation is genuinely unclear, when the clinical picture has competing constraints and no single correct answer, and when you have to commit to a recommendation and defend it. That capacity is different in kind from recall. You cannot build it by drilling more recall. You need a different cognitive operation, and a different mode.

Case Study is that mode.

<!-- → [IMAGE: A simple two-column diagram contrasting a well-structured board exam question (single correct answer, four distractors) with an ill-structured clinical scenario (multiple defensible paths, competing constraints, no clean stopping rule) — illustrates Jonassen's 1997 distinction visually] -->

---

## The problem David Jonassen named

In 1997, David Jonassen drew a line that medical and engineering educators had been dancing around for years. A well-structured problem, he wrote, has a single correct path and a single correct answer. An ill-structured problem has multiple acceptable paths, competing constraints, and no clean stopping rule. The instructional design implications are not the same. The cognitive operations required are not the same (*Educational Technology Research and Development*, 45(1), 1997).

This is not a subtle distinction. The board exam is almost entirely well-structured. Four options. One correct stem. Three distractors that are wrong in ways the examiners have thought about carefully. The boards are a machine for measuring whether you can retrieve and reason about things you have been taught, under timed conditions, when the answer exists. They measure this well.

Clinical practice is almost entirely ill-structured. The seventy-eight-year-old with vague abdominal pain and a mental status the night nurse described as "a little foggier than yesterday" does not present with four options and one correct stem. She presents with incomplete information, a respiratory rate that has been climbing for four hours, and a physician who has to make a decision in the next ten minutes with what she has.

Three years before Jonassen's paper, in 1994, the Carnegie Foundation commissioned the study that made this visible at scale. Their report on medical education — *Educating Physicians*, published in 2010 after five years of site visits to US and Canadian medical schools — concluded that medical curricula had optimized for the boards and produced students who were confident and brittle. They knew the right answers. They could not decide under ambiguity. Two years earlier, the same foundation had said the same thing about engineering (Sheppard, Macatangay, Colby, and Sullivan, *Educating Engineers*, 2008).

The gap is not news. Programs have known about it for decades. The question is what you build to close it, and whether that thing can run at scale.

---

## What case-based learning actually does

The mechanism underneath Case Study is not new, and it is worth being precise about it rather than gesturing at it.

Howard Barrows formalized problem-based learning at McMaster's medical school in the 1970s. His observation was simple: students who acquire knowledge in the context of a problem retrieve it better when a similar problem appears in practice. The case is not just an application of the concept — it is a retrieval cue. Knowledge acquired without a case context tends to stay inert. You can retrieve it when prompted directly. You cannot retrieve it spontaneously when you see a patient who triggers the same pattern (*Problem-Based Learning*, Barrows and Tamblyn, 1980).

Susan Williams sharpened this in 1992. The case encodes the knowledge in a situated context. The situated context is what makes the later retrieval possible — not because retrieval from cases is easier, but because the encoding matches the eventual retrieval conditions (*Journal of the Learning Sciences*, 2(4), 1992).

Cindy Hmelo-Silver's 2004 meta-review gave the empirical picture. Problem-based learning underperforms direct instruction on immediate factual recall. It outperforms it on delayed transfer — on assessments six months out, on novel problems that require applying the concept in a situation the student has not seen before (*Educational Psychology Review*, 16(3), 2004). This is the same pattern Robert Bjork has documented across a much wider range of learning research: the conditions that produce the most durable learning often produce the most effortful, least fluent performance in the short term. Immediate performance and durable learning are not the same thing, and optimizing for one can undermine the other. Chapter 7 returns to this in detail.

Case Study is Medhavy's operationalization of this body of work. The design question is not whether case-based learning works — the evidence on that is reasonably clear. The design question is how you run it with fidelity across three hundred students, five sections, and three rotating instructors.

<!-- → [TABLE: Summary of Hmelo-Silver 2004 meta-review findings — rows: immediate recall, delayed transfer, application to novel problems; columns: direct instruction, problem-based learning; cells: relative performance. Helps reader see the trade-off clearly rather than reading it as an either/or] -->

---

## The consistency problem at scale

A program with thirty nursing students and one experienced clinical educator does not need a software solution for case-based learning. The educator already runs case discussions in seminar. She knows her students. She reads the room in real time — when a student is guessing rather than reasoning, she can hear it in the hedge. When a student has missed a critical consideration, she surfaces it without giving the answer. The facilitation is continuous and calibrated.

This does not scale.

A program with three hundred students across five sections inherits a different problem. How consistent is the facilitation across instructors? Does every section surface the same critical considerations? Does every student who stalls get a useful hint rather than either the answer or silence? In a paper-based case discussion, the answer to all three questions is: it depends on who is running the seminar that day.

Case Study is the four-instructor consistency problem solved in software. The AI facilitates the discussion inside a pre-written, faculty-reviewed scenario. It asks questions. It offers graduated hints when the student stalls. It surfaces considerations the student has missed. It does not give the answer. The facilitation behavior is consistent across every section and every student because it is specified in advance by the faculty member who designed the case.

The critical word in that last sentence is *specified*. The faculty member does not simply hand over a case scenario to the AI and let the AI decide how to facilitate it. She configures the AI's role inside the case: which question the AI opens with, which hints it offers if the student stalls at each stage, which considerations it surfaces if the student misses them. Without that specification, the AI defaults to its own facilitation pattern, which may or may not match the pedagogical intent of the case. The configuration is part of the work.

---

## Why the cases must be faculty-reviewed

Here is the tempting version: let the AI generate case scenarios on demand. Cheaper. Instantly scalable. Personalized to the student's current weak points.

The problem is not quality. It is a different kind of problem.

A large language model writing a cardiology case can produce a clinically incoherent vignette that reads fluently. A dosage wrong by a factor of ten. A drug interaction that does not exist. A clinical presentation that no human patient has ever had. The vignette sounds like medicine. It is not medicine. And a student who reasons through a clinically incoherent case learns incoherent reasoning — not because she failed, but because she succeeded at the task in front of her, and the task was built on a wrong foundation.

In clinical education, plausible-confident-wrong is a patient-safety risk. A student who learns incorrect reasoning from a well-structured, faculty-reviewed wrong case is a problem. A student who learns incorrect reasoning from a fluent, AI-generated wrong case, multiplied across a cohort, is a different scale of problem.

The American Association of Medical Colleges and parallel guidance documents in 2024–2025 explicitly recommend faculty review of any AI-generated clinical scenario before student exposure. The empirical evidence on how often AI-generated cases contain clinical errors, and whether those errors produce measurable harm to learning, is thin — no large randomized trial has been run. The safety-engineering argument does not require the empirical evidence. In safety-critical domains, you do not field the system that might produce plausible-confident-wrong outputs and then wait for the harm signal.

Medhavy's design choice is this: every Case Study scenario is authored or reviewed by a faculty member who owns the content. The AI facilitates the discussion within the reviewed scenario. The AI does not invent the clinical facts. This is a process commitment, not a feature toggle. A program that wants to deploy Case Study has to commit to the faculty review pipeline. That commitment is part of what Case Study is.

<!-- → [INFOGRAPHIC: Two-path diagram — Path A: AI-generated scenario → student works case → incoherent reasoning produced at scale; Path B: Faculty-authored/reviewed scenario → AI facilitates discussion → student reasoning is built on verified clinical ground. The infographic should make the safety-engineering argument visible without requiring the reader to hold both paths in working memory] -->

---

## The assistance dilemma

Inside a single Case Study session, the AI does not start by asking the hardest question. It starts broadly — "what do you notice about this patient's presentation?" — and escalates only when the student demonstrates engagement with the previous level. If the student is producing nothing, the AI moves down a rung and offers a more pointed prompt. If the student is moving fast and confident, the AI does not over-scaffold.

Kenneth Koedinger and Vincent Aleven named the underlying tension in 2007. Too much help produces offloading: the student lets the system do the thinking. Too little produces shutdown: the student gives up. Neither is learning. And the optimal level of help is not universal — it depends on the student, the concept, and the specific moment in the reasoning (*Educational Psychology Review*, 19, 2007).

A skilled human tutor solves this in real time by reading the room. The software solution is a graduated assistance ladder: a specified sequence of hints at increasing specificity, triggered by signals from the student's engagement rather than from a fixed timer. Chapter 8 describes the seven signals in detail. What matters here is that the ladder exists and that it is specified by the faculty member at case design time, not improvised by the AI during the session.

This is the structural reason Case Study is harder to deploy than Ask AI or Quiz Me. Ask AI and Quiz Me run on content alone. Case Study runs on content plus a facilitation specification. The facilitation specification is work. It is the work that turns a case scenario from a demonstration into a learning event. Programs that skip the specification and let the AI improvise get a plausible-looking case discussion. They do not get Case Study.

---

## The prerequisite gate

There is a condition under which Case Study fails, and it has nothing to do with the quality of the case or the facilitation specification. It fails when the student does not yet have the underlying mechanism.

A student who does not understand what beta blockade does cannot reason about whether a sixty-four-year-old with COPD and a resting heart rate of fifty-two should be on one. She cannot reason about it because she has no schema to reason with. What she will do instead is match surface features to cases she half-remembers and produce an answer with no mechanism beneath it. The AI then either reveals the answer, which is offloading, or refuses, which is shutdown. Both outcomes are pedagogical failures, and neither is a failure of Case Study — they are failures of sequencing.

John Sweller and Graham Cooper established the boundary condition in 1985. Novices learn more from studying worked solutions than from attempting novel problems they have no schema for. The schema has to exist before problem-solving practice builds on it (*Cognition and Instruction*, 2(1), 1985). This is not a limitation of weak students. It is a cognitive architecture constraint. You cannot reason about what you do not yet know.

Medhavy enforces a prerequisite gate: a Case Study unlocks only after the relevant Quiz Me concepts have hit a retention threshold. The student cannot leap to the clinical case before the basics are durable. This constraint has a cost — the integration of recall and judgment is delayed. The cost is justified by what you prevent: a cohort of students who have been through Case Study scenarios and have learned to produce plausible-sounding reasoning with no mechanism underneath it.

The sequence is Acquire → Retain → Apply. Ask AI is Acquire. Quiz Me is Retain. Case Study is Apply. The modes are not interchangeable, and they are not a menu. They are a sequence with a logic, and the logic runs in one direction.

<!-- → [CHART: A horizontal progression diagram — Ask AI (Acquire), Quiz Me (Retain), Case Study (Apply), Glimmer (Generate) — with arrows showing prerequisite gates between them and brief labels on each gate: "retention threshold," "ambiguity threshold," "integration threshold." Helps reader see Case Study's position in the four-mode sequence without having to hold the whole architecture in working memory] -->

---

## The worked example: one student, three stages

A second-year pharmacy student. She has heard the term *beta blocker* in cardiology lecture. She does not yet have a working mental model.

In Ask AI, she asks how beta blockade works. The mode does not lecture her. It asks what she noticed about heart rate in the prerequisite section on adrenergic receptors. She has to retrieve. She articulates that adrenergic stimulation increases heart rate. Ask AI builds from there with further questions. By the end of the session, she has constructed an explanation. She built it; it was not handed to her.

Over the next three weeks, Quiz Me schedules retrieval practice — the mechanism at the receptor level, the cardiac and noncardiac effects, the major drug names, the contraindications. The first retrievals are effortful. By week three, she can answer the core facts under timed conditions without prompting. The mechanism is durable.

Now the Case Study gate opens.

She is handed a sixty-four-year-old man with COPD, heart failure with reduced ejection fraction, a resting heart rate of fifty-two. Should this patient be on a beta blocker? Which one? At what dose? What would change her answer?

She knows what beta blockade does. The case asks her to decide whether it is appropriate when the picture is complicated. The AI opens: "What did you weigh first?" She names the heart failure indication, then the COPD concern, then the bradycardia concern. She arrives at a reasoning that names the trade-off and commits to a recommendation. She defends the recommendation. The AI surfaces one consideration she did not name — the specific pharmacology of cardioselective agents in COPD at low doses. She revises. The work is judgment under ambiguity, not recall.

Three modes. Three cognitive operations. Three stages of a sequence that has a logic. Chapter 6 takes the same student into the fourth mode, which is a different thing in kind: not applying what she knows, but producing something original and defending it.

---

## What Case Study is not

It is not an essay assignment with an AI grader. The AI does not grade the session. The AI facilitates the discussion and surfaces reasoning. Faculty review happens on the scenario before the student ever sees it. The AI's role is during the case, not after it.

It is not a replacement for faculty-run case discussions. If a program already runs case discussions with experienced faculty in small groups, with real-time facilitation, Case Study adds little. The question is always a scale question. When case discussions are uneven across instructors, or asynchronous, or simply do not exist for some learning objectives because the program cannot staff them — that is when Case Study is the right move.

And it is not a decision that the program can revisit after deployment if the faculty review pipeline turns out to be too expensive to maintain. The review commitment is not optional at a later stage. Either the pipeline exists and is funded, or the cases are not faculty-reviewed, and a program running unreviewed AI-generated clinical scenarios in safety-critical domains is accepting a risk that no major guidance document currently recommends accepting. The commitment is binary: you build the pipeline before you deploy, or you do not deploy Case Study.

Chapter 12 makes the timeline and the cost concrete.

---

## Exercises

1. **(Understand)** For one concept in your curriculum, describe in one paragraph what a student who has completed Ask AI and Quiz Me on that concept can reliably do. Then describe what they still cannot do that Case Study would address. Identify the specific form of ambiguity in the gap — competing constraints, missing information, multiple defensible paths — and name which one Case Study would train.
2. **(Apply — to your own deployment)** Identify one faculty member in your program who has the domain expertise to write and review Case Study scenarios for a high-priority learning objective. Estimate the time required, per scenario, for them to author the case and complete the Socratic-laddering review (where the scenario's hint sequence is specified). Estimate the format they would need to produce. Write a one-paragraph proposal you could send them.
3. **(Evaluate)** In your deployment, what percentage of your learning objectives require students to apply knowledge under ambiguity without a single correct answer? Those are Case Study candidates. Write the percentage and a one-paragraph defense of the estimate. If the figure is under ten, you have evidence that Case Study may not yet be the right Medhavy commitment for your program. If it is over thirty, the prerequisite-gate plumbing becomes the operational question — see Chapter 12.
