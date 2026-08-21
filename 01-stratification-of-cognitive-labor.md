# The Stratification of Cognitive Labor

*Routine execution is contracting; judgment is growing — in every knowledge field.*

Open the U.S. Bureau of Labor Statistics *Occupational Outlook Handbook* and look up two jobs that sound, to almost anyone, like the same job.

The first is **Computer Programmers**. The BLS projects employment in this occupation to **decline 6% between 2024 and 2034** — a shrinking field, with most of its roughly 5,500 annual openings coming from people leaving, not from growth. The Handbook is unusually direct about why: automation, including AI, is absorbing "repetitive programming tasks," and the higher-skilled work is "shift[ing] to other workers, such as software developers" [High confidence: this is BLS's own projection and its own stated reasoning].

The second is **Software Developers, Quality Assurance Analysts, and Testers**. Same industry. Same tools. Adjacent desks. The BLS projects this occupation to **grow 15% over the same decade** — "much faster than average" — with around 129,200 openings a year, and it credits the growth to the very forces shrinking the programmers: AI, automation, connected devices, and security demand [High confidence].

Two occupations a layperson would treat as synonyms. One contracting six percent, the other growing fifteen. A **twenty-one-point divergence**, inside the same field, drawn not by a pundit but by the government's own occupational taxonomy. If you want the thesis of this book in a single data point, it is here: the question is not *is my field safe?* It is *which bundle of work am I doing?*

![Two bars from a zero baseline: Computer Programmers projected at −6 percent and Software Developers/QA at +15 percent, with the 21-point gap bracketed between them.](images/01-stratification-of-cognitive-labor-fig-01.png)

*Figure 1.1 — Inside one field, the BLS projects the execution bundle down 6% and the judgment bundle up 15% — a 21-point split.*

## Two bundles wearing one job title

What separates a "programmer" from a "developer" in the BLS framework is not the industry, the credential, or even most of the day-to-day. It is the *bundle of tasks* the title encodes. "Programmer," in the older sense the classification preserves, leans toward translating a specification into working code — execution. "Developer," "QA analyst," "architect" lean toward deciding what to build, why, how the pieces fit, what could break, and whether the result is correct and safe — judgment. The taxonomy is, in effect, two different bundles of work that happen to share a vocabulary.

This is the unit of analysis the rest of the book runs on. The thing AI is reshaping is not the *occupation*. It is the *task bundle*. Occupations are just bundles with names. When a tool gets good at one kind of task and not another, it does not retire a job title — it hollows out one part of the bundle and leaves the other standing. The programmer-versus-developer split is so clean because, by accident of history, the two halves of the software bundle were already filed under different names. In most fields they are not, which is exactly why the sort is harder to see — and why you have to do it yourself.

Two things draw the line between the contracting bundle and the growing one. The first is **routineness**: how repeatable and codifiable the task is, how well it can be specified in advance. Writing boilerplate, reconciling a standard report, drafting a first pass from a template — routine, and exposed. The second is **context-dependence**: how much the task requires reading a specific situation that no training corpus fully contains — this client, this judge, this patient, this organization at this moment. The more a task is routine and context-free, the more it migrates to the machine. The more it is non-routine and context-bound, the more it stays with you. We will give this its formal treatment in Chapter 3. For now, hold the shape: *execution contracts, judgment grows.*

## The same pattern, across the field

Software is the clearest case because it is the best measured — BLS gives us two occupation codes pulling apart by twenty-one points. The honest question is whether the same sort is happening elsewhere, or whether software is simply first. The evidence says the pattern is general, but the quality of the evidence drops sharply once you leave software. We mark that difference rather than smoothing over it.

The table below is the chapter's central exhibit. The software row is **BLS-quantified**. Every other row is **qualitatively documented** — the direction is well-attested across industry reporting, professional surveys, and field accounts, but it is *not* measured at BLS rigor. Read the difference between the rows as part of the data.

| Field | Contracting (execution) | Growing (judgment) | Evidence grade |
|---|---|---|---|
| **Software** | Routine/repetitive programming (programmers, −6% to 2034) | Architecture, QA, integration, design (developers/QA, +15%) | **BLS-quantified [High]** |
| **Finance** | Junior deck-building, reconciliation, first-pass analysis | Midlevel/senior interpretation, capital judgment | Qualitative [Medium] |
| **Law** | Document review, basic research, routine drafting | Strategy, negotiation, reading a court and a client | Qualitative [Medium] |
| **Medicine** | Routine transcription, image flagging, scheduling | Diagnostic synthesis, complex-care coordination | Qualitative [Medium] |
| **Education** | Quiz generation, first-draft materials, routine grading | Curriculum judgment, mentorship, reading a learner | Qualitative [Medium] |
| **Management** | Routine scheduling, status reports, dashboards | Strategic alignment, turnaround, accountability | Qualitative [Medium] |

The shape repeats. In each row, the contracting column is the codifiable, specifiable, repeatable work — the part you could write a clean prompt for. The growing column is the part that requires holding the situation in your head, weighing what is not in the data, and being answerable for the call. That repetition across fields is the reason this is a *pattern* and not a software anecdote. But the confidence repeats too: outside software, this is a well-supported direction, not a precise measurement. If anyone shows you a tidy cross-sector table with hard percentages in every cell, be suspicious — the data to fill it in at BLS quality does not yet exist.

## The pyramid becomes a diamond

Finance gives us the sharpest non-software view, because someone went and asked the people who set the headcount.

In 2025, the Oliver Wyman Forum and the New York Stock Exchange surveyed roughly **500 chief financial officers** of public companies — firms representing about 12% of global market capitalization — about how they expect AI to reshape their finance functions over the next few years. The results describe a structural change in the shape of the workforce, not just its size.

**Ninety-one percent** expect total finance headcount to stay flat (61%) or fall (30%) [High confidence for the survey figures]. So far that is just "we're not growing." But the composition tells the real story. **Sixty-four percent** expect to shift away from junior roles. Asked where the work is moving, they pointed toward midlevel (41%) and senior (23%) staff, with only **13%** expecting a shift toward junior roles. The traditional shape of a professional firm — a wide base of juniors, a narrower band of midlevels, a few seniors at the top, the *pyramid* — is, in the CFOs' intentions, becoming a **diamond**: a thin junior base, a fat middle, a senior tip.

![A wide-based pyramid of junior, midlevel, and senior tiers transforming via an arrow into a diamond with a thin junior base, fat midlevel, and senior tip.](images/01-stratification-of-cognitive-labor-fig-02.png)

*Figure 1.2 — The CFO-stated shift: the pyramid's wide junior base — the old training apparatus — collapses into a diamond's thin base.*

Two cautions, both load-bearing. First, this is **intent, not realized outcome** — a survey of expectations, not a measurement of what happened. At the time of the survey, around 70% of these CFOs were still piloting or planning, and only about 8% had deployed AI at scale. The intent leads the deployment, which leads the actual headcount. Treat the diamond as a stated plan with [Medium] confidence as evidence of *realized* change. Second, it is one sector, surveyed once, in 2025 — date-stamp it and expect it to move.

But notice what the diamond does to a person, not just a chart. The pyramid's wide base was not only cheap labor. It was the *training apparatus*. The juniors at the bottom were doing the work that turned them, over years, into the midlevels and seniors above them. Squeeze the base and you have not just cut costs — you have narrowed the channel through which the middle and top get refilled. We will spend the next chapter on exactly this, because it is where the diagnosis turns genuinely worrying. For now, register that the diamond is the same execution-contracts-judgment-grows story told in the shape of an org chart.

## The caveat that keeps you honest: no crash, yet

Here is where a careless version of this argument falls apart, and where the honest version earns its keep.

If routine cognitive work is contracting across every knowledge field, you would expect to see it in the aggregate numbers — rising unemployment in exposed occupations, falling hours, depressed earnings. **You do not.** The Yale Budget Lab, tracking the labor market through late 2025 and into early 2026, finds **no significant relationship** between an occupation's AI exposure and its change in employment or unemployment. The occupational mix is shifting slightly faster than its historical pace, but that trend *predates* widespread AI [High confidence for the aggregate-stability finding].

A second, independent source agrees. Humlum and Vestergaard, in *Large Language Models, Small Labor Market Effects*, used Danish administrative payroll registers — real records for about 25,000 employees across roughly 7,000 firms in eleven exposed occupations — and found **negligible near-term effects on earnings and hours**, even where adoption was widespread (around 41% of workers in a linked survey reported using ChatGPT for work tasks) [High confidence for the null effect on hours and earnings].

Two well-designed studies, different countries, different methods, same answer: no aggregate crash. A book trying to scare you would bury this. The point of stating it plainly is that it tells you what *kind* of change you are in. **The absence of a crash is not the absence of a sort.** The disruption is *compositional* — it is happening in the mix, not the total. The total can hold steady while the base hollows out and the top thickens, because the people leaving the bottom are matched, in the headline number, by the people staying in the middle. An iceberg does not warn you by changing the air temperature.

This is the discipline the book asks of you, made concrete. Doom cherry-picks the −6% and ignores the +15% and the flat unemployment rate. Hype waves the flat unemployment rate as proof that nothing is happening and ignores the diamond and the hollowing base. The honest read holds the whole table at once: aggregate stability *and* compositional stratification, both true, neither cancelling the other. You will not feel the sort in the unemployment statistics. You will feel it the first time your firm posts zero roles at your level — or, worse, the first time you discover you have been doing the contracting half of your own bundle without noticing.

## The mechanism: why a taxonomy can tell the future

It is worth pausing on *why* the BLS split is more than a curiosity. Occupational taxonomies are not predictions. They are descriptions — built by classification methodologists cataloguing what people in a job actually do. So why does this descriptive accident line up so precisely with where AI bites?

Because the taxonomy already encodes the distinction that matters. To file "programmer" separately from "developer," BLS had to notice that one bundle is more about translating specifications into working artifacts and the other is more about judgment, design, and verification. That distinction — execution versus judgment, routine versus non-routine, codifiable versus context-bound — is precisely the seam along which current AI is strong on one side and weak on the other. AI is, at its core, a system trained to predict plausible continuations from patterns in its data. That makes it powerful at the codifiable, repeatable, well-specified half of almost any bundle and weak at the half that requires reading a situation its training never fully captured. The taxonomy and the technology are sorting along the *same line*. The classification looks predictive only because it was, all along, a quiet map of which work is which. Where your field has not drawn that line into separate job titles, the line is still there — running invisibly through your own week.

## What it means for you

You cannot answer "is my job safe?" because it is the wrong question — it treats your occupation as the unit, and the occupation is just a bundle with a name. The right question, the one the BLS split forces, is: *which of my tasks are execution, and which are judgment?* Because those two halves of your own week are on different trajectories, and almost nobody's job title tells them apart.

This reframing is not comfort and it is not doom. It is precision. It moves you off the headline ("AI is coming for analysts / coders / lawyers"), which is too coarse to act on, and onto something you can actually work with: the composition of your own days. The contracting half of your bundle is the half a competent stranger could do from a clean specification. The growing half is the half that needs *you* — your context, your stakes, your judgment about what is not in the brief. If most of your week is the first half, the trajectory is not on your side, and you need to know that now, while the aggregate numbers are still calm. If most of it is the second, you are better positioned than your job title suggests — and the move is to protect and grow that half deliberately.

## The move: sort your week

Here is the first concrete action of the book, and it is deliberately small.

Take last week. Write down the tasks that actually filled it — not your job description, the real list. For each one, ask a single question: *could a competent person who is not me do this well from a clean, written specification, with no access to my context, my relationships, or my stakes?*

- If **yes** — it is **execution**. It belongs in the contracting column. This is the part AI fits, the part your firm can buy more cheaply over time, the part that does not, by itself, make your judgment worth paying for.
- If **no** — and you have to be honest about *why* not — it is **judgment**. It belongs in the growing column. Note specifically what makes it un-specifiable: the context only you hold, the accountability you carry, the call that no brief could make for you.

Now look at the ratio. Not to panic — to locate yourself. Most people are surprised, and not always pleasantly, by how much of their week lives in the contracting column. That surprise is the point. You cannot defend a bundle you have not sorted, and AI cannot sort it for you, because the boundary runs through your context and your stakes — which is to say, through exactly the part the machine cannot see. The sort is the first thing only you can supply.

Keep the list. You will use it again in Chapter 3, where we sharpen "execution versus judgment" into a finer instrument — the map of your own exposure.

## Bridge

The sort you just did is by *task*. But the BLS split and the CFO diamond both hinted at a second axis the task view alone can miss — one that is sharper, more measurable, and more alarming. The contraction is not falling evenly across the bundle. It is falling on a *level*. In the next chapter, we look at who is actually being squeezed, and find that it is not defined by your title at all. It is defined by your seniority — and the squeeze is breaking the ladder that makes experts in the first place.

## Sources

- U.S. Bureau of Labor Statistics. *Occupational Outlook Handbook* — *Computer Programmers* (projected −6%, 2024–2034) and *Software Developers, Quality Assurance Analysts, and Testers* (projected +15%, 2024–2034). OOH, 2025 update.
- Oliver Wyman Forum & New York Stock Exchange. CFO survey ("the diamond workforce"), ~500 CFOs, 2025 (reported via Oliver Wyman Forum and CFO Dive).
- Yale Budget Lab. *Evaluating the Impact of AI on the Labor Market.* Recurring CPS updates, 2025–2026.
- Humlum, A., & Vestergaard, E. *Large Language Models, Small Labor Market Effects.* NBER Working Paper w33777 / BFI WP 2025-56, 2025.
- Autor, D. H., Levy, F., & Murnane, R. J. *The Skill Content of Recent Technological Change.* Quarterly Journal of Economics 118(4), 2003. (Routine-task hypothesis; full treatment in Chapter 3.)
- Acemoglu, D., & Restrepo, P. *The Race between Man and Machine.* American Economic Review 108(6), 2018. (Displacement and reinstatement; full treatment in Chapter 3.)
