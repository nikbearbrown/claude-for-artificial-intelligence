# Chapter 13 — The Enriched Layer: Beyond the Book

*A book teaches. The enriched layer makes the student practice, retrieve, and defend their thinking — and neither you nor the student does that alone.*

---

You open the Kindle app on your phone and find it there: *AI for Designers*, $0.99, approved 27 hours after you submitted. You tap through the first few chapters on the Kindle. The prose you rewrote in Chapter 8 reads like you. The figures carry arguments. The LLM Exercises pass the three-question audit. The book is real.

And then the book sits there.

The reader who downloads it tomorrow will read it — or skim it, or quote-mine it, or read the first two chapters and come back to it next month. The book is a one-way surface. It says things. It does not know whether the reader understood them. It cannot ask whether they tried the exercise in Chapter 4 and what happened. It cannot probe whether the concept in Chapter 7 has been remembered three weeks from now, or lost. It cannot follow up.

A book teaches. That is a genuine and underappreciated thing. But what comes after reading? The research literature on learning and memory is unambiguous on one point: a single pass through material — however well-written, however well-argued — is not enough for durable understanding. Roediger and Butler's 2011 review of retrieval-practice effects in *Annual Review of Psychology* puts it plainly: the act of recalling information produces stronger retention than an equivalent period of re-reading it.[^roediger] You cannot make the reader recall something by writing it well. You can only create the conditions in which recall becomes possible. That is what the enriched layer does.

This chapter is a map. It names the artifacts that live beside the book — the quiz bank, the case studies, the glimmers, the spaced-repetition cards, the Ask AI loop — and explains why each one exists and what problem it solves. It does not deep-dive any single artifact. Chapters 14 through 20 do that. What this chapter does is argue for the architecture: one source, many surfaces, a human+AI loop on each one.

[^roediger]: Roediger, H. L., & Butler, A. C. (2011). "The Critical Role of Retrieval Practice in Long-Term Retention." *Annual Review of Psychology*, 62, 265–281.

---

The source of truth for *ai-for-designers* is `chapters/*.md`. You know this from Part 1. The EPUB that ships to Kindle is a build output — pandoc reads the chapter files and produces a file. You do not edit `combined.md`. You edit the chapter files.

The enriched layer is the same principle extended. Every quiz question, every case study, every spaced-repetition card, every glimmer prompt is generated from the chapter files. You do not hand-write a Canvas quiz. You do not manually type Anki cards. You run a script or a prompt that reads your chapters and produces the artifact. The output is formatted for whatever surface it will live on — a Canvas `.imscc` upload, an Anki `.apkg` file, a React component, a Medhavy configuration. The chapter files are still the source of truth. The enriched artifacts are still build outputs.

The architecture has one decisive implication for authoring: when you revise a chapter, the enriched artifacts update. You do not maintain parallel versions. You run the relevant generator against the revised chapter, and the new case study or quiz bank reflects the new chapter. This is the only model that scales. An author who hand-maintains a quiz bank alongside a revised manuscript will eventually drift — the quiz will test what the first draft said, not what the revised chapter says. The generator keeps them synchronized.

This is also the only model that does not require the author to be a learning designer. You are a domain expert with something to teach. The case study generator knows what a teaching case looks like. The spaced-repetition generator understands the Ebbinghaus curve. The glimmer generator knows how to build a prompt that will make a student defend a claim. You bring the domain content. The generator brings the pedagogical format. The collaboration is the point.

---

So what are these artifacts, and why does each one exist?

**Quizzes** are the familiar one. You have been assessed by multiple-choice questions since grade school, and that familiarity is the first thing to understand about them: they require no defense because no one has forgotten what they are. A quiz checks whether the reader can recognize a correct answer under controlled conditions. In the context of a Canvas course or a Medhavy session or a web-based practice module, a quiz provides the first checkpoint — can the reader reconstruct the basic claim? The educational literature on this is settled enough that Chapter 16 on spaced repetition devotes serious attention to the mechanism. Quizzes are not the whole story of assessment, but they are a proven part of it, and because the concept needs no justification, this chapter spends little time on it. The quiz bank for *ai-for-designers* is generated from the chapter files. It covers both recognition (here is the concept, identify the correct description) and application (here is a scenario, select the appropriate response). Chapter 17 on the Canvas export and Chapter 20 on Ask AI Everywhere describe how the quiz bank travels across surfaces.

**Case studies** need more explanation. A quiz tests whether you know what something is called. A case study tests whether you can use the knowledge in a situation where the knowledge is not pre-labeled. This matters because most professional situations arrive without labels. A freelance designer getting a brief does not know in advance that this is an "information hierarchy problem" — she has to recognize it. Transfer learning research, starting from Bransford and Brown's *How People Learn* synthesis, consistently finds that recognition-level assessment does not reliably predict transfer performance.[^bransford] The teaching case is the artifact that creates the conditions for transfer: here is a concrete situation, what would you do? Chapter 14 covers the mechanics of how cases are generated, what distinguishes a teaching case from a worked example, and why the distinction matters for the student who reads it. For now: the case study exists because the quiz does not reach the kind of judgment the domain actually requires.

**Glimmers** are the novel one, and they deserve a real introduction here because unlike quizzes and cases they have no obvious precedent in conventional pedagogy. A glimmer is not a quiz and it is not a case study. It is a prompt that makes the *student* defend their thinking to an AI. Not "ask the AI to explain this concept" — the opposite: the student articulates their understanding, and the AI interrogates it. The mechanism is Socratic in structure but AI-native in execution. The name comes from the idea that understanding, when you first have it, is a glimmer — provisional, possibly fragile, not yet tested. The glimmer prompt makes the student turn toward the glimmer and examine it out loud. What you think you understand often reveals its own gaps when you try to explain it to something that will ask follow-up questions without mercy or social grace. Chapter 15 develops this in full. For now: the glimmer exists because the hardest thing to assess from outside a student's head is whether they actually understand something or merely recognize it, and the glimmer creates an externalization that makes the difference visible.

**Spaced-repetition cards** address a different failure mode: forgetting. A student who understands a concept the day they read the chapter may not have that concept available three weeks later when a client situation calls for it. This is not a failure of intelligence or attention; it is how human memory works. Ebbinghaus's forgetting curve, documented in *Über das Gedächtnis* in 1885, shows that memory for new information decays rapidly in the first days after initial encoding and then more slowly.[^ebbinghaus] The antidote is spaced retrieval: encountering the material again at the moment forgetting is about to occur. Anki, the open-source spaced-repetition application, implements a scheduling algorithm based on this research — it shows you a card at the right interval to maintain retention with minimal review time. The spaced-repetition generator for *ai-for-designers* produces an `.apkg` file: a deck the student downloads into Anki and reviews on their own schedule. Chapter 16 develops the mechanism and the build pipeline. For now: the spaced-repetition cards exist because retention is time-dependent and the book cannot control when the reader reads it.

**The Ask AI loop** is the capstone artifact and the hardest to explain briefly. Every surface in the enriched layer — the Canvas course, the React site, the Medhavy session, even the Kindle book through a companion prompt — can carry a version of Ask AI: an entry point where the student poses a question and gets a response tuned to the book's domain and level. The book you wrote taught at a fixed level. The Ask AI loop responds to where this particular student is. One student needs a simpler explanation of a concept the chapter assumed; another student needs a harder question pushed back at them. Neither service is possible from a fixed text. The loop is not a vending machine — the goal is not to give students answers, but to maintain a human+AI dialogue around the content that keeps the student thinking. Chapter 20 develops this in full, including the parallel-LLM companion prompt that makes Ask AI available alongside any surface including the Kindle book itself. For now: the loop exists because the book cannot respond to the reader, and the enriched layer can.

[^bransford]: Bransford, J. D., Brown, A. L., & Cocking, R. R. (Eds.). (2000). *How People Learn: Brain, Mind, Experience, and School* (expanded ed.). National Academy Press.
[^ebbinghaus]: Ebbinghaus, H. (1885). *Über das Gedächtnis: Untersuchungen zur experimentellen Psychologie*. Duncker & Humblot. English translation: *Memory: A Contribution to Experimental Psychology* (1913). Teachers College, Columbia University.

---

The surfaces are where these artifacts live and travel. The artifact is a thing; the surface is where a student encounters it.

The Canvas course is the LMS surface. A Learning Management System is what universities, continuing education programs, and corporate training departments use to deliver course material to enrolled students. Canvas is the most widely deployed LMS in US higher education as of 2026. [verify — LMS market share current as of writing] The `.imscc` format — IMS Common Cartridge — is an open standard that packages a course as a single uploadable archive: pages, quizzes, assignments, a syllabus. The build script produces a `.imscc` from the chapter files and the generated quiz bank. An instructor uploads it to Canvas, and a course exists. Chapter 17 covers the build script, what goes into the cartridge, and how IgniteAI further refines the Canvas experience after upload.

The React site is the public-web surface. A React site built from `.mdx` and `.tsx` components can render the book's chapters, embed the quiz bank, surface case studies as interactive scenarios, and carry the Ask AI loop — all from the same chapter files. The build script produces the component scaffold; a developer takes it from there. Chapter 18 describes what the script produces and where the developer picks up. The React site is where the enriched layer reaches readers who do not have a Canvas enrollment — workshop participants, independent learners, people who found the book on the web.

Medhavy is the AI-tutor layer. It sits on top of the Canvas course via LTI (Learning Tools Interoperability), the standard that lets external tools embed inside an LMS. Where Canvas provides structure and the quiz bank provides assessment, Medhavy provides adaptive dialogue — a student working through a case study can ask for a hint, and Medhavy responds at the level the student is at. Chapter 19 describes what Medhavy adds and what the developer and administrator hand-off requires. It is the surface with the most setup friction and the deepest student engagement potential.

The Kindle book itself — the $0.99 artifact from Chapter 12 — is the starting surface, not the final one. A reader who downloads the Kindle book is not yet in the enriched layer. But the companion prompt in Chapter 20 makes Ask AI available alongside any Kindle or PDF session. The Kindle book is the entry point. The enriched layer is what the student finds when they go further.

---

Here is the claim this architecture rests on, stated plainly so it can be tested.

A book is a one-way surface. It carries the author's argument with high fidelity — better, for most topics, than a lecture, because the reader can slow down, re-read, follow the reasoning at their own pace. But the book cannot respond to what the reader does with the argument. It cannot tell whether the concept landed or didn't. It cannot call out the reader who skimmed the case. It cannot surface the question the reader was too embarrassed to ask in the workshop. A book is a monologue, and a very good monologue is still a monologue.

The enriched layer adds the response direction. Quizzes let the reader check themselves. Cases demand that the reader construct a response, not just recognize one. Glimmers make the reader articulate their understanding and defend it. Spaced-repetition cards intercept forgetting before it consolidates. Ask AI responds to where this particular reader is in this particular moment.

None of these require the author to do more writing. That is the architecture's central economy. You wrote the chapters. The generators read the chapters and produce the artifacts. You review and approve the generated output; you do not author it from scratch. The human judgment in the loop is editorial — does this case study actually represent a situation the target reader would face? Is this glimmer prompt asking the right question? — not compositional.

The trade-off to name explicitly: the generated artifacts are not as good as artifacts a master learning designer would build by hand with domain expertise and a year's time. The case study a skilled instructional designer crafts after ten interviews with practitioners is better than the case study the generator produces from a chapter file. But that master-crafted case does not exist for most books, because most books do not have a year's instructional design budget behind them. The generated artifact is in the book; the master-crafted artifact is not. The enriched layer is a bet on the second-best option that actually ships.

---

The seven chapters that follow each take one artifact or surface and develop it in full. Chapter 14 covers case studies: what a teaching case is, why it beats a worked example for transfer, how the generator produces one, and what review the author owes it. Chapter 15 covers glimmers: the mechanism, the prompt structure, the student experience, and why a glimmer is not a quiz. Chapter 16 covers spaced-repetition cards: the forgetting curve, the Anki build pipeline, and what the student deck looks like for *ai-for-designers*. Chapter 17 covers the Canvas export: the `.imscc` build script, what goes into the cartridge, and how IgniteAI refines the course after upload. Chapter 18 covers the React site: what the `.mdx` and `.tsx` scaffold contains and where the developer takes it. Chapter 19 covers Medhavy: what the AI-tutor layer adds, what the LTI integration requires, and what the developer and administrator hand-off looks like. Chapter 20 is the capstone: Ask AI on every surface, the parallel-LLM companion prompt, and the argument that the enriched layer closes the loop Chapter 1 opened — the fluency trap, now on the student's side of the desk.

Each of those chapters stays at author-instructor altitude. The script or prompt that produces the artifact lives in the corresponding appendix. You run the tool; the chapter explains why the artifact exists and what makes a good one; the appendix tells you what to run.

The source of truth remains `chapters/*.md`. Every artifact is a build output. The author never hand-writes any of them.

---

## AI Wayback Machine — Benjamin Bloom

In 1956, Benjamin Bloom chaired the committee that produced *Taxonomy of Educational Objectives, Handbook I: Cognitive Domain* — what everyone since has called Bloom's Taxonomy. The taxonomy arranged cognitive operations in six levels: knowledge, comprehension, application, analysis, synthesis, evaluation. The argument was that most formal education tested only the first two levels — recognition and recall — while professional competence required all six.

The enriched layer maps to this argument fairly directly. A quiz lives at recognition and recall. A case study lives at application and analysis. A glimmer, if it's working, pushes toward evaluation — the student is not just applying a framework but defending whether the framework is the right one to apply here. The spaced-repetition card serves retention across all levels.

What Bloom could not have anticipated is the Ask AI loop — a surface where the level of the question adapts to where the student is. A student who answers a recall question correctly can immediately be handed an application question; a student who struggles with application can be offered a re-explanation calibrated to their confusion. The static taxonomy assumes the curriculum decides the level in advance. The adaptive loop lets the dialogue determine it.

> **Prompt to run in Claude or ChatGPT:**
>
> "Look up the revised version of Bloom's Taxonomy (Anderson & Krathwohl, 2001) and compare it to the original 1956 version. What specifically changed, and why? Then ask: which level of the revised taxonomy is hardest to assess with a multiple-choice question, and what format of assessment would better reach it? Apply this to one specific concept from a domain you know well."

The domain application is the exercise. The taxonomy is the scaffold. Notice that the prompt asks you to *apply* it — not to define it, not to recognize it in a list. That's deliberate.

---

## Exercises

**Exercise 13.1 (Apply).** For your book — or for *ai-for-designers* if you do not have one yet — list each chapter and assign the enriched artifact type that would most benefit readers of that chapter. Options: quiz, case study, glimmer, spaced-repetition card, Ask AI session. You may assign more than one type per chapter. Justify each assignment in one sentence: what specific gap does this artifact type address for this chapter's content?

**Deliverable:** A table with three columns — chapter title, artifact type(s), one-sentence justification.

**Exercise 13.2 (Analyze).** Take one chapter from your book (or from *ai-for-designers*) and write three quiz questions at the recognition level and one case study prompt at the application level. For the case study prompt, write one sentence explaining what professional judgment the case is designed to surface. Compare: what does the quiz assess that the case does not, and what does the case assess that the quiz cannot?

**Deliverable:** Three quiz questions, one case study prompt, one explanatory sentence, and a two-sentence comparison.

**Exercise 13.3 (Evaluate).** The enriched-layer architecture makes a bet: a generated artifact that ships is better than a master-crafted artifact that doesn't exist. State the conditions under which you think this bet fails — when would the generated artifact be so far below the quality threshold that it damages rather than helps the student experience? Name at least one specific failure scenario. Then name one review step the author can take that most reduces the risk of that failure.

**Deliverable:** One failure scenario, one review step, and a one-paragraph defense of why that review step is the highest-leverage intervention.

**Exercise 13.4 (Challenge).** Map the enriched layer surfaces from this chapter — Canvas course, React site, Medhavy AI tutor, Kindle book + companion prompt — against the students who would realistically reach each one for your book's target audience. Who reaches which surface? Are there students in your target audience who reach none of them? What would it take to reach one more segment? The answer may be "the cost is not worth it" — that is a legitimate answer if it is argued.

**Deliverable:** A one-paragraph profile per surface (who reaches it, from your target audience), plus a one-paragraph assessment of coverage gaps and whether they are worth closing.

---

## Bridge — Chapter 14

The enriched layer is now named. You know what it contains, why each artifact exists, and how the single-source architecture produces it. The artifacts are build outputs. The chapter files are still the source of truth.

The next chapter earns its keep by answering the hardest question in applied pedagogy: what is the difference between a teaching case and a worked example, and why does the difference matter for transfer? A worked example shows you how it's done. A teaching case puts you in a situation where you have to figure out what to do. Those are not the same skill. Chapter 14 makes the distinction precise, shows you what a generated case looks like for *ai-for-designers*, and tells you what the author owes the generated output before it ships to students.

---

## References

1. Roediger, H. L., & Butler, A. C. (2011). The Critical Role of Retrieval Practice in Long-Term Retention. *Annual Review of Psychology*, 62, 265–281. https://doi.org/10.1146/annurev-psych-120709-145157
2. Bransford, J. D., Brown, A. L., & Cocking, R. R. (Eds.). (2000). *How People Learn: Brain, Mind, Experience, and School* (expanded ed.). National Academy Press.
3. Ebbinghaus, H. (1885). *Über das Gedächtnis*. Duncker & Humblot. English edition (1913): *Memory: A Contribution to Experimental Psychology*. Teachers College, Columbia University. https://psychclassics.yorku.ca/Ebbinghaus/index.htm
4. Bloom, B. S. (Ed.). (1956). *Taxonomy of Educational Objectives, Handbook I: Cognitive Domain*. David McKay.
5. Anderson, L. W., & Krathwohl, D. R. (Eds.). (2001). *A Taxonomy for Learning, Teaching, and Assessing: A Revision of Bloom's Taxonomy of Educational Objectives*. Longman.
6. IMS Global Learning Consortium. *IMS Common Cartridge Profile* (v1.3). https://www.imsglobal.org/cc/ccv1p3/imscc_Overview-v1p3.html
