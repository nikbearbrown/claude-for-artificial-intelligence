# Chapter 3 — Specification
*Doing the Thinking the Model Cannot Do for You.*

It is 4:11 PM on a Wednesday and Priya Banksy is having her third bad iteration in a row with Claude.

Her editor has asked her to summarize a 62-page industry report — a clean-energy storage trade group's annual deployment outlook — for the next morning's editorial standup, where the desk will pick which two story angles to commission for the week. Priya is ten months past her Pew correction. She has the Loop down. She has been writing specifications. She thought she had this one. She uploads the PDF, types *summarize this report for tomorrow's editorial meeting*, and gets back a clean 600-word summary. It is fine. It is not what her editor wants. Her editor wants the parts the desk could turn into reporting angles, not a neutral summary. Priya types: *summarize this report for tomorrow's editorial meeting, focusing on the most reportable findings.* She gets another 600-word summary, slightly differently weighted, still not it. Her editor wants something that fits in five bullet points on a slide for the standup. Priya types: *summarize this report in five bullet points.* She gets five bullets, each three sentences long, and her editor wants each bullet to be one short clause readable from twenty feet away in a conference room.

By the third iteration Priya has spent forty minutes and produced something her editor will rewrite anyway. She closes the tab. She concludes, briefly, that Claude is not very good at this.

Claude is not good at this because Priya has not told Claude what *this* is.

This is the thing I want to understand with you, because it is not a prompting failure in any deep sense. It is a failure of *specification*, which is different from prompting, and which most people who pick up an AI tool never learn to do because nobody has named it separately.

The difference is this: a prompt is what you type. A specification is what you know before you type it.

Language models are, among other things, fluency machines. They are extraordinarily good at producing coherent, plausible-sounding output in whatever direction you point them. The catch is that if the direction is unclear, the fluency just makes the wrong output look convincing. You get something that reads well and misses the point, which is in some ways worse than something that obviously fails — at least the obvious failure tells you immediately to try again. When Priya got three different polished summaries that were each not quite right, the polish was making it harder to see the problem, not easier.

When people say "the AI didn't give me what I wanted," they usually mean one of two things. Either the model genuinely misunderstood a clear request — this happens, but less often than people think. Or they didn't yet know what they wanted with enough precision for anyone — model or human — to give it to them. The second failure is much more common, and much less visible, because the model's fluency produces output that looks like the problem was almost solved, which creates the impression of a near-miss rather than a specification failure.

The specification move is, in part, a diagnostic on yourself. That is exactly why it is hard.

---

Here is what a working specification contains. I am going to name five components, and the list is not glamorous. It is infrastructure — the kind of thing that sounds boring because it holds something up rather than being the thing held.

![Figure 3.1 — A five-part diagram](images/03-specification-fig-01.jpg)

The first is **intent**: not the immediate task, but the goal the task serves. Priya's intent was not *produce a summary*. Her intent was *give the editorial desk five reportable-angle bullets they can argue against tomorrow morning to pick the week's two stories.* Those are not the same thing, and the model had no way to know which one she meant. The intent statement is what tells the model — and you — what counts as success.

The second is **constraints**: what the output has to fit inside. Format constraints: five bullets, one clause each, no sub-bullets. Length constraints: under a hundred words total. Source constraints: only claims that appear in the report, not the model's outside knowledge. Audience constraints: the standup attendees, who have not read the document. Constraints are the parts of the specification the model would otherwise guess at — and guess wrong — while producing output that looks like it could be right.

The third is **success criteria**: how you will know, after the fact, that the output is good. *The editor uses it in the standup without rewriting* is a real success criterion. *Each bullet would survive a reporter asking "show me where in the report this comes from"* is a real success criterion. Without success criteria, every output looks plausibly fine, and you are left with a vague dissatisfaction you cannot diagnose.

The fourth is **exclusions**: what the model is not supposed to do. Do not invent sources. Do not pad bullets to make them feel substantive. Do not include the executive summary verbatim. Do not characterize the trade group's framing as if it were independent. This sounds like a strange thing to have to specify. But language models fill in blanks. If you leave a blank, they will fill it with their best guess at what looks complete. Exclusions are the specification saying: *please leave that blank blank.*

The fifth is **output format**: what the deliverable looks like structurally. Markdown or plain text. Bullet list or prose. Five items on their own lines or a flowing paragraph. This feels like a detail. It is not a detail. The format constrains the kind of thinking the model has to do, and a bullet list and a paragraph on the same intent will produce different content, not just different presentation.

Now watch what Priya would have sent if she had specified before prompting:

> **Intent:** Give the editorial desk five reportable-angle bullets they can argue against tomorrow morning to pick the week's two stories from the clean-energy-storage deployment outlook.
>
> **Constraints:** Five bullets total, one clause each, ≤15 words per bullet, source only the attached report, audience has not read the report, audience is reading the bullets off a slide from across a conference room.
>
> **Success criteria:** Editor uses them in the standup without rewriting; each bullet survives a reporter asking "show me where in the report"; the desk picks two stories from the five candidates.
>
> **Exclusions:** Do not editorialize beyond what the report supports. Do not pad. Do not include the executive summary verbatim. Do not present the trade group's framing as if independent.
>
> **Output format:** Five bullets, each on its own line, no sub-bullets, no preamble, no closing sentence.

| Prompt as sent | Component groping toward — but never stated | What the omission cost |
|---|---|---|
| *"Summarize this report for tomorrow's editorial meeting."* | Nothing. No component is present. | Model guessed the task. Produced a neutral 600-word summary — polished, directionless, unusable. |
| *"Summarize this report for tomorrow's editorial meeting, focusing on the most reportable findings."* | **Intent** — partially. Adds purpose-direction but the actual goal (slide artifact, story-selection standup, reportable-angle bullets) remains unstated. | Model reweighted the summary slightly. Still 600 words, still not slide-ready. The polish made the near-miss hard to name. |
| *"Summarize this report in five bullet points."* | **Output Format** — partially. Adds bullet structure but omits length per bullet, preamble rules, and hierarchy constraints. | Model produced five bullets, each three sentences long. Format was closer; content was still unfit for a slide read from across a conference room. |
| **Complete specification:** Intent (standup angle-selection slide) + Constraints (≤15 words per bullet, report only, unread audience, conference-room read) + Success Criteria (editor uses without rewriting; bullets survive reporter scrutiny; desk picks two stories) + Exclusions (no editorializing, no padding, no verbatim executive summary, no trade-group framing) + Output Format (five bullets, own lines, no sub-bullets, no preamble) | **All five components present.** | Editor uses it in the standup without rewriting. |

That is not a prompt. It is the thinking a prompt needs to encode. The actual prompt Priya types may be two or three sentences long — but those sentences will carry all five components because she now knows what they are.

---

I want to admit something about why this is hard, because the difficulty is not what most people expect.

Most people, when they first try to specify before prompting, discover that they do not fully know what they want. They thought they did. They sit down to write the intent statement and find they have not yet decided what the goal is. They sit down to write the success criteria and find they have none. They sit down to write the exclusions and realize they had been counting on the model to make those decisions for them — even though they would never have described it that way.

This is uncomfortable. It is also the specification doing its job.

Think about what happens in a well-run organization when someone delegates a task. The good editor does not walk up to a reporter and say *can you write something about the storage report?* and walk away. She says: *I need five slide-ready bullets from the trade group's storage outlook — one clause each, no longer than fifteen words, only claims that are in the document, by 8:30 tomorrow, because we are using them at the 9 AM standup to argue for the two stories we'll commission this week.* The reporter now has enough to do the work. The editor had to do that thinking before she opened her mouth.

Language models are not different. They are, in a certain mechanical sense, colleagues who have read a great deal and who will attempt in good faith to do what you ask. What they cannot do is want things on your behalf. They cannot supply the goal you forgot to specify. And because they are fluency machines, when the goal is missing, they will produce something that sounds like a goal was present — something plausible, coherent, and wrong in a way that is difficult to name.

The specification move forces you to do the thinking the delegation requires. This is why experienced practitioners produce better output not primarily because they know better phrases, but because they have learned to specify before they prompt. The specification is the work. The prompt is the document recording it.

---

Let me say something about templates, because this is where the specification stops being slow.

The five components feel like overhead the first time. They feel like overhead the fifth time. By the twentieth time you do the same kind of task, the overhead is gone — because you have a template.

A template is a specification you wrote once for a category of recurring work, with the variable parts marked, that you fill in rather than invent from scratch. Priya's report-summary-for-standup specification, captured as a template, becomes:

> **Intent:** Give [recipient] a [length/format] artifact for [specific purpose].
>
> **Constraints:** [format details], source: only [permitted sources], audience: [who reads it].
>
> **Success criteria:** [recipient action/test 1]; [recipient action/test 2]
>
> **Exclusions:** Do not editorialize. Do not pad. Do not include [common over-include item]. Do not [role-specific failure mode].
>
> **Output format:** [structural details, length, sections].

![A filled-in specification template card — Priya's clean-energy-storage-summary task with all five fields completed](images/03-specification-fig-03.png)
*A filled-in template card*

The next time Priya summarizes a long document for a high-stakes deliverable, she fills in the brackets. The thinking she did the first time is now infrastructure. The template does not do the thinking for her — she still has to know her intent, her constraints, her success criteria. But it reminds her to have them, and it gives her a form to put them in.

Build templates for the five tasks you do most often this quarter. Refine them as you discover what was missing. The fluent practitioner has a small library of templates and rarely starts a specification from scratch. The literate user invents the wheel every time, and every time runs into the same missing components she forgot last time.

This chapter is where your portfolio's **Specification Library** opens. You will fill it in by the end of the chapter.

---

There is a level of practice above templates, which is the use of *patterns*. A pattern is a compressed structure for part of the specification — a shorthand that the model handles especially well. I want to introduce one pattern here, not because it is magic, but because seeing one will help you understand what all patterns are.

The pattern is called **role-and-rubric**, and it has two pieces.

The role piece assigns the model a specific professional persona: not *act like a friendly assistant* but *act as a senior energy-policy researcher with a decade of grid-storage experience preparing one-page bullet summaries for a newsroom editorial standup.* The role compresses a great deal of constraint and tone into a single phrase the model can hold in mind while generating. The model does not have that experience in any meaningful sense. But it has read enough text produced by people in that role that the assignment shifts the statistical weight of its output toward what such a person would actually write.

The rubric piece supplies explicit criteria the output will be judged against: *each bullet must be defensible against a reporter asking "where in the report is this"; no claim that goes beyond what the report supports; tone declarative, not hedged; no language that mirrors the trade group's framing; total under a hundred words.* The rubric is the success criteria and exclusions components, made explicit in a form the model can self-check against.

| Specification component | How role-and-rubric handles it |
|---|---|
| **Intent** | Partially. The role assignment implies a purpose ("senior policy researcher preparing one-page summaries") but does not state the goal the task serves. Still needs an explicit statement of what success looks like for this specific output. |
| **Constraints** | Poorly. Role implies tone and register but says nothing about length, permitted sources, or audience. These must still be stated explicitly. |
| **Success Criteria** | Well — this is what the rubric does. Explicit, testable criteria ("each bullet must be defensible against a reporter asking 'where in the report is this'") are the rubric's native function. |
| **Exclusions** | Well — also rubric territory. "No claim that goes beyond what the report supports" is a clean exclusion the rubric encodes directly. |
| **Output Format** | Not addressed. Neither the role nor the rubric specifies markdown vs. plain text, bullet vs. prose, or structural details. Must still be stated separately. |

Role-and-rubric is one pattern. There are others — chain-of-thought, few-shot examples, constraint stacking. Each compresses different parts of the five components into a structure the model handles well. They are scaffolds for the same five components, not alternatives to them. The mistake I see most often is reaching for a pattern before specifying. Someone reads about chain-of-thought and starts adding *think step by step* to every prompt, regardless of whether step-by-step reasoning is what the task requires. Patterns serve the specification. The specification does not serve the pattern. If you do not yet know your intent, adding *think step by step* will give you a fluent, step-by-step, wrong answer.

---

I want to address something the chapter so far has left implicit.

When you force yourself to write down the intent, you will sometimes discover that you have not decided what success looks like. When you write down the constraints, you will sometimes discover that two of them are in tension — you want it short and you want it comprehensive, and you have not yet decided which one wins. When you write down the exclusions, you will sometimes discover that what you were actually planning to ask the model to do is make a judgment call you should be making yourself.

These discoveries are not a sign that specification is too much work. They are the specification doing its job, which is to surface the parts of the task you had not yet thought through. A language model is a fluency amplifier. Give it half-formed intent, and it produces fluent half-formed output. Give it well-formed intent, and it produces fluent well-formed output. The fluency amplifies whatever you brought. This is not a flaw in the technology. It is a property of all powerful delegation: the quality of the output is bounded by the quality of the brief.

Sometimes, even with discipline, you do not yet know what you want. You are at the beginning of a problem, feeling around its edges. This is fine. *Exploratory* is itself a specifiable intent: *surface three to five distinct framings of this question without committing to one; optimize for variety over polish; do not produce a finished artifact.* That is a specification for uncertainty. It tells the model you are not looking for a polished output you will feel committed to — you are looking for raw material you can think with. Specification under uncertainty is not a contradiction. It is honesty about what stage of work you are in. The mistake is skipping the specification because the task feels unclear, which usually produces polished output that answers a question you were not actually asking, which you then feel oddly obligated to accept.

---

There is a prior question this chapter has been deliberately avoiding: whether to pass the task to the model at all.

Some tasks should not be delegated. Some should be delegated in pieces, with strong human judgment at the joins. Some should never leave your hands entirely. The specification move is how you get good output when you have decided to delegate. The question of *whether* to delegate — and what it costs when you do — is what the next chapter takes up.

Specification gets you a well-formed task to hand off. Delegation asks whether you should hand it off in the first place, and if so, how much of it. Those are different questions, and the order matters. You cannot ask the delegation question well until you have specified the task clearly enough to see what the task actually is. Which is one more reason the specification move comes first.

---

### Translate before you move on — build your Specification Library and open your PROJECT.md

Priya's task was a summary-for-editorial-standup. In your field, what is the equivalent? Not one task — your five most common recurring task types. The pieces of work that recur often enough in your week that the specification's cost amortizes across many uses.

For a clinician: the structured-note write-up, the patient-handoff brief, the chart review summary, the referral letter, the literature-search brief for an unfamiliar case. For a software engineer: the pull-request summary, the design-doc draft, the post-mortem write-up, the architecture-decision record, the user-facing release note. For a marketing manager: the campaign brief, the competitive-positioning memo, the audience-segment summary, the launch-readiness note, the executive summary. The specific five vary with the role. The shape — recurring, AI-amenable, distinct enough to need different specifications — is invariant.

**The Specification Library — Chapter 3 Portfolio Artifact (Layer B, deliverable):**

Build it. Five templates, one per recurring task type. Each template covers all five components with bracketed variables for the parts that change per instance and pre-populated constants for the parts that don't. Each template includes 1–2 exclusions specific to your role's typical failure modes for that task type.

For each template, also write one fully filled-in worked example — a specific instance you could imagine on your desk this week. The worked example is half the value. The template alone leaves the reader (your future self, a colleague who picks up the library) staring at brackets.

Save the library as `portfolio/03-specification-library/` (a folder, not a single file — one file per template, plus a worked example for each). The library is a pure Layer B artifact: every line is your domain's content. A future employer reading it sees exactly how you specify the work that fills your week.

**Open your PROJECT.md template.** This chapter is also where you draft the structure of the `PROJECT.md` template you will instantiate for every significant piece of work in Layer B from here forward. The PROJECT.md template has two layers — intent (what the project means, who the work is for, what success looks like) and technical state (what is built, what is pending, what was generated and accepted versus rejected). Save as `portfolio/PROJECT-template.md`. The keystone End-to-End Case Study in Chapter 8 will be the first project that gets a fully populated `PROJECT.md` instantiated from this template.

**Update your CLAUDE.md.** Add the rule the chapter has been arguing for, in your own language: something close to *I do not open the tool until I have written the five components down, in some form, somewhere I can see them.* That rule is the operational core of everything else the book teaches. Make it explicit in your `CLAUDE.md` so it travels with you.

---

*What would change my mind on this chapter.* If careful empirical work showed that experienced practitioners produce equivalent-quality output from one-sentence prompts and from full five-component specifications — that the specification is decorative for people who have done it enough times that it lives in muscle memory — I would have to revise the claim that specification is the load-bearing skill. What I observe is the opposite: experienced practitioners specify more, not less, and the specification gets tighter, not looser, as the task gets harder. But the observation is informal, and I hold it accordingly.

*Still puzzling.* I do not yet have a clean answer to when the cost of full specification exceeds the cost of iteration. For very small tasks — reword this sentence, fix this heading — it almost certainly does. The break-even point is task-dependent, and I have not found a rule that generalizes cleanly.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Specification, formalized at the level engineers use when they validate datasets and deployments, is called **reconstructing the epistemic frame**. The advanced book makes the point that every dataset and every prompt embeds a frame — what it claims to represent, what it actually represents, what it excludes — and that the most consequential failures live in assumptions the practitioner never wrote down: scope, sampling, definition, time, access. The five components in this chapter are the practitioner-grade version. The six-step epistemic-frame reconstruction in the advanced book is the engineering-grade version, with an explicit prediction-lock you do before you see any output, so the gap between expectation and observation can teach you.
>
> Reaching for the deeper version pays off when you specify automations (Chapter 10 of this book) or design AI deployments other people will rely on.
>
> See *Computational Skepticism for AI*, **Chapter 5 — Data Validation: Reconstructing the Epistemic Frame Behind a Dataset**.

---

### A note about AI

Specification is the capacity the model most rewards and most masks. A model will produce something for almost any prompt, which means underspecified prompts succeed often enough to mask the cost of underspecifying.

Where the model genuinely helps: rewriting your specification at three levels of precision and showing the resulting outputs side by side. The contrast makes the cost of vague specification visible in a way that abstract advice never does.

Where the model does damage: producing the specification for you. The specification has to encode what you actually want, which is a judgment the model cannot make.

The rule: practice specification by writing it. The model can show you the consequences of vague writing. It cannot do the writing for you.

---

## LLM Exercise — Chapter 3: Specification

**Project:** AI Fluency for [Your Role] — Your Specification Library

**What you're building this chapter:** Your portfolio's first Layer B deliverable folder — five specification templates, one per recurring task type in your role, each with a worked example. Plus the opening draft of your `PROJECT.md` template. Plus one new rule added to your `CLAUDE.md`.

**Tool:** Claude Project (continue — your Role Dossier, Worked Loop Log, Practitioner Profile Part 1, and CLAUDE.md are in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile Part 1, and CLAUDE.md are in the Project context.

Botspeak Chapter 3 watches Priya — ten months past Chapter 0 — produce
three failed iterations on a single summarize-for-the-editorial-standup
task. The chapter introduces the five specification components: INTENT
(the goal the task serves), CONSTRAINTS (what the output must fit
inside), SUCCESS CRITERIA (how I'll know it's good), EXCLUSIONS (what
the model is NOT supposed to do), OUTPUT FORMAT (structural details).

For Chapter 3's portfolio artifacts, do three things.

TASK 1 — IDENTIFY THE FIVE MOST COMMON TASK TYPES IN MY ROLE.
Not nine, not three. Five. The task types should be:
- High-frequency (each appears multiple times per month for someone in
  my role)
- Distinct enough that they require different specifications
- AI-amenable (it's plausible to do them with AI assist)
- Spanning the role — not all the same kind of work

For each task type, name it precisely and give 2–3 examples of when
it occurs.

TASK 2 — A SPECIFICATION TEMPLATE PER TASK TYPE + A WORKED EXAMPLE.
For each of the five task types, produce a fillable specification
template covering all five components, with bracketed variables for
the parts that change per instance and pre-populated constants for
the parts that don't. Include 1–2 EXCLUSIONS specific to my role's
typical failure modes for this task type.

The template format I want:

TEMPLATE — [task type name]

Intent: Give [recipient] a [length/format] artifact for [specific purpose]
Constraints: [bracketed format details], source: [permitted sources], audience: [who reads it]
Success criteria: [recipient action/test 1]; [recipient action/test 2]
Exclusions: Do not [role-specific failure mode 1]. Do not [role-specific failure mode 2]. Do not [generic failure mode].
Output format: [structural details, length, sections]

Then, for each template, write one fully-filled-in worked example
showing what the template looks like populated for a specific instance
I could imagine on my desk this week. The worked example is half the
value — the template alone leaves the reader staring at brackets.

Save each template + worked example as a separate file under
`portfolio/03-specification-library/`. One file per task type.

TASK 3 — DRAFT MY PROJECT.md TEMPLATE.
Draft my personal PROJECT.md template — the Layer A scaffold I will
instantiate for every significant piece of work in Layer B of my
portfolio going forward. Two layers:

LAYER 1 — INTENT (what the project means, who the work is for, what
success looks like, the question the work is answering, where the
load-bearing judgment lives).

LAYER 2 — TECHNICAL STATE (what is built, what is pending, what was
generated by the model and accepted, what was rejected and why, what
verifications have been run, what was done by hand).

Save as `portfolio/PROJECT-template.md`. The keystone End-to-End Case
Study in Chapter 8 will instantiate this template for the first time.

TASK 4 — ADD ONE RULE TO MY CLAUDE.md.
Add the chapter's operational rule, in my own language. Something close
to: "I do not open the tool until I have written the five components
down, in some form, somewhere I can see them." Phrase it in a way that
fits my actual workflow.

Append the rule to my existing `portfolio/CLAUDE.md`.

End with one paragraph on the role-specific specification trap: what
is the failure mode that practitioners in my role most often produce
when they specify badly? What in my role tends to be most often left
unsaid? Save that paragraph at the top of the specification library
folder as `00-the-trap.md`.
```

---

**What this produces:** Your portfolio gains a folder (`portfolio/03-specification-library/`) containing five templates + five worked examples + the role's specification trap, plus a new file (`portfolio/PROJECT-template.md`) and an addition to `portfolio/CLAUDE.md`. The Specification Library is the first Layer B deliverable folder in your portfolio. ~3,000–5,000 words across the artifacts.

**How to adapt this prompt:**

- *For your own project:* The templates' value depends on the EXCLUSIONS section being honest about your role's typical failure modes. Be specific about what gets botched.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful here if your role's tasks are code-heavy and the templates can live as structured prompt files in a repo. Otherwise, plain Markdown.
- *For Cowork:* Recommended. Cowork can manage the multi-file folder structure cleanly.

**Connection to previous chapters:** Chapter 2's nine scenes named where your capacities currently fail. Chapter 3 builds the operational antidote at the Specification step. The PROJECT.md template opened here will be instantiated for the first time in Chapter 8's keystone case study.

**Preview of next chapter:** Chapter 4 produces the second half of your Practitioner Profile — the Delegation Map. Combined with Chapter 2's capacities self-assessment, the Profile becomes one consolidated diagnostic artifact in your portfolio.

---

## Exercises

### Warm-Up

**1. Name and test the five components.** *(Component recall | Difficulty: low)*
Without looking back, name the five specification components. For each one, write a single sentence describing what goes wrong when that component is missing — not in theory, but in practice. What does the output look like? What does the failure feel like from the user's side?

**2. Diagnose a weak prompt.** *(Component identification | Difficulty: low)*
Take this prompt: *"Write an email to my team about the new meeting policy."* Identify which of the five components are present and which are absent. Then rewrite it as a full specification. Your specification should be specific enough that a model — or a competent human colleague — could produce the deliverable without asking a single clarifying question.

**3. Trace Priya's iterations.** *(Component sequencing | Difficulty: low)*
Return to Priya's three prompts. For each iteration — *summarize this report for tomorrow's editorial meeting*, then *focusing on the most reportable findings*, then *in five bullet points* — name the single specification component she added (or groped toward) with that iteration, and the components still missing at that point. Then name the one component whose absence caused the most damage across all three attempts.

---

### Application

**4. Write a full specification.** *(All five components | Difficulty: medium)*
You are a marketing analyst preparing a competitive summary for a product launch. Write a complete five-component specification for this task. It should be specific enough that a model — or a competent colleague — could produce the deliverable without asking a clarifying question. Then identify which component was hardest to write, and explain why.

**5. Find the internal conflict.** *(Constraint tension | Difficulty: medium)*
Below is a specification with a hidden conflict:

> **Intent:** Produce a thorough analysis of all relevant risks.
> **Constraints:** Two pages maximum.
> **Success criteria:** A senior executive can read it in under three minutes and feel fully informed.
> **Exclusions:** Do not omit anything material.
> **Output format:** Prose paragraphs, no headers.

Name the conflict. Explain what will happen if this specification is sent to a model without resolving it. Then rewrite the specification to resolve the tension — you will have to make a real decision about which constraint wins.

**6. Explain the pattern's limits.** *(Role-and-rubric | Difficulty: medium)*
Explain why role-and-rubric is not a substitute for the five-component specification. Which components does it compress well? Which does it leave unaddressed? Give a concrete example — a specific task and a specific role assignment — where using role-and-rubric without addressing the missing components would produce a plausible but wrong output.

**7. Defend the templates.** *(Templates as infrastructure | Difficulty: medium)*
A colleague argues: "Templates are just bureaucracy. Good practitioners know what they want intuitively and don't need to fill out a form." Construct the strongest version of this argument — make it as compelling as you can. Then explain why you agree or disagree, using the chapter's reasoning about where specification overhead actually goes and what it does when it lands there.

---

### Synthesis

**8. Build a template library.** *(Specification across domains | Difficulty: hard)*
You are building a template library for a legal research team. Their three most common tasks are: summarizing case law for a partner review memo, drafting initial client intake questions, and checking a contract clause against a regulatory standard. Write a specification template for each task. For each template, note which component was hardest to generalize across instances of that task type, and why.

**9. Connect specification to the diagnostic.** *(Specification + self-knowledge | Difficulty: hard)*
The chapter claims the specification move is "in part, a diagnostic on yourself." Connect this to the chapter's discussion of exploratory work. Under what conditions is the diagnostic uncomfortable in a productive way — meaning it surfaces something you needed to know? Under what conditions is it a signal that you should not be delegating this task at all? Where does the chapter leave this question open, and what would you need to know to close it?

---

### Challenge

**10. Solve the still-puzzling.** *(Open-ended | Difficulty: high)*
The chapter ends with a stated puzzle: "I do not yet have a clean answer to when the cost of full specification exceeds the cost of iteration." Propose a framework for answering this question. Your framework should account for at least four variables — task type, stakes, novelty, and practitioner experience level — and should make a falsifiable prediction: given a specific task description, your framework should tell you whether to specify fully or iterate. Then identify the weakest assumption in your framework and explain what evidence would cause you to revise it.

**11. Teach the five components.** *(Feynman test | Difficulty: high)*
Design a 45-minute session for a team of ten that teaches the five-component specification to people who have never heard the term. Your design should specify: the opening problem you would pose and why it is the right problem, the order in which you would introduce the five components and why that order, the single exercise you would run after the third component is introduced, and how you would close the session. For each design decision, cite the chapter's reasoning about why specification is hard to learn and where the difficulty actually lives.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **W. Edwards Deming** was arguing that most failures are failures of the *system* — not the worker, not the tool — decades before anyone said "prompt engineering." His concept of the *operational definition* made the same claim this chapter does: you cannot measure quality, assign a task, or evaluate an outcome until you have defined, with enough precision that two people would reach the same conclusion, what you are actually asking for. A vague request is not a starting point. It is an instruction to guess. Here's a prompt to find out more — and then make it better.

![W. Edwards Deming, c. 1980s. AI-generated portrait based on a public domain photograph.](images/w-edwards-deming.jpg)
*W. Edwards Deming, c. 1980s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

![W. Edwards Deming](../images/w-edwards-deming-efb.png)

*Puppet Art by [Nik Bear Brown](https://www.nikbearbrown.com/).*

**Run this:**

```
Who is W. Edwards Deming, and how does his concept of the operational
definition connect to the idea that careful specification — not better
tools or smarter workers — is the main defense against failure? Keep
it to three paragraphs. End with the single most surprising thing about
his career or ideas.
```

→ Search **"W. Edwards Deming"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain the operational definition in plain language, as if you've never heard the phrase "operational definition"
- Ask it to compare Deming's fourteen points to the five-component specification template in this chapter — which points map cleanly, which don't
- Add a constraint: "Answer as if you're writing a memo to a manager who thinks quality problems are always the fault of the people doing the work"

What changes? What gets better? What gets worse?

---

## References

1. W. Edwards Deming, *Out of the Crisis* (MIT Press, 1986). Operational definitions; system-vs-worker causes of quality failure. See also Wikipedia, "W. Edwards Deming," https://en.wikipedia.org/wiki/W._Edwards_Deming
