# Reading Your Own Exposure Map

*The safe tasks are not the ones in your job title.*

In 2023, a team of researchers ran one of the cleanest experiments anyone has run on AI and professional work. Dell'Acqua, Mollick, Lakhani, and colleagues took **758 consultants** at Boston Consulting Group — real consultants, doing the kind of analytical work they are paid for — and randomly assigned some of them access to GPT-4. The study was preregistered, meaning the researchers committed to what they were testing before they saw the results, and it has since been peer-reviewed and published in *Organization Science*. This is about as trustworthy as field evidence on this question gets [High confidence].

The headline looked like an unambiguous win. On a set of tasks that fell *inside* the AI's competence — idea generation, structured creative and analytical work — the consultants using GPT-4 completed **12.2% more tasks**, did them roughly **25.1% faster**, and produced **higher-quality** output. If the study had stopped there, it would be one more entry in the "AI makes knowledge workers more productive" file.

But the researchers had planted a second kind of task — one designed to fall *outside* the frontier of what the AI could reliably do, a problem where the tool's confident answer was, in a subtle way, wrong. On those tasks, the consultants with AI performed about **nineteen percentage points worse** than the consultants without it.

Read those two results together and you have the chapter. The same tool, used by the same people, on the same afternoon — a large boost on one kind of task and a large *penalty* on another. The boundary between the two was not marked. The consultants could not see it. And on the wrong side of it, AI did not slow them down or refuse — it confidently handed them fluent, plausible, wrong work, and a meaningful share of them accepted it. The researchers called the boundary a **jagged frontier**, and the failure mode the **trust trap**. It is the most important picture in this book, because it is the title made literal: the consultants felt faster and more capable, and on the outside-frontier tasks they were measurably worse.

![A jagged ink boundary cuts across a field of task dots; the inside-frontier region (AI augments, +12% tasks and 25% faster) is shaded, the outside-frontier region (AI confidently wrong, −19 points worse) is unshaded, and a ringed trust-trap dot sits just outside the boundary while appearing to be inside.](images/03-exposure-map-fig-01.png)

*Figure 3.1 — The frontier is jagged and unmarked: inside it AI augments (+12% tasks, 25% faster); just outside it AI hands you fluent, confident, wrong work (−19 points).*

## The frontier is jagged, and it runs through your job

The instinct, when you hear "AI is good at some tasks and bad at others," is to imagine a clean line — easy tasks on one side, hard tasks on the other, your safe work neatly quarantined from your exposed work. The BCG experiment demolishes that picture. The frontier is not clean. It is **jagged**: it juts unpredictably into work you would have thought was safe and retreats just as unpredictably from work you would have thought was exposed. Two tasks that feel equally difficult to you can sit on opposite sides of it.

This jaggedness is not a quirk of one study; it is a property of how the technology works, and it has a consequence that matters more than the productivity numbers. Because the frontier is jagged and unmarked, you cannot locate it by intuition. The tasks where AI helps and the tasks where it quietly hurts *feel the same from the inside* — both produce a fluent, confident, finished-looking artifact. The only signal that a task was outside the frontier is that the output is wrong, and noticing *that* requires the very judgment you were tempted to delegate. The trust trap is not a failure of lazy people. The BCG consultants were elite professionals. It is a structural feature of working with a tool that is fluent everywhere and correct only somewhere.

Which means the central skill of this chapter is not avoiding AI. It is building a *map* of where your own frontier runs — task by task, because nobody else can draw it for you.

## The frameworks: a hundred years of sorting tasks

The good news is that you are not the first person to try to sort tasks by how exposed they are to a machine. There is a deep literature here, and it converges on a single unit of analysis and a single counterintuitive result.

The founding text is **Autor, Levy, and Murnane (2003)**, "The Skill Content of Recent Technological Change." Their insight, now twenty years deep in citations, is that the right unit is not the job but the **task**, and that machines **substitute for routine tasks** — the repetitive, codifiable, rule-followable ones — while they **complement non-routine tasks** — problem-solving, judgment, and interaction [High confidence — foundational]. An occupation is just a bundle of tasks; a technology hollows out the routine tasks in the bundle and leaves the non-routine ones. This is the formal version of the execution-versus-judgment sort from Chapter 1. One honest caveat the authors could not have foreseen: they expected automation to hit *middle*-skill routine work and spare high-skill writing and analysis. Large language models broke that expectation — the frontier moved up the skill ladder into exactly the white-collar work ALM thought was safe.

**Acemoglu and Restrepo (2018)** supplied the engine that explains why some bundles shrink and others grow. In their model, automation has two opposing effects: a **displacement effect** (the machine takes over tasks, removing labor from them) and a **reinstatement effect** (new tasks get created that need labor). The frontier between them is not fixed; it evolves. Whether a field contracts or grows depends on which effect wins, which is why Chapter 1's table had both a contracting and a growing column [High confidence — as theory].

Then come the people who tried to *measure* exposure, and their results are the counterintuitive heart of this section:

- **Felten, Raj, and Seamans (2021)** built the **AI Occupational Exposure index** by mapping AI capabilities onto the abilities each occupation requires. When they extended it to generative AI in 2023, they found that the *most* exposed occupations were highly educated, highly paid, white-collar ones — the **inverse** of every prior automation wave, which had hit manual and middle-skill work [High confidence for the method; Medium as a predictor of actual employment].
- **Eloundou, Manning, Mishkin, and Rock (2023)**, in "GPTs are GPTs" (later in *Science*), mapped LLM capability onto thousands of work tasks and found that **about 80% of the U.S. workforce has at least 10% of their tasks exposed**, and roughly **19% have at least half their tasks exposed**. The effect spans all wage levels, and — again — *higher*-income jobs are *more* exposed [High confidence for the exposure figures].

Sit with the inversion. Every previous wave of automation came for routine physical and middle-skill work and left the credentialed knowledge worker alone. This one walked straight up to the knowledge worker's desk. If you have spent a career assuming that education and analytical work were a moat, the exposure indices say the moat is exactly where the water is rising.

## Exposure is not impact — and the gap is where you live

Here is the move that separates an honest exposure map from a panic. **Exposure is not the same as impact**, and confusing the two is the most common error in this whole conversation.

"Exposure" means a task *could* be done, in whole or part, by current AI. "Impact" means it *was* — that a real job changed, contracted, or vanished. The gap between them is large, and it is not noise. The authors of the exposure studies say so themselves: Eloundou's paper explicitly cautions that exposure does not equal impact, and the early predictions of mass white-collar displacement over-shot what actually happened. The OECD's Georgieff and Hyee (2022) found **no clear relationship** between an occupation's AI exposure and its employment growth. And recall Chapters 1 and 2: the aggregate numbers show no crash. Observed displacement has lagged predicted exposure substantially [Medium confidence for the exposure-impact gap].

Why the gap? Three reasons, and all three are where your defensible position lives. First, **organizational friction** — deploying AI into a real workflow is slow, messy, and half-finished, which is why those CFOs were mostly still piloting. Second, **complementarity** — high exposure often means the task gets *augmented* (you get faster) rather than *automated* (you get replaced); exposure measures what the tool can touch, not whether touching it removes the human. Third — and this is the jagged frontier again — much exposed work is *outside* the reliable frontier even though it is technically "exposed," so delegating it triggers the trust trap rather than a clean handoff.

So a high exposure score is not a verdict. It is a flag that says: *AI will touch this task — now decide whether that means it makes you faster or makes you unnecessary.* That decision is not in the index. It is in the specifics of your task and your context, which is precisely why you have to map it yourself.

## Rising tides, not crashing waves — but the tide is rising

If exposure is not impact, the natural next question is: *for how long?* Is the outside-frontier work safe forever, or just safe for now?

The most concrete answer in the current literature comes from MIT FutureTech's 2026 working paper, *Crashing Waves vs. Rising Tides*. The researchers had thousands of domain-expert workers evaluate more than 3,000 real work tasks — over 17,000 evaluations in total — and asked, for each, how well current AI could do it and how that was trending. Their metaphor is the title's: AI is not arriving as **crashing waves** (one occupation wiped out at a time) but as **rising tides** (broad, simultaneous, gradual gains across many tasks at once).

Their numbers: AI completed roughly three-to-four-hour human tasks at about **50% success in mid-2024**, rising to about **65% by late 2025**, and they **project 80–95% success on most text-related tasks by 2029**, at a minimally sufficient level of quality [Medium confidence — this is a *projection* from a *preliminary* working paper, not an observation; date-stamp it 2026 and re-check it annually].

I want to be precise about how to hold this, because it is the chapter's most perishable claim and the easiest to abuse in either direction. It does **not** say you are safe (the tide is rising, and rising broadly). It does **not** say it is over (this is a trend extrapolation, not a measurement, and trends bend). What it says is the operationally useful thing: the durable, outside-frontier capacities are **last to go, not never gone.** The frontier is moving in one direction, slowly and broadly, and your judgment-bearing work buys you time and altitude — not permanent immunity. Plan accordingly: the goal is not to find tasks the tide will never reach, but to stay on the high ground as long as possible while building the capacities that keep you valuable even as the water rises.

One sharpening of the threat, which the older indices underweight. The exposure indices (AIOE, GPT-exposure) were built to measure *narrow-tool* substitution — can a model do this one task? The newer worry is **agentic** systems: tool-using, multi-step, self-correcting AI that strings tasks into whole workflows. A task-by-task index will systematically *underestimate* what an agent that automates an entire pipeline can displace — and this is part of why entry-level hiring (Chapter 2) is contracting *ahead* of any single task being fully automated: firms are reorganizing the pipeline, not just swapping one task. *(This "agentic task exposure" framing is increasingly discussed but does not yet rest on a single canonical study — treat it as an emerging analytical lens, not a settled measure.)*

## The mechanism: why the map has to be personal

Step back and ask why no index can hand you your own answer. Why must you draw the map yourself?

Because the deciding variable is **context**, and context does not live in the data the indices are built from. Acemoglu's distinction between "easy-to-learn" and "hard-to-learn" tasks gets at it: some tasks are hard for AI not because they are computationally difficult but because the knowledge they require — *this* client's risk appetite, *this* court's posture, *this* organization's politics at *this* moment — was never written down anywhere a model could train on it. Michael Polanyi named this in 1966: *we know more than we can tell.* The tacit, situated, context-bound part of expert work resists codification not because it is fancy but because it is *local* — true here, now, for these stakes, and nowhere captured in a corpus.

This is why an exposure index can tell you that "legal drafting" is exposed but cannot tell you whether *your* drafting is exposed — because your drafting includes reading a specific judge and a specific client's appetite for risk, and that part is invisible to the index. It is why "writing analysis" scores as highly exposed and yet the analysis that integrates an ambiguous situation with real stakes stays outside the frontier. The index sees the *task category*. The frontier runs through the *task as you actually do it*, and where it runs depends on how much of your version is context-bound. That information exists in exactly one place: your own head. The map is personal because the frontier is personal.

## What it means for you

The exposure map reframes the safety question one final, sharper time. Chapter 1 asked: which of my tasks are execution and which are judgment? This chapter adds the jagged frontier and the trust trap, and the question becomes: *for each task, which side of my own frontier does it sit on — and when AI touches it, does it augment me or replace me?*

The dangerous tasks are not the ones you would guess. They are not the obviously hard ones (AI often won't touch those well, and you'll catch its failures). They are the ones that *look* inside the frontier but are subtly outside it — where AI produces fluent, confident, plausible, wrong work, and where the only thing standing between that output and a bad decision is your willingness to actually check it. Those are the trust-trap tasks, and they are exactly where productivity feels highest and safety is lowest. Your durable bundle — the high ground — is the context-bound, accountability-bearing, hard-to-learn work where the frontier has not reached and where, even when AI helps, the human with stakes is the one who has to make the call.

## The move: map your tasks against the frontier

Take the task list you made in Chapter 1 — the real tasks of a real week. Now run each one through a simple two-by-two, and be honest, because the value of the map is entirely in its honesty.

**Axis one — frontier:** Is this task *inside* my frontier (AI does it reliably and I can verify the result quickly) or *outside* it (AI produces confident output I cannot easily verify, or that depends on context AI doesn't have)?

**Axis two — relationship:** When AI touches this task, does it *augment* me (I stay in the loop, get faster, still make the call) or *substitute* for me (the task could run end-to-end without me)?

Four quadrants fall out, and each implies a different stance:

- **Inside + augment:** Use AI freely; this is your faster Tuesday. Low risk.
- **Inside + substitute:** This is your *exposed* work — the task that can run without you. Do not build your value here; the tide reaches it first.
- **Outside + augment:** Use AI, but as a *suspect* — this is trust-trap territory, where you must verify rather than accept. Your judgment is the product.
- **Outside + substitute:** Rare and precious — context-bound work that needs you *and* resists automation. This is your durable bundle. Protect and grow it.

![A two-by-two matrix with frontier (inside/outside) on the horizontal axis and relationship (augment/substitute) on the vertical: Inside+Augment is your faster Tuesday, Inside+Substitute is exposed work, Outside+Augment is the trust trap, and the highlighted Outside+Substitute cell is the durable high ground.](images/03-exposure-map-fig-02.png)

*Figure 3.2 — Sort every task on two axes; the highlighted Outside+Substitute cell — context-bound work that needs you and resists automation — is the high ground to defend.*

Mark which quadrant each task falls in. Then look at where your week actually lives. If most of it is "inside + substitute," your trajectory needs deliberate work, starting now. If you have a real cluster in "outside + substitute," you have high ground — name it precisely, because that is the thing you will defend and train for in the rest of the book. The map is not a one-time exercise; the frontier moves, so the map is a habit. But you can only build the habit once you have drawn it once, honestly, by hand — which no index will do for you, because the frontier runs through your context, and your context is the one thing the machine cannot see.

## Bridge

You now have a diagnosis (stratification), a sharper diagnosis (the seniority squeeze), and a personal map (your jagged frontier). The map points repeatedly to the same high ground: the outside-frontier, context-bound, judgment-bearing tasks. Part II asks the question the map raises — *why* does that work stay human, and how long can it? We begin with the capacity the trust trap most directly threatens: supervisory judgment, the skill of catching the fluent, confident, wrong answer. It turns out to be both the core of your defense and the thing that passive AI use most quietly erodes — the hardest problem in the book.

## Sources

- Dell'Acqua, F., McFowland III, E., Mollick, E. R., Lifshitz-Assaf, H., Kellogg, K., et al. *Navigating the Jagged Technological Frontier: Field Experimental Evidence of the Effects of AI on Knowledge Worker Productivity and Quality.* Harvard Business School Working Paper 24-013 / SSRN 4573321, 2023; published in *Organization Science*, 2025. (758 BCG consultants.)
- Autor, D. H., Levy, F., & Murnane, R. J. *The Skill Content of Recent Technological Change: An Empirical Exploration.* Quarterly Journal of Economics 118(4), 2003.
- Acemoglu, D., & Restrepo, P. *The Race between Man and Machine.* American Economic Review 108(6), 2018.
- Felten, E. W., Raj, M., & Seamans, R. *Occupational, Industry, and Geographic Exposure to Artificial Intelligence.* Strategic Management Journal 42(12), 2021; generative-AI extension, 2023.
- Eloundou, T., Manning, S., Mishkin, P., & Rock, D. *GPTs are GPTs: An Early Look at the Labor Market Impact Potential of Large Language Models.* arXiv:2303.10130, 2023; published in *Science*, 2024.
- Mertens, M., Thompson, N. C., et al. *Crashing Waves vs. Rising Tides: Preliminary Findings on AI Automation from Thousands of Worker Evaluations of Labor Market Tasks.* MIT FutureTech, arXiv:2604.01363, 2026.
- Georgieff, A., & Hyee, R. *Artificial Intelligence and Employment: New Cross-Country Evidence.* OECD, 2022.
- Polanyi, M. *The Tacit Dimension.* 1966.
