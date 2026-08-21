# Chapter 1 — The Loop and the Three Modes
*The machine predicts. You decide. Everything else is what you build between those two facts.*

---

I want to start with something that sounds simpler than it is.

When you give a prompt to a large language model, the model does not look up the answer. It does not reason through the problem the way you might, testing hypotheses and discarding wrong ones. It predicts — one word at a time, each word chosen because it is the most probable continuation of everything that came before it, given the patterns the model learned from reading an enormous amount of text.

That is the whole mechanism. Everything else follows from it.

The model can produce a fluent paragraph on a topic it was never explicitly taught because fluency is a pattern, and patterns generalize. The model can produce a citation that does not exist because the *shape* of a citation is a pattern — author, year, title, journal — and the model can fill in that shape with words that fit the pattern without ever having seen the specific source it is now generating. The model sounds confident because confident text is a pattern, and the model has seen a lot of confident text.

Confidence is a textual feature. It has no necessary relationship to correctness.

| What it looks like | What is actually happening |
|---|---|
| Fluent paragraph | Pattern continuation — the model produces coherent prose because fluency is a learned pattern, not evidence of understanding |
| Confident citation | Citation-shaped placeholder — author, year, title, journal filled in to match the pattern of a citation, not a real source |
| Round number | Statistically plausible filler — a number that fits the expected shape of a statistic in context, generated without any underlying data |

I want you to sit with that for a moment. Every failure mode we are going to spend this book on — the invented source, the plausible-sounding number that turns out to be wrong, the paragraph that is subtly off in a way you have to look up to catch — is a direct consequence of this one fact about how the system produces output at all. Not bugs. Direct consequences. The fluent practitioner does not encounter these failures occasionally; she works inside them constantly, and she knows what the failure shapes look like before they arrive.

That is the one technical fact I need you to carry. Now let me show you what running the Loop looks like in practice — well-executed, but not yet the eighteen-months-of-reflexes version that comes in Chapter 8.

---

It is 10:17 AM on a Thursday and Priya Banksy is opening her laptop in her publication's offices. Nine months have passed since the Tuesday in Chapter 0. The Pew correction is in the publication's archive; the practice has been changing in her hands since.

The Climate desk's morning meeting just ended. A federal grid-storage rule landed yesterday afternoon — three hundred pages of regulatory text, an industry press release calling it transformative, a smaller energy-justice group calling it inadequate, and a deadline of 1 PM for a thousand-word explainer on the publication's audience-facing site. The story is hers.

She does not open Claude. She opens a blank document.

For seven minutes she writes — not the piece, but about the piece. Who is going to read this? The publication's general audience on their morning commute, the policy people who already know what the rule says, the reporters at trade outlets who will write the in-depth versions tomorrow. What question does she actually need to answer in a thousand words? Not *what is the rule* — anyone can look that up. The question is *who is right about what it does* — the industry framing or the energy-justice framing, and on what evidence. What does she already know about FERC rulemaking in this segment, and what does she not? What sources will the editor trust on first read, and what will get kicked back as PR-laundering? At the bottom of the page, in two sentences, she writes the shape of the output: 950–1,050 words, structured as *what the rule does*, *what each side is claiming*, *what the rule actually changes for whom*, with three primary-source links and one named expert quote.

Then she opens Claude.

Her first prompt is 280 words long. It includes the audience, the task, the structure, the things to avoid, and an explicit instruction: *do not invent sources or named studies; if you do not know, say so.* The response comes back in seconds. It is competent. It contains three things she immediately wants to argue with — including a confident-sounding paragraph about "industry analysts" that does not name any. She does not edit and ship. She types a second prompt: *steelman the industry's claim that the rule will slow deployment, sourcing only from the actual rule text and the two trade-association comment letters in the docket.* The model produces a bear case sharper than her first instincts had given her — and points at one specific paragraph in the rule that she had skimmed past.

Over the next hour she cycles between the document and the chat window. Sometimes she hands the model a small, bounded task — *summarize what Section 219(b) of the rule actually changes about interconnection queue treatment* — and edits the response heavily. Sometimes she hands it a question — *what would a project developer doing 200-megawatt-scale storage care about in this rule that a 5-megawatt-scale developer would not* — uses the answer to refresh her own thinking, and writes the paragraph herself. Twice she catches a suspiciously round statistic in the model's output. The first one — *"approximately 40% of currently queued storage projects would be affected"* — has no source the model can name. She opens the FERC docket, finds the actual figure (37.2%, in a comment letter), and corrects it. The second — *"deployment delays of 18–24 months are typical at this stage of rulemaking"* — turns out to be a fabricated statistic shaped to look like industry analysis. She removes it entirely.

At 11:48 she has a draft she would not be embarrassed to publish. She does not publish it yet. She runs through, in her head, which parts she stands behind and which are still tentative. She writes a four-line note naming what the AI did and what she did: *outline scaffold drafted with Claude, rule-text summary section drafted with Claude (verified against the docket directly), all named studies and statistics verified independently with primary-source links, named-expert quote obtained by phone this morning, framing and conclusions are mine.* She saves the document. She sends it to her editor with that note at the top.

That is competent practice. Now let me tell you what actually happened.

---

Priya did five things, in roughly this order, none of them optional.

The first was specification. She specified the work before she opened the tool. The seven minutes at the blank document were not warm-up. They were the most important seven minutes of the morning. Most of what made her first prompt good was not in the prompt — it was in the thinking that preceded the prompt. The prompt was the residue of the thinking.

Watch what happens to someone who skips this. A practitioner who opens Claude and types *help me write an explainer on the new grid-storage rule* as their first move is not giving the model a task. They are asking the model to guess the task. The model will guess. It will produce something. The something will be reasonable-sounding and miss the point, not because the model is dumb but because there was no specification for the output to be good against. The failure is upstream of the model. The model is doing exactly what it should given what it was given, which was nothing.

The second was delegation. Priya did not ask Claude to do everything, and she did not ask it to do nothing. She made decisions — some deliberate, some by reflex — about which parts of the work to hand over and which to keep. The framing — *what question is this piece actually answering* — she did herself; the model would have produced something competent and bland. The rule-text summarization she handed over almost wholesale, because reading three hundred pages of regulatory text in the available time was not possible, and the model was good at this kind of synthesis (with verification). The contested framing — *who is right about what this rule actually does* — she sketched the structure of and asked the model to surface the strongest version of each side, with primary-source citations she would verify. Different parts of the work have different shapes, and the practitioner does not treat them the same.

The third was conversation. The first prompt did not produce the right output. The first prompt did not produce the right output *even though* the first prompt was 280 carefully chosen words. The first prompt rarely produces the right output. Priya did not, at any point, treat one round of input-and-response as the deliverable. She kept refining. She introduced an adversarial move — *steelman the industry's claim, sourcing only from the actual rule text and the comment letters* — that surfaced a counterargument she had not held strongly enough on her own. She used the model the way you use a colleague who is fast, well-read, and slightly too agreeable: by pushing back on it.

The fourth was discernment. When she got output, she did not assume it was good. She read it for what kind of error it might be. The suspiciously round 40% was not a sign the model was dumb. It was the shape of a placeholder — a number that fits the pattern of what a statistic should look like in this context, generated without any particular source. Priya has been learning to recognize that shape since Chapter 0's Pew survey. She is, nine months in, building up a library of the kinds of mistakes this kind of model makes, and she runs each output past that library before she ships anything. This step takes the longest to develop. It is also the step that, when missing, is hardest to fake.

The fifth was diligence. The four-line note to the editor is not bureaucratic disclosure. It is the practice of a person whose name is on the work. If the editor asks tomorrow how Priya got to the framing, she can show her. If a reader queries the 37.2% statistic, she can show which docket it came from. The work has a story. The story belongs to Priya.

Specify. Delegate. Converse. Discern. Be diligent. These five steps are what I am going to call the Loop.

*Figure 1.2*

---

The Loop is not a checklist you run once. It is a cycle, and the steps loop back on themselves. Halfway through conversation, you may discover your specification was wrong — you go back. Halfway through discernment, you may realize you delegated something you should have kept — you go back. The picture I want in your head is not five boxes with an arrow running left to right. It is five boxes with arrows running in every direction, including a thick return arrow from diligence back to specification, because when a recurring task changes shape, the whole cycle starts over. We will come back to those return arrows in Chapter 8, where Priya — eighteen months further into her practice — runs a Tuesday with two of them. For now: hold the cycle, not the line.

---

What Priya did is the easy case, and I want to be precise about why it was easy — because the precision matters for everything that follows.

It was easy because she was sitting at her keyboard while the model was running. Every output crossed her eyes before it went anywhere. Every error she could catch by looking. The model did not take any actions in the world; it produced text, and Priya decided what to do with the text. The Loop was running in its most forgiving configuration: the one where the human is always in the room.

There are two harder configurations, and the book is organized around them.

The first harder configuration is when Priya is not there at the moment of execution. She has set up a recurring AI-assisted task — a Monday-morning market-intel summary, a daily competitive-coverage scan, a weekly newsletter draft — and the model is running while she is in a meeting, or on a reporting trip, or asleep. The Loop does not go away. But the steps reweight. Specification now has to anticipate problems Priya will not be there to catch. Diligence has to be designed in advance, because there is no real-time human eye on the output. Discernment may not happen at all on a given day, because the volume of output exceeds what any human can verify item by item.

The failure mode here is slow and quiet. An error in a one-off deliverable is visible immediately. An error in a recurring automated process accumulates. By the time someone notices the weekly summary has been citing a source that does not exist, seventeen weeks have gone by, and the error has propagated into seventeen documents that other people used. The blast radius of a specification mistake is proportional to how many times the specification runs before someone catches the problem. I am going to call this mode Automation, and Part II is about it.

![Figure 1.3 — Timeline showing error accumulation in an automated process](images/01-the-loop-and-the-three-modes-fig-03.jpg)

The second harder configuration is when the model is taking actions in the world on Priya's behalf. Not producing text she reviews — sending emails, posting to social media, calling APIs, modifying files. The model now has hands. The blast radius of an error grows in ways text-only mistakes cannot grow, because some actions cannot be undone. Discernment now has to happen before the action, not after. Diligence now has to account for failure modes that are specific to autonomy: the model taking a locally reasonable action in a context it has misread, the model escalating in a way no one authorized, the model acting without a clear model of who the affected stakeholders are.

The Chapter 11 case — an automated headline generator that pushes a draft to the publication's social channels 47 minutes before any editor reviews — is this configuration's characteristic failure. The system had a goal, available tools, no stakeholder model, no sense of proportionality, and no pause between deciding and executing. Each of those absences is a direct consequence of deploying the easy configuration's assumptions into a situation where those assumptions no longer hold. I am going to call this mode Agency, and Part III is about it.

Three modes. Five Loop steps. The Loop has to run in each mode, and the steps reweight as the mode changes. Augmentation — Priya at the keyboard, Part I — is where most of a practitioner's day still happens, and it is the mode we treat first and at length. Automation and Agency are where the stakes get higher and the design discipline gets harder.

The table below fixes the relationships. Not because you need to memorize it, but because having the whole picture in one place before we spend twelve chapters inside the details is the right way to start.


| Mode | Human presence during execution | Steps that reweight | Characteristic failure mode | Where covered |
|---|---|---|---|---|
| **Augmentation** | Human is present at the keyboard; every output crosses human eyes before use. | Conversation and Discernment stay central because the human can refine, challenge, verify, and edit in real time. | Fluent but wrong output gets accepted because the user mistakes confidence for correctness. | Part I |
| **Automation** | Human is not present when the task runs; the system executes on a schedule or trigger. | Specification and Diligence become heavier because problems must be anticipated and review systems designed in advance. | Small errors accumulate quietly across repeated runs before anyone notices. | Part II |
| **Agency** | Human may not review each decision before action; the system can take actions in the world. | Discernment and Diligence must move before execution, with stronger boundaries, permissions, and escalation rules. | The system takes a locally reasonable but globally harmful action because it lacks context, stakeholder awareness, or proportionality. | Part III |

---

I want to say one more thing about the mechanism before we move on, because it bears directly on how to read everything that follows.

The model's confidence is a textual feature. I said this at the beginning and I want to close with it because the temptation to forget it is strong. The output is fluent. The output is well-organized. The output sounds like it knows what it is talking about. None of that is evidence of correctness. All of it is evidence of a model that has read a lot of fluent, well-organized, confident text and has learned to produce more of the same.

The fluent practitioner has internalized this so completely that she has stopped being surprised by it. When the model produces a round number, she does not think *this might be wrong.* She thinks *this is the shape of a placeholder.* When the model produces a confident paragraph on a contested topic, she does not think *I should double-check this.* She thinks *I know exactly what kind of error could be hiding here, and here is how I will find it if it is there.*

That shift — from *this might be wrong* to *I know what wrong looks like here* — is what separates fluent from literate. It does not come from a checklist. It comes from the accumulated experience of running the Loop many times and learning, case by case, what the failure shapes look like in the particular domains you work in. Priya, at month nine, is partway there. By Chapter 8 she will be most of the way. By the time she leaves for a different publication in Chapter 13, the shift is no longer effortful.

The chapters that follow are designed to accelerate that accumulation. Not to give you a set of rules you follow mechanically, but to give you the concepts that let you see what is happening when the Loop runs and when it breaks. By the time you finish Part I, the Loop should feel less like a process you are consulting and more like something you are doing without thinking about it — the way a good driver does not think about steering, but can still describe exactly what they are doing if you ask.

Chapter 2 maps the nine cognitive capacities the Loop actually uses. Some of them you already have at the level the work demands. Some you do not yet. The map you draw at the end of Chapter 2 — your Practitioner Profile — is the diagnostic that pairs with the 90-day plan you build at the end of the book.

---

### Translate before you move on — and produce the Worked Loop Log

Priya's task was a 90-minute daily explainer in journalism. In your field, what is the equivalent? A 90-minute task you do regularly. Not the smallest task in your week; not the largest. The middle-weight task that recurs and where the Loop's structure earns its keep.

For a clinician: a structured-note write-up after a clinic patient. For a software engineer: a code review on a pull request. For a marketing manager: a campaign brief for an internal stakeholder. For a teacher: a unit plan for the following week. For a research scientist: a methods section for a draft paper. For a lawyer: a research memo on a defined question. The exact task changes with the domain. The shape — *bounded, recurring, requires real judgment, takes about 90 minutes well-executed* — is invariant.

**The Worked Loop Log — Chapter 1 Portfolio Artifact (Layer B with A template, deliverable + log):**

Pick one such task in your work that you will run in the next week. Before you start, sketch the five-step Loop structure on a page — Specify / Delegate / Converse / Discern / Be Diligent — with two-line stubs under each. Then run the task. As you go, fill in what you actually did at each step, with time-stamps where you can.

Save the log as `portfolio/01-worked-loop-log.md`. Two pages, no more. Time-stamped. Specific. Five sections, one per Loop step, plus a one-paragraph retrospective at the end naming where the structure helped and where it felt like overhead.

The Worked Loop Log is the second piece in your portfolio. It is also the *first piece* of your eventual End-to-End Case Study in Chapter 8 — the keystone. Chapter 8 takes one sustained task through the full Loop with loop-backs. The Worked Loop Log is the smaller-scale version that proves you can run the steps cleanly on one bounded task before you scale up to the keystone.

There is one more artifact this chapter opens that you will accrete across the book: your **`CLAUDE.md`** — the personal coding/process constitution for how you work with AI in your field. Open it now. Write three things in it:

1. *What I will not improvise without explicit instruction.* (Example for journalism: I will not generate citations the model cannot ground in a specific public document.)
2. *What I always specify before opening the tool.* (Example: audience, structure, source rule, exclusions.)
3. *What I always do before shipping.* (Example: verify every named source against the primary document; remove any statistic the model cannot trace to a named dataset.)

Save as `portfolio/CLAUDE.md`. We will return to it in Chapter 3 (Specification), Chapter 4 (Delegation), and Chapter 6 (Discernment), adding more rules as the book gives you reasons to.

---

**What would change my mind.** If a working practitioner could be shown to produce fluent-level outcomes while reliably skipping one of the five Loop steps — if there is a stable productive workflow that genuinely does not need, say, Specification, or genuinely does not need Discernment — the framework needs revision. Every practitioner I have watched who skips a step produces work that fails in a predictable way at that step's locus. But "what I have watched" is not a controlled study, and I want to be honest about that.

**Still puzzling.** I do not have a clean answer to which Loop step is most often the bottleneck for a given practitioner, or how you would measure it. My intuition is that Specification is the most-skipped, Discernment is the most-faked, and Diligence is the most-deferred. I do not yet have data that separates those three claims.

---

## Exercises

### Warm-up

**1. Name the step.** Reread the Priya narrative. For each of the following moments, identify which Loop step is primarily operating and write one sentence explaining your reasoning. *(Tests: ability to recognize the five Loop steps in context.)*

- She opens a blank document and writes about the piece for seven minutes before opening Claude.
- She types a second prompt asking the model to steelman the industry's claim, sourcing only from the rule text and comment letters.
- She opens the FERC docket to check a suspiciously round 40% figure.
- She writes a four-line note to the editor describing what the AI did and what she did.

**2. The mechanism in plain language.** In two to three sentences, explain to a colleague who has never taken this course why a language model can produce a citation that does not exist. Do not use the word "hallucination." Do not say the model is "confused" or "wrong" — explain the actual mechanism. *(Tests: retention of the core technical fact about prediction vs. lookup.)*

**3. Modes at a glance.** For each scenario below, name the mode (Augmentation, Automation, or Agency) and identify the one Loop step most likely to fail if the practitioner treats it the same way they would in Augmentation mode. *(Tests: ability to distinguish the three modes and their reweighting logic.)*

- A marketing manager builds a prompt that generates a weekly social media report from a shared data sheet, scheduled to run every Monday morning without review.
- A developer deploys an AI assistant that can book calendar appointments on a user's behalf when asked.
- A researcher drafts a literature review section by section, reading each output before moving to the next.

---

### Application

**4. Diagnose the skip.** Here is a prompt sent to a language model: *"Write something about our Q3 results."* Which Loop step was skipped before this prompt was written? Rewrite the prompt to correct for the skip. Your rewritten prompt should be at least 80 words and must include: the intended audience, the task's purpose, the desired structure, and one explicit constraint on what the model should not do. *(Tests: ability to apply Specification in practice, not just recognize it in theory.)*

**5. Identify the failure shape.** A colleague hands you a model-generated paragraph that includes the sentence: *"According to a 2021 McKinsey survey, 73% of executives reported that AI integration had reduced operational costs by an average of 34%."* Describe in concrete terms what kind of error this might be, why the model would produce it whether or not the underlying data is real, and what verification step you would take before including it in a deliverable. *(Tests: application of Discernment — recognizing the placeholder-number failure shape.)*

**6. Reweight the Loop.** Priya's team wants to automate the daily morning explainer she currently writes manually. Write a brief specification (150–200 words) for the automated version. Your specification must address: what the model should produce, what sources it should and should not use, what a failure output looks like so a downstream reviewer can catch it, and how often a human should review a sample of outputs to catch systematic error. *(Tests: ability to adapt Specification and Diligence for Automation mode.)*

---

### Synthesis

**7. The blast radius argument.** The chapter claims that "the blast radius of a specification mistake is proportional to how many times the specification runs before someone catches the problem." Using this claim, construct a concrete argument — not abstract, with a specific hypothetical scenario — for why the diligence step in Automation mode must be designed before the automation runs, not added after a problem appears. Your argument should be 200–300 words. *(Tests: integration of Specification, Diligence, and the Automation mode.)*

**8. Loop vs. no Loop.** Describe a plausible scenario in which a practitioner skips the Conversation step and still produces a good deliverable. Then explain why this does not constitute evidence that the Conversation step is optional. Your answer should engage directly with the chapter's claim about what the first prompt "rarely" produces. *(Tests: ability to reason about the Loop's design rather than just its steps — and to distinguish a lucky outcome from a reliable process.)*

---

### Challenge

**9. Where the modes blur.** The chapter presents Augmentation, Automation, and Agency as three distinct modes. Describe a real or plausible workflow where the boundary between two of the three modes is genuinely unclear — where it is not obvious which mode's design discipline applies. What question would you ask to determine how to treat it? What would the answer tell you about how to weight the Loop steps? There is no single correct answer; the goal is a rigorous argument. *(Tests: ecosystem thinking — seeing the framework's edges and reasoning about them rather than applying it mechanically.)*

**10. The Feynman test.** The chapter ends with a claim about what separates fluent from literate: the shift from *this might be wrong* to *I know what wrong looks like here.* Explain this distinction to someone who has never read this chapter, using a domain they know well (cooking, carpentry, music, medicine — your choice). Your explanation should make the distinction feel concrete and earned, not abstract. Then: what would a practitioner have to do, specifically, to make that shift in a domain they are new to? *(Tests: depth of understanding of Discernment — and whether the student can teach the concept, not just recognize it.)*

---

### A note about AI

The three modes — manual, augmented, automated — are not abstractions. Each one names a specific relationship between you and the model, and each has its own failure pattern.

Where the model genuinely helps: surfacing which mode you are actually operating in, when you thought you were operating in another. The model can describe what you delegated and what you retained in a given workflow, and the description often surprises the operator.

Where the model does damage: deciding the mode for you. The choice of mode is a values choice — what risk are you willing to take that the model is wrong, and what cost are you paying for the speed of automation. The model has no stake in either.

The rule: the loop's mode is your call. The model can help you see which mode you are in. It cannot tell you which mode you should be in.

---

## LLM Exercise — Chapter 1: The Loop and the Three Modes

**Project:** AI Fluency for [Your Role] — Your Portfolio's Second Artifact

**What you're building this chapter:** Two pieces. (a) The **Worked Loop Log** — one real bounded task in your work taken through all five Loop steps, time-stamped, saved to `portfolio/01-worked-loop-log.md`. (b) The first three rules in your **`CLAUDE.md`** — your personal coding/process constitution, saved to `portfolio/CLAUDE.md`. Both are Layer A templates filled with Layer B (your domain's) content.

**Tool:** Claude Project (continue from Chapter 0; your Role Dossier is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier from Chapter 0 and
my Baseline Audit are in the Project context.

Botspeak Chapter 1 watches Priya (a journalist nine months past her
Chapter 0 wake-up) run a 90-minute daily explainer task through all
five Loop steps — Specification, Delegation, Conversation, Discernment,
Diligence — competently but not yet at the eighteen-months-of-reflexes
mastery of Chapter 8. The chapter also names the three Modes
(Augmentation / Automation / Agency).

For Chapter 1's portfolio artifacts, do two things.

TASK 1 — DRAFT MY WORKED LOOP LOG.
Help me pick one bounded, recurring, ~90-minute task from my work and
draft the Worked Loop Log for it.

The task I will run:
- What it is: [FILL IN — e.g., "Friday client-update memo," "patient
  note after a clinic visit," "pull-request code review," "unit plan
  for next week," "methods section draft for a paper section"]
- How often I do it: [FILL IN]
- Who consumes the output: [FILL IN]
- Why it requires judgment (not just lookup): [FILL IN]

Walk me through the Worked Loop Log structure:
- Section 1 — SPECIFY. What I write before opening the tool. Audience,
  task, structure, source rule, exclusions. ~150 words.
- Section 2 — DELEGATE. What I hand to the model, what I keep, what
  I sketch and ask the model to fill. ~150 words.
- Section 3 — CONVERSE. The prompts I write and the adversarial moves
  I deploy. Show at least one steelman or edge-case probe. ~200 words.
- Section 4 — DISCERN. What I check, against what, looking for what
  kinds of errors. Name at least two failure shapes (the kind of
  placeholder number, the kind of citation that does not exist, etc.)
  ~150 words.
- Section 5 — BE DILIGENT. The AI Use Disclosure I attach, plus one
  note to my template/CLAUDE.md so I do not need to learn this twice.
  ~100 words.
- Retrospective — One paragraph. Where the structure helped. Where it
  felt like overhead. What changed for next time.

Time-stamp the sections. Be specific to my actual task, my actual
tools, my actual stakeholders. The log should be ~800–1,200 words
total. Save as `portfolio/01-worked-loop-log.md`.

TASK 2 — OPEN MY CLAUDE.md.
Help me draft the first three rules of my personal CLAUDE.md — my
coding/process constitution for AI work. Three sections:

1. WHAT I WILL NOT IMPROVISE WITHOUT EXPLICIT INSTRUCTION.
   2–4 rules specific to my field. (Examples for journalism:
   "I will not generate citations the model cannot ground in a
   specific public document." For a software engineer: "I will not
   commit code Claude generated without running it locally first.")

2. WHAT I ALWAYS SPECIFY BEFORE OPENING THE TOOL.
   The four or five elements I always include in a specification
   for my recurring task types. Audience, structure, source rule,
   exclusions, success criteria — your version.

3. WHAT I ALWAYS DO BEFORE SHIPPING.
   The verification or diligence moves I run on every consequential
   output before it leaves my desk.

Save as `portfolio/CLAUDE.md`. Note: this file is a LIVING document
— we will return to it in Chapter 3 (Specification), Chapter 4
(Delegation), and Chapter 6 (Discernment), adding rules as the book
gives me reasons to.
```

---

**What this produces:** Your portfolio's second and third artifacts — the Worked Loop Log (a real task taken through all five Loop steps) and the first version of your living `CLAUDE.md`. Both saved to `portfolio/`. Both will grow.

**How to adapt this prompt:**

- *For your own project:* Pick a task you will *actually run* this week. The Worked Loop Log written from a hypothetical task is structurally weaker than one written from a real one. The whole point is that the log is evidence, not aspiration.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful for setting up the `portfolio/` folder structure cleanly.
- *For Cowork:* Recommended. Cowork can walk the portfolio folder and remind you what files exist.

**Connection to previous chapters:** Chapter 0 produced the Baseline Audit (one piece of past work, audited). Chapter 1 produces the Worked Loop Log (one piece of current work, run with the Loop visible) and opens the `CLAUDE.md`. The portfolio is now three artifacts deep.

**Preview of next chapter:** Chapter 2 produces the first half of your Practitioner Profile — the Nine Capacities self-assessment. The Profile pairs with the delegation map you build in Chapter 4 to become one combined diagnostic artifact.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **W. Ross Ashby** was formalizing how a controller must match the variability of the system it controls decades before most people had heard of human-AI loops. Here's a prompt to find out more — and then make it better.

![W. Ross Ashby, c. 1948. AI-generated illustration based on a public domain photograph.](images/w-ross-ashby.jpg)
*W. Ross Ashby, c. 1948. AI-generated illustration based on a public domain photograph (Wikimedia Commons).*


**Run this:**

```
Who was W. Ross Ashby, and how does his Law of Requisite Variety connect
to a practitioner cycling through Augmentation, Automation, and Agency
on a single task? Keep it to three paragraphs. End with the single most
surprising thing about his career or ideas.
```

→ Search **"W. Ross Ashby"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "requisite variety" in plain language, as if you've never heard of cybernetics
- Ask it to compare Ashby's idea of a controller to a fluent practitioner running the Loop on a Tier-C task
- Add a constraint: "Answer in the style of a museum placard at a cybernetics exhibit"

What changes? What gets better? What gets worse?

---

## References

1. W. Ross Ashby, *An Introduction to Cybernetics*, London: Chapman & Hall, 1956. https://en.wikipedia.org/wiki/An_Introduction_to_Cybernetics
