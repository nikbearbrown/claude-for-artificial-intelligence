# Chapter 7 — Diligence
*A process does not hold still. The model changes. The world changes. The use case expands. Any of these, unmonitored, can turn a well-designed workflow into a broken one while every individual actor in the system behaves exactly as they did on day one.*

---

Here is a question worth sitting with before we get into the machinery.

When a process goes wrong — not spectacularly, not all at once, but slowly, over months, in ways nobody noticed — who is responsible?

The answer, in most organizations that have added AI to a recurring workflow, is: everyone and no one. Everyone had a role. No one owned the outcome. And the reason that answer keeps recurring is not bad luck, not malice, not negligence in any particular person's individual actions. It is a structural problem — a predictable consequence of how AI gets introduced into ongoing work — and it has a tractable fix that almost nobody has put in place.

That fix is what this chapter is about. But I want to start with the mechanism, because you cannot defend against what you cannot name.

---

Priya's publication spent February setting up an AI-assisted audience-segmentation tool. The tool helped Climate-desk editors decide which stories to commission based on what audience segments were reading what — surfacing the patterns in engagement that editors otherwise had to infer by feel. The setup team validated it against the previous quarter's Climate readership data. The recommendations looked indistinguishable from what the senior commissioning editor would have suggested, slightly faster and more consistent. The team approved it. The tool went into the desk's weekly commissioning rhythm.

Nine months later, in early November, Priya — now seventeen months past Chapter 0 and helping oversee the desk's AI deployments — is reviewing the tool's commissioning recommendations from the last quarter for an entirely unrelated reason. She is looking for examples for a conference talk on editorial AI. Reading the recommendations side by side, she notices something she had not noticed receiving them one week at a time. The tool has been systematically deprioritizing story candidates whose initial engagement signal comes from lower-income and rural readership clusters — flagging them as "low projected reach" — at a rate that is too consistent to be noise.

The audit she triggers takes another two weeks. The finding: the tool has been quietly under-weighting stories that disproportionately serve those audiences. The editorial team has explicit commitments around exactly that, written into the desk's editorial values document. The drift is not a single decision anyone made. It is a structural failure that compounded across months.

Priya wants to know who introduced the drift. The investigation finds that nobody did. Nobody changed the tool. Nobody changed the rubric. Nobody changed the workflow. What actually happened was all of the following, simultaneously, slowly:

In May, the segmentation vendor pushed an update. The update changed the way the model weighted engagement signals from short-form readers versus long-form readers. The change was small. It was not announced in any detail. The new weighting happened to be more sensitive to a signal that, in this publication's reader pool, correlated with income bracket and geographic concentration. Nobody chose this. Nobody noticed it. The model just got slightly different, and the difference accumulated. That is model drift.

In March, the publication had completed an acquisition that expanded its audience into two new metropolitan markets — and a viral piece had broadened the readership beyond the urban-coastal profile the tool had been validated against. The pool of readers hitting the segmentation tool in October looked structurally different from the pool in February. The rubric had been designed and validated against February's pool. Nobody re-validated it against October's. The assumptions baked into the specification no longer matched the world the specification was operating in. That is context drift.

In July, an editor on the Politics desk — who had not been part of the original Climate setup — started using the tool to inform her own commissioning decisions. The original tool had been designed for Climate-desk reader engagement patterns. The criteria for Politics commissioning are different — the engagement signals correlate with different reader behaviors. The tool was applying Climate-tuned criteria to Politics-desk story candidates, scoring them on a frame the tool was never built for. Nobody had re-spec'd the tool for the new desk. Nobody had told the July editor that the tool was not designed for this use case. That is use case drift.

Three drifts. Each one, on its own, might have been small enough to miss. Together, compounding over nine months, they broke the process in a way that harmed real coverage decisions and real readers. And not one of them required anyone to make a wrong decision.

*Figure 7.1*

This is the structural fact about recurring AI-assisted work that Chapters 1 through 6 did not fully prepare you for: the process does not hold still. The model changes. The world changes. The use case expands. Any of these, unmonitored, can turn a well-designed workflow into a broken one while every individual actor in the system behaves exactly as they did on day one.

---

Priya, faced with the finding, has a second problem on top of the first. Not only did the process fail — she cannot find the locus of the failure in any single person's decision. And when she tries to change the process going forward, she discovers she cannot find who owns it.

This is not an accident. There are three mechanisms that routinely obscure accountability when AI is in a recurring workflow, and understanding them is what makes it possible to design against them.

The first is process laundering. When an AI produces an output and a human approves it, accountability for the output distributes in a way that lets everyone tell a true and exculpatory story. The human approver says: the AI produced it; I just reviewed it. The AI vendor says: we provide a tool; the customer is responsible for appropriate use. The original setup team says: we set it up correctly in February; what happened after wasn't our responsibility. Every statement is accurate. Together, they produce a situation in which no one is accountable, even though every output had a human signature somewhere in its chain.

You will recognize process laundering in any post-incident conversation where every participant can give a complete, accurate account of their own role and still leave the cause of the problem unexplained. The fix is not to assign blame retroactively. The fix is to name, in advance, a single accountable human for each significant recurring AI-assisted process — the person whose job includes monitoring whether the process is still working, not just using it.

The second mechanism is tool diffusion. When a tool works, it spreads. The Politics-desk editor in July picked up the segmentation tool because it seemed useful and nobody told her not to. This is a rational thing for an individual to do. The aggregate effect, across a team or an organization, is that the original specification loses authority. New users are operating with partial, possibly garbled, possibly outdated understandings of what the tool was designed for. The original setup team may not know who is using the tool now. The use case has evolved without the specification evolving with it.

The fix is not to lock down tools or require formal approval for every extension. The fix is to maintain a living document for each significant AI-assisted process: who set it up, what it was designed for, what it was explicitly *not* designed for, who is currently using it, and who to talk to before extending it to a new use case. The document is cheap to maintain and expensive not to have.

The third mechanism is the verification gap. In most workflows, checking whether the process is still working is someone's responsibility in general and no one's in particular. The Climate-desk editors assumed the setup team was monitoring for problems. The setup team assumed the editors would say something if they noticed an issue. The result is that systematic verification doesn't happen — only reactive verification, after something goes wrong loudly enough to force attention, or after someone like Priya happens to look across a quarter of recommendations at once.

The verification gap closes only one way: scheduled checks, with dates and owners, on someone's calendar. Not an aspiration. Not a norm. A calendar entry that recurs and has a name attached to it.

*Figure 7.2*

---

There is a protocol that defeats all three mechanisms. I want to give it to you in the most concrete terms I can, because the value is not in the theory but in actually running it.

The first component is a documented specification. A document that answers: what does this process do, on what inputs, producing what outputs, for what use case, validated against what, approved by whom. The document is accessible to everyone who uses or manages the process. When a new colleague joins and starts using the tool, she reads the spec first. When the use case changes — when someone wants to extend the tool from Climate-desk commissioning to Politics-desk commissioning — the spec is updated formally, not silently, and the update triggers re-validation.

Without the documented specification, you do not know what the process was supposed to do, which means you have no baseline to check drift against. The spec is the foundation.

The second component is drift checks on a schedule. A set of known inputs — a test set, a benchmark, a sample of historical cases where you know what the right output is — that you re-run against the process on a fixed cadence. Once a month, once a quarter, calibrated to the stakes and the pace of change.

The drift check answers: has the process changed? Are outputs still meeting the criteria the workflow depends on? If outputs have changed, what changed — the model, the data, the use case? The answers get documented. If the drift is small and benign, you note it and continue. If the drift is significant, you investigate before the accumulation turns into an audit finding.

The third component is outcome audits. A periodic look at the downstream consequences of the process — not just the immediate outputs, but the outcomes those outputs produce — broken down by whatever attributes matter for fairness, accuracy, and quality.

For the segmentation tool, this meant: look at commissioning outcomes by reader-demographic cluster, by region, by income bracket, by story type. Are some groups of readers systematically having their stories deprioritized? Is the distribution shifting over time? The outcome audit is the check that model-drift-on-test-sets can miss: a model might produce the right outputs on your benchmark while producing different outputs on the actual distribution it operates on. The outcome audit catches that.

Priya's publication should have been running this audit monthly. They were not. When the audit eventually happened, it was forced by Priya happening to look across a quarter at once — which is the worst time for an audit, because by then the drift had compounded for nine months.

The fourth component is a named accountable human. One person whose job description includes maintaining this process — not just using it. The person whose name is in the spec as the process owner. The person who has the drift checks and outcome audits on their calendar. The person who is on the hook when the process fails, and who therefore has a personal incentive to make sure it does not.

The named owner does not have to be the most senior person in the room. She has to be someone with the time, the access, and the authority to actually do the work. She has to know she owns it. And the organizational structure has to treat ownership as a real accountability, not a nominal one.

Four components. None of them is technically sophisticated. Each of them is, in most organizations, missing for most AI-assisted processes.

| Component | The question it answers | What it prevents | Minimum cadence | Who owns it |
|---|---|---|---|---|
| **Documented specification** | What does this process do, on what inputs, producing what outputs, for what use case, validated against what, approved by whom? | Tool diffusion — secondary users extending the process to cases it was never designed for | Update on any change to inputs, outputs, use case, or model | Process owner; stored where every user can find it |
| **Drift checks on a schedule** | Has the process changed? Are outputs still meeting the criteria the workflow depends on? | Model drift and context drift accumulating undetected between cycles | Monthly for high-stakes; quarterly minimum | Named process owner; calendar entry, not an aspiration |
| **Outcome audits** | Are the downstream consequences of this process still acceptable — broken down by the attributes that matter for fairness, accuracy, and quality? | Silent failures that pass benchmark tests but harm real-world subpopulations | Quarterly; monthly in regulated domains or where the population shifts | A reviewer *other than* the process owner |
| **Named accountable human** | Who is on the hook if this process fails — and who therefore has a personal incentive to make sure it doesn't? | Process laundering and the verification gap — the structural conditions in which everyone can give an accurate account of their own role and the cause of failure still goes unexplained | Reviewed at any personnel change or scope expansion | One named person with a named backup and a named escalation path |

---

I want to make a stronger claim than "diligence helps you catch problems early," because while that is true, it undersells what the four components actually do.

Diligence is primarily about defensibility.

Here is what I mean. When a process fails — and processes fail; the question is when, not whether — the consequential question is not who to blame. The consequential question is: what do we change, and how quickly, and how do we address the harm that already happened? Getting good answers to those questions requires knowing what the process was supposed to do, how it deviated, when the deviation started, and why nobody caught it.

A process running the four diligence components can answer all of those questions. Here is the spec. Here is the scheduled check that should have caught the drift in June. Here is what we found when we ran it — and here is why we did not flag it, which is a solvable problem. Here is the named owner who will lead the remediation.

A process without the four components produces the situation Priya walked into: an audit that cannot identify the mechanism cleanly, a team that cannot distribute accountability without finger-pointing, and an editorial leadership that either reprimands someone for a structural problem or reprimands nobody and leaves the organization with the impression that nothing was wrong.

The four components make the process accountable in a way that protects the people in it. Diligence is not a safeguard against failure. It is a safeguard against organizational confusion when failure happens — and confusion, in my experience, causes more lasting damage than the failure itself.

---

Most of what I have described assumes you have some authority over the process — that you are setting it up, or managing it, or in a position to propose how it should be maintained.

You may not be. You may be one of many users of a process you did not design and do not officially own.

The four components are still available to you, partially. You can document your own use of the tool — what you use it for, what you have learned about its limits, what cases you have found where it performs unexpectedly. You can escalate that documentation to whoever does own the process. You can decline to extend a tool to use cases you know it was not designed for, and explain why.

What you cannot do is force accountability on a process that the organization has not structured to receive it. This is a real constraint. The chapter is not pretending otherwise. What I would say is that the political moment for proposing the four-component protocol is usually after a near-miss, not after everything is running smoothly. Small failures are good opportunities. Large failures are bad ones. Get the protocol in place during a small failure, if you can.

And make sure that your own name on a process is on a process you are diligently maintaining. The accountability cuts both ways: the four components protect you as well as holding you to account.

Priya, after the audit, ended up the named accountable human for the segmentation tool's redesign and ongoing oversight. The role was new at the publication and somewhat ad hoc. She negotiated for one half-day every two weeks formally allocated to the work, with a recurring check on her calendar. The publication did not have a budget category for it. Her editor approved the time anyway, because the audit had concentrated minds.

---

The three drifts I named — model, context, use case — are not exhaustive. Data drift, where the data the process ingests changes character over time, is related to context drift but distinct; a workflow processing reader feedback will behave differently in a quarter when sentiment is unusually polarized than in a normal quarter. Regulatory drift, where the legal environment shifts in ways that change what the process is permitted to do, is real and consequential in domains like hiring, lending, healthcare, and — increasingly — content recommendation systems.

The four-component protocol handles all of these, because the protocol is not tuned to any specific drift type. The documented specification records what the process was designed for. The drift check detects when outputs are changing. The outcome audit detects when consequences are changing. The named owner decides what to do about it. The mechanism does not care which drift triggered the check.

The next chapter assembles everything from the first half of the book — specification, delegation, conversation, discernment, verification, diligence — into a single narrated workflow. You will see how the pieces fit together in real time, and where the feedback loops are that the chapter sequence made look linear.

---

### Translate before you move on — produce the Diligence Framework Applied

Priya's case was a publication's audience-segmentation tool drifting across model, context, and use case over nine months until the demographic-deprioritization pattern surfaced. In your field, what is the equivalent? Pick one AI-assisted system you currently use, own, or work alongside — and walk it against the framework.

For a clinician: the AI-assisted triage tool in the ED. For a software engineer: the AI-assisted code review or test generation tool the team has been using. For a marketing manager: the audience-segmentation or campaign-targeting tool the firm relies on. For a teacher: the AI-assisted grading or plagiarism-detection tool. For a research scientist: the AI-assisted literature-search or analysis pipeline. For a lawyer: the AI-assisted discovery or contract-review tool. The specific tool varies. The pattern — *a system that is recurring, has multiple users, was validated for one context, may have drifted across model, context, or use case* — is invariant.

For self-study readers without an organizational AI system in their direct work, the substitute is to pick a public AI system in your field and analyze it as if you had inherited responsibility for it. The analysis is weaker as evidence but valid as practice.

**The Diligence Framework Applied — Chapter 7 Portfolio Artifact (Layer A template + Layer B application, framework):**

Build it. For one specific AI-assisted system in your work (or one you analyze from the outside), walk the four-component protocol:

1. *Documented specification.* If one exists, attach it (or excerpt it). If not, draft what it should say.
2. *Drift checks on a schedule.* Name the cadence, the procedure, the owner, the calendar item. If no checks are currently being run, draft what the schedule should be.
3. *Outcome audits.* Name the metric, the cuts, the threshold for escalation, the reviewer (must be someone other than the owner). Run one audit if you can.
4. *Named accountable human.* Name the person — or, if no one currently owns the process, name who should own it and what authority they would need.

Plus a fifth section: *Drift assessment.* Has model drift, context drift, or use case drift happened to this system, that you can detect from where you sit? Document what you find.

Save as `portfolio/07-diligence-framework.md`. Three to four pages. The framework is a Layer A template (the four components are the same structure for every reader) filled with Layer B application (your domain's specific system, your specific cadence, your specific outcome metric). A future reader sees how you apply governance to recurring AI work, not just how you generate single outputs.

**Update your DESIGN.md.** Add a section on the maintenance and ownership criteria your domain expects for any AI-assisted system that runs in your work. Specifically: what does ownership look like in your field, what does the outcome audit measure, and what triggers escalation to a senior reviewer. This section pairs with the verification standard from Ch 6 to form the quality side of `DESIGN.md`. The ongoing-stewardship side.

**Update your CLAUDE.md** with the chapter's operational rule: *No recurring AI-assisted process I am part of runs without a documented spec, a scheduled drift check, an outcome audit, and a named accountable human. If any of those four is missing, I am part of the verification gap.*

---

**What would change my mind.** If a high-quality empirical study showed that organizations running the four diligence components for a year produced no fewer audit findings than organizations that did not — that the components are decorative rather than functional — the chapter is wrong about the mechanism. The pattern I have observed runs the other direction. Organizations with the components catch problems earlier, including problems they had no prior reason to anticipate. But the observation is informal.

**Still puzzling.** I do not have a clean answer to who pays for diligence work in organizational terms. The work is real. It takes time. Most organizational budgets do not have a line item for it. The fluent practitioner often ends up doing the diligence work on top of her assigned role rather than as a recognized component of it — as Priya does after the segmentation-tool audit. I do not have a fix for that.

---

## Exercises

### Warm-up

**1. Name the drift.** For each scenario below, identify which drift type is operating (model drift, context drift, use case drift) and write one sentence explaining the mechanism. *(Tests: ability to distinguish drift types in context.)*

- A company uses an AI tool to flag potentially fraudulent transactions. Six months in, the tool's false-positive rate doubles. Investigation reveals the vendor silently updated the underlying model in the prior quarter.
- A legal team deploys an AI contract-review tool trained on US contracts. A new analyst begins running European vendor agreements through it without telling anyone.
- An AI customer-sentiment tool was validated against reviews from a normal business quarter. It is now running during a product recall, when customer sentiment is structurally angrier than the validation set.

**2. Process laundering, identified.** Write the three exculpatory statements — one each from the human approver, the AI vendor, and the original setup team — that together produce the accountability gap in the segmentation-tool case. Then write one sentence explaining why each statement is both true and insufficient on its own. *(Tests: retention of the process laundering mechanism and its structural character.)*

**3. The four components, applied.** You are setting up a recurring AI-assisted process: a weekly summary of customer support tickets, delivered every Monday to the product team. For each of the four diligence components, write two to three sentences describing concretely what it looks like for this specific process — not a restatement of the general definition, but the actual artifact, schedule, or role you would create. *(Tests: ability to instantiate abstract components into a specific workflow.)*

---

### Application

**4. Diagnose the segmentation case.** Priya's publication was running the four-component protocol incompletely — some components were present in weakened or implicit form, others were absent entirely. For each of the four components, describe whether it was present, absent, or degraded in the publication's workflow as described in the chapter. For each absent or degraded component, describe specifically what having it in place would have changed about the outcome. *(Tests: ability to apply the four-component framework as a diagnostic tool, not just a setup checklist.)*

**5. Write a living document.** You are the process owner for an AI tool that generates first-draft project status reports from a shared project-management database, used by eight project managers across two teams. Write the living document for this process. It should include: what the process does and does not do, who set it up and when, who is currently using it, what the process was validated against, what the explicit not-designed-for cases are, who to contact before extending it, and the name and calendar cadence of the scheduled drift check. Aim for one page. *(Tests: ability to produce the actual artifact, not just describe it.)*

**6. Blast radius by drift type.** The chapter claims that the blast radius of a specification mistake is proportional to how many times the specification runs before someone catches the problem. Apply this claim specifically to context drift. Describe a scenario in which context drift accumulates silently for six months in a high-stakes domain (healthcare, lending, hiring, content moderation, or safety — your choice), estimate the blast radius, and identify the specific diligence component that would have caught the drift earliest if it had been in place. *(Tests: integration of the blast-radius framing from Chapter 1 with the drift mechanics introduced here.)*

---

### Synthesis

**7. The defensibility argument.** The chapter's central claim is that diligence is primarily about defensibility, not early detection. Explain the difference between those two purposes. Then construct a scenario in which the four components catch no problems for a year — the process runs cleanly — but their presence still produces a meaningful organizational benefit. Your scenario should make the defensibility argument concrete rather than abstract. *(Tests: ability to hold the chapter's strongest claim and reason from it rather than from the more obvious early-detection framing.)*

**8. Accountability without authority.** The chapter acknowledges a real constraint: a practitioner who is one of many users of a process she did not design cannot force accountability on a process the organization has not structured to receive it. Describe a specific situation in which this constraint is in play. What can the practitioner actually do within the constraint? What should she escalate, to whom, and when? What should she refuse to do even if instructed? *(Tests: integration of the accountability argument with the organizational-reality section — reasoning about what diligence looks like when you do not own the process.)*

---

### Challenge

**9. The verification gap as a design problem.** The chapter says the verification gap closes only one way: scheduled checks with dates and owners on a calendar. Make the strongest possible argument against this claim — identify a scenario in which calendar-based verification would fail to catch a drift that a different detection mechanism would have caught earlier. Then explain what that scenario implies about how the four-component protocol should be designed, without abandoning the protocol's core logic. *(Tests: ability to stress-test the chapter's claims and reason about their limits.)*

**10. Regulatory drift and the four components.** The chapter names regulatory drift as a real risk in hiring, lending, healthcare, and content recommendation, but does not fully develop it. Choose one of those domains. Describe a plausible scenario in which a change in the legal environment turns a compliant AI-assisted process into a non-compliant one. Identify which of the four diligence components is best positioned to catch this drift, explain what it would need to look like in practice in that specific domain, and name what organizational role or function would need to be involved that might not currently be part of a typical AI process-ownership structure. *(Tests: ability to extend the framework into a domain-specific context where the standard instantiation of the components is insufficient.)*

---

### A note about AI

Diligence is the capacity to verify before shipping. The cost of skipping diligence is hidden in the moment and unrecoverable later.

Where the model genuinely helps: producing a checklist of verifications appropriate to the task and walking through each one with you. The checklist is useful even when generic, because it makes the verification explicit.

Where the model does damage: performing the verifications for you and reporting that the work passed. The model cannot run your code, query your database, or check your facts against the world. Its report of passing is not evidence of passing.

The rule: the model can structure the verification. The verification itself has to be done against the world, not against the model's claims about the world.

---

## LLM Exercise — Chapter 7: Diligence

**Project:** AI Fluency for [Your Role] — Your Diligence Framework

**What you're building this chapter:** The **Diligence Framework Applied** — the four-component protocol walked against one specific AI-assisted system in your work (or analyzed from the outside if you have none in your direct work). Plus an update to your `DESIGN.md` on maintenance and ownership criteria. Plus one new rule in your `CLAUDE.md`.

**Tool:** Claude Project (continue — your portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, Verification Protocol, PROJECT.md template, CLAUDE.md, and
DESIGN.md (opened in Chapter 6) are in the Project context.

Botspeak Chapter 7 watches Priya — seventeen months past Chapter 0 —
discover that the publication's audience-segmentation tool has been
quietly deprioritizing coverage of lower-income and rural readers for
nine months. Three drifts compounded: a May vendor model update
(model drift), a March acquisition that broadened the reader pool
(context drift), and a July Politics-desk editor who picked up the
tool (use case drift). Three mechanisms obscured accountability:
process laundering, tool diffusion, verification gap. The chapter
introduces the FOUR-COMPONENT DILIGENCE PROTOCOL: documented spec,
drift checks on a schedule, outcome audits, named accountable human.

For Chapter 7's portfolio artifact, do three things.

TASK 1 — APPLY THE FOUR-COMPONENT PROTOCOL TO ONE SYSTEM.
Pick one AI-assisted system I currently use, own, or work alongside.
If I don't have one in my direct work, pick a public AI system in my
field and analyze it as if I had inherited responsibility for it.

Walk the four components:

1. DOCUMENTED SPECIFICATION. What does this system do, on what inputs,
   producing what outputs, for what use case, validated against what,
   approved by whom? If a spec exists, attach or excerpt it. If not,
   draft what it should say.

2. DRIFT CHECKS ON A SCHEDULE. Name the cadence (weekly / monthly /
   quarterly). The procedure (specific re-run, comparison, sample
   review). The owner. The calendar item. If no checks are currently
   being run, draft what the schedule should be.

3. OUTCOME AUDITS. Name the metric (what to measure). The cuts (by
   what demographic / category / use case). The threshold (what
   triggers escalation). The reviewer (must be someone OTHER than
   the process owner). Run one audit if I can — even a back-of-the-
   envelope one — and report what it shows.

4. NAMED ACCOUNTABLE HUMAN. Name the person. If no one currently
   owns the process, name who should own it and what authority they
   would need. Include backup and escalation path.

5. DRIFT ASSESSMENT. Has model drift, context drift, or use case
   drift happened to this system, that I can detect from where I
   sit? Document what I find — be willing to say "I cannot tell from
   my vantage; here is what I would need to know."

Save as `portfolio/07-diligence-framework.md`.

TASK 2 — UPDATE MY DESIGN.md.
Add a section on maintenance and ownership criteria my domain
expects for any AI-assisted system in my work:

- What ownership looks like in my field (a specific role, a specific
  set of responsibilities, a specific reporting structure)
- What the outcome audit measures (specific to my domain — accuracy
  by subpopulation, fairness by demographic, calibration by use
  case)
- What triggers escalation to a senior reviewer

Append this as a new section in `portfolio/DESIGN.md`. DESIGN.md is
a living document — Chapter 11 (stakeholder model criteria for
agentic systems) and Chapter 12 (HITL protocol design) will add
more.

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule: "No recurring AI-assisted
process I am part of runs without a documented spec, a scheduled
drift check, an outcome audit, and a named accountable human. If
any of those four is missing, I am part of the verification gap."

Push back if my Drift Assessment section says "I cannot detect any
drift." That answer is almost certainly underspecified — either the
system is genuinely well-governed (rare), or I have not looked at
the right cuts (more common). Press on which cuts I have not
examined and which I would need access to.
```

---

**What this produces:** Your portfolio's seventh framework artifact and a meaningful update to your `DESIGN.md`. The Diligence Framework Applied is the artifact that documents your capacity to govern an AI-assisted system over time, not just produce single outputs. ~3,000–4,000 words across the new material.

**How to adapt this prompt:**

- *For your own project:* The framework's value depends on being applied to a real system you actually engage with. A fully hypothetical analysis is structurally weaker than an analysis of a system you have observed.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful only if part of the drift check can be scripted (a comparison script that re-runs known inputs).
- *For Cowork:* Recommended.

**Connection to previous chapters:** Chapter 6 built the Verification Protocol — how to check a single output before it ships. Chapter 7 builds the Diligence Framework — how to keep checking when outputs recur. The verification and the diligence cover the lifecycle of an AI-assisted process: from one piece of work to a process that runs.

**Preview of next chapter:** Chapter 8 — the keystone. The End-to-End Case Study. Every Layer A framework and every Layer B deliverable you have built across Chapters 0 through 7 comes together on a single sustained piece of your own work. The case study is the portfolio's gravitational center.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Walter Shewhart** invented statistical process control in the 1920s — the idea that you set a baseline, measure variation against it on a fixed cadence, and act when deviation crosses a threshold. That is the drift-check component of the four-component protocol, stated in manufacturing terms a century before anyone worried about model updates or use case creep. His deeper claim was that quality cannot be inspected in at the end; it has to be designed in through ongoing monitoring. Here's a prompt to find out more — and then make it better.

![Walter Shewhart, c. 1930s. AI-generated portrait based on a public domain photograph.](images/walter-shewhart.jpg)
*Walter Shewhart, c. 1930s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Walter Shewhart, and how does his work on statistical process
control connect to the idea that diligence in AI work means monitoring
for drift on a schedule rather than inspecting outputs after something
goes wrong? Keep it to three paragraphs. End with the single most
surprising thing about his career or ideas.
```

→ Search **"Walter Shewhart"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain the control chart in plain language, as if you've never taken a quality-engineering course
- Ask it to compare Shewhart's PDCA cycle to the four diligence components in this chapter
- Add a constraint: "Answer as if you're defending the drift-check budget to a skeptical manager"

What changes? What gets better? What gets worse?

## References

1. "Walter A. Shewhart." Wikipedia. https://en.wikipedia.org/wiki/Walter_A._Shewhart — Confirms Shewhart as the originator of statistical process control and the control chart (the May 16, 1924 memo), and the principle that quality is designed in through ongoing monitoring rather than inspected at the end.
