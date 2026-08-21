# Chapter 2 — The Nine Capacities
*The gap between two equally smart people isn't skill — it's a constellation you can learn to see.*

I have been watching people use AI tools for the last two years, and I keep noticing the same puzzle. Take two equally smart engineers, or two analysts, or two journalists, and watch them work with the same tool on the same kind of task. One of them gets dramatically better results than the other. The gap is not in their raw intelligence. It is not in their familiarity with the tool. It is not, usually, in how much they know about machine learning. The gap is somewhere else, and for a while I couldn't name where.

I want to show you what I mean through one case, because this is the kind of thing that is better seen than described. The case is Priya's — twelve months past her Chapter 0 wake-up, three weeks past the publication of a data-driven piece she had been particularly pleased with. The case happened to her. It is also the case that taught her she needed more than the Loop's structure. She needed the cognitive capacities the Loop draws on.

It is a Tuesday morning, and a letter has just landed in the publication's general inbox.

The piece Priya wrote three weeks ago was a state-by-state analysis of clean-energy policy timelines: how long, on average, did it take between a state's announcement of a major incentive program and the first publicly reported industry investment decision triggered by it. The story's framing was that some states acted fast and some did not, and the difference mattered for federal coordination. Priya had pulled the announcement dates and investment-decision dates from a state-by-state dataset, asked Claude to calculate the lag times in months, and reported the averages with state-level call-outs.

The letter is from a state energy analyst in one of the highlighted states. The analyst is polite and specific. The piece reports the state's lag time as 4 months. The analyst's office calculates it as 7 months. The difference is not noise. It is a category difference — the state's program was announced in a fiscal-year reference frame, and the publicly-reported investment decisions are dated in calendar time, and the conversion is non-trivial because the state's fiscal year begins in July. Claude's calculation had handled most states correctly. The states where fiscal year and calendar year diverged had been silently mishandled.

The piece is now in question. The error is in one state on a table with twelve states. Priya does not yet know how many other states it affected. The correction will go up tonight.

Now here is the question I want to sit with for a moment: what, exactly, did Priya do wrong?

Notice that it is not one thing. She did not fail at one cognitive task. She failed at several, and they are not the same kind of failure. I want to pull them apart, because the pulling-apart is the move this chapter is really about.

She failed, first, at deciding what to delegate. She handed the model the whole calculation — including the part that required someone to hold in mind a working model of the relationship between fiscal years and calendar years across state programs. She treated the model as a function that returns answers. She should have treated it as a draftsman that returns drafts.

She failed, second, at evaluating the output. She read the lag-time table, but she did not stress-test it. She did not ask, before publication: *what would have to be true for these numbers to be wrong?* That question is a different cognitive move from *do these look right?* The first asks you to imagine the world in which the calculation fails. The second asks whether the numbers match a vague mental picture of correctness. They feel similar from the inside. They are not. Priya made the second move when the situation required the first.

She failed, third, at handling uncertainty honestly. The model had not said, "I am ninety percent confident these calculations handle the fiscal-year edge cases correctly." Models do not say things like that. They produce confident-looking output, and you have to import the uncertainty yourself. Priya did not. The output looked certain, so she treated it as certain. The sleight of hand was the model's, but the cure was always going to be hers.

And she failed, fourth — this one is the subtle one, the slow one — at staying in the practice. Priya used to think carefully about fiscal-year conversions because she had to. As a junior reporter she had once spent half a day chasing down whether a budget figure was reported in fiscal or calendar terms. The model has, over the last year, taken that thinking out of her daily routine. Not out of her abilities; she can still do it when she tries. But out of her daily routine. And a muscle you stop using does not fail suddenly. It gets slow before it atrophies. You do not feel it getting slow. You feel it the day it fails to do what you needed, and by then the gap has been accumulating for months.

Four different failures, all at once, all in what looked like a simple table on a routine piece. Now let me tell you something interesting: if I told you a similar story about a clinician picking AI-generated drug-interaction summaries without specifying the patient's renal function, or a hiring manager running résumés through an AI tool he has not audited, or a graduate student handing in a literature review he did not read — you would find a different combination of similar failures each time. But you would always find a combination. Never just one.

That is what I have been trying to understand. People who use AI well are not doing one thing right. They are doing a constellation of things right, and the constellation has a shape.

I am going to claim the shape has nine points. The number is not sacred. I have looked at enough working practitioners that nine seems to fit the cases I have seen, but nine might be eight or eleven with more data. The count is bookkeeping. The capacities are what matter.

![Figure 2.1 — A "constellation" diagram with nine labeled nodes arranged in a loose organic cluster](images/02-the-nine-capacities-fig-01.jpg)

Here they are, briefly, before I give any of them the treatment they deserve.

The first is **strategic delegation**: deciding, before you begin, what the model should do and what you should do, and why. Priya's first failure. The diagnostic question is: *what should I give the AI, what should I keep, and why?* A fluent practitioner can answer this in seconds. A novice cannot answer it at all and so hands the model the whole task, which is the same as not deciding.

The second is **effective communication**: telling the model what it actually needs to know. Intent, constraints, audience, success criteria. When this fails, the model fills in the blanks with its best guess at what you meant. The best guess will be slightly different each time — which is how you get the experience of "the model is inconsistent," when in fact you have been inconsistent and the model has been faithfully reflecting your inconsistency back at you. I find this the funniest of the nine, because the failure looks like the model's failure and is in fact yours.

The third is **critical evaluation**: reading the output for what kind of error it might contain. This was Priya's second failure, and I think it is the most under-practiced of the nine. Most people read AI output for whether it *sounds* right. Reading it for whether it *is* right is a different activity. It requires you to hold, in your head, a model of the kinds of failure this kind of system produces. Without that internal model, you have nothing to check against except plausibility. Plausibility is a very low bar.

The fourth is **technical understanding**: knowing enough about how the system works to predict where it will fail. Not at research depth. Practitioner depth. Enough to know that a language model will hallucinate citations because of how it was trained, and so you should always check citations. Enough to know that an image model will produce six fingers because of the structure of its training data, and so you should always count fingers. The diagnostic question is: *do I have a working model of why this thing succeeds and fails?* This is the capacity I find most often missing in otherwise sophisticated users. They use the tool well in cases where it happens to work, and have no theory of when it will not.

The fifth is **ethical reasoning**: noticing when the use case has stakeholders other than yourself and the AI, and acting on that noticing. The hiring manager who deploys an unaudited screening tool has failed at this. So has any team that ships a product affecting other people's lives without asking who might be harmed. I want to be direct: this is not a soft skill. It is the capacity that keeps you from shipping something that gets someone hurt, gets you sued, or both.

The sixth is **stochastic reasoning**: handling uncertainty honestly. Yours, the model's, the world's. The diagnostic question is: *what kind of probabilistic claim is this, and what would calibrate my belief in it?* A model will give you a number — say, "sixty-five percent probability the Fed cuts rates" — and the number will look like a number, and you will use it as if it were a number, and it may be the model's best guess at last week's market-implied probability with no fresh information at all. The capacity is not "be good at probability." The capacity is "ask, every time, what kind of probabilistic claim is in front of me and where it came from."

The seventh is **learning by doing**: using AI in ways that amplify your skills rather than replace them. This was Priya's fourth failure, the slow one. The diagnostic question is: *am I building the skill, or consuming the output?* AI use can be the most powerful learning multiplier you have ever had. It can also be the fastest skill atrophier. Which one it is depends almost entirely on how you use it — not whether you use it. Most people who think they are using AI to learn are using it in a way that prevents learning. Most people who think AI is making them weaker simply have not found the specific moves that turn AI use into accelerated practice. These are learnable. The chapter that covers this will show you what they are.

The eighth is **rapid prototyping**: treating model output as a draft to be tested in the world, not as the work itself. The product manager who hands AI-generated feature ideas to engineering without any user testing has failed at this. The model produced options. The model did not produce validation. The diagnostic question is: *am I testing this against reality, or just against my own approval?* Approval is cheap. Reality is the only thing that talks back.

The ninth is **theoretical foundations**: keeping enough domain knowledge in your own head that the AI amplifies your understanding rather than substituting for it. The graduate student who hands in a literature review without reading the foundational papers has the prose without the foundation — which means she cannot tell good prose from prose with subtly wrong framing. The diagnostic question: *do I understand the underlying material well enough to judge whether this output is good?* Without that, you are not collaborating with the model. You are taking dictation from it.

| Capacity | Diagnostic question | Primary loop step | Durability |
|---|---|---|---|
| **Strategic Delegation** | What should I give the AI, what should I keep, and why? | Delegate | Durable |
| **Effective Communication** | Am I telling the model what it actually needs to know? | Specify | Temporary |
| **Critical Evaluation** | Would I bet on this output, and on what evidence? | Discern | Contested |
| **Technical Understanding** | Do I have a working model of why this system succeeds and fails? | Discern | Temporary |
| **Ethical Reasoning** | Who could be harmed by this output or deployment, and am I tracking that? | Be Diligent | Durable |
| **Stochastic Reasoning** | What kind of probabilistic claim is this, and what would calibrate my belief in it? | Discern | Contested |
| **Learning by Doing** | Am I building the skill, or consuming the output? | All steps | Durable |
| **Rapid Prototyping** | Am I testing this against reality, or just against my own approval? | Converse | Temporary |
| **Theoretical Foundations** | Do I understand the underlying material well enough to judge whether this output is good? | Discern | Temporary |

Nine. Each one a cognitive capacity. Each one a place where I have watched real practitioners fail. And — the part that took me longest to see — each one separable enough to practice on its own.

That last claim is the one I am least confident in, and I want to say so directly. It is possible that these nine correlate so strongly with general professional judgment that "develop the nine capacities" reduces, empirically, to "get better at your job." If that is true, the architecture in this book is decorative — it produces the right behavior, but the decomposition into nine is not doing real work. I have looked at this carefully and I believe the decomposition earns its keep. I can identify practitioners who are strong in some of these and weak in others, and the patterns are not random. But I do not have longitudinal data. If a careful study showed that fluent practitioners share four or five of these and the rest are noise, I would update. The list comes from observation, not theory. Observation can be wrong.

Now I want to say something about durability, because it matters for how you invest.

Some of these capacities are durably the human's responsibility, in any future I can foresee. Strategic delegation is one. Someone has to be accountable for the work, and accountability cannot be delegated to a model. Your name on the work is your name on the work, and the question of what to delegate is an accountability question, not a capability question. Ethical reasoning is the same. When the lawsuit is filed, when the patient is harmed, when the algorithm denies the loan, when the published statistic turns out to be wrong — the model is not the defendant. You are.

Learning by doing is durable in a different way: you have a body and the model does not, and the skills you have built into your daily practice are yours regardless of what the model can do at any given moment.

Critical evaluation and stochastic reasoning are contested. Models are getting better at calibrated self-doubt and uncertainty quantification. In some narrow domains, a well-tuned model may already produce better-calibrated probabilistic claims than a well-trained human. The practitioner of 2028 may have to update which parts of these she still owns and which she has reasonable grounds to lean on the model for. I cannot tell you yet which parts those will be. You will be able to tell, when the time comes, because the practice you have built will give you the sensors to notice.

The remaining four — effective communication, technical understanding, rapid prototyping, theoretical foundations — are temporarily irreducible at varying timelines. Models will erode parts of each. The judgment of what is a good prototype, what is a load-bearing theoretical foundation, what level of technical understanding is actually sufficient — that is going to remain yours longer than the production of those things.

![Figure 2.3 — Horizontal durability spectrum](images/02-the-nine-capacities-fig-03.jpg)

I am being explicit about this because I want the book to age well in your hands. The durable capacities, you are investing in for the whole career. The temporary ones, you still need now, and the book will try to teach them. When the timeline closes on any of them, you will be among the first to notice. That is one of the hidden returns on building a practice: the practice gives you the sensors to know when a capacity is no longer load-bearing. Someone who only read about these things will not have those sensors.

Let me end with something practical.

Take the nine capacities and ask yourself, for each one, where you are. Not precisely. On a four-level scale. *Untrained* means you have not knowingly practiced this and may not even know what it would feel like to practice it. *Aware* means you can name the capacity and recognize when it is at issue, but you do not yet have a routine for it. *Practicing* means you have a routine and you execute it imperfectly. *Fluent* means it is reflex — you do it without thinking, and you can teach it.

| Capacity | Untrained | Aware | Practicing | Fluent | Notes |
|---|:---:|:---:|:---:|:---:|---|
| **Strategic Delegation** | ☐ | ☐ | ☐ | ☐ |  |
| **Effective Communication** | ☐ | ☐ | ☐ | ☐ |  |
| **Critical Evaluation** | ☐ | ☐ | ☐ | ☐ |  |
| **Technical Understanding** | ☐ | ☐ | ☐ | ☐ |  |
| **Ethical Reasoning** | ☐ | ☐ | ☐ | ☐ |  |
| **Stochastic Reasoning** | ☐ | ☐ | ☐ | ☐ |  |
| **Learning by Doing** | ☐ | ☐ | ☐ | ☐ |  |
| **Rapid Prototyping** | ☐ | ☐ | ☐ | ☐ |  |
| **Theoretical Foundations** | ☐ | ☐ | ☐ | ☐ |  |

*Figure 2.4*

Don't agonize. Five minutes. Pick the level that is closer to true than the alternatives and move on.

When you have nine answers, look at them and pick the two capacities you most want to move up one level in the next ninety days. Not the ones you are already strongest in — that is comfortable and unproductive, and I have watched many smart people make exactly that mistake. Pick the ones that are slightly painful to look at honestly. Those are the ones where deliberate practice will buy you the most working capability in the next three months.

You are going to come back to these two at the end of the book — in Chapter 13's 90-Day Plan — and the comparison between what you said you would work on and what you actually improved at will teach you something about yourself that I cannot teach you here.

The Loop, which the previous chapter introduced, is the workflow. The nine capacities are what the workflow draws on. The Loop tells you what steps to take. The capacities are what makes those steps go well or badly. Hold both in your head as we go. The rest of the book develops them in parallel, and the chapters are designed so that you can read them in the order that matches the two capacities you just wrote down.

Priya, by the way, made her two picks the day the correction went up. She picked Critical Evaluation and Learning by Doing — the second and fourth of her four failures. The Strategic Delegation failure she could fix by writing a delegation map at the top of every data-heavy piece, and that habit was already forming. The Stochastic Reasoning failure was real but downstream of the other three: if she stopped treating confident model output as certain, the probability question took care of itself. The two she picked were the ones she could not fix by procedure. They required a different kind of attention, which is exactly what the 90-Day Plan is for.

---

### Translate before you move on — and start the Practitioner Profile

This chapter ends with the first half of a portfolio artifact you will complete in Chapter 4.

**The Practitioner Profile — Part 1 (Layer A template + Layer B content, diagnostic):**

Run the self-assessment. Mark a box for each of the nine capacities. Take five minutes. Don't agonize.

Then, below the table, name your two priority capacities — the two you most want to move up one level in the next ninety days — and write one sentence for each on *why*. Not "because I'm weak there" — that's not yet a reason. Something specific: a failure mode you recognize in your own work, a kind of task where you notice the gap, a senior practitioner whose strength you want to match.

Save as `portfolio/02-practitioner-profile.md`. This file is incomplete — Chapter 4 adds the Delegation Map as the second half. The combined Practitioner Profile becomes one consolidated diagnostic artifact in your portfolio. Future readers (a future employer, an admissions panel, your future self) read it to understand what kind of practitioner you are and where you are growing.

The Practitioner Profile is a Layer A diagnostic — the structure is the same for every reader — filled with Layer B content (your honest self-assessment in your domain). The honesty is what makes it credible. A profile that says you are *fluent* across all nine capacities is either lying or has not been worked through. A profile that names two specific gaps you are actively practicing against is the document a future reader respects.

---

*What would change my mind.* If a careful empirical study showed that fluent AI practitioners systematically share fewer than nine of these capacities — say, four or five appear together and the rest are decorative — the architecture needs revision. The list emerged from observation, not from theory. It is testable, and I would update if the test came back differently.

*Still puzzling.* I do not yet know whether the nine capacities are separable in practice. They may correlate so strongly with general professional judgment that "develop the nine capacities" reduces, empirically, to "develop professional judgment generally." I think they are separable enough to teach individually. I do not have the longitudinal data to be sure.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Three of the Nine Capacities have full chapters of treatment in the advanced volume, useful when you decide one of them is the capacity you most need to develop:
>
> - **Stochastic Reasoning** — the deeper book starts from Bayes' theorem and base rates and shows why a "99% accurate" test can be useless on a rare event, and what calibration curves reveal that accuracy hides. See *Computational Skepticism for AI*, **Chapter 2 — Probability, Uncertainty, and the Confidence Illusion**.
>
> - **Critical Evaluation** — the deeper book gives you the four verification layers (fact, reasoning, framing, omission) and treats the *technically-accurate-practically-misleading* failure mode formally. See *Computational Skepticism for AI*, **Chapter 6 — Model Explainability**.
>
> - **Ethical Reasoning** — the deeper book proves that three reasonable definitions of fairness cannot all hold on the same dataset when base rates differ, and gives you the *defended-choice* deliverable that engineers in regulated industries are increasingly required to produce. See *Computational Skepticism for AI*, **Chapter 7 — Fairness Metrics**.

---

## Exercises

### Warm-Up

**1. Name the failure.** *(Capacity identification | Difficulty: low)*
Return to Priya's story. Four distinct failures are pulled apart in the opening movement. For each one, write a single sentence naming what Priya should have done differently at exactly that moment. Stay at the level of action, not theory — what is the specific move she skipped?

**2. Match the diagnostic question.** *(Capacity recall | Difficulty: low)*
Without looking back, write the diagnostic question for any five of the nine capacities. Then check. For each you missed or got wrong: what made it not stick? Rewrite it in your own words — one that you would actually ask yourself mid-task.

**3. Identify the missing specification.** *(Effective communication | Difficulty: low)*
A marketing associate prompts an LLM: "Write a tagline for our new product line." She gets ten options, picks one, and the client approves it. Six months later the tagline turns out to echo a competitor's decade-old slogan. List every piece of information she failed to give the model, in the order that omission became consequential. Then write the prompt she should have sent.

---

### Application

**4. Decompose a real task.** *(Strategic delegation | Difficulty: medium)*
Take a task you actually completed in the last week — with AI or without. Break it into its component subtasks. For each subtask, apply the strategic delegation diagnostic: *what should I give the AI, what should I keep, and why?* Write out your reasoning for at least three subtasks. Then ask: did you actually split the work this way? If not, what would have changed if you had?

**5. Import the uncertainty.** *(Stochastic reasoning | Difficulty: medium)*
A model returns this output in response to a business decision question: "Based on current trends, there is approximately a 70% chance that the new feature will increase retention." Write three questions you would ask — or three investigations you would run — before using that number in a decision. For each question, name the kind of uncertainty it is probing: the model's training data, the model's reasoning process, or the underlying variability of the world.

**6. Stress-test an output.** *(Critical evaluation | Difficulty: medium)*
Take any AI-generated text output you produced or received in the last month. Apply the question Priya failed to ask: *what would have to be true for this to be wrong?* Generate at least three specific failure scenarios. For each: how would you check whether that failure is present? What is the cheapest verification that would catch it?

**7. Classify the durability.** *(Technical understanding + theoretical foundations | Difficulty: medium)*
The chapter places critical evaluation and stochastic reasoning in the "contested" category — capacities where models may erode the human's role on a shorter timeline than the durable ones. Pick one of these two. Write a one-paragraph argument that the chapter has it wrong — that this capacity is actually durable, and a well-reasoned case can be made that humans will always need to own it. You do not have to believe the argument. Argue from evidence, not from instinct.

---

### Synthesis

**8. The hiring manager case.** *(Ethical reasoning + strategic delegation + critical evaluation | Difficulty: medium-high)*
A hiring manager screens 200 résumés for an engineering role by passing all of them through an AI tool that returns a ranked top 20. She does not audit the tool, does not examine how it was trained, and reviews no résumé outside the top 20. Identify every capacity she failed to exercise. For the two you consider most consequential: explain not just what she failed to do but what specific harm could result. Then describe the minimum practice — one action per capacity — that would have meaningfully reduced that risk without abandoning the tool.

**9. Design the atrophy test.** *(Learning by doing | Difficulty: high)*
The chapter describes a failure that is slow — a capacity that gets weak before it visibly fails. Priya had used to verify fiscal-year conversions when she was a junior reporter; the AI had taken that out of her routine without taking it out of her ability. Choose a professional skill from your own domain that you believe is in your daily practice right now. Describe, concretely, what early-warning signs would tell you that skill is being quietly eroded by AI use — before the first visible failure. Then design a specific practice routine, executable in under 20 minutes per week, that would keep the skill load-bearing regardless of how much AI you use alongside it.

---

### Challenge

**10. Audit the architecture.** *(All nine — critical stance | Difficulty: high)*
The chapter admits it does not have longitudinal data to confirm the nine-capacity decomposition is doing real work. Treat this as an invitation. Based on your own experience using AI tools professionally, make one of the following arguments in 400–600 words, supported by at least two concrete cases or observations:

- One of the nine capacities should be split into two distinct capacities (name the split and explain what separate failure it captures).
- Two of the nine should be merged (they reliably co-occur and cannot be meaningfully separated in practice).
- A tenth capacity is missing (name it, give its diagnostic question, describe the failure its absence causes).

You are not required to be right. You are required to argue from evidence rather than from theory alone.

---

### A note about AI

The nine capacities are a framework for what fluent practice looks like. The model can recite the framework. Reciting is not practicing.

Where the model genuinely helps: testing your understanding of each capacity against worked scenarios. Paste a workflow and ask the model which capacities it exercises and which it skips. The diagnosis is useful even when imperfect.

Where the model does damage: assessing whether you are personally fluent. The model has not seen you work. It can produce a confident self-assessment for you, which is the worst possible substitute for the actual self-assessment.

The rule: use the framework on your work; do not use the model to grade you on the framework.

---

## LLM Exercise — Chapter 2: The Nine Capacities

**Project:** AI Fluency for [Your Role] — Your Practitioner Profile

**What you're building this chapter:** Two pieces. (a) Nine domain-specific failure scenes — one per capacity — that anchor each capacity in your role's actual tasks. (b) The first half of your **Practitioner Profile** — the capacities self-assessment with two priority picks named honestly. Both saved to `portfolio/`. The Profile pairs with the Delegation Map from Chapter 4 to become one consolidated diagnostic artifact.

**Tool:** Claude Project (continue — your Role Dossier, Baseline Audit, Worked Loop Log, and CLAUDE.md are in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier from Chapter 0, my
Worked Loop Log from Chapter 1, and my opening CLAUDE.md are in the
Project context.

Botspeak Chapter 2 watches Priya — a journalist twelve months past
Chapter 0 — receive a Letters-to-the-Editor email about a state-by-state
lag-time table in a piece she wrote three weeks earlier. The model had
silently mishandled fiscal-year-to-calendar-year conversions for several
states. The chapter unpacks four distinct capacity failures from that
one error and uses the constellation to introduce the Nine Capacities
plus the four-level self-assessment (untrained / aware / practicing /
fluent).

For Chapter 2's portfolio artifacts, do two things.

TASK 1 — NINE FAILURE SCENES IN MY ROLE.
Write nine short failure scenes, one per Capacity, all set in my role.
Each scene 100–200 words. Each scene a different (named) person in a
different sub-context of the role. Each scene a clean instance of the
capacity's failure mode. Use real tools, real artifacts, real
stakeholders for my role.

The Nine Capacities and the chapter's diagnostic question for each:

1. STRATEGIC DELEGATION — what should I give the AI, what should I keep,
   and why?
2. EFFECTIVE COMMUNICATION — am I telling the model what it actually
   needs to know to do this well?
3. CRITICAL EVALUATION — would I bet on this output, and on what
   evidence?
4. TECHNICAL UNDERSTANDING — do I know enough about how this system
   works to recognize when it's failing?
5. ETHICAL REASONING — who could be harmed by this output or this
   deployment, and am I tracking that?
6. STOCHASTIC REASONING — what kind of probabilistic claim is this, and
   what would calibrate my belief in it?
7. LEARNING BY DOING — am I still building the skill, or just consuming
   the output?
8. RAPID PROTOTYPING — am I treating model output as the work, or as a
   draft I will pressure-test in the world?
9. THEORETICAL FOUNDATIONS — do I understand the underlying material
   well enough to judge whether this output is good?

Resist the temptation to make all nine scenes about the same task type.
Spread them across my role's sub-contexts so the scenes engage different
parts of the work.

Save the nine scenes as `portfolio/02-nine-scenes-in-my-role.md`. (This
is a supporting file in the portfolio — not the Practitioner Profile
itself, which comes next.)

TASK 2 — DRAFT MY PRACTITIONER PROFILE (PART 1).
Help me draft the first half of my Practitioner Profile. The Profile is
a Layer A diagnostic — the structure is standard — filled with Layer B
content (my honest self-assessment in my domain).

The Profile has three sections:

1. CAPACITIES SELF-ASSESSMENT. The nine-row table from Chapter 2,
   filled in honestly. For each capacity: my current level (untrained
   / aware / practicing / fluent) plus one specific note — a failure
   I recognize, a task type where I notice the gap, a senior practitioner
   whose strength I want to match.

2. TWO PRIORITY CAPACITIES. The two I most want to move up one level
   in the next 90 days. One sentence each on WHY — not "because I'm
   weak" but something specific. These two will become the 90-Day
   Plan in Chapter 13.

3. PLACEHOLDER FOR PART 2. A note that the second half of the
   Practitioner Profile (the Delegation Map) will be added in
   Chapter 4, after which the combined Profile becomes one consolidated
   diagnostic artifact in my portfolio.

Push back on me if my self-assessment looks too generous — a Profile
that rates fluent across the board is either lying or unworked.

Save as `portfolio/02-practitioner-profile.md`.
```

---

**What this produces:** Two additions to your portfolio. The nine scenes file (`portfolio/02-nine-scenes-in-my-role.md`) — a research artifact you can update as you encounter your own failures. The Practitioner Profile Part 1 (`portfolio/02-practitioner-profile.md`) — the first half of one of the portfolio's three diagnostic artifacts. ~2,500–4,000 words across the two.

**How to adapt this prompt:**

- *For your own project:* The nine scenes ARE the playbook's diagnostic instrument. Don't rush them. A reader who recognizes themselves in three of nine scenes is a reader the playbook has already earned.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Not the right fit — this is narrative and self-reflection.
- *For Cowork:* Recommended. Cowork can manage the multi-file split (`02-nine-scenes-in-my-role.md` and `02-practitioner-profile.md`).

**Connection to previous chapters:** Chapter 0 produced the Baseline Audit, Chapter 1 produced the Worked Loop Log and opened the `CLAUDE.md`. Chapter 2 produces the first half of your Practitioner Profile (the capacities side). Chapter 4 produces the second half (the delegation side). Combined, they are one diagnostic artifact in the finished portfolio.

**Preview of next chapter:** Chapter 3 produces the Specification Library — 1–3 worked specifications for your most common task types, plus your `PROJECT.md` template. The Specification Library is the third piece of evidence in your portfolio's Layer B (the first being the Worked Loop Log, the third being the End-to-End Case Study in Chapter 8).

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Lev Vygotsky** was working out how cognitive capacities form — that they live first in the joint activity between a learner, the world, and a tool, and only later become individual reflexes — decades before anyone worried about AI-mediated skill atrophy. The capacities in this chapter are not innate traits the reader either has or doesn't. They are made and unmade through the company a learner keeps with their tools. Here's a prompt to find out more — and then make it better.

![Lev Vygotsky, c. 1930. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/lev-vygotsky.jpg)
*Lev Vygotsky, c. 1930. AI-generated portrait based on a public domain photograph.*

![Lev Vygotsky](../images/lev-vygotsky-755.png)

*Puppet Art by [Nik Bear Brown](https://www.nikbearbrown.com/).*

**Run this:**

```
Who was Lev Vygotsky, and how does his concept of the Zone of Proximal
Development connect to the idea that the Nine Capacities are built
through mediated practice with tools — including AI — rather than
learned in the abstract? Keep it to three paragraphs. End with the
single most surprising thing about his career or ideas.
```

→ Search **"Lev Vygotsky"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "Zone of Proximal Development" in plain language, as if you've never taken a psychology course
- Ask it to compare Vygotsky's account of mediated tool use to the early-warning signs of a capacity going slack from AI use
- Add a constraint: "Answer as if you're writing a footnote in a chapter called The Nine Capacities"

---

## References

1. L. S. Vygotsky, *Mind in Society: The Development of Higher Psychological Processes*, Cambridge, MA: Harvard University Press, 1978. https://en.wikipedia.org/wiki/Zone_of_proximal_development
