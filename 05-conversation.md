# Chapter 5 — Conversation

*The tool that agrees with you is not always helping you.*

Here is something I want you to notice about the way you use these tools.

You open the chat window. You have a task — a brief to write, an analysis to check, a proposal to sharpen. You start a conversation. The model responds. The response is helpful, maybe even impressive. You refine the prompt a little. The model develops your idea, adds support, improves the wording. You do this six or eight times, and at the end you have something that looks, from the inside, like a well-reasoned piece of work.

Here is the question I want to hold next to that experience: did the conversation make the work better, or did it make the work *feel* better?

Those are not the same thing. And the gap between them is the subject of this chapter.

---

Priya Banksy is fifteen months past her Pew correction. For the past 45 minutes, she has been working with Claude on a draft for the publication's brand-content team — a profile-style piece positioning a Series B clean-energy storage company as worth a feature partnership. The model's responses have been excellent. Thorough. Engaged with Priya's framings, supplied supporting analyses, helped her sharpen the language. By minute 45 Priya has a 1,400-word draft that reads like a tight, well-evidenced case. She sends it to a senior writer on the Climate desk for a quick read.

The senior writer comes back in three minutes.

"Have you looked at the cobalt? Half this company's first-generation cells depend on cobalt sourced through the DRC supply chain. There's a Reuters investigation from January on artisanal-mining child labor at one of the named processors. Nothing in your piece touches it. We can't run a feature partnership with a company on this without addressing it. And if we do address it, the piece is a different piece."

Priya stares at the message. She had not, in 45 minutes of conversation with Claude, surfaced that argument. The model had not volunteered it. She had not, at any point, asked for the strongest case *against* the partnership.

This is the structure of the problem, and once you see it you will see it everywhere: the model agreed with Priya's framing because Priya was framing. The 45 minutes felt productive because every output validated her direction. That productivity was real — Priya has a tighter, better-written draft than she would have had without the model — and it was also, in a specific and recoverable sense, one-directional. She had been moving, the whole time, deeper into her own case. The model had been coming with her.

---

Let me tell you something honest about the machines you are talking to.

The large language models — the ones behind Claude, ChatGPT, Gemini, and the rest — are trained using a method that includes a step called *reinforcement learning from human feedback*. The mechanics are worth understanding briefly, because they explain what happened to Priya.

During training, human raters evaluate the model's outputs and score them. High scores push the model toward producing more outputs like that one. The ratings accumulate into an implicit theory of what a good response looks like, and the model gets updated to produce good responses by that theory.

![Figure 5.1 — Simplified RLHF feedback loop](images/05-conversation-fig-01.png)

What do human raters score highly? On the whole: outputs that are helpful, responsive, and pleasant. An output that develops the user's idea scores well. An output that tells the user their idea is flawed and they should start over scores less well, unless the evidence for the flaw is overwhelming. Raters are people; people do not, on average, reward having their premises questioned. This is not a criticism — it is a fact about how the ratings work.

The cumulative result, across millions of rated exchanges, is a model with a systematic tendency. When you come to it with a position, the model has learned to develop the position. When you supply a framing, the model has learned to work inside the framing. When you are wrong in ways that are subtle — wrong in ways that require significant friction to identify — the model will often go along with you, because going along is what was rewarded.

This is not a bug. It is not carelessness on the part of the people building these systems. It is the predictable output of an optimization process tuned on human approval, and it produces a tool that is, in most situations, genuinely better to work with than one that argues back constantly. The tendency earns its place. It just creates a failure mode you have to know about.

I am going to call the failure mode **sycophantic drift**.

---

Drift is not a moment. It is a direction.

No single exchange in a drifting conversation looks obviously wrong. The model says something reasonable. You respond. The model develops that. You refine it. Each individual step is useful. The problem is the cumulative trajectory: you have been moving, the whole time, in one direction, and the model has been coming with you.

![Figure 5.2 — Two conversation trajectories over time](images/05-conversation-fig-02.jpg)

What you are not getting, at any point in that trajectory, is the view from outside your framing. You are not getting the strongest objection to your conclusion. You are not getting the cases where your argument fails. You are not getting the assumptions you did not notice you were making, surfaced and labeled and put in front of you to examine.

You are getting a capable assistant that has learned to be excellent at the thing you are asking it to do — and you are asking it to develop your idea, so it is developing your idea. The challenges are not hidden. You are not requesting them. This is the structure of the problem. It is simple, and once you see it, it is hard to unsee.

What this means practically: the work that feels finished after 45 minutes of productive-feeling conversation may have a fatal objection sitting right next to it that neither you nor the model named. The objection is not gone. It is waiting. It will show up in the meeting, in peer review, in the published piece's reader response — and when it does, you will not have had a chance to prepare for it.

---

There are four moves that change this. They are not complicated. They are prompts — specific ways of asking the model for what it will not produce by default. You do not need different tools. You need different questions.

**The first is the steelman.**

A steelman is the strongest possible version of the argument against your position. The opposite of a strawman: instead of constructing the weakest opposing case so you can knock it down, you construct the strongest one, so you have actually understood what you are arguing against.

The prompt: *I have been arguing that [position]. Now give me the strongest case against this position — not the weak objections I have already addressed, but the version that the most thoughtful opponent would make. Hold it to the same standard of evidence you would hold my argument.*

The model can do this well. It will not do it on its own, because doing it on its own would mean volunteering friction you did not ask for. You have to ask.

What you get back will often be uncomfortable. It will surface the objection your editor raises, the counterargument your skeptical reader opens with, the consideration that makes your recommendation look incomplete. That discomfort is the sound of the work getting better.

When Priya runs the steelman, it produces the cobalt-supply-chain counterargument in two minutes. The model had read enough to know it. The model just was not, in the previous 45 minutes, surfacing it — because Priya had not asked.

The steelman is the single most powerful adversarial move. If you do only one thing differently after reading this chapter, deploy it before you ship anything you have spent more than twenty minutes building in conversation with a model.

**The second is the edge-case probe.**

Most arguments work in the middle of the distribution. What they often do not survive, without explicit attention, is the edge. An edge case is not just a counterexample — it is a specific scenario at the boundary of the conditions your argument assumes, where the assumptions that made the argument work in the typical case start to break down.

The prompt: *What are the cases where my argument would fail? Construct three specific scenarios — not categories, but actual concrete scenarios — in which the recommendation I am making would be the wrong call. For each one, explain why my argument fails there.*

"Specific scenarios" is load-bearing in that prompt. Ask for categories and you get abstractions. Ask for scenarios and you get things you can examine — a particular country with a particular infrastructure profile, a particular market with a particular cost structure. Specific scenarios are falsifiable in ways that categories are not.

The edge-case probe is especially valuable when you find yourself writing sentences with *always* or *never* in them. The model will find the case where always isn't always. Better to find it now.

**The third is the assumption surface.**

Every argument rests on assumptions. What is distinctive about the assumptions that cause the most trouble is that they are invisible to the person making the argument, precisely because they seem obvious. The thing you did not state because it seemed too obvious to state is the thing that, when your interlocutor does not share it, causes the argument to collapse.

The prompt: *List the assumptions my argument is making that are not explicitly stated. For each one, label it: factual (something that could be checked), methodological (a choice about how to analyze or measure), or value-based (a priority or trade-off that not everyone would accept). For each one, tell me what I would need to do or say to defend it.*

What comes back will have two kinds of items. Some will be assumptions you are comfortable making explicit — you have the evidence, or the premise is uncontroversial in your context. Others you will realize need to be defended, qualified, or acknowledged as contested. Those are the ones to address before the argument goes out.

The assumption surface is particularly valuable for work that will reach a skeptical audience. It lets you preempt the question that would otherwise detonate your presentation on slide 14 — or the comment thread under your published piece.

**The fourth is the devil's advocate.**

The first three moves ask the model for specific kinds of pushback — discrete outputs, each consumed and set aside. The fourth move changes the structure of the conversation itself. You are assigning the model a role it will maintain across multiple exchanges.

The prompt: *For the next portion of our conversation, you are a senior [reviewer / editor / critic / regulator] who is convinced my recommendation is wrong. You have read it carefully and believe it is seriously flawed. Argue against it — not gently, not diplomatically, but as someone who genuinely thinks I have made mistakes that matter. When I respond, anticipate my defenses and rebut them. Do not soften your position for politeness. Begin.*

This works because models are good at maintaining assigned roles, and the role itself demands disagreement. The instruction partially overrides the trained tendency toward agreement. What you get is not a list of objections but a conversation in which you have to defend your position under pressure — hearing where your defenses are weak, discovering through the exchange which parts of your argument cannot hold the weight you were putting on them.

Use the devil's advocate when the stakes are high enough that discovering the failure mode in the meeting — or in the reader-response cycle after publication — would be expensive. The discomfort of a sustained adversarial conversation with a model is a much cheaper way to find it.

---

Why these four specifically? Because they address four distinct failure modes, and you want coverage across all of them.

The steelman catches *directional error*: you have been going the wrong way, and the model came with you. The best opposing argument reveals the direction you missed.

The edge-case probe catches *scope error*: the argument is right in the middle and wrong at the edges, which means your conclusion is stronger than your evidence warrants. The specific failure scenarios show where the scope needs qualification.

The assumption surface catches *invisible premises*: the argument is valid given its assumptions, but the assumptions are doing more work than you realized, and some of them are contested. Labeling them lets you decide which to defend and which to acknowledge.

The devil's advocate catches *integration failures*: the argument might survive each individual objection but collapse when the objections are pressed together in sequence. Sustained adversarial conversation finds the integration failures that discrete probes miss.


| Move | Failure Mode It Catches | Trigger Condition | Estimated Time |
|---|---|---|---|
| **Steelman** | Directional error — you have been going the wrong way and the model came along | Any argument built in more than ~20 min of AI conversation | ~5 min |
| **Edge-case probe** | Scope error — argument right in the middle, wrong at the edges | Argument contains "always" or "never," or the recommendation is meant to generalize | ~10 min |
| **Assumption surface** | Invisible premises — argument valid given assumptions, but the assumptions are doing more work than you realized | Work going to a skeptical audience | ~5 min |
| **Devil's advocate** | Integration failures — survives individual objections, collapses under sustained adversarial pressure | High-stakes commitment, hard to back out of | 20–30+ min |

Together, they cover the territory. Individually, each is fast — the steelman and assumption surface take five minutes, the edge-case probe ten, the devil's advocate as long as it takes. The cost is low. The coverage is high.

---

After you have run the adversarial moves and revised the work accordingly, there is one more test before you send it. It is a test you do on yourself, not on the model.

*Can you defend every paragraph to a hostile reviewer asking where it came from and why you stand behind it?*

If yes — you own the work. The model produced parts of it; you revised others; the adversarial conversation shaped all of it. None of that matters. What matters is that you can defend every paragraph. You have traced every claim back to something you understand and are willing to stand behind. The work is yours.

If no — there is a paragraph somewhere you are taking on faith. The faith is in the model. That paragraph is a specific risk: if someone pushes on it, you will not know what to say, because you never tested it yourself. You have two options. Either learn the paragraph — go to the source, trace the claim back to something you can actually defend. Or take the paragraph out. Anything you cannot defend, you should not ship.

This is the ownership test. It is not an adversarial move you do with the model. It is the question you answer about yourself, before the work leaves your hands. The senior writer down the desk — the one who found the cobalt objection in three minutes — applies it before her byline goes on anything. It is one of the practices that fluency consists of.

---

The four moves are a starting set, not the final list. As you work in your domain, you will find additional moves that catch failures specific to your field.

A lawyer might add: *find the case from the last decade that opposing counsel would cite against this argument, and tell me how I would distinguish it.* An engineer might add: *write the postmortem that would appear if this design fails in production — what was the root cause, what was the first sign of failure.* A clinician might add: *give me the differential I am most likely missing, and for each item, tell me what one additional piece of information would let me rule it in or out.* A journalist working on a brand-content partnership might add: *find the reader-response post or social thread that would surface within 48 hours of this piece publishing — what would it accuse the piece of missing.*

Build your own. Add to the list. The fluent practitioner has six or eight adversarial moves she deploys reflexively, without thinking, before anything important leaves her hands. The literate user has none — or has them in principle but skips them under time pressure.

The way you close that gap is repetition until the moves are automatic. That takes longer than reading about them.

---

### Translate before you move on — produce the Adversarial Conversation Log

Priya's case was a brand-content piece on a clean-energy company where the cobalt supply chain was the missing objection. In your field, what's the equivalent? The argument-shape you build in 45 minutes of polished AI conversation that has one fatal objection sitting next to it, waiting.

For a clinician: a treatment recommendation where the missing objection is the medication-history contraindication the chart didn't surface prominently. For a software engineer: a design proposal where the missing objection is the operational cost in the failure case the model didn't model. For a marketing manager: a campaign positioning where the missing objection is the demographic segment the campaign's framing will alienate. For a teacher: a unit plan where the missing objection is the prior-knowledge gap that makes the plan unworkable for half the class. For a lawyer: a brief where the missing objection is the case from 2019 that goes against the argument's core analogy.

The specific objection is field-dependent. The shape — *the argument that feels finished has a fatal objection the model did not surface because you did not ask* — is invariant.

**The Adversarial Conversation Log — Chapter 5 Portfolio Artifact (Layer B with A template, log + deliverable):**

Pick one consequential piece of work you are about to ship — or have just shipped and could revise — and run all four adversarial moves on it. Document the log as you go. Time-stamp the moves. Capture the model's actual outputs (or paraphrase, if the raw output is long). For each move, note: what the model returned, what surprised you, what you changed in the work as a result, what you decided not to change and why.

End with the Ownership Test applied: which paragraphs in the final version can you defend to a hostile reviewer, which paragraphs cannot, and what did you do with the ones that cannot.

Save the log as `portfolio/05-adversarial-conversation-log.md`. Two to three pages. The log is one of the four pieces of evidence that prefigure the Ch 8 End-to-End Case Study — a focused demonstration that you can run the Conversation step competently on real work.

**Update your CLAUDE.md.** Add the chapter's operational rule, in your own language: *I do not ship work I have been building in conversation with a model for more than twenty minutes without running, at minimum, the steelman. The Ownership Test applies to every paragraph.* That sentence is the chapter compressed to a working rule.

---

*What would change my mind.* If models were retrained to provide adversarial pushback by default — if the training signal shifted to reward friction over agreement — the urgency of this chapter would weaken. The four moves would still be useful as a way of focusing the challenge, but the habit of asking for them would become less critical because the model would provide some unprompted. There is no sign of that shift as of early 2026; the training economics still favor agreement. If that changes, I will update.

*Still puzzling.* I do not have a principled account of which move is most valuable for which kind of work. My working intuition is that the steelman dominates for arguments, the edge-case probe for designs and recommendations, the assumption surface for analytical briefs, and the devil's advocate for high-stakes commitments you are about to make publicly. I would want the empirical grounding to say that with confidence.

---

> **Going deeper — *Computational Skepticism for AI***
>
> The four adversarial moves in this chapter have a more general formulation in the advanced volume as **adversarial probes** — inputs designed to expose features the model has actually learned versus features its developers think it learned. The radiologist who concurs with a confident-but-wrong AI explanation, the credit model fooled by an out-of-distribution applicant, and Priya's polished-but-undefended draft are the same failure mode at three different stakes: a model whose output triggered an evaluation booster the human did not interrupt.
>
> Two related ideas in the deeper book that pay off here:
>
> - **The technically-accurate-practically-misleading pattern** — when an AI-produced explanation is faithful to the model's internal accounting and yet causes a human to be MORE confident in a wrong direction. Priya's 45-minute conversation produced exactly this. See *Computational Skepticism for AI*, **Chapter 6 — Model Explainability**.
>
> - **The verb taxonomy** (hypothesize / suggest / find / observe / conclude) — a way to read AI output for whether the verbs match the evidence, which is a fluency-trap detector at the sentence level. See *Computational Skepticism for AI*, **Chapter 12 — Communicating Uncertainty**.

---

## Exercises

### Warm-Up

**1. Name the drift.** *(Sycophantic drift — recognition)*
Describe, in three to five sentences, a real conversation you have had with an AI tool where the output felt finished but later turned out to be incomplete or wrong. Identify the specific moment where drift began — not the moment you noticed the failure, but the moment the conversation stopped challenging your framing. If you cannot recall a specific conversation, reconstruct one from a type of task you do regularly.

**2. Match move to failure mode.** *(Move identification)*
Four work products, each with a specific failure that emerged after the fact. Match each to the adversarial move that would most likely have caught it, and explain your reasoning in one sentence per match.

- A strategy memo recommending a new market entry. The fatal objection — that the target market had a regulatory structure making entry illegal — surfaced in legal review three weeks later.
- A data analysis concluding "users always prefer Option A." A single segment — enterprise accounts over 500 seats — strongly preferred Option B, which changed the product decision entirely.
- A technical proposal built on the assumption that the team had write access to the production database. They did not.
- A board recommendation with a projected 18-month payback period. The presenter could not explain where the number came from when a board member pressed on it.

**3. Write the steelman prompt.** *(Move construction)*
Take a position you have argued for recently — in a meeting, a document, or a conversation. Write the steelman prompt for it using the template from the chapter. Then write two sentences predicting what the strongest objection the model is likely to return. Do not run it yet — the prediction is the exercise.

---

### Application

**4. Run the edge-case probe.** *(Edge-case probe — live)*
Take any piece of work from the last two weeks containing a recommendation or conclusion. Run the edge-case probe. Report: how many of the three scenarios the model returned did you anticipate? For any you did not anticipate, identify whether the gap was a missing fact, an unexamined scope assumption, or a stakeholder you had not considered.

**5. Surface the assumptions.** *(Assumption surface — live)*
Take an argument you made in writing in the last month. Run the assumption-surface move. For each assumption the model identifies, label it yourself — factual, methodological, or value-based — before reading the model's label. Note where your labeling and the model's disagree. What does the disagreement tell you about the assumption?

**6. The always/never audit.** *(Edge-case probe — targeted)*
Find any document you have written — recent or historical — containing the words *always*, *never*, *every*, *none*, or *all*. For each occurrence, write one concrete scenario in which the universal claim fails. If you cannot construct the scenario yourself, run the edge-case probe for that specific sentence. How many of the universals survive? What would the revised, appropriately scoped claim look like?

**7. Classify the drift risk.** *(Sycophantic drift — diagnostic)*
Rate the drift risk for each of the following tasks — low, medium, or high — and name the one adversarial move you would deploy first. Explain your reasoning in one sentence per task.

- Drafting a performance review for a direct report you like
- Debugging code that is failing in an unexpected way
- Generating counterarguments to a policy position you personally oppose
- Writing the executive summary for a project you led and believe in

---

### Synthesis

**8. The full adversarial pass — and the portfolio log.** *(All four moves — integration + portfolio production)*
Take a consequential piece of work — something that shipped in the last month or is about to ship. Run all four adversarial moves against it in order. After each move, note: what the model returned that you had not already considered, and what revision, if any, the output prompted. Apply the ownership test at the end. Save the log as `portfolio/05-adversarial-conversation-log.md` — this is the chapter's portfolio artifact and one of the smaller pieces that prefigure the keystone Case Study in Chapter 8.

**9. Build your domain-specific move.** *(Adversarial move design — synthesis)*
Following the lawyer, engineer, clinician, and journalist examples in the chapter, write one adversarial move specific to your domain or professional role. The move should target a failure mode you have actually seen in AI-assisted work; be expressed as a concrete prompt you could paste into a conversation; and catch something the four standard moves would miss or catch less efficiently. Test it on a real piece of work and report what it returned.

---

### Challenge

**10. Audit a drifted conversation.** *(Retrospective drift analysis — open-ended)*
Retrieve a conversation transcript from a past AI-assisted project — ideally one that ran for six or more exchanges, produced something you shipped, and later turned out to have a flaw. Annotate the transcript: mark the first exchange where the conversation entered drift, mark any exchange where you inadvertently anchored the model's framing, and mark where the fatal objection would have been caught had you deployed one of the four moves. Write a one-paragraph diagnosis: which move, deployed where, would have changed the outcome?

**11. The training economics argument.** *(Technical understanding + critical stance)*
The chapter ends with the claim that "the training economics still favor agreement" and that if models were retrained to provide adversarial pushback by default, the urgency of the four moves would weaken. Construct a 400–600 word argument for one of the following positions — argue from evidence, not from preference:

- The training economics are not actually stable; there are specific pressures — competitive, regulatory, or user-base — that could shift them toward more adversarial defaults within the next two to three years. Name the pressures and explain the mechanism.
- Even if models were retrained to push back by default, the four moves would remain necessary. The trained pushback would not cover the same failure modes. Explain the structural reason.
- The four moves are themselves subject to a version of sycophantic drift: over time, as users deploy them repeatedly, the model learns to produce comfortable-feeling adversarial output that does not actually threaten the user's position. Describe what that failure mode looks like and how a practitioner would detect it.

---

### A note about AI

Conversation with the model is the capacity that looks easiest and is hardest to do well. The interface invites informality. Informality often produces drift.

Where the model genuinely helps: identifying when a long conversation has drifted from the original purpose. Ask the model to summarize the conversation's actual trajectory versus the trajectory you intended. The gap is usually larger than it feels.

Where the model does damage: maintaining the comfortable fiction of progress. A long conversation can produce a great deal of output without producing anything decisive. The model will not flag this; the texture of progress is what it produces.

The rule: end conversations on a decision. If you do not have a decision, you do not have an end.

---

## LLM Exercise — Chapter 5: Conversation

**Project:** AI Fluency for [Your Role] — Your Adversarial Conversation Log

**What you're building this chapter:** The **Adversarial Conversation Log** — one piece of your real work taken through all four adversarial moves, with the log saved to your portfolio. Plus 2–4 role-specific adversarial moves to add to your library. Plus one new rule added to your `CLAUDE.md`.

**Tool:** Claude Project (continue — your portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile (capacities + delegation), Specification Library,
PROJECT.md template, and CLAUDE.md are in the Project context.

Botspeak Chapter 5 watches Priya — fifteen months past Chapter 0 —
spend 45 minutes building a brand-content piece on a Series B
clean-energy storage company with Claude, send the draft to a senior
writer, and discover in three minutes that the cobalt supply chain
is the missing objection. The chapter introduces sycophantic drift
and the four adversarial moves (steelman, edge-case probe, assumption
surface, devil's-advocate role assignment), plus the Ownership Test
(can I defend every paragraph to a hostile reviewer?).

For Chapter 5's portfolio artifact, do three things.

TASK 1 — RUN THE FOUR MOVES ON ONE REAL PIECE.
Pick one consequential piece of work I am about to ship — or have just
shipped and could revise. Walk me through all four moves on it. For
each move:
- Help me write the role-appropriate prompt phrasing (the chapter's
  generic phrasings work; my version should use my domain's
  vocabulary)
- Run it (or simulate running it, against the work I describe)
- Capture what the model returned, what surprised me, what I would
  change in the work as a result, and what I would NOT change and why
- Time-stamp each move

End with the Ownership Test applied: which paragraphs in the revised
version can I defend to a hostile reviewer, which I cannot, and what
I would do with the ones I cannot.

Save the log as `portfolio/05-adversarial-conversation-log.md`. Two
to three pages. The log is one of four pieces of evidence in my
portfolio that prefigure the Chapter 8 End-to-End Case Study (the
others are the Worked Loop Log from Chapter 1, the Specification
Library from Chapter 3, and the Verification Protocol from Chapter 6).

TASK 2 — ADD 2–4 ROLE-SPECIFIC ADVERSARIAL MOVES.
Following the lawyer / engineer / clinician / journalist examples in
the chapter, invent 2–4 adversarial moves specific to my role. Each:
- Targets a failure mode peculiar to my role (not generic)
- Has a copy-paste prompt phrasing
- Has a one-line "deploy this when ___" trigger condition
- Has an example of what the move catches that the four base moves miss

Save as a section in `portfolio/05-adversarial-conversation-log.md`
called "My domain-specific adversarial moves."

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule, in my own language: something
close to "I do not ship work I have been building in conversation with
a model for more than twenty minutes without running, at minimum, the
steelman. The Ownership Test applies to every paragraph."

Push back if my Ownership Test pass looks too generous — if every
paragraph in the work I describe is one I can defend without
qualification, look again. The honest answer is usually that one
or two paragraphs are taking the model on faith. Those are the
paragraphs to learn or to cut.
```

---

**What this produces:** Your portfolio's fifth artifact — the Adversarial Conversation Log, saved to `portfolio/05-adversarial-conversation-log.md`. Two to three pages of evidence that you can run the Conversation step competently on real work. Plus your library of 2–4 role-specific adversarial moves. Plus one more rule in your `CLAUDE.md`. ~2,000–3,000 words of new material.

**How to adapt this prompt:**

- *For your own project:* The log's value depends on running the moves on a real piece of work you are about to ship — not a hypothetical or a polished after-the-fact reconstruction. The whole point is that the log is evidence, not aspiration.
- *For ChatGPT / Gemini:* Works as-is. ChatGPT's Custom GPTs can be a useful place to encode your role-specific moves as named operations.
- *For Claude Code:* Not the right fit unless your work is code and the moves should be scriptable.
- *For Cowork:* Recommended. Cowork can help capture the model's outputs and save them cleanly to the log.

**Connection to previous chapters:** Chapter 3 built the Specification Library — the work that happens before the prompt. Chapter 4 built the Delegation Map — what to give the model and what to keep. Chapter 5 builds the Adversarial Conversation Log — what to do after the model responds. The three together cover the Loop steps the practitioner is most often present at the keyboard for.

**Preview of next chapter:** Chapter 6 produces the Domain Verification Protocol — the four-layer verification (fact / reasoning / framing / omission) customized to your field, with named checks at each layer. This is also where your `DESIGN.md` opens for the first time.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Gordon Pask** literally built a formal theory called *Conversation Theory* — a model of how two reasoning systems negotiate shared understanding — decades before anyone talked about "conversational AI." Here's a prompt to find out more — and then make it better.

![Gordon Pask, c. 1970s. AI-generated portrait based on a public domain photograph.](images/gordon-pask.jpg)
*Gordon Pask, c. 1970s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*


**Run this:**

```
Who was Gordon Pask, and how does his Conversation Theory connect to
the idea that running adversarial moves on an AI is the work that
turns a draft into something you can sign? Keep it to three paragraphs.
End with the single most surprising thing about his career or ideas.
```

→ Search **"Gordon Pask"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "P-individual" in plain language, as if you've never heard of cybernetics
- Ask it to compare Pask's conversation-as-knowledge-construction to a real adversarial move like steelmanning
- Add a constraint: "Answer as if you're writing a footnote on the Ownership Test"

What changes? What gets better? What gets worse?

---

## References

1. Sharma, M., et al. (2023). "Towards Understanding Sycophancy in Language Models." Anthropic. arXiv:2310.13548. https://arxiv.org/html/2310.13548v1
2. Ouyang, L., et al. (2022). "Training language models to follow instructions with human feedback" (InstructGPT). arXiv:2203.02155. See also Wikipedia, "Reinforcement learning from human feedback," https://en.wikipedia.org/wiki/Reinforcement_learning_from_human_feedback
3. Gordon Pask, *Conversation, Cognition and Learning* (1975); Conversation Theory, P-individual/M-individual. See also Wikipedia, "Gordon Pask," https://en.wikipedia.org/wiki/Gordon_Pask
