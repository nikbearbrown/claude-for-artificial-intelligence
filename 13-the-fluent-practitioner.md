# Chapter 13 — The Fluent Practitioner

*Frequency is not fluency. The question that separates them is whether you can name, on any piece of work, what the AI did and what you did that it could not — and whether you can show someone the work itself, not just the claim.*

It is a Wednesday in the spring of Priya Banksy's third year in US journalism. Two years and three months ago, she sent a feature to publication with a fabricated Pew survey in it. Eighteen months ago, she sent a scoping memo to her editor that caught the same kind of failure in fourteen seconds. Today she is sitting at a different desk at a different publication — she moved last month, an editorial lead at a small investigative outlet that needed someone who could work with AI tools across their newsroom without compromising what makes the place worth reading.

The conversation that got her the role started with a document. The publication's editor-in-chief had asked her, by email, to send "anything that would help us understand how you work." Most candidates send a clip reel. Priya sent her portfolio's Cover Memo — one page, plain language, addressed to a reader who had never heard of *Botspeak* — and the link to the End-to-End Case Study folder it pointed at. The editor read both before their second conversation. The second conversation was about the work, not about whether Priya could do the work. The portfolio had already settled that.

This is what the book has been building toward. Not the answer to the closing question. The artifact that *is* the answer.

---

There is a question that separates two kinds of people who use AI in their work, and it is not the question most people expect.

It is not: do you use AI tools? Almost everyone does. It is not: do you use them often? Frequency is not fluency. It is not: do you understand how large language models work at a technical level? That helps, but knowing the architecture does not make you good at the work any more than knowing how a piano works makes you good at playing one.

The question is this: *what specifically did the AI do in this piece of work, and what specifically did you do that it could not?*

Most people, asked that question on their own work, cannot answer it. They say something like "the AI helped me draft it and I cleaned it up," which is true in the way "I cooked with heat" is true about a meal — accurate about the mechanism, completely silent about the judgment. They cannot separate their contribution from the model's. They cannot name where the work required domain knowledge the model did not have. They cannot say with any precision which parts they stand behind on their own authority and which parts they delegated.

This is not a failure of capability. It is a failure of attention. They have been using the tool without developing a practice around the tool, and without a practice, the tool is just a faster typewriter — producing more output without building any skill.

This book exists to produce something specific in you: the ability to answer that question. Not the vocabulary for it — though the book has given you vocabulary — but the genuine capacity underneath the vocabulary, earned through the reps. And: an artifact that answers the question on your behalf, without requiring the asker to take your word for it. The closing chapter is about both — how to make sure the reps happen, and what your portfolio now allows you to hand over.

---

The honest re-assessment question is not what you now know. It is what you now *do differently*.

Reading without running produces literacy, not fluency. If you worked through this book without putting the Loop on a real task, without running the four-layer verification on a real deliverable, without writing a five-component specification before a real piece of work, then the framework is in your head but not yet in your hands. The framework in your head is useful. It is not the same thing as the practice. The practice is in the hands.

If you did run the exercises — if you took the mid-chapter moves seriously and ran them on real work — then something should have changed that you can point to specifically. A piece of output you caught that you would have shipped three weeks ago. A delegation you declined that you would have made three weeks ago. A specification you wrote that produced good output on the first pass because you had thought clearly about intent and constraints before you typed anything. These are the receipts of practice.

The portfolio is the receipts made visible. If you have been building it across the book — the governing files, the customized frameworks, the case study, the audits — you do not need to argue that your practice has changed. You can show it.

If you cannot point to a specific change in real work, the remaining question is whether the obstacle was time — in which case the 90-day plan below is what matters now — or whether the framework, as I have given it to you, does not fit your domain cleanly enough to be immediately actionable. The second possibility is real. It deserves a direct response.

---

The Nine Capacities, the Decision Node model, the four adversarial moves — these are the vocabulary this book uses. They are not domain-neutral in detail, even if they are domain-neutral in structure. A pharmacist's fluency includes checks and constraints and judgment calls that a journalist's fluency does not, and vice versa. The Loop is the same. The specific contents of the Loop are not.

When a framework does not fit your domain cleanly, the temptation is to either force-fit it — applying the vocabulary awkwardly to work it was not quite built for — or abandon it for not being specific enough. Both are mistakes. The right move is translation.

Translation is the work of taking the framework's structure and filling it with your domain's specific content. What does *Strategic Delegation* mean for someone who writes code, versus someone who writes legal briefs, versus someone who designs clinical trials? The Capacity is the same. The specific judgment calls it requires — which AI outputs to trust, which to verify independently, where the domain knowledge the model lacks lives in your field — are different in each case.

The translation is its own kind of fluency. It is, in fact, a sign that the framework has been genuinely absorbed rather than memorized: you can see why it maps onto your work and where its vocabulary needs adjustment to fit. Senior practitioners in any field do this naturally with every framework they encounter. It is not a special skill for AI work. It is just pattern-recognition applied to your own domain, which you are better positioned to do than any author writing for a general audience.

Your portfolio is the translation made operational. The `CLAUDE.md` and `DESIGN.md` you have accreted are not the generic templates the book described. They are the field-specific governance documents you produced by filling those templates with the conventions, constraints, and verification checks that matter in your work. A future reader of your portfolio can see exactly where the framework met your domain and what each met-up produced.

The concrete way to do the translation, going forward: pick a senior person in your field whose AI work you respect. Watch what they do. Ask them — directly, if you can — what they verify that others do not, what they will not delegate to a model regardless of how good the output looks, what failure modes they have seen that others missed. The answers to those questions are your domain's specific addenda to this framework. They will not all be in this book. Add them to your `CLAUDE.md` and `DESIGN.md` as they come. Those files are living documents.

---

There is a structural reason why some people develop fluency and others do not, and it is not about starting talent.

The literature on deliberate practice identifies three ingredients that distinguish practice that builds capability from experience that just accumulates. The first is feedback — not vague feedback, but specific feedback, tied to specific outputs, close in time to the output. When you run the four-layer verification on a piece of work, the verification is feedback. It tells you, specifically, which claims did not hold up and why. When you write an AI Use Disclosure before shipping, the disclosure is feedback: if you cannot complete it honestly, you learn something about what you did not check.

The second is working at the edge of current ability. Not the comfortable zone where AI helps you do what you already know how to do, faster. The uncomfortable zone where you are asking it to help you do something you do not yet know how to do well, or where you are pushing the verification harder than feels necessary, or where you are making the specification more precise than you are confident about. Staying in the comfortable zone produces experience without improvement. The edge is where the capacity moves.

The third is repetition — not of the same thing, but of the same *type* of thing. The specification move, practiced daily, becomes automatic. The four-layer verification, practiced on consequential work, becomes fast. The delegation map, sketched at the top of every AI-assisted task, becomes the first thing you do rather than the thing you forget. Automaticity is the sign that a practice has become a capacity. The reps are what produce automaticity.

![Figure 13.1 — Three-ingredient deliberate practice model](images/13-the-fluent-practitioner-fig-01.jpg)

Most AI use fails to meet any of these three criteria. The feedback is vague — did it seem right? The work stays in the comfortable zone — tasks the user already knows how to evaluate. The repetition is of the same comfortable pattern, not of the skill being developed. This is how people accumulate years of AI use without accumulating fluency. The years are real. The practice, in the technical sense, was not.

---

Pick two capacities — not nine, not five, not the ones you think you should develop. The two you most want to move one level up in ninety days. The movement of two, done seriously, compounds. The aspiration to move nine, done diffusely, moves nothing.

For each of the two, you need three things.

A daily rep. Something specific, recurring, tied directly to the capacity, that you do every working day. The rep should take under five minutes on most days and should produce an artifact you could look back at. For *Effective Communication*, the rep is writing a five-component specification — intent, constraints, success criteria, exclusions, output format — before every consequential prompt. Not after. Before. The five-component spec, written daily, becomes automatic in about thirty working days. For *Critical Evaluation*, the rep is running the two-step verification on every Tier C output: first, does this hold up against the sources it claims to use; second, is there anything here that should make me distrust the parts I cannot independently check. For *Strategic Delegation*, the rep is a three-line delegation map at the top of every AI-assisted task: what the task is, what the model will produce, what I will produce that it cannot. The map takes ninety seconds. It forces the judgment before the work begins rather than after.

A weekly review. Fifteen minutes, same time, same day, every week. One question: did the rep actually happen this week, and what did I learn? The review is not an assessment of quality. It is a forcing function for noticing. Most deliberate practice dissolves not because the practitioner decides to stop but because the rep becomes invisible — it happens or does not happen without any moment of attention. The fifteen-minute review creates the moment of attention. It also, over ninety days, produces a log of what you learned — which becomes part of your portfolio, the next evidence that the practice is active.

A 90-day artifact. Something specific, at the ninety-day mark, that is the downstream product of the practice. Not a process artifact — a capability artifact. A piece of analysis that, on the four-layer verification, holds up without revision. A brief that a skeptical reader cannot identify as AI-assisted, not because you hid it but because the judgment is visibly yours. An automation design that earns a stakeholder's approval without negotiation because the anticipatory specification addressed every question before it was asked. The artifact is what the practice is *for*. It is the answer to the question of whether ninety days of reps moved anything. Name it now. Write it on the same page as the plan. If the artifact you name is too vague to know whether you have achieved it in ninety days, make it more specific until it is not. **Save it to `portfolio/13-90day-plan.md` and add the resulting capability artifact to the portfolio when the ninety days are up.**

| Slot | Capacity name | Daily rep — what / how long / artifact | Weekly review — day / time / the one question | 90-day artifact (specific enough to evaluate) |
|---|---|---|---|---|
| **Capacity 1** | _________________ | _________________ / _____ min / _________________ | _____ / _____ / _________________ | _________________ |
| **Capacity 2** | _________________ | _________________ / _____ min / _________________ | _____ / _____ / _________________ | _________________ |

*Figure 13.2*

Two capacities. Three commitments per capacity. Ninety days. This is not a large ask. It is a precise one. Precision is what most professional development plans lack, which is why most professional development plans do not produce development.

---

I want to come back to the opening question, because I want to give you the full version of the answer — not the vocabulary, but what the answer sounds like when the practice is there behind it.

The question: what specifically did the AI do in this work, and what specifically did you do that it could not?

Here is what a fluent practitioner's answer sounds like on a real piece of work — a publication-class investigative scoping memo, of the kind that appears in earlier chapters:

*I used the model to draft the company-snapshot and trade-press synthesis sections. The source list for those sections was verified independently; the three primary documents I relied on are linked in the appendix. I did the founder-background analysis without the model in places that required reading the regulatory filings against what was claimed publicly — those signals require knowing how that particular financing structure has been used in this segment before, and that pattern recognition is not in the model's training in any actionable form. The risk assessment is mine. I used the model to surface candidate risk factors and rejected three of its five suggestions — I can tell you which three and why if you want to audit the judgment. The four-hypothesis framework in the recommendation was developed in conversation with the model and then narrowed by me. The recommendation at the end is mine. The accountability for the memo is mine. If something in here is wrong, it is wrong because I missed it, not because I trusted a model I should not have.*

That answer takes ninety seconds to give. It separates the model's contribution from the practitioner's. It names the specific places where domain knowledge the model did not have was brought to bear. It assigns accountability cleanly. It surfaces the verification rather than burying it. It is, in any professional setting — an interview, an editorial meeting, a regulatory review, a hiring conversation — the kind of answer that tells the asker that the work is trustworthy without requiring them to audit every line.

| Sentence or phrase from the answer | What it does | What the vague literate-user answer omits |
|---|---|---|
| *"I used the model to draft the company-snapshot and trade-press synthesis sections."* | Names what the AI did specifically — which sections, which moves | The literate user says "helped me draft it" without naming which parts |
| *"The source list for those sections was verified independently; the three primary documents I relied on are linked in the appendix."* | Surfaces the verification — what was checked, against what, where it can be audited | The literate user buries or omits verification entirely |
| *"I did the founder-background analysis without the model in places that required reading the regulatory filings against what was claimed publicly."* | Names where domain expertise was load-bearing — and *why* the model could not substitute | The literate user cannot name this — which means she does not know it |
| *"The recommendation at the end is mine. The accountability for the memo is mine."* | Assigns accountability cleanly to a single named person | The literate user leaves accountability ambiguous — "we put it together" |

*Figure 13.3*

The literate user gives the vague answer because she has not been paying the kind of attention that produces the specific answer. The fluent practitioner gives the specific answer because she has been paying that attention in every piece of work she has done, over the months and years of the practice, until the attention is no longer effortful — it is just how she works.

That is what the ninety days is for. Not to produce the answer to the question. To build the habit of attention that makes the answer available, on demand, on any work, without preparation.

---

There is a second form of the answer that this book has been building toward, and it is in some ways more important than the spoken version.

It is the form where you do not have to give the answer. You hand someone the portfolio.

The portfolio is the answer to the closing question, written in advance, on every piece of work it documents. The End-to-End Case Study answers it for one major piece. The Specification Library answers it for your typical task types. The Verification Protocol answers it for your standards. The Diligence Framework answers it for any AI system you currently work with. The Baseline Audit and the Final Audit answer it for your past work, before and after.

The fluent practitioner does not need to argue for her fluency. She hands someone the portfolio. The portfolio argues for her.

This is why the Cover Memo at the front of the portfolio matters. It is the cover letter every unfamiliar reader sees first. One page. No book jargon. The reader who picks up your portfolio in twenty minutes between meetings should be able to read the Cover Memo, scan the case study, glance at the audits, and form an accurate judgment of how you work. The Memo does not boast. It points at the artifacts. The artifacts make the case.

If you do not yet have a Cover Memo — if your portfolio is still a folder of pieces without a front door — that is the most important single thing to draft now. The template is in Appendix C. The exercise at the end of this chapter walks you through the first complete draft.

---

The field is changing fast enough that some specific tool or technique in this book will be obsolete before many readers finish it. The Loop will not be obsolete. The Capacities will not be obsolete. The ability to separate your contribution from the model's and stand behind your contribution on your own authority will not be obsolete — it will become more valuable as the field matures and the organizations operating in it get better at distinguishing practitioners who have it from those who do not.

Three years into the AI-saturated workplace, the signal I see consistently is that senior practitioners can already tell the difference. They can tell by the quality of the questions a candidate asks about AI use. They can tell by how quickly someone can explain what judgment they applied in work that was AI-assisted. They can tell by whether someone knows what the failure modes of their own AI-assisted workflow are without being asked to check. They can tell, increasingly, by whether someone has a portfolio they can hand over — and what is in it.

These are not technical signals. They are practice signals. They are downstream of attention paid over time.

The book is over. The practice is not. The ninety days is how it starts. What comes after ninety days is yours.

Priya, on her Wednesday, three years past Ch 0, is not at the end of her practice. She is at a different point along it. The portfolio she handed her new editor before the second interview is older than the role she now holds. She will update it this month. She will update it again in a year. The portfolio is a living artifact — same shape, evolving contents, the way the practitioner herself is the same person whose specific judgments improve over time.

If you do nothing else with this book, do this: keep your portfolio alive. Update it when your role changes. Add the case studies that matter. Redo the audits when your past work no longer reads the way it did. The portfolio is the throughline of your career across the AI transition. The closing question is answered, again and again, by what is in it.

---

### Translate before you close — and complete the portfolio

This is the last chapter of the book, and it produces the last set of portfolio artifacts: the **Final Audit**, the **90-Day Plan**, and the **Cover Memo**.

**The Final Audit** (Layer B, diagnostic — paired with Ch 0 Baseline Audit). Open the Baseline Audit you wrote at the end of Chapter 0. Find the piece of past work it audited. Audit it again, today, using the four-layer verification frame from Chapter 6 — but now with the capacities and reflexes you have built across the book. Three sections, no more than half a page total:

1. *Piece audited.* Same piece as the Baseline Audit. Same metadata.
2. *Load-bearing claim — re-read.* The same single most consequential element from the Baseline. What do you now see in it that you did not see then?
3. *Verification trace — done.* What would the verification look like if you ran it on this piece now? Run it. Note what holds up and what does not.

Save the Final Audit as `portfolio/13-final-audit.md`. The pair — Baseline and Final, the same piece of work seen by the same person twice — is the cleanest single comparison your portfolio offers. If the two audits read identically, the book did not teach. If they read differently — if you can now see things in your past work that you could not see when you started — the book did what it set out to do.

**The 90-Day Plan** (Layer A template + Layer B content, synthesis). The template in Figure 13.2 is the structure. Pick two capacities. Define the daily rep, the weekly review, and the 90-day artifact for each. Save as `portfolio/13-90day-plan.md`. Schedule the weekly reviews on your calendar right now. The plan that is not on the calendar does not happen.

**The Cover Memo** (Layer A template + Layer B content, synthesis). The template lives at `portfolio/00-cover-memo-template.md` (also reproduced in Appendix C). One page. Six sections. Plain language. No book jargon. Addressed to a reader who has never heard of *Botspeak*. The Memo points at the artifacts in your portfolio and tells the unfamiliar reader the shortest path through them.

If you cannot write your Cover Memo cleanly, that is information about your portfolio, not your writing. It means the portfolio does not yet have an argument it can name out loud. Go back to the artifacts. Re-read the case study. The Memo writes itself once the portfolio is coherent. **If the Memo will not write — that is the most important diagnostic the book offers. Pay attention to it.**

Save the Memo as `portfolio/cover-memo.md` at the top level of your portfolio folder. It is the first thing every future reader sees.

The portfolio is now complete. Seventeen artifacts. Five sections. One case study at the center. One pair of audits to bracket the change. One Cover Memo to lead the unfamiliar reader through. Add a date to the top of each artifact. Plan to update them on a schedule that fits your work. The portfolio is yours now.

---

*What would change my mind.* If, ten years from now, practitioners I would describe as fluent turn out to be no more effective than well-trained literate users — if the distinction is rhetorical rather than functional — the book is wrong about what matters. I do not yet have ten years of evidence. The early signal is that the distinction is real, is growing, and is increasingly visible to the people doing the hiring. I would update on contrary evidence. I have not seen it yet.

*Still puzzling.* I do not know whether nine is the right number of capacities. It is the number I observe doing work. It might consolidate to six as the field's vocabulary stabilizes. It might expand to twelve as new capability classes emerge. The structure of the capacities is more durable than the count, and I would not be surprised if a future edition of this book has fewer than nine, named differently, in ways I cannot yet see.

---

> **Going deeper — *Computational Skepticism for AI***
>
> The closing artifact this chapter asks of you — a defensible, specific account of what the AI did and what you did that it could not — has a longer form in the advanced volume. There it is called both the **AI Use Disclosure** (a supervisory log on a single piece of work) and the **cognitive profile** (a map of where the AI is genuinely strong, where it is structurally weak, and where it is absent for a given deployment). The closing chapter of the deeper book treats this as the engineer's most important structural authority: the authority to say *this AI should not be deployed for this purpose* — to refuse, on the basis of named limits the validation toolkit cannot reach. Three categorical limits in particular do not yield to capability scaling: the **meaning gap** (the model manipulates symbols without grasping what they mean in the world), **intentionality** (the model has no aboutness toward the world), and the **data-world gap** (training data is at best an imperfect proxy for the deployment context).
>
> If you find yourself, after the 90-day plan, wanting to deepen the practice into engineering-grade work — auditing real deployments, writing defensible fairness choices, building maintenance loops for AI in production — the advanced volume is the next book. It is harder. It assumes the practitioner discipline this book teaches.
>
> See *Computational Skepticism for AI*, **Chapter 4 — The Frictional Method** and **Chapter 14 — The Limits of AI**.

---

## Exercises

### Warm-Up

**1. The question, applied — and the artifact, found.** *(Core question — recognition + portfolio match)*
Choose a piece of AI-assisted work you produced in the last two weeks — a draft, an analysis, a summary, anything you used a model to help produce. Answer the chapter's opening question about it: what specifically did the AI do, and what specifically did you do that it could not? Write your answer in the ninety-second form the chapter describes — separating contributions, naming the domain knowledge you brought, assigning accountability. Then: which artifact in your portfolio supports the answer? Name the file. If no artifact supports it, that is what your portfolio is missing.

**2. Literacy versus fluency.** *(Distinction — internalization)*
The chapter distinguishes literacy (vocabulary in your head) from fluency (capacity in your hands). Using the cooking-with-heat analogy as a model, construct your own analogy from a domain you know well that captures the same distinction. Then use your analogy to explain what it would take to move from literacy to fluency in AI work — not in general, but specifically for someone at the stage you were at when you started this book.

**3. The three ingredients, located.** *(Deliberate practice — structure)*
For each of the three deliberate-practice ingredients — specific feedback, working at the edge, typed repetition — identify one specific practice from this book (not from this chapter; from an earlier chapter) that supplies that ingredient. For each, write two sentences: what the practice is and exactly how it supplies the ingredient.

---

### Application

**4. Design your 90-day plan.** *(90-day plan — live construction; portfolio artifact)*
Following the structure in the chapter exactly, write your personal 90-day plan and save it to `portfolio/13-90day-plan.md`. Choose two capacities. For each, define the daily rep (what it is, how long it takes, what artifact it produces), the weekly review (day, time, the one question you will ask), and the 90-day artifact (named specifically enough that you will know in ninety days whether you achieved it). The plan should be specific enough that a colleague could read it and tell you whether the artifact you named is too vague. Then schedule the weekly reviews on your calendar. The plan that is not on the calendar does not happen.

**5. Run the Final Audit.** *(Final Audit — portfolio artifact; paired with Ch 0)*
Open `portfolio/00-baseline-audit.md` from Chapter 0. Audit the same piece of past work again, today, in the same three-section form (Piece audited / Load-bearing claim — re-read / Verification trace — done). Compare the two audits side by side. Write one paragraph naming what changed — not "I am better now" but specifically what you can now see in the piece that you could not see when you wrote the Baseline. Save as `portfolio/13-final-audit.md`.

**6. The translation.** *(Framework translation — domain-specific)*
Choose your domain. Identify one place where the book's vocabulary does not fit your domain cleanly — where a capacity, a concept, or a framework step requires translation rather than direct application. Describe what the translation looks like: what the book's term means in your domain, what the domain-specific version of the judgment call is, and what a senior practitioner in your field would add that is not in the book. Add the translation as a note to your `CLAUDE.md` and `DESIGN.md`.

---

### Synthesis

**7. Draft the Cover Memo.** *(Cover Memo — portfolio artifact; the most important single page)*
Using the template at `portfolio/00-cover-memo-template.md`, draft your Cover Memo. One page. Six sections. No book jargon. Addressed to a reader who has never heard of *Botspeak*. Save as `portfolio/cover-memo.md` at the top level of your portfolio folder.

Hand the draft to one person who has not read this book and ask them: *if you were going to hire someone in my field, would this Memo make you want to read the portfolio?* If they say yes, the Memo is doing its job. If they say no, the issue is almost never the writing — it is that the portfolio does not yet have an argument the Memo can name. Go back to the case study. The Memo writes itself once the portfolio is coherent.

**8. The signal senior practitioners read.** *(Practice signals — reasoning)*
The chapter closes by claiming that senior practitioners can already distinguish fluent from literate users — by the questions they ask, how quickly they can articulate their judgment, whether they know their own workflow's failure modes without being prompted, and whether they have a portfolio they can hand over. For each of the four signals, explain what it reveals about the practitioner's underlying practice — what habit of attention each signal is downstream of, and how long it takes to develop.

---

### Challenge

**9. The Feynman test for the whole book.** *(Full synthesis — Feynman test)*
Apply the Feynman test to the book as a whole. Suppose a colleague who has not read it asks you: "What does it actually mean to be fluent at AI work, and how do you get there?" Write your answer in 250–300 words. Your answer should not recite chapter titles or framework names. It should make the core argument in your own words, using examples from your own domain, in the voice of someone who has absorbed the framework rather than summarized it.

**10. The ten-year question.** *(Epistemic standards — study design)*
The "What would change my mind" section is unusually specific: if fluent practitioners turn out to be no more effective than well-trained literate users over ten years, the book is wrong. Design the study that would test this claim. What would you measure, in whom, over what period, with what comparison group, and what outcome would constitute evidence that the fluency/literacy distinction is rhetorical rather than functional? Your design does not need to be feasible with current resources — it needs to be rigorous enough that if it came back with contrary evidence, a reasonable person would update.

---

### A note about AI

Fluency is the integration of the nine capacities under load. The chapter argues that fluency is a real and learnable state. The note examines what the model can and cannot do for someone working toward it.

Where the model genuinely helps: showing you specific examples of fluent practice in domains you do not yet work in. Pattern exposure accelerates pattern recognition. The model has read more transcripts of fluent practitioners than you will.

Where the model does damage: telling you that you are fluent. Fluency is demonstrated by work, not by self-report and not by the model's report. The model will produce a confident assessment of your fluency on request, and the assessment is worthless as evidence.

The rule: fluency is what your work shows, not what the model says about your work.

---

## LLM Exercise — Chapter 13: The Fluent Practitioner

**Project:** AI Fluency for [Your Role] — The Portfolio, Closed

**What you're building this chapter:** The three closing artifacts that complete your portfolio — the Final Audit, the 90-Day Plan, and the Cover Memo — produced in a single session against everything you have built across the book.

**Tool:** Claude Project (continue — your Role Dossier and all prior chapter artifacts are in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Closing my AI Fluency portfolio. My Role Dossier from Chapter 0, my
End-to-End Case Study from Chapter 8, and every chapter artifact in
between are in the Project context.

Botspeak Chapter 13 closes the book with three portfolio artifacts: the
Final Audit (paired with the Chapter 0 Baseline Audit), the 90-Day Plan,
and the Cover Memo (one page, addressed to a reader who has never heard
of Botspeak).

Do three things in this session.

TASK 1 — THE FINAL AUDIT.
Open the Baseline Audit I wrote at the end of Chapter 0 (paste it below
or reference the file). Help me audit the same piece of past work again,
in the same three-section structure (Piece audited / Load-bearing
claim — re-read / Verification trace — done). The Final Audit should
honestly compare to the Baseline — what do I now see in the piece that
I did not see then? What would the four-layer verification turn up
today? Save as `portfolio/13-final-audit.md`.

Then write one paragraph for the bottom of the Final Audit comparing
the two audits — what changed, named specifically. The pair is the
cleanest evidence of fluency the portfolio offers.

[PASTE BASELINE AUDIT HERE]

TASK 2 — THE 90-DAY PLAN.
Help me design my 90-Day Plan using the Botspeak structure: two
capacities, three commitments each (daily rep, weekly review, 90-day
artifact). The capacities should be the two most likely to compound for
my role at my current career stage. The daily rep should be a five-
minute move tied to my actual tasks. The 90-day artifact should be a
named, specific capability artifact a senior person in my role would
recognize as a developmental milestone.

Save as `portfolio/13-90day-plan.md`.

TASK 3 — THE COVER MEMO.
Help me draft my Cover Memo following the six-section template
(who I am / why this portfolio exists / what it contains / what is
not in it / the before-and-after / how to read it in twenty minutes).
One page. No Botspeak vocabulary. The Memo points at the artifacts
I have built; it does not boast.

Then push back. Read the Memo as if I had not read this book. Is it
legible? Is there book jargon I did not notice? Does it name the
artifacts clearly enough that a future reader could find them? Mark
the places where the Memo requires the reader to take my word for
something rather than pointing them at evidence.

Save as `portfolio/cover-memo.md` at the top level of my portfolio
folder.
```

---

**What this produces:** The three closing artifacts of your portfolio — Final Audit, 90-Day Plan, Cover Memo — drafted in one session and saved to your portfolio folder. The portfolio is now complete: seventeen artifacts, five sections, one case study at the center, one pair of audits to bracket the change, one Cover Memo to lead unfamiliar readers in.

**How to adapt this prompt:**

- *For your own project:* The Final Audit and the Cover Memo are the two most important artifacts in the whole portfolio. The 90-Day Plan is what makes it durable. Take this session seriously — it is the bookend to the entire book.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful for final folder organization. Ask Claude Code to set up the `portfolio/` directory structure cleanly and generate an index file.
- *For Cowork:* Recommended for assembling and reviewing the portfolio as a whole. Cowork can walk the folder, identify gaps, and help you draft the index.

**Connection to previous chapters:** Every chapter has produced one or more portfolio artifacts. This chapter closes the set. The Final Audit pairs with Chapter 0. The Cover Memo references the End-to-End Case Study from Chapter 8 as the centerpiece. The 90-Day Plan is what keeps the portfolio alive after the book ends.

**Preview of next chapter:** There is no next chapter. The next thing is to hand someone your portfolio and watch what they do with it. The first feedback you get is data for the portfolio's next revision — which you will do in three months, and again three months after that, for as long as your career remains the throughline of your practice.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Yuen Ren Chao** spent a lifetime studying what makes a speaker actually fluent — usage patterns, switching moves, the gap between rule and practice — decades before anyone called any of it "AI fluency." Here's a prompt to find out more — and then make it better.

![Yuen Ren Chao, c. 1950s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/yuen-ren-chao.jpg)
*Yuen Ren Chao, c. 1950s. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Yuen Ren Chao, and how does his study of linguistic fluency
connect to the idea of a fluent AI practitioner who runs the Loop
without having to consult the templates? Keep it to three paragraphs.
End with the single most surprising thing about his career or ideas.
```

→ Search **"Yuen Ren Chao"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain linguistic competence versus performance, in plain language
- Ask it to compare Chao's account of fluency to the 90-day plan in this chapter
- Add a constraint: "Answer as if you're writing the Cover Memo for a portfolio that travels with the practitioner across roles"

What changes? What gets better? What gets worse?

---

## References

1. Ericsson, K. A., Krampe, R. T., & Tesch-Römer, C. (1993). "The Role of Deliberate Practice in the Acquisition of Expert Performance." *Psychological Review*, 100(3), 363–406.
2. "Yuen Ren Chao" (Zhao Yuanren). *Encyclopaedia Britannica*. https://www.britannica.com/biography/Zhao-Yuanren
