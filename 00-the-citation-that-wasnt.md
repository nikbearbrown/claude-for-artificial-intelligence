# Chapter 0 — The Citation That Wasn't

*What the literate practitioner doesn't know they don't know.*

It is 9:42 on a Tuesday morning in Boston, and Priya Banksy is staring at an email she did not expect.

She had published the piece on Friday — forty-two hundred words on what Gen Z believes about the energy transition, prepared on a one-week turnaround for the publication's Climate vertical. Clean structure. Tight prose. The argument hedged in the right places. Eleven hyperlinked citations, including a 2024 Pew Research survey whose finding — *78% of Americans aged 18–29 say they would pay a premium for energy from renewable sources* — anchored the second-most-shared section of the piece. By Sunday evening the piece had been shared eleven thousand times.

The research editor at a competing publication had spent the weekend pulling the citations. Ten checked out. The eleventh did not. There was no 2024 Pew survey on the subject. Not the survey. Not the question wording. Not the 78% figure, which the research editor's email said politely "does not appear in any Pew dataset we have been able to locate," and could Priya help them understand how this happened before the publication's 1 PM editorial meeting?

Priya knows what happened. She had asked Claude for a draft of the section with citations. Claude had given her a draft with citations. She had clicked through nine of the eleven links — the ones to news articles and IEA reports she half-recognized — and they were fine. She had not clicked the Pew link. She had not asked the model whether the survey was real. She had pasted the section into her draft, polished the language, and shipped it. She had not, at any point, treated the output as something that still required pricing.

I want you to sit with that for a moment before we go further, because the failure here is not the one most people will name. Most people who hear this story will say Priya was lazy, or careless, or used the wrong tool. None of those things is true. Priya is twenty-nine years old with a BA from one of India's best-regarded communications programs and a one-year US master's behind her. She prepared meticulously for the case interviews and writing tests that landed her this job. She has used Claude through her master's, through job hunting, through the mock pieces she practiced during onboarding, and in all of those contexts the model gave her useful work. Her publication's onboarding included three slides on AI use. The most important slide said: *Always verify AI outputs before publication.* Priya nodded along. She did not know what verifying actually meant.

That gap — between hearing an instruction and knowing what it actually requires — is the subject of this book.

---

| AI Literacy | AI Fluency |
|---|---|
| Opens a chatbot and types a request | Specifies the task before delegating it |
| Reads the output and judges it by how it looks | Reads the output looking for where it could be wrong |
| Copies and pastes into the deliverable | Treats output as raw material, not finished work |
| Cites what the model returns | Verifies which citations are worth betting the audience's trust on |
| Polishes the prose before shipping | Runs a verification move calibrated to the failure mode |

*"AI Literacy" vs "AI Fluency"*

Let me name two things that look identical from the outside and are not.

The first is AI literacy. Priya has this. She can open a chatbot, type a prompt, read the output, copy and paste. She can, at a taste level, tell polished output from rough output. She has gotten useful work out of these tools many times. Nearly every working professional under fifty has AI literacy now, even when they think they don't, even when their managers worry that they don't. The bar is low and the world has largely cleared it.

AI literacy is necessary. It is not sufficient. It is not sufficient, in particular, when you have a job and the deliverables go to readers. Walking into that situation with only AI literacy is Priya's situation on Tuesday morning. The output looked polished. The output read competent. The output was wrong in a way the literate user cannot detect, because the failure mode is exactly the kind a literate user does not yet know to look for.

The second thing is AI fluency. Priya does not have this — yet. The senior editor down the hall does. It is the actual difference between Priya's piece on Friday and a piece by a senior writer given the same brief.

A senior writer three years ahead of Priya would not have shipped that piece. Not because she is smarter. Not because she is more careful in some vague, unspecifiable way. Not because she has read more books about AI safety. She would not have shipped it because she has a workflow Priya does not yet have. She runs the AI through five steps where Priya ran it through one. When a chatbot hands her eleven citations, she has a habit — a learned reflex — of asking: *which of these are the ones I'd bet the publication's reputation on?* She knows that the citation step is exactly the place a model hallucinates, and she has a verification move calibrated to that risk. She is not surprised when the model fabricates a source. By Tuesday morning, she is only surprised when it doesn't.

That difference is teachable. It has structure. It is not a personality trait, not a function of native carefulness, not something you absorb from another year of undirected experience with the tools. It is a discipline. It is what this book is for.

---

Here is the metaphor I keep coming back to.

A young American goes to India on her first work trip. She has, at some point, picked up a little Hindi — the way Americans pick up a little Hindi when they take a semester of it in college, or date someone whose parents are from Mumbai, or spend a week on Duolingo before the flight. She knows the Devanagari script well enough to sound out syllables, slowly. She knows *namasté* means hello. She knows *kitna* is "how much" and *kahan* is "where." She thinks of herself as someone who can manage.

She arrives at a major railway junction — Nagpur, say, or Itarsi, a hub where a dozen lines cross — and she has forty minutes to find the right platform for the Howrah Express. The departure board is in Hindi. She can read it, after a fashion. She sounds out the letters, matches a few syllables to the train name she wrote in her notebook, finds what looks like a match, and heads confidently toward Platform 7.

The train on Platform 7 is not the Howrah Express. She misread a conjunct consonant — a ligature that collapses two letters into one shape — the kind of thing a real reader processes automatically and a slow reader gets wrong under time pressure. The Howrah Express left from Platform 4. It is now gone.

The tourist who speaks no Hindi at all was never in danger of this. She knew, from the moment she arrived, that she could not read the board. So she found a railway employee, showed him her ticket, and was walked to Platform 4 with ten minutes to spare. She was not surprised when she needed help. She had built "needing help" into her plan.

The Hindi-literate tourist is the one stranded on the wrong platform. She had just enough to feel confident. She did not have enough to catch the error. She had not built "needing help" into her plan because she believed — reasonably, given her experience — that she could handle it. She was the only one who walked into a situation she could not manage and then managed it wrong.

The fluent speaker does not miss the train either, but for a different reason than the tourist who asked for help. She reads the board in one glance, confirms the platform, and has time to buy chai. She did not need to be careful. Careful is what you need when you might be wrong. She was not going to be wrong.

Not being able to read a sign can strand you. But misreading a sign you were confident you could read — that is the specific failure of the person in the middle. Confidence is load-bearing when it is warranted. When it is not, it is the mechanism of the mistake.

Priya, at 9:42 in the morning, is the tourist on the wrong platform. She had enough AI capability to feel confident. She did not have enough to catch the error. The piece looked right. It read like research. The polish was real. The underlying judgment — the judgment that should have caught the eleventh citation — was not there.

This book is not fluency for its own sake. It is the working competence of someone who shows up at the junction *trying* — how do I read this board, how do I confirm I have the right platform, how do I know when I should hand the ticket to someone else. The functional, daily-use skill that gets you on the right train.

---

There is one specific failure mode worth naming now, because it is the one Priya fell into and because most fluent practitioners had to climb out of it themselves before they could see it clearly.

A literate user asked to produce a deliverable gets four pages of output from the chatbot. Four pages, with headings and transitions and bulleted exhibits. The output *looks* like work. It looks, in the way a novice perceives work, exactly the way work is supposed to look. The literate user reads it, lightly polishes it, and ships it. The output is polished. The judgment that should have shaped it is invisible — because the polish is doing the job that judgment used to do.

A fluent practitioner, handed the same four pages, immediately becomes suspicious of them. She knows, because she has been burned, that a language model can fill four pages with confident, structured, citation-bearing prose that is nonetheless wrong in places that matter. To her, the four pages are not work. They are raw material. The work — the part she has to do, the part the model cannot do for her, the part her job actually depends on — has not yet started.

Here is what is strange about this. In almost every other domain, volume is a reasonable proxy for quality. A long memo took someone longer than a short memo. A thick report required more research than a thin one. The world we grew up in trained our intuitions on this correlation, and those intuitions are right nearly everywhere — except here.

Language models broke the correlation. They produce volume at constant cost. The four pages took the same effort to generate as the four sentences. Volume in the post-LLM world is not evidence of effort and not evidence of quality. To the literate eye, it still looks like both. To the fluent eye, it looks like raw material that has not yet been priced.

This is why working professionals ship deliverables their senior colleagues wouldn't, and why those deliverables read polished and read wrong. It is not the only reason. It is the easiest one to name on the first page.

---

I want to be honest about what this book can and cannot do.

It will give you a workflow — five steps, run as a cycle. Specification, Delegation, Conversation, Discernment, Diligence. We will spend a chapter on each. By Chapter 8 you will have run the full cycle on a real task — a piece of your own work — with yourself in the loop. By Chapter 10 you will have learned to run it without yourself in the loop. By Chapter 12 you will have learned to run it when the AI is taking actions in the world on your behalf and not just producing text.

It will give you a vocabulary — names for the moves the senior writer makes that Priya does not yet, so you can recognize them when you are making them and notice when you are skipping them.

**It will give you a portfolio.** This is new. Every chapter of this book produces an artifact you keep. By Chapter 13 you will have a brand-portable record of your AI fluency: three living governing files documenting your method, six customized frameworks adapted to your domain, three pieces of self-knowledge, and one end-to-end case study of your own work taken through every step the book teaches. A future employer, admissions committee, or peer reviewer can read the portfolio without having read this book. The portfolio is the evidence. The closing question of the book — *what specifically did the AI do, and what did you do that it could not?* — is answered by handing over the portfolio.

It will not teach you a specific AI tool. The examples use Claude, with sidebars for ChatGPT and Gemini, but the tools change every six months and the discipline does not. It will not teach AI ethics in the comprehensive sense. It will not teach you the inner workings of language models. There is one paragraph, in Chapter 1, on how an LLM produces its output, because that paragraph does work. The rest of the model-internals literature is a field you can visit afterward.

What it will teach is AI fluency. The difference between Priya on Friday and a senior writer on the same brief. The difference between the practitioner who uses AI to do their job better and the practitioner who uses AI and does their job worse.

---

I will tell you now what I think is the most interesting thing about Priya's situation, because it is easy to miss if you are focused on the mistake.

Her publication hired her specifically because she was AI-fluent at the literacy level. They valued the speed. They counted on it. They gave her a one-week turnaround on a piece that, five years ago, would have been a three-week project for a writer and a fact-checker. The publication bet on AI as a productivity multiplier, and they were right to bet on it, and they staffed the piece assuming the multiplier would hold.

The multiplier did hold. Priya produced forty-two hundred words in four days. The piece looked like four days of work. The piece cost less time and money than four days of pre-AI work would have cost. Everything about the economics worked the way it was supposed to.

And then one citation was wrong, and the whole piece was now in question, and the publication's reputation with its audience had taken a hit it would need months to repair.

This is what I mean when I say AI literacy is not sufficient. The literate user produces *a lot* of work. The problem is that the work is unpriced — the literate user cannot look at her own output and tell where the value is and where the rot is. The publication bet on a productivity multiplier and got one. What they did not yet know is that the multiplier comes with a verification cost, and that someone has to pay it. If Priya does not pay it before the piece publishes, the audience pays it afterward, and the cost the audience pays is denominated in trust.

| Who pays | When | In what currency | Consequence |
|---|---|---|---|
| Fluent practitioner | Before delivery | Her time | Clean deliverable |
| Literate practitioner | Never | Nothing upfront | Audience discovers the error |
| Audience / employer / client | After delivery | Trust, relationship, repair time | Confidence in the practitioner and the publication takes a hit |

The fluent practitioner pays the verification cost in her own workflow, before the work leaves her desk. That is most of what fluency *is*. That is most of what this book teaches.

It is now 9:58 AM on a Tuesday in Boston. Priya has three hours until the 1 PM editorial meeting where she will help draft the correction. The next thirteen chapters are about how she should have spent the previous four days, and what — between now and 1 PM — she can salvage.

By Chapter 8 we will be back at this kind of Tuesday. Priya will be eighteen months further into her career. She will face a comparable brief. She will not ship a citation that doesn't exist. The arc from this Tuesday to that one is the arc the book teaches and the arc the reader walks alongside her, in their own field, with their own work.

Open Chapter 1. We'll start at the beginning.

---

**What would change my mind.** If a serious longitudinal study of working-professional AI use showed that the literate–fluent gap closes within a year of normal job exposure, without any structured framework — that practitioners self-teach fluency from sheer reps — the book's central premise weakens. I have not seen such a study. The closest evidence I am aware of points the other way: literacy plateaus, and the fluency gap persists or widens.

**Still puzzling.** I do not yet have a clean way to distinguish "fluency" from "good judgment shaped by enough painful experience." It is plausible that what I am calling fluency is simply what painful experience teaches anyway, and that naming the moves and rehearsing them just compresses the timeline. I have not yet seen the experiment that would prove it.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Priya's failure has a name in the academic literature: the **fluency trap**. Fluent output triggers an evaluation booster — readers trust well-written prose more than the evidence warrants. The trap doesn't only fool literate users; it amplifies whatever evaluation the reader was going to make, including the wrong ones. The fabricated citation is the visible symptom; the trust-in-the-fluency is the mechanism.
>
> The companion advanced volume *Computational Skepticism for AI* opens by naming this directly and gives you four philosophical moves to interrupt it before it does damage — Cartesian doubt, Hume's induction limit, Popperian falsifiability, and the Plato's Cave move — plus the Five Supervisory Capacities the deeper book is organized around.
>
> See *Computational Skepticism for AI*, **Chapter 1 — The Skeptic's Toolkit**.

---

### Translate before you move on — and start your portfolio

Priya's failure was a journalism artifact: a fabricated source for a load-bearing statistic. In your field, what's the equivalent? Stop and answer before turning the page.

For a clinician, the equivalent is a fabricated drug-interaction reference. For a research scientist, a fabricated primary-literature citation. For a lawyer, an invented precedent. For a teacher, a misattributed pedagogical study. For a marketing manager, a made-up consumer-survey finding. For a chemist, a synthesized-instrument reading. The exact artifact changes with the domain. The shape of the failure — *the load-bearing claim that rests on a source the literate user did not verify* — is invariant.

This chapter ends with the first piece of work you will keep. It is called the **Baseline Audit**, and it is the opening artifact of your portfolio.

**The Baseline Audit — Chapter 0 Portfolio Artifact (Layer B, diagnostic):**

Pick one piece of AI-assisted work you have produced in the last three months. A document, a report, a memo, a piece of code, an analysis, a teaching plan, a brief, an email thread — anything you used AI to help produce. Open it now.

Find the one most consequential single claim in it — the claim that, if false, would cost the most. The 78% figure. The recommendation. The dosage. The deadline. The named source. The conclusion the rest of the work depends on.

Trace that claim back. Where did it come from? Did you verify it at the time? Could you verify it now, without the AI's help? If you cannot — note that. If you can but did not — note that too.

Save the audit as `00-baseline-audit.md` in a new folder called `portfolio/` somewhere you can find it. Three sections, no more than half a page total:

1. *Piece audited.* What was the work, who was it for, when did it ship.
2. *Load-bearing claim.* The single most consequential element, named.
3. *Trace.* Whether it would survive a verification attempt today, and what specifically would need to be checked.

The Baseline Audit is paired with the **Final Audit** you will produce in Chapter 13 — the same piece of work, audited again, eighteen chapters later. The pair is the cleanest possible evidence of fluency: the same reader, the same artifact, two judgments separated by the book. If the Baseline and the Final read identically, the book did not teach. If they read differently — if you can now see in your own past work what you could not see today — the book did its job.

The portfolio is a living artifact. Open it now. We will be adding to it for the rest of the book.

---

### A note about AI

The chapter opens on a fabricated citation. The note's question is what makes that fabrication different from a human error of memory.

Where the model genuinely helps: explaining why hallucinated citations have the shape they do — author names that sound plausible, journal titles that approximate real ones, page numbers in plausible ranges. The pattern recognition is useful for spotting them in others' work.

Where the model does damage: producing the citation you needed but never had. The shape will be right. The substance will not exist. You will not catch it unless you check.

The rule: every citation from the model is unverified until you have opened the cited source in your own browser.

---

## LLM Exercise — Chapter 0: The Citation That Wasn't

**Project:** AI Fluency for [Your Role] — Your Domain Field Manual

**What you're building this chapter:** A **Role Dossier** you'll pin to your Claude Project for the rest of the book, and the **Baseline Audit** you just sketched above — drafted, structured, and saved.

**Tool:** Claude Project (set up "AI Fluency for [My Role]" — you'll return every chapter) + your file system (the `portfolio/` folder you just created).

---

**The Prompt:**

```
I am working through "Botspeak" by Nik Bear Brown and across the book I will
build a portfolio of AI-fluency artifacts in my own field. This is the
setup chapter — Chapter 0, The Citation That Wasn't. I need help with two
tasks.

TASK 1 — SPECIFY THE ROLE. The role should be:
- One I actually work in (or am about to enter)
- Specific enough to be useful — not "knowledge worker" but "junior associate
  at a regional law firm" or "growth marketer at an early-stage SaaS company"
  or "clinical pharmacist on a hospital night shift"
- Bounded enough that the failure modes are recognizable to anyone in the role
- Big enough that the playbook helps a real population

My context:
- Role / job title: [FILL IN]
- Industry / sector: [FILL IN]
- Career stage of the playbook's reader: [0–6 months / 6–18 months / 18–36 months / 5+ years]
- 2–3 task types I do most weekly: [LIST]
- Whether AI use is sanctioned, unsanctioned, or contested in my workplace: [FILL IN]

Push back if my role is too broad. Help me sharpen until the playbook would
be unmistakably for someone in this role and not someone in an adjacent one.

TASK 2 — DRAFT THE BASELINE AUDIT. Chapter 0 introduces the Baseline Audit
as the first portfolio artifact. I will redo it as a Final Audit in
Chapter 13. The pair is the book's before-and-after evidence of fluency.

Help me draft mine. The piece I am auditing:
- What it was: [FILL IN — document, report, memo, code, analysis, teaching plan, brief, etc.]
- Who it was for: [FILL IN]
- When it shipped: [FILL IN]
- How I used AI in producing it: [FILL IN — research, drafting, citations, code, structure, all of it]

The most consequential single claim in the piece:
- The claim itself: [FILL IN]
- Why it's load-bearing — what depends on it: [FILL IN]

Walk me through a trace of that claim. For each:
- Where did it come from in the AI session?
- Did I verify it at the time? How?
- Could I verify it now, without the AI's help? What would I check?
- What specifically would not survive a hostile re-read?

End with:
1. A one-paragraph "Role Dossier" I can pin to my Claude Project's system
   prompt so every future chapter exercise inherits the role context.
2. The Baseline Audit itself, formatted as the three sections in Botspeak
   Chapter 0: Piece audited / Load-bearing claim / Trace. No more than half
   a page total.

Save the Baseline Audit as `portfolio/00-baseline-audit.md`.
```

---

**What this produces:** A Role Dossier (pinned to the Project for every future exercise) and the Baseline Audit (saved to your portfolio folder). The first of seventeen artifacts. Twelve more to come.

**How to adapt this prompt:**

- *For your own project:* Fill in the bracketed fields. If you wear multiple hats, pick the role you'll keep growing in for the next two years.
- *For ChatGPT / Gemini:* Works as-is. Set up as a Custom GPT for persistence. Gemini's Drive integration handles the portfolio folder cleanly.
- *For Claude Code:* Not yet — this chapter is conceptual. Claude Code becomes useful starting Chapter 3 when you build the Specification Library.
- *For a Claude Project:* Recommended. The Role Dossier becomes part of the system prompt going forward.
- *For Cowork:* Recommended for managing the portfolio folder. Ask Cowork to create the folder structure: `portfolio/00-baseline-audit.md`, `portfolio/CLAUDE.md`, `portfolio/DESIGN.md`, `portfolio/PROJECT-template.md` (the last three are stubs you'll fill across the book).

**Connection to previous chapters:** None — this is Chapter 0. The Role Dossier and the Baseline Audit are the foundation every subsequent chapter exercise builds on.

**Preview of next chapter:** Chapter 1 takes a typical task in your role and walks the full Loop on it — your role's version of Priya's Tuesday at her best. The Worked Loop Log becomes the second piece in your portfolio.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Henriette Avram** was teaching computers to handle bibliographic references with structural integrity decades before most people had heard of "AI hallucinations." Here's a prompt to find out more — and then make it better.

![Henriette Avram, c. 1970s. AI-generated portrait based on a public domain photograph.](images/henriette-avram.jpg)
*Henriette Avram, c. 1970s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

![Henriette Avram](../images/henriette-avram-eod.png)

*Puppet Art by [Nik Bear Brown](https://www.nikbearbrown.com/).*

**Run this:**

```
Who was Henriette Avram, and how does her work on MARC (Machine-Readable
Cataloging) connect to the problem of fabricated citations from AI? Keep it
to three paragraphs. End with the single most surprising thing about her
career or ideas.
```

→ Search **"Henriette Avram"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain how MARC actually represents a citation, as if you've never thought about citation as a data structure
- Ask it to compare Avram's verification approach to how today's retrieval-augmented systems try (and fail) to ground citations
- Add a constraint: "Answer as if you're writing a footnote in a textbook about the Citation That Wasn't"

What changes? What gets better? What gets worse?

---

## References

1. Library of Congress, "Henriette Avram, 'Mother of MARC,' Dies," *Library of Congress Information Bulletin*, May 2006. https://www.loc.gov/loc/lcib/0605/avram.html
