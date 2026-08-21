# Chapter 7 — What Canvas Measures and What It Misses

Open the Canvas analytics for any course you ran last year. You will see numbers. Time on page. Click count. Module completion percentage. Quiz score. Submission rate. The numbers are accurate. They are visualized cleanly. They tell you, with what looks like precision, who is engaged and how much.

You have made decisions on these numbers. So has every dean who has sat through an instructional-technology budget meeting. You were not wrong to use them. The numbers are what the tool was designed to give you, and the tool was designed well.

This chapter is not an argument against Canvas. Canvas was built to administer courses, and it administers them well — assignments collected, grades computed, deadlines tracked, completion logged. The argument is that *administration metrics* and *learning evidence* are different categories of measurement. That difference has always existed. What changed recently is the size of the consequences.

---

## What the numbers actually measure

Canvas's five most-used metrics, stated honestly:

Time on page tells you how long a session was active on a given resource. It catches the student who never opened the module. It misses the student whose tab was open in the background while she watched something else on another screen.

Click count tells you how many times a student interacted with a page. It catches the student who never touches the interactive elements. It misses whether the clicks reflected thought or reflexive scrolling.

Module completion rate tells you what percentage of required elements were marked done. It tracks workflow. It does not tell you whether the student understood what she completed or could do it again unaided.

Quiz score tells you percentage correct on a Canvas quiz. It is a performance check. It does not tell you whether the performance came from study, from an open textbook, or from a tool the student used between reading the question and entering the answer.

Submission rate tells you whether assignments arrived on time. It manages workflow. It does not tell you who wrote the submission.

Each of these metrics is accurate for what it captures. Each misses something you now need to know. The miss is not Canvas's fault. The miss is what happens when you use an administration tool to answer a learning question — and when the gap between those two questions has been industrially widened.

<!-- → [TABLE: Five Canvas metrics side-by-side — columns: Metric, What it measures, What it misses, Whether AI access changes the signal — rows: time on page, click count, module completion, quiz score, submission rate] -->

Neil Selwyn wrote in 2015 that what gets measured in education is what is easy to count, and what is easy to count drives what gets treated as evidence (*Learning, Media and Technology*, 40(1), 2015). Verbert and colleagues surveyed learning-analytics dashboards in 2014 and found that most of them visualize engagement, and very few have validated links to learning outcomes (*Personal and Ubiquitous Computing*, 18(6), 2014). This pattern — engagement analytics are accurate measurements of engagement and weak predictors of learning — has been true for at least a decade. What is new is not the pattern. What is new is that a tool now sits between the student and the assignment that makes the performance look excellent regardless of what the learning is doing.

---

## The performance-learning distinction

Robert Bjork has been making the same argument since the early 1990s, and it is worth stating slowly because it is genuinely counterintuitive.

Conditions that produce better immediate performance often produce worse durable learning. Conditions that produce worse immediate performance often produce better durable learning. The conditions that produce durable learning — spacing, interleaving, testing yourself before you feel ready, varying the context of practice — feel harder in the moment, produce slower apparent progress, and are consistently less preferred by students. Bjork called these *desirable difficulties*. Slow on the way in, sticky on the way out (Bjork, 1994, in Metcalfe and Shimamura, *Metacognition*).

Soderstrom and Bjork's 2015 review in *Perspectives on Psychological Science* collected twenty years of evidence for this claim. The cleanest single demonstration is Karpicke and Roediger's 2008 experiment in *Science*. Students who tested themselves once outperformed students who restudied four times — but only if you waited a week to measure them. Immediately after the study session, the restudy group looked ahead. The testing group looked slower and less confident. A week later, the testing group had held its knowledge and the restudy group had lost most of it. The students who performed better in the short term learned less. The students who struggled more in the short term retained more. The immediate measurement and the durable measurement pointed in opposite directions.

There is a further complication. Students' own judgments of their learning are systematically miscalibrated. They believe they have learned material they have not. They prefer study conditions that produce less durable learning because those conditions feel more fluent. A faculty member watching a classroom cannot reliably distinguish a student who is learning from a student who is performing. The engagement signals that look like learning — animated participation, confident quiz answers, fluent written work — are not reliable indicators that knowledge is being built in the form that will still be there six months later.

This distinction between performance and learning is uncontroversial in cognitive psychology. It has been uncontroversial since the 1990s. What is new is not the distinction. What is new is that an AI tool will now make the immediate performance look excellent for any student who uses it, regardless of whether any learning is happening at all. The gap that Bjork named was always there. It is now being produced at scale, invisibly, by a tool that fits in a browser tab.

This is the Bastani finding.

---

## The Bastani finding

In 2024 and 2025, Hamsa Bastani and colleagues at Wharton ran a randomized controlled trial in Turkish high schools. Roughly a thousand students learning mathematics were divided into three groups: no AI access, access to an unguarded GPT-4, and access to a GPT-4 wrapped in a custom interface designed to behave like a Socratic tutor. Students were measured on practice problems while they had AI access, then again on a final exam without it (Bastani et al., *Generative AI Can Harm Learning*, PNAS, 2025).

The findings, stated plainly.

During practice, the unguarded GPT-4 group scored roughly forty-eight percent higher than the no-AI control. If you were watching the dashboard during this period, you would have concluded the AI was working.

On the final exam without AI access, the unguarded GPT-4 group scored seventeen percentage points below the no-AI control. The same students. The same content. The group that had access to the unguarded AI was measurably worse off than the group that had no AI at all.

The GPT Tutor wrapper — the same underlying model, constrained to facilitate rather than answer — recovered most of the gap. The exam scores for the wrapped-AI group were far closer to the no-AI control than to the unguarded group.

[Bastani et al. 2025 PNAS; note the published correction at 10.1073/pnas.2518204122 for the seventeen-percentage-point figure — verify exact phrasing of the correction before citing in the final published version of this book.]

Now pause on the engagement data throughout the practice phase. Time on task, problems attempted, completion rates — essentially indistinguishable across all three groups. The dashboard could not tell apart the group that gained nearly half a standard deviation from the group that lost a comparable amount. The dashboard was working as designed. It was not designed to see what the exam saw.

<!-- → [TABLE: Bastani et al. 2025 results summary — rows: during-practice performance, final exam performance, engagement metrics; columns: no-AI control, unguarded GPT-4, GPT Tutor wrapper — cells show the divergence between practice-phase dashboard signals and exam outcomes] -->

This is the load-bearing piece of evidence in the chapter. One randomized trial, in one country, in one subject. The book takes it as the strongest currently available evidence for the claim, with explicit acknowledgment that replication is pending. The cognitive-psychology backbone — the Bjork distinction, Karpicke and Roediger, the metacognition literature — supports the finding mechanistically. Bastani is the empirical anchor. The mechanism is older.

The chapter's claim is not that AI is harmful. The Bastani study's own finding is that the same AI, with a different wrapper, produced learning. The AI is not the variable. The wrapper is the variable. And Canvas, by itself, cannot tell you which wrapper your students are using or what outcome they are getting.

---

## The decoupling problem

Before 2023, a well-written assignment was reasonable evidence that the student could write it. After 2023, it is not. This is the decoupling problem, and it is worth being precise about it rather than vague.

Ethan Mollick has stated the mechanism more clearly than anyone in the faculty-facing literature. When a graduate-level essay can be produced in three minutes by a model the student already has access to, the artifact — the essay itself — is no longer reliable evidence of the student's capability (*Co-Intelligence: Living and Working with AI*, 2024). The link between *student submitted essay* and *student can write essay* has been broken, not in individual cases, but at the population level.

Every faculty member teaching since 2023 has had the experience of reading a beautifully written submission from a student who cannot discuss the material orally. The oral discussion is the symptom. The decoupling is the mechanism. The artifact stopped carrying evidence of the process that produced it.

For Canvas's gradebook, this is a category problem. The gradebook records artifact quality. Artifact quality used to be a strong correlate of what the student learned. It is now a weaker correlate. The score on the assignment looks the same as it always did. What the score *means* has changed.

Canvas faithfully records what was submitted. The question is what the submission now tells you about what the student can do — and the honest answer is: less than it used to. The gradebook is not broken. The gradebook is working correctly on a measurement that no longer carries the signal it used to carry.

---

## Two students, same dashboard

Two students take the same Canvas module on beta-blockade in pharmacology. Same content. Same assignment. Same time window.

<!-- → [TABLE: Two-student comparison — rows: time on module, click count, module completion, module quiz score, submitted assignment quality, six-weeks-later retention quiz; columns: Student A, Student B — the first five rows are indistinguishable; the sixth row is where the divergence appears] -->

Canvas sees this: forty-seven minutes on the module for each. Around a hundred and forty clicks each. One hundred percent completion for each. Eighty-eight percent on the module quiz for each. High-quality submission for each. Canvas reports identical engagement for both students.

What happened inside those forty-seven minutes was different. Student A worked through the module, used the AI as a hints-only tool, was required to retrieve and articulate before getting help, struggled on the harder material, and left with a durable mental model of why beta-1 selective blockade produces different outcomes in a heart-failure patient than non-selective blockade. Student B opened the module in one tab and an unguarded chatbot in another, used the chatbot to write the assignment, passed the quiz because the questions were findable, and left without having engaged the material at the level the module required.

Six weeks later, in a clinical-reasoning scenario without resources to hand, the two students perform differently. The Canvas record says the same thing about both of them.

Canvas was not lying. It was reporting engagement, faithfully. The engagement *was* the same, measured the way Canvas measures it. What differed — the cognitive process underneath the engagement — was not in Canvas's measurement vocabulary, and there is no version of Canvas analytics that would have detected the difference. The gap is not a resolution problem. It is a category problem. What you need is not better engagement data. What you need is a different kind of data altogether: behavioral traces of the cognitive engagement itself, not the surface signature of the engagement.

Those traces exist. They have been documented in cognitive psychology for decades, separately and in fragments. What they look like in practice, and how they are assembled into a coherent measurement layer, is what Chapter 8 is about.

---

## What would change my mind

If the Bastani finding fails to replicate — if a comparable randomized trial in a different subject and country shows that engagement metrics under AI access do track learning outcomes — the chapter's central empirical demonstration weakens substantially. The Bjork distinction and the Karpicke and Roediger finding would remain. The case for measurement-aware AI architecture would remain. But the sharpest piece of evidence — same engagement profile, opposite learning outcome — would no longer be available, and the argument would have to lean harder on the older cognitive-psychology literature, which is less vivid to a non-research reader. Bastani does most of the rhetorical work in this chapter. If it does not replicate, the chapter needs to be rewritten.

There is a separate question about magnitude. The aggressive version of this chapter's claim is that any performance-based assessment in an AI-available environment no longer reliably measures learning. That version is not yet established. The conservative version — that the gap has widened enough to justify a different measurement category for high-stakes professional programs — is what the current evidence supports. I am making the conservative claim. If someone wants to press me on the aggressive claim, I will tell them the evidence is not there yet.

---

## Exercises

1. **(Analyze)** Open the Canvas analytics for one of your current courses. List every metric the dashboard shows you. For each metric, write one sentence on what it measures and one sentence on what genuine learning it cannot detect. Star the metrics you have used to make decisions in the last year.

2. **(Analyze — application to your deployment)** Imagine you have ten minutes with a skeptical senior faculty member who trusts the Canvas gradebook and does not see the gap. What single piece of evidence — the Bastani finding is the chapter's suggestion — would you walk them through? Write the two-minute explanation. The explanation cannot use the phrase *desirable difficulties* or *performance/learning distinction*. It has to land without jargon.

3. **(Evaluate — application to your deployment)** Identify the single highest-stakes assessment in your curriculum. It might be a board prep exam, a capstone, a clinical-readiness check. Ask: is that assessment currently scored on artifact quality, on engagement data, or on learning evidence? Write the honest answer in one sentence. Then write what would have to change about the assessment if you switched the scoring basis to learning evidence, and what your faculty would have to give up to make the switch.
