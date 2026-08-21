# Chapter 20 — Ask AI Everywhere

*The tool that answers without a loop does not teach. It performs teaching. The student cannot tell the difference until the exam.*

---

Your student is sitting with your book open. The chapter on decision trees is on the screen — or the Kindle, or the Canvas module, or the React site you handed to a developer three weeks ago. She has a question. Not a quiz question. A real one: the worked example used exactly four features and she wants to know whether the number four was a pedagogy choice or whether decision trees actually degrade past some feature count, and if so, what happens at the margin.

That is a good question. It is precisely the kind of question a textbook cannot fully answer in the flow of the chapter — too specific, too dependent on what she already knows, too much of a thread to pull without derailing the surrounding argument. It is the question a good office-hours conversation handles in ninety seconds.

Where she asks it depends entirely on where she is reading. On Canvas, she gets IgniteAI. On Medhavy, she gets a native tutor with a memory of where she has been in the course. On Kindle or a static PDF, there is no embedded AI at all — but this book ships her a companion prompt she pastes into Claude or ChatGPT alongside the chapter text, and the loop begins. On a React site, there is a chat component wired to an API, with a system prompt you wrote and guardrails you specified.

Same question. Four different loops. Four different memories, four different trust models, four different guarantees about what the AI knows about this reader in this course.

The author's job across all four surfaces is the same thing Chapter 1 asked of you as a professional: keep the AI as a provocation, not a vending machine. The fluency trap does not stop at the author's desk. It migrates. It travels from the author who outsources their judgment to the student who outsources hers. The answer that arrives polished and complete and with no loose threads stops her thinking at exactly the point where her thinking should have just started.

This chapter is where the book closes the loop. Everything before here was about building the artifact. This is about what happens when the artifact meets a student.

---

## The Surface Map

Before the argument, the map. The same Ask-AI question travels four different routes depending on where the book lives.

**Canvas → IgniteAI.** Canvas is the LMS most university instructors already live in. When you exported the `.imscc` in Chapter 17, the package carried your chapter pages, your quiz questions, your outcomes statements, and — if you did the work there — context that IgniteAI uses when a student asks a question inside your course. IgniteAI is already embedded in the Canvas environment at institutions that have licensed it; your lever as the author-instructor is the course structure you gave it to stand on. Outcomes statements, aligned objectives, and context notes seeded into Canvas pages are not decoration. They are the material IgniteAI draws on when it answers. A thin `.imscc` gives IgniteAI thin context to work with. The answer quality reflects the quality of your course design, not just the quality of the underlying model.

**Medhavy → native tutor with course memory.** Medhavy, described in Chapter 19, is an AI-native tutor layer connected to your course via LTI. The distinction that matters here: Medhavy's Ask AI function accumulates context across student sessions. It knows — in the aggregate and in the individual — which concepts are generating questions, which phrasing confuses, which exercise results in the most re-reads. That memory makes it the richest loop in this stack. A student asking about decision tree feature counts on Medhavy is asking inside a system that can see she already asked two questions about overfitting last Tuesday. The response can reflect that. The author's job is the same as with IgniteAI: the course structure you gave Medhavy is the scaffolding it leans on. Better scaffold, richer loop.

**React site → embedded model.** In Chapter 18, `build-react-site.py` generated an `AskAI.tsx` placeholder — a chat component wired to an API endpoint, with a system prompt you specified and guardrails you declared. The developer who picks up your handoff activates it; you wrote what the component says about itself, what it refuses, and how it frames its uncertainty. On the React site, Ask AI has no course memory unless you build session state into the API layer. It knows what you told it in the system prompt, and it knows what the student types. That is the scope. The author's job here is not the implementation. It is the system prompt: the document that tells the embedded model who it is, what this course is for, what the student is expected to bring to the conversation, and — critically — what the model should refuse to do for the student even when the student asks.

**Kindle / PDF → parallel LLM.** This is the path that has no native AI. The EPUB or PDF contains no embedded model, no API call, no LTI handshake. What it can contain is a companion prompt — a short, carefully written passage the reader pastes into Claude or ChatGPT or Gemini alongside the relevant chapter text, which instantiates a tutor-like loop in whatever LLM they have access to. The companion prompt is the "+1" a static format cannot host natively. It is the author's intervention into a format that would otherwise offer the reader nothing but the text itself. The full, ready-to-paste companion prompt is in Appendix 97.

| Surface | AI mechanism | Memory | Author's lever |
|---|---|---|---|
| Canvas | IgniteAI (embedded) | Course-session | Outcomes, alignment, context notes in `.imscc` |
| Medhavy | Native tutor (LTI) | Persistent, per-student | Course structure + Medhavy configuration |
| React site | Embedded model (AskAI.tsx) | Session-only unless you build more | System prompt + guardrails |
| Kindle / PDF | Parallel LLM (companion prompt) | None — user brings their own LLM | Companion prompt in the appendix |

---

## The Fluency Trap, Student Edition

Chapter 1 described the trap with a designer and a creative brief. Here is the same trap with a student and a decision tree.

The student is on Kindle. She has the chapter open. She also has Claude in another window. She pastes a short question: *In the chapter I'm reading, decision trees use four features. Why four? Does the number matter?*

A well-calibrated model, given no further context, will produce a response that is technically correct, appropriately hedged, and approximately 300 words. It will explain that feature count in a decision tree relates to the number of attributes in the training data, that feature selection methods like information gain or Gini impurity determine which features get split on, that tree depth and feature count interact, and that in a textbook example the number four likely reflects a pedagogical simplification rather than a principled choice. The response is fluent. It is not informed by this course, this chapter, or this student's specific level of confusion.

The student reads it. She nods. She turns the page.

Nothing happened. She received a plausible answer to a question that was actually a signal — a signal that she does not yet understand the relationship between training data, feature selection, and generalization. The answer she got did not engage that misunderstanding. It addressed the surface syntax of her question while leaving the underlying confusion intact. The AI performed teaching without teaching.

This is what happens when the loop is not a loop. The model answered. The student accepted the answer. No one checked whether the answer engaged what the student actually needed. The interaction closed with the student feeling slightly more informed, which is exactly how the fluency trap closes: with a feeling of resolution where no resolution occurred.

The loop the author is trying to build is different. It is not: student asks → AI answers → student closes tab. It is: student asks → AI interrogates — *what makes you think it's the number four specifically, rather than the choice of split criterion?* → student thinks → student answers → AI advances the conversation → student builds something she did not have when she opened the window.

The interrogation is the design choice. An AI tutor that interrogates rather than spoon-feeds is not a harder-to-use AI tutor. It is a pedagogically different one. The question is whether the author designed the loop — in the system prompt for the React site, in the context notes in the Canvas `.imscc`, in the companion prompt for Kindle readers — or whether the author left the loop design to the model's defaults.

The model's defaults answer. Yours provoke.

---

## What the Author Controls (and What They Don't)

The surfaces differ in how much the author can shape the loop. This is where the trade-offs need naming, because the urge to treat all four surfaces as equivalent is wrong and will produce equivalent disappointment on three of them.

**IgniteAI, Canvas.** The author controls the course structure that IgniteAI reads: the outcomes, the alignment, the sequencing logic, the context notes embedded in Canvas pages. What the author does not control: the underlying model IgniteAI runs on, its retrieval strategy, or whether two students asking the same question in the same course receive meaningfully different responses. IgniteAI answers better when the author gave it better material. There is no guarantee of identical behavior across courses, cohorts, or question phrasings that look similar but are not.

**Medhavy.** The author controls the Medhavy course configuration, the system-prompt context Medhavy is given about the course, and the per-chapter notes that shape its tutor persona. What the author does not control: Medhavy's per-student model inference, its forgetting and recall curves, or how it weighs session history when formulating a response. The richest loop comes with the least authorial transparency about what is happening inside it.

**React site (AskAI.tsx).** The author controls the system prompt and the guardrails entirely — this is the one surface where the author's words go directly into the model's instruction context, unmediated by a third-party LMS product. What the author does not control: the developer's implementation of the API call, the latency and rate-limiting behavior of the underlying API, or what happens when the model ignores the system prompt because the student's question pattern jailbreaks around it. Write the system prompt as if a student will try to get the model to do their homework for them, because some will.

**Parallel LLM, Kindle / PDF.** The author controls the companion prompt and nothing else. What the author does not control: which LLM the student uses, whether the student pastes the chapter text faithfully or summarizes it, whether the student uses the companion prompt at all, or what version of Claude / ChatGPT / Gemini is available in six months when a new reader opens the book. The companion prompt depends entirely on the student's willingness to engage. It is the most honest of the four loops: it makes the student's participation explicit and visible in a way the other surfaces conceal.

The named trade-offs map directly onto what Chapter 1 called the irreducibly human layer — the decisions that must remain yours. The model, on every surface, will trend toward fluency without provocation. It will answer. The author who designs against that tendency — who writes system prompts that interrogate rather than resolve, who seeds Canvas with questions not just content, who builds a companion prompt that refuses to just explain — keeps the loop human.

---

## Designing the Loop, Surface by Surface

### Canvas: Seeding IgniteAI with the Questions You Want It to Ask

The Canvas page is not just reading material. It is context for IgniteAI. Every learning objective, every annotated example, every "Before you continue, consider:" prompt you embed in a Canvas page is potential material for a better AI response.

The move that matters most: state the expected confusion. If decision trees generating with four features is a known sticking point — students always want to know if the number is magic — put that in the page notes explicitly. Not as content the student reads, but as context the instructor leaves for IgniteAI. *Students often fixate on the feature count here; the important confusion is between "how many features did we use" and "how does the model select which features matter." Point toward the split criterion, not toward the number.* That instruction does not guarantee IgniteAI asks about split criteria. It increases the probability that when a student asks about feature count, the response is not purely about feature count.

This is author-level instructional design, not AI configuration. The AI configuration is whatever IgniteAI's system allows. The instructional design is yours.

### Medhavy: Building the Richest Loop

Medhavy accumulates session context. The student who asks about feature counts on Tuesday, and who struggled with overfitting questions last Tuesday, is presenting a coherent pattern of misunderstanding about model complexity. Medhavy can surface that pattern. The author's job is to give Medhavy the interpretive frame — the learning architecture from Chapter 2 and Chapter 4 — that makes the pattern visible as a pattern rather than noise.

The practical move: structure your Medhavy course configuration with explicit prerequisite knowledge maps. *Concept X depends on concepts A and B; if a student asks about X and has not yet demonstrated A, redirect to A.* This is not AI magic. It is course design translated into a format Medhavy can use. The richer the map, the better the tutor. The student who has been fighting with overfitting for two sessions does not need to be told what a split criterion is. She needs to be asked what she thinks is happening at the leaves when the tree grows too deep.

### React Site: Writing the System Prompt That Doesn't Spoon-Feed

The system prompt is where the author spends their design attention on the React surface. The temptation is to write a system prompt that makes the AI maximally helpful — explain clearly, give examples, be patient. That system prompt produces a good tutor for students who are already thinking. It produces a vending machine for students who are not.

A different approach: design the system prompt to refuse to answer until the student has answered. Here is a pattern:

> You are the course tutor for [Course Name]. A student has come to you with a question. Before answering, ask them what they already think the answer might be — even a rough guess. When they provide a guess, respond to the guess, not to the original question. If the guess is close, tell them what they got right and what to sharpen. If the guess is wrong, ask them what would change their mind. Only provide a full explanation after the student has made at least one genuine attempt.

That instruction does not guarantee Socratic dialogue. Language models can be talked out of instructions by persistent students. But it sets the default in a direction that produces learning rather than completion. The system prompt is the closest thing to the author's voice inside the AI loop. Write it deliberately.

The guardrails are the second design choice. State what the model should decline: *Do not write code for the student's assignments. Do not solve exercises that appear to be graded work. Do not provide answers to questions that are verbatim matches to end-of-chapter exercises.* The guardrails will not catch everything. Students find workarounds. State them anyway, because the stated boundary shapes the majority of the interaction even when it does not shape every interaction.

### Kindle / PDF: The Companion Prompt

The companion prompt is the author's intervention into a format that otherwise offers no loop at all. A reader who opens the Kindle book on a Saturday morning and has a question has two options without the companion prompt: re-read the chapter and hope the answer is there, or open an LLM and ask from scratch with no course context. The companion prompt gives them a third option: a ready-to-paste instruction that instantiates a course-aware tutor in whatever LLM they have access to.

The companion prompt is in Appendix 97. The design principles behind it are worth stating here, because the author who wants to write their own version needs to understand what the prompt is trying to do.

It does not summarize the chapter. The student already has the chapter. It provides the course context the chapter text does not carry: what this course is for, what level of expertise the student brings to the conversation, what the student has already covered before this chapter, and — the key design choice — an instruction to the LLM to interrogate rather than explain. A companion prompt that just says *you are a helpful tutor, help this student understand the chapter* produces IgniteAI without IgniteAI's course context. A companion prompt that says *ask the student what they think before you explain anything, push them to articulate their confusion before you address it* creates a loop in a format that cannot host one natively.

The companion prompt also carries an honest limitation disclosure. The student pastes it into an LLM they chose, with a version of the model the author cannot predict, in an interaction the author cannot see. The companion prompt should acknowledge this: *I am a tutor prompt, not a live course tool. The LLM you are using may produce inaccurate or outdated information. Verify specific claims against the chapter text.* That sentence is not cover-your-ass boilerplate. It is the author being honest about what this format can and cannot guarantee.

---

## The Argument This Book Was Building Toward

Every chapter in this book was, in some sense, about keeping the AI in its correct position. In Chapter 1, the designer who sends the unreviewed brief to the client has let the AI cross the line from tool to decision-maker. The brief is fluent, uninformed, and on its way to destroying an eight-year relationship. The AI did not do anything wrong. The designer did.

The same structure runs through the student side of the desk. The student who pastes a question into Claude, reads the answer, turns the page, and files it away as understood — she did not do anything wrong either, exactly. She used the tool. The tool produced a fluent response. The cognitive reward for processing fluency arrived, and her brain marked the question as resolved. She is eighteen months from the exam, or from the interview, or from the client call where the question comes back in a form the textbook didn't cover, and she will discover that the resolution was an illusion.

This is not an argument against using LLMs to study. It is not an argument that students should be forced to struggle alone with material they could clarify in thirty seconds. It is an argument about *what the loop is for*. The loop is for learning, which means the loop must produce changes in the student's mental model. A loop that produces changes in the student's mental model requires the student to externalize their current mental model — to state what they think, to guess, to be wrong about something in a way that the AI can engage with. A loop that skips that step produces the feeling of learning without the learning.

The author who designed the surface — the system prompt, the Canvas context notes, the companion prompt, the Medhavy configuration — either built the externalization requirement into the design, or they didn't. If they didn't, the loop defaults to answer-vending. Not because the AI is bad. Because the AI, at every surface, will trend toward fluency if no one tells it not to.

Chapter 1 named the fluency trap for the author. Chapter 20 names it for the student. The author's job does not end when the book ships. It extends through every surface the book reaches. The question *how will a student use AI with this material?* is a design question. Design it, or the model will design it for you. The model's default design is fluent, helpful, and decision-free.

Close the loop. Keep the human in it.

---

## AI Wayback Machine — Socrates

The Socratic method is named after a man who wrote nothing and taught through questions that refused to resolve. Plato's *Meno* is the cleanest demonstration: Socrates works with an uneducated slave boy on a geometry problem — the doubling of a square — and over thirty exchanges the boy arrives at the answer himself, without Socrates ever stating it. Every time the boy is close, Socrates asks a question. Every time the boy is wrong, Socrates asks a different question. The answer arrives in the boy's mind, from the boy's own reasoning, shaped by an interlocutor who refused to shortcut the process.

> **Prompt to run in Claude or ChatGPT:**
>
> "Read the *Meno* excerpt on the geometry lesson with the slave boy (Plato, *Meno*, roughly 82b–85b). Describe the specific conversational technique Socrates uses — not the 'Socratic method' in the abstract, but the actual question types, the specific moments where he refuses to give the answer, and the times he gives false leads. Then tell me: if you were implementing a system prompt for an AI tutor designed to replicate this technique, what five specific instructions would you give the model?"

Socrates had no system prompt. He had a conviction that knowledge is recollection and that the role of the teacher is not to fill an empty vessel but to turn a lamp that is already lit. The AI+1 frame does not require you to share that metaphysics. It requires you to take the operational consequence seriously: the design choice that matters most is the one that makes the student do the thinking.

---

## LLM Exercises

### Exercise 20.1 (Apply) — Draft a system prompt for the AskAI component

Your React site's `AskAI.tsx` component needs a system prompt. Using the pattern from this chapter as a guide — interrogate before explaining, refuse to do the work for the student, acknowledge uncertainty — draft a system prompt for your own course's embedded AI.

**Paste this into Claude, ChatGPT, or Gemini:**

> I am building a React-based course site for a textbook on [your topic]. The site includes an embedded chat component called AskAI. I want to design a system prompt for this component that makes it an interrogating tutor rather than an answer-vending machine. Specifically: the AI should ask the student what they already think before explaining anything; it should respond to the student's guess rather than to their original question; and it should not directly solve exercises or assignments.
>
> Help me draft a system prompt that achieves this. After you draft it, identify the two most likely ways a student would work around the restrictions you've built in, and suggest modifications to make the prompt more robust against those workarounds. Finally, note any tension between being helpful and being pedagogically sound — and tell me where you'd draw the line.

**Deliverable:** A system prompt for your AskAI component, with two anti-workaround modifications and a one-paragraph note on the helpfulness-versus-pedagogy tension.

---

### Exercise 20.2 (Analyze) — Test the companion prompt against a chapter

Take the Parallel-LLM Companion Prompt from Appendix 97. Open a chapter from your own textbook. Paste the companion prompt plus the chapter text into Claude or ChatGPT. Then ask a question that you would genuinely expect a confused student to ask about that chapter.

Evaluate the AI's response on three dimensions:
1. Did it interrogate before explaining, or did it explain immediately?
2. Did it surface the specific confusion the question carried, or did it address the surface syntax?
3. Would a student with a genuine misunderstanding come away from this exchange with their misunderstanding corrected, or merely addressed?

**Paste this evaluation prompt:**

> I just had the following exchange with an AI tutor [paste the exchange]. I want you to evaluate the AI's response as a pedagogy critic. Did it interrogate before explaining? Did it surface a genuine misunderstanding or just address the surface question? Did it produce a change in understanding, or the feeling of a change? Be harsh.

**Deliverable:** The exchange, the evaluation, and one specific change to the companion prompt you would make based on what you observed.

---

### Exercise 20.3 (Evaluate) — Compare the four surfaces

You now have the map of all four surfaces. For your own book and course context, evaluate them on three axes: (a) richness of the loop — how much does the AI know about this student and this course? (b) author's control — how much can you shape the AI's behavior? (c) probability of hitting the fluency trap — given the average student using this surface, how likely is the AI to answer without interrogating?

**Paste this into Claude:**

> I am an author-instructor with an AI-enriched textbook that deploys across four surfaces: Canvas with IgniteAI, Medhavy (an AI-native LMS tutor), a React site with an embedded model, and Kindle with a parallel-LLM companion prompt. I want to evaluate these surfaces for the risk that students will use the AI as an answer-vending machine rather than a thinking tool.
>
> For each surface, tell me: (1) what architectural features of that surface make it prone to fluency-trap AI use, and (2) what design intervention — in the course structure, system prompt, or companion prompt — would most reduce that risk. Then rank the four surfaces by answer-vending risk from highest to lowest, and explain your ranking.

**Deliverable:** The AI's evaluation plus your own one-paragraph assessment of whether you agree, with one specific disagreement noted if any.

---

## Bridge — The Book

There is no Chapter 21. The book ends here.

What you have, at the close of Chapter 20, is a pipeline that runs from a blank TIKTOC.md to a Kindle-ready EPUB, a Canvas course export, a React site scaffold, and a Medhavy-ready LTI configuration — and now, a set of decisions about how AI meets students on every one of those surfaces.

The fluency trap is still there. It was there in Chapter 1, on the author's side of the desk. It is here in Chapter 20, on the student's side. It is the same trap. The professional who outsources their judgment to a polished AI output, and the student who outsources their understanding to a polished AI explanation, are caught in the same mechanism: statistical coherence without communicative intent; processing fluency rewarded as correctness; the "is it informed?" check skipped.

The author's job was never to use AI. It was to keep AI in its correct position. The tool that provokes, that interrogates, that reflects the student's thinking back at them in sharpened form, that refuses to resolve what the student needs to resolve — that tool serves the same function the author's own judgment serves in Part 1. It keeps the human in the loop.

The TIKTOC.md is still on disk. The chapters directory still exists. The build script still runs. The pipeline is ready for the next book.

So is the question you should be asking every time you design an AI surface: *am I building a loop, or a vending machine?*

The answer you give that question is the answer to Chapter 1.

---

## Prompts

### Figure 20.1 — The four-surface Ask AI loop

Build a four-quadrant comparison diagram as one standalone HTML file with inline CSS and D3 7.9.0 from the CDN. Data shape: four objects, each with four fields — surface name, AI mechanism, memory model (none / session / persistent), and author's lever. Marks: four equal rectangular cells in a 2×2 grid, each labeled with its surface name, mechanism, and memory level. Channels: grid position encodes surface (Canvas top-left, Medhavy top-right, React site bottom-left, Kindle/PDF bottom-right); a vertical fill gradient inside each cell encodes memory richness (none = light, session = medium, persistent = deep). Annotation: each cell carries a one-line author's-lever note in smaller type. No quantitative axis. Deliverable: one self-contained HTML file, inline CSS, D3 7.9.0 CDN, responsive via ResizeObserver, accessible SVG with title/desc.

### Figure 20.2 — The fluency trap, student edition

Build a two-column contrast diagram as one standalone HTML file with inline CSS and D3 7.9.0 from the CDN. Data shape: two flow paths, each with four labeled nodes. Left path (answer-vending): student asks → AI answers → student nods → page turns. Right path (interrogating loop): student asks → AI interrogates → student externalizes → understanding updates. Marks: two vertical chains of rounded-rectangle nodes, one on each side, joined at the top by a shared source node (the student's question). Channels: left column = answer-vending path (neutral fill); right column = interrogating-loop path (primary series color); a red X terminator on the left path's leaf node marks the closed-without-learning outcome. No quantitative axis. Annotation: label each node; label the X as "fluency trap." Deliverable: one self-contained HTML file, inline CSS, D3 7.9.0 CDN, responsive via ResizeObserver, accessible SVG with title/desc.

---

## References

1. Bender, E. M., Gebru, T., McMillan-Major, A., & Mitchell, M. (2021). "On the Dangers of Stochastic Parrots: Can Language Models Be Too Big?" *Proceedings of FAccT '21*, 610–623. https://dl.acm.org/doi/10.1145/3442188.3445922
2. Alter, A. L., & Oppenheimer, D. M. (2009). "Uniting the Tribes of Fluency to Form a Metacognitive Nation." *Personality and Social Psychology Review*, 13(3), 219–235.
3. Reber, R., Schwarz, N., & Winkielman, P. (2004). "Processing Fluency and Aesthetic Pleasure." *Personality and Social Psychology Review*, 8(4), 364–382.
4. Plato. *Meno* (trans. G. M. A. Grube, rev. C. D. C. Reeve). In *Plato: Complete Works*, ed. John Cooper. Hackett, 1997. Geometry lesson: 82b–85b.
5. Ambrose, S. A., Bridges, M. W., DiPietro, M., Lovett, M. C., & Norman, M. K. (2010). *How Learning Works: Seven Research-Based Principles for Smart Teaching*. Jossey-Bass. Chapter 2 on prior knowledge activation.
6. Chi, M. T. H., & Wylie, R. (2014). "The ICAP Framework: Linking Cognitive Engagement to Active Learning Outcomes." *Educational Psychologist*, 49(4), 219–243.
7. Koedinger, K. R., et al. (2023). "An Astonishing Regularity in Student Learning Rate." *Proceedings of the National Academy of Sciences*, 120(13). https://doi.org/10.1073/pnas.2221311120
