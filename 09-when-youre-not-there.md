# Chapter 9 — When You're Not There
*The Loop Without You in the Moment.*

Here is a question worth sitting with before we go any further.

When you use an AI tool in the ordinary way — you type a prompt, you read the output, you decide whether to keep it or revise it — there is a human in the loop at every step. You are that human. The human is there not because anyone designed the system that way; the human is there because the system is just a chat window and you are sitting in front of it. The quality control is structural. It costs you nothing to achieve, because the act of reading the output before doing anything with it is the quality control.

Now suppose you automate something. Suppose you set up a process where the model runs on a schedule — every Monday morning, say, pulling last week's news, generating a summary, posting it to a Slack channel before anyone arrives. The process runs. The model generates output. The output goes somewhere and acts in the world. And you are not there.

The question is: where did the quality control go?

This is not rhetorical. The quality control did not disappear. It has to exist somewhere, in some form, or the automation is a reliability time-bomb waiting for its trigger. The work of this chapter is to show you exactly where the quality control has to go, and why designing it in deliberately is the difference between an automation that serves you and one that eventually produces the call from your editor asking how something like this happened.

---

Let me make this concrete with the kind of failure that actually occurs.

Priya, nineteen months past Chapter 0, has been on the hook for the publication's Monday-morning automated market-intel summary for seven weeks. The automation was built by a predecessor at the publication; she inherited it when her oversight role expanded. Every Monday morning the system pulls the past week's articles from a curated set of trade publications, hands them to a language model with a structured prompt, and posts a one-page market-intel summary to the Climate-and-Energy editorial Slack channel before the team arrives. For seven Mondays the automation has run cleanly. The desk reads the summary. Editors cite it in meetings. Priya, as the new owner, has been checking it some weeks and not others; the runs she has checked have looked fine.

In week seven, one of the source articles turns out to be wrong. A trade publication ran a story Thursday about a major utility's filing for a new transmission corridor; on Friday afternoon, the publication issued a retraction — the filing had been mischaracterized by their source. The retraction did not flow back into the automation's source cache. The model, working only from the original article as the automation had ingested it Thursday night, summarized the filing as current fact. The summary posted Monday morning. A senior editor on the Climate desk, working on the Monday afternoon commissioning meeting, pitched the desk on a reaction piece to the (retracted) filing. A reporter was assigned. The reporter started drafting Tuesday morning. By Wednesday afternoon — when another editor, reading the trade publication's most recent issue, caught the retraction — the reaction piece was halfway done. It was killed. The reporter lost two days of work. The publication came very close to publishing analysis of a story that was not true.

Notice the shape of this failure. The model did not hallucinate. It did not fabricate. It faithfully summarized a real article from a real publication. The article was simply no longer true by the time the model read it, and the model had no way to know that, and the spec — which Priya had inherited but not rewritten — had not anticipated the possibility. This is not a model failure. It is a design failure — specifically, the failure you get when you remove the human from the loop and do not replace the human with anything.

![Figure 9.1 — A seven-week timeline of the inherited automation. Weeks 1–6 marked "clean runs / trust accumulates." Week 7 marked with the retraction event and its downstream consequences.](images/09-when-youre-not-there-fig-01.jpg)

In ordinary augmentation work, this error never happens. Priya — or any editor — would have read the source article herself, or at minimum read the model's summary before forwarding any claim from it into a commissioning conversation, and would likely have checked the trade publication's current state before agreeing to commission a reaction piece. The error is impossible when a human is actively in the loop. Given enough recurrences, it is nearly inevitable when the human has been systematically removed.

---

Every chapter up to this one has described a loop: you specify the task, you delegate some portion to the model, you have a conversation that refines the output, you apply the verification layers from Chapter 6, and you maintain the practice over time. That loop runs with you at the keyboard. You conduct it in real time.

When you automate something, the loop does not disappear. It runs. But you do not. Every step still has to happen — specification, delegation, conversation, discernment, maintenance — but some steps that were reflexive in person become impossible without explicit design. The automation changes where the weight falls.


| Loop step | In augmentation | In automation |
|---|---|---|
| **Specification** | Covers the specific inputs you have in front of you; you're in the context and know what you're working with | Must cover a *class* of future inputs you haven't seen yet, in conditions that will change — silence in the spec is where failures live |
| **Delegation** | A real-time decision you can walk back if the output looks wrong | A design-time commitment made before any specific inputs arrive; much harder to reverse once the system is running |
| **Conversation** | Iterative — you push back, add context, run adversarial moves in the moment | Frozen at whatever prompt you wrote at setup; there is no one to push back on week seven's output |
| **Discernment** | Applied in real time to the specific output before it leaves your desk | Cannot happen in real time at volume; must shift to sampling, adversarial test cases, and periodic audits — with gaps between each |
| **Maintenance** | A good practice that catches drift and names accountability over time | The only mechanism by which you learn the system is failing; without explicit design, it does not happen |


**Specification** becomes harder, not easier. When you write a one-off task, your spec covers one set of inputs you have in front of you. You know the context because you are in it. When you specify an automation, you are specifying a class of tasks the system will run against inputs you have not yet seen, in conditions that will change over time. The inherited spec was correct for the normal case — articles from the curated list that were currently accurate. It was silent on what to do when an article had been retracted. A good spec for automation has to anticipate the ways the inputs will deviate from the design case, and has to specify what the system should do when they deviate. The silence in the spec is where the failures live.

**Delegation** shifts from a real-time decision to a design-time commitment. In ordinary work, you decide in the moment which parts to delegate, and you can walk that decision back if the output looks wrong. In automation, you have already delegated, in advance, to a system that will run the same delegation every recurrence. The commitment is much harder to walk back, because the system runs without you. The question of what to delegate has to be answered more carefully, at design time, before any of the specific inputs have arrived.

**Conversation** gets frozen. When you are at the keyboard, the conversation with the model is iterative — you push back, you add context, you run the adversarial moves from Chapter 5. In automation, the conversation is whatever prompt you wrote at setup time, run exactly that way every recurrence. There is no one to push back on week seven's output. Whatever corrective moves you want the system to make, you have to bake them in as standing instructions. The model does not have a peer reviewer. You are not there to be one.

**Discernment** is where Priya's inherited automation failed. In ordinary work, discernment is what you do before the output leaves your desk — the four verification layers applied to the specific thing you just built. In automation, discernment cannot happen in real time on every output, because the volume is too high and you are not there. Discernment has to shift to a different schedule: periodic sampling, adversarial test cases run at intervals, retrospective audits. These are approximations, with gaps. The gaps are where the failure happens in week seven.

**Maintenance** becomes the most important step, not a nice-to-have afterthought. In ordinary work, maintenance is the practice of keeping a process healthy over time — checking for drift, auditing outcomes, naming who is accountable. In automation, maintenance is the only mechanism by which you learn that the system is failing. Without explicit maintenance design, the automation runs until someone notices a bad output — which means the failure has already propagated some number of times before it was detected.

The reweighting is worth sitting with. Specification and maintenance become load-bearing in ways they are not in ordinary work. Discernment has to be redesigned around the absence of a real-time human. The conversation has to be preloaded with the corrections the model would need in advance. None of this is obvious when you set the automation up — or when you inherit one and start running it — because the setup feels like any other task: write a prompt, test it on a few examples, confirm it works. Or: read the spec, see that it has been running cleanly for some weeks, trust it. The testing does not reveal the reweighting. The reweighting only becomes visible when the failure arrives.

---

There is something about automation failures that is not obvious until you think it through carefully.

When a model produces a wrong output in ordinary augmentation work, the blast radius is bounded. One piece of work. You catch the error, you correct it, you ship the corrected version. The damage is proportional to the rework.

When a model produces a wrong output in an automation, the blast radius is proportional to *how long the failure goes undetected multiplied by the downstream consequences of each wrong output*. If the publication's automation produces a wrong output every Monday for six weeks before anyone notices — six weeks, not one — there are six wrong summaries in the desk's history, and six weeks of commissioning conversations made partly on their basis, and the task of auditing the damage is much harder than correcting a single piece of work.

The scaling can be worse than linear if wrong outputs compound. A wrong competitive read in week three shapes how an editor frames a story in week four. The wrong frame shapes a commissioning decision in week five. The decision structures a reporter's beat in week six. By week seven, the wrong output from week three has influenced a chain of things that cannot be easily unwound. This is not a worst case. It is a realistic case for any automation whose outputs feed into a running process.

*Figure 9.3*

The design implication is stark: you cannot rely on accidentally noticing that an automation is failing. In ordinary work, you notice because you are reading the output. In automation, you have deliberately arranged not to read the output in real time. Noticing has to be designed. It has to be a scheduled, explicit, accountable activity, built in at setup time — or at the moment you inherit responsibility — because if it is not built in, it does not happen. And the blast radius grows from the moment the first wrong output appears until the moment someone happens to look.

---

Before automating any task — or before accepting ownership of an existing automation — three tests. If the task fails one of them, do not automate it (or do not continue running it in current form) without explicit additional safeguards. If it passes all three, automation is appropriate; the next chapter will show how to specify and design the maintenance around it.

**Is the scope bounded?** Can you describe, in a single paragraph, exactly what the task does and what it does not do, in terms you would defend to your editor or manager? The inherited Monday automation's task was: summarize the past week's articles from this curated list of sources, in this format, at this time. That is bounded. The edges are clear. Compare to: automate market intelligence. That is not bounded. The surface area is too large for any spec to be tight, which means the model will be making scope decisions in real time that you have not authorized it to make. If the task is not bounded, you cannot specify it well, and if you cannot specify it well, you cannot design the discernment and maintenance around its failure modes.

**Are the inputs predictable?** Are the inputs the system will receive within a known range that your design cases actually represented? The Monday automation's inputs were mostly predictable — trade publication articles in a known format from a curated source list. Two failure modes were invisible during setup: retracted articles, and behind-paywall articles the model could not fully read. These were rare but possible. The model had never encountered them during testing. They were waiting in the tail of the input distribution.

The question to ask is not whether the typical input is predictable. The typical input is almost always predictable. The question is whether the *atypical* inputs — the ones that are rare but real — are represented in your design cases, and whether the spec tells the model what to do when it encounters them. If the spec is silent on the atypical inputs, the atypical inputs are where the failures will be.

**Is the blast radius acceptable if the system fails continuously for weeks?** This is the test most often skipped because failure feels hypothetical during setup. It does not feel hypothetical after the commissioning meeting where the reaction piece had to be killed. The right way to run this test is to assume the failure will happen — not as a possible outcome, but as a scheduled event — and to ask what the accumulated damage will be when you finally notice. If the damage is manageable and the outputs are low-stakes enough that continuous failure would be caught and corrected without lasting consequences, then automating is appropriate. If six weeks of wrong outputs would have already propagated into decisions that are hard to reverse, either do not automate, or build in explicit human checkpoints that catch each output before it acts in the world.

These three tests take five minutes. They prevent most of the cases where automation should not have been deployed in the first place — and they are the same tests you run on the day you inherit an automation someone else built.

---

The phrase Priya writes down, after the killed reaction piece, is: *designing the noticing is part of designing the system.* That sentence names the thing that distinguishes a well-designed automation from one that is waiting to fail. It applies whether you are building one or inheriting one — and on the day you inherit, redesigning the noticing is the first thing.

Designing the noticing means deciding, at setup time or at inheritance time, how you will learn that the system is producing wrong outputs before those outputs have been acting in the world for weeks. There are three forms this takes.

*Sampling* is the simplest: commit, at setup or inheritance time, to reading a fraction of the outputs in full on a scheduled basis. Not spot-checking whenever it occurs to you, but a regular, accountable practice — Priya now reads the full Monday summary every Tuesday morning and spot-checks one source per week against its current state. Sampling does not catch every failure. It catches failures that are persistent enough to appear in the sample, which is most of the failures that matter.

*Adversarial test cases* are inputs you construct to probe the failure modes you identified during the bounded-scope and predictable-inputs tests. In Priya's case, an adversarial test case might be a retracted article inserted into the source list — or a known-paywalled article whose metadata implies one claim and whose accessible text contains a different one — to see whether the model flags it or silently summarizes it. You run these test cases periodically, not just at setup, because the model's behavior can shift when the inputs shift. Adversarial testing is how you find the failure mode before it finds you.

*Outcome auditing* is periodic review of what the automation produced against what actually turned out to be true. Once a quarter, Priya reviews the past quarter's market-intel summaries against what actually happened in the segment. The audit catches systematic bias or systematic omission that sampling might miss because each individual output looked plausible. Outcome auditing is the slowest of the three forms but the one that catches the failures that are structurally correct and substantively wrong — the ones that look fine on the day and turn out to have been quietly misleading.

![Figure 9.4 — A three-panel reference card for the noticing forms](images/09-when-youre-not-there-fig-04.jpg)

Building these three practices in at design time — or at inheritance time, which is when most readers of this chapter will be running them — is not optional infrastructure. They are the quality control that replaces the human who is no longer there.

---

The two things this chapter has established are the conditions for appropriate automation and the shape of the noticing design. Chapter 10 takes both into depth: what anticipatory specification looks like when done carefully — the kind of spec that prepares the system for inputs it has not yet seen — and how to build the discernment and maintenance practices into the automation's design from the first day. By the end of that chapter you will be able to specify a small automation with the failure modes addressed in writing and the noticing built in.

---

### Translate before you move on — produce the Automation Inheritance Audit

Priya's case was inheriting a publication automation that ran cleanly for six weeks and surfaced its inherited blind spot in week seven. In your field, what is the equivalent? Most readers will not be building new automations from scratch. Most readers will be inheriting them — from a predecessor, from a vendor, from a team that set the system up and moved on. The discipline this chapter teaches is mostly the discipline of running the appropriateness tests on something already running.

For a clinician: a clinical-decision-support tool the EHR vendor enabled by default. For a software engineer: an automated test-generation or pull-request-summarization tool the team adopted some months ago. For a marketing manager: a campaign-personalization or send-time-optimization tool that came with the platform. For a teacher: an AI-assisted plagiarism-detection or essay-feedback tool the school enabled. For a research scientist: an automated literature-monitoring service the institution licensed. For a lawyer: an automated docket or compliance-monitoring tool the firm subscribes to. The specific tool varies. The shape — *a system running on a schedule that someone else specified, whose inputs and outputs you have at most partial visibility into* — is invariant.

**The Automation Inheritance Audit + Noticing Protocol — Chapter 9 Portfolio Artifact (Layer A template + Layer B audit, diagnostic + framework):**

Pick one automation you have inherited, run, or could plausibly be asked to oversee. Apply the appropriateness-test screen and design the noticing protocol you would run on it from this week forward.

Five sections:

1. *The automation named.* What it does, on what inputs, producing what outputs, on what schedule, for whom. Include what the spec (if any) says and what it is silent on.
2. *The three appropriateness tests.* Bounded scope — pass, partial, or fail with one-line justification. Predictable inputs — same, with a named tail-input failure mode. Acceptable blast radius if the automation fails continuously for six weeks — what is the realistic accumulated damage?
3. *Drift assessment.* Has model, context, or use case drift happened to this automation that you can detect from where you sit? If you cannot tell, name what you would need access to.
4. *The noticing protocol from this week forward.* Sampling (cadence, what you read, owner). Adversarial test cases (cadence, what inputs you construct, what the model should do with each). Outcome auditing (cadence, metric, reviewer who is not the owner).
5. *The deployment verdict.* Continue running as-is, continue running with stated modifications, or recommend pausing pending redesign. Defend the verdict in one paragraph.

For self-study readers without an automation in their direct work, the substitute is to pick a public AI automation in your field and audit it as if you had been asked to inherit it. The audit is structurally similar; only the access to operational data is weaker.

Save as `portfolio/09-automation-audit.md`. Three to four pages. The audit is one of the three diagnostic artifacts in your finished portfolio — alongside the Practitioner Profile (Chs 2 + 4) and the paired Baseline / Final Audit (Chs 0 and 13).

**Update your DESIGN.md.** Add a section on automation-noticing criteria your domain expects: what sampling cadence is reasonable in your field, what adversarial test cases your field has documented failure modes for, what outcome metrics your domain holds automations accountable to. This section will pair with the Ch 10 specification work for the automations you go on to spec.

**Update your CLAUDE.md** with the chapter's operational rule: *I do not own a running automation without sampling, adversarial test cases, and outcome auditing on my calendar. If I inherit one without those, the first week's work is putting them in place. Designing the noticing is part of designing the system — and redesigning the noticing is the first thing on the day of inheritance.*

---

*What would change my mind.* If automation infrastructure evolved to include retraction-detection, drift-detection, and outcome-monitoring as default turnkey capabilities — things you configure rather than design from scratch — the manual design work I describe here would shift. Some platforms are beginning to move in this direction. The discipline would remain the practitioner's even then; what changes is how much of the implementation is handed to you. As of early 2026, the implementation is mostly yours.

*Still puzzling.* I do not have a clean estimate of what fraction of currently deployed AI automations would fail an honest run of the three appropriateness tests. My sense, from watching organizations adopt these tools, is that it is high — most were built without the tests being run, because the tests feel like friction during the excitement of setup. I would like data on this. I do not have it.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Priya's retraction failure is, in the language of the advanced volume, a **hidden assumption that failed silently** — the system was built on the assumption that sources are durable, the assumption was never written down, and the model had no way to know when the assumption had broken. The deeper book argues that procedural data validation (distributions, missingness, correlation checks) is necessary but not sufficient — that the failures that actually break deployments live in structural assumptions invisible to standard checks. The cure is the **six-step epistemic-frame reconstruction** that explicitly enumerates what the data is claimed to represent, what it actually represents, and what it excludes — including a prediction-lock about the failure pattern you would expect if a particular assumption broke.
>
> The advanced book also distinguishes prediction systems (where the worst output is wrong information) from **consequence systems** (where the worst output is wrong action in the world). The Monday automation sits in between: it produces information, but the information drives consequential action by editors. This in-between zone is where most current automations sit — and where the loop reweighting in this chapter is most urgent.
>
> See *Computational Skepticism for AI*, **Chapter 5 — Data Validation** and **Chapter 9 — Validating Agentic AI**.

---

### A note about AI

Asynchronous operation is the capacity to set the model working without supervision. The loop's normal feedback structure does not apply.

Where the model genuinely helps: walking through what could go wrong while you are not watching, before you launch the run. The pre-mortem is the substitute for the absent feedback loop.

Where the model does damage: confident reports of completed work when the work was not actually completed correctly. Asynchronous failures are the worst kind because by the time you check, the failure has compounded.

The rule: design the unsupervised run so that the cost of a silent failure is bounded. The model will not flag silent failures itself.

---

## LLM Exercise — Chapter 9: When You're Not There

**Project:** AI Fluency for [Your Role] — Your Automation Inheritance Audit

**What you're building this chapter:** The **Automation Inheritance Audit + Noticing Protocol** — appropriateness tests applied to one inherited automation in your work, plus the sampling / adversarial-test / outcome-audit protocol you will run on it from this week forward. Plus an update to your `DESIGN.md` on automation-noticing criteria. Plus one new rule in your `CLAUDE.md`.

**Tool:** Claude Project (continue — your full portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, Verification Protocol, Diligence Framework, End-to-End Case
Study, PROJECT.md template, CLAUDE.md, and DESIGN.md are in the
Project context.

Botspeak Chapter 9 watches Priya — nineteen months past Chapter 0 —
inherit the publication's Monday-morning market-intel automation.
Week 7 of her oversight, the automation summarizes a retracted
article as live news. A reaction piece is commissioned, drafted for
two days, then killed when another editor catches the retraction.
The chapter introduces the three APPROPRIATENESS TESTS (bounded
scope, predictable inputs, low blast radius), the loop reweighting
for automation, and the three NOTICING FORMS (sampling, adversarial
test cases, outcome auditing).

For Chapter 9's portfolio artifact, do three things.

TASK 1 — RUN THE AUDIT ON ONE AUTOMATION.
Pick one automation I have inherited, run, or could plausibly be
asked to oversee in my work. If I have none in direct work, pick
a public AI automation in my field and audit it as if I had been
asked to inherit it.

Walk the audit in five sections:

1. THE AUTOMATION NAMED. What it does, on what inputs, producing
   what outputs, on what schedule, for whom. Include what the spec
   (if any) says and what it is silent on. Specific.

2. THE THREE APPROPRIATENESS TESTS.
   - Bounded scope: pass / partial / fail, one-line justification
   - Predictable inputs: pass / partial / fail, with one named
     tail-input failure mode the design cases probably missed
   - Acceptable blast radius if the automation fails continuously
     for 6 weeks: estimate the realistic accumulated damage

3. DRIFT ASSESSMENT. Has model, context, or use-case drift happened
   to this automation that I can detect? If I cannot tell, name
   what I would need access to in order to assess.

4. THE NOTICING PROTOCOL FROM THIS WEEK FORWARD.
   - Sampling: cadence, what I read, owner (probably me)
   - Adversarial test cases: cadence, what inputs I construct,
     what the model should do with each
   - Outcome auditing: cadence, metric, reviewer (someone other
     than me)

5. THE DEPLOYMENT VERDICT. Continue running as-is, continue with
   stated modifications, or recommend pausing pending redesign.
   Defend the verdict in one paragraph.

Save as `portfolio/09-automation-audit.md`. Three to four pages.

TASK 2 — UPDATE MY DESIGN.md.
Add a section on automation-noticing criteria my domain expects:

- What sampling cadence is reasonable in my field? (Daily,
  weekly, monthly — and why?)
- What adversarial test cases does my field have documented
  failure modes for? (For journalism: retracted articles,
  paywalled articles, source-impersonation, fabricated quotes.
  Your field has its own list.)
- What outcome metrics does my domain hold automations
  accountable to?

Append to `portfolio/DESIGN.md` as a new section.

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule: "I do not own a running
automation without sampling, adversarial test cases, and outcome
auditing on my calendar. If I inherit one without those, the first
week's work is putting them in place. Designing the noticing is
part of designing the system — and redesigning the noticing is
the first thing on the day of inheritance."

Push back if my appropriateness-test answer says "pass" on all three
without a single qualifier. The default for inherited automations is
"partial" on at least one test — the spec is rarely complete enough
to fully pass any of them. Press on which qualifier I should add.
```

---

**What this produces:** Your portfolio's eighth framework artifact, the third diagnostic in your portfolio, a meaningful update to your `DESIGN.md`, and another rule in your `CLAUDE.md`. The Automation Inheritance Audit is the artifact that documents your capacity to take responsibility for an AI system you did not build. ~3,000–4,000 words across the new material.

**How to adapt this prompt:**

- *For your own project:* Pick a real automation, not a hypothetical. The audit is structurally weaker on a hypothetical because you cannot assess drift, cannot inspect actual outputs, cannot test the model's behavior on real tail inputs.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful for scripting the adversarial test cases — a small set of input variations the test loop runs on a schedule.
- *For Cowork:* Recommended.

**Connection to previous chapters:** Chapter 7 built the Diligence Framework — the four-component protocol for governing recurring AI work. Chapter 9 specifies the application of that framework to a specific automation, with the appropriateness tests as a pre-condition. Together they cover the discipline of taking responsibility for AI systems that run.

**Preview of next chapter:** Chapter 10 — anticipatory specification for automation. The six common ambiguity types and the four automation failure modes, applied to one specific automation you would build or rebuild. The Automation Specification artifact is the most directly deployable single artifact in your portfolio.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Norbert Wiener** invented cybernetics in the late 1940s — the study of feedback, control, and what happens to a system when its corrective loops break down. His central warning, stated plainly in *The Human Use of Human Beings* (1950), was that automated systems amplify errors without correction when no feedback mechanism catches them in time. That is precisely what happened to the publication's Monday automation: the system ran correctly, the feedback loop was absent, and the error propagated until a Wednesday catch forced it into view. Here's a prompt to find out more — and then make it better.

![Norbert Wiener, c. 1950s. AI-generated portrait based on a public domain photograph.](images/norbert-wiener.jpg)
*Norbert Wiener, c. 1950s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Norbert Wiener, and how does his work on cybernetics and
feedback loops connect to the problem of designing AI automations
that run without a human in the loop — specifically to the idea that
blast radius scales with time-to-detection? Keep it to three
paragraphs. End with the single most surprising thing about his
career or ideas.
```

→ Search **"Norbert Wiener"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "cybernetics" in plain language, as if you've never encountered the concept
- Ask it to compare Wiener's feedback-loop thinking to the three noticing forms in this chapter
- Add a constraint: "Answer as if you're sketching a governance policy for an inherited weekly automation"

What changes? What gets better? What gets worse?

## References

1. "Norbert Wiener." Wikipedia. https://en.wikipedia.org/wiki/Norbert_Wiener — Confirms Wiener as the founder of cybernetics (foundational text *Cybernetics*, 1948) and the publication of *The Human Use of Human Beings* in 1950, together with his thesis that intelligent behavior arises from feedback mechanisms and control.
