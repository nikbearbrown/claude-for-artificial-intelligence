# Chapter 6 — Problem Formulation (Part 1: Reframe Before You Engage)

In the spring of 1847, a young Hungarian physician at the Vienna General Hospital was looking at two numbers that should have been the same and were not.

The hospital ran two maternity clinics. The First Clinic, staffed by doctors and medical students, had a death rate from puerperal fever — childbed fever, a sepsis that killed new mothers within days of delivery — that averaged around ten percent and reached above eighteen percent in the worst months. The Second Clinic, staffed by midwives, ran under four percent — a fraction of that. Same hospital. Same city. Same disease. Women begged to be admitted to the midwives' clinic. Some, knowing the numbers, chose to give birth in the street rather than enter the First Clinic, and the streetborn mothers survived at better rates than those delivered by physicians.

Ignaz Semmelweis could have formulated this problem in the way that came most readily, the way the data themselves seemed to invite. The mortality differential could be treated as *noise* — the kind of statistical fluctuation that two wards will show — or as a property of the *patients*: perhaps the women admitted to the First Clinic were sicker, poorer, more susceptible. These framings were available, conventional, and required nothing of him. They were also, we now know, dead wrong, and they would have killed every mother the framing failed to save.

The formulation that saved lives was not the one the data handed him. It was a different question entirely: *what do the doctors do that the midwives do not?* And the answer, once he asked it, was waiting. The doctors performed autopsies. They went from the dissection of corpses to the examination of laboring women, often without washing. Semmelweis hypothesized that some "cadaverous particles" were being carried on physicians' hands from the dead to the living. In May 1847 he instituted handwashing with a solution of chlorinated lime — chosen because it removed the smell of the cadaver, which he took as a proxy for removing whatever the smell signified. The First Clinic's mortality fell from 18.3 percent in April 1847 to 2.2 percent that June, into line with the midwives'. [High]

Hold two cautions firmly, because the textbook version of this story is a lie of convenience. First, **Semmelweis did not have germ theory.** This was a generation before Pasteur and Lister. His causal account — "cadaverous particles" — was partial and, in its mechanism, wrong. He was right about the intervention and incomplete about why it worked. Second, he was **rejected.** His contemporaries, lacking the theoretical frame to accept a mechanism he could not fully explain, dismissed him; he died in an asylum, his reform unadopted at scale in his lifetime. The honest lesson is not "Semmelweis the germ-theory hero." It is sharper and more useful: *a correct, salient reframe can precede a correct mechanism, and being right about the formulation is no guarantee of being heard.*

This is the capacity this chapter names. AI systems, like the conventional framings available to Semmelweis, optimize toward the **common and the likely**. The supervisor's job is to reframe toward the **salient and the important** — and to do it *before* engagement, not after, because by the time the tool has run, the framing is already baked into everything it produced.

## Common-and-Likely Versus Salient-and-Important

Recall the structural claim from earlier in this book: a statistical system optimizes for what is common and likely given its training distribution. In Chapter 4 that claim explained why fluency does not track groundedness. Here it explains something about *problems* specifically, and it is the second-most-important consequence of the architecture.

Ask a capable model to "frame this problem" and it will produce a framing — fluently, instantly, confidently. But the framing it produces is the *modal* one: the formulation most represented in the distribution of past problems resembling yours. That is almost always the conventional, tractable, well-trodden framing — the one a thousand prior cases reached for. For most routine work, the modal framing is fine; it is modal precisely because it usually works. The danger is the case where the modal framing is *exactly the trap* — where the conventional question is tractable and answerable and beside the point, and the salient question is the one almost nobody asked.

Semmelweis's modal framing was "the patients are sicker" or "it's noise." His salient framing was "what do the doctors do that the midwives don't?" Notice that the salient framing was, at the time, *less* tractable: it pointed at a cause for which no theory existed. A system optimizing for tractability and conventionality would never have reached it, because nothing in the distribution of prior medical reasoning pointed there. Reaching it required a grounded sense of *what mattered here* — a values-and-context judgment about which differential between the wards was worth treating as signal.

This is why we sharpen the slogan from the previous capacity. The solve-verify asymmetry, at the level of problems, is really a **formulate-versus-optimize asymmetry.** The AI will optimize a given formulation flawlessly. Only a human can decide that the formulation itself was wrong. Hand the machine "minimize ward mortality variance" and it will do an excellent job on a problem that doesn't matter. The reframe is the move it cannot originate.

![A problematic situation splits into a wide grey modal path labeled tractable, conventional, and worthless, and a narrow red salient path labeled harder, less tractable, and correct about what matters.](images/06-problem-formulation-part-1-fig-01.png)

*Figure 6.1 — One situation, two framings: the model reaches for the wide modal path; the salient reframe is the move it cannot originate.*

## The Co-Evolutionary Model of Problem and Solution

There is a tempting picture of how problem-solving works: first you define the problem, then you solve it. Define, then solve. Clean, sequential, and almost entirely false to how serious work actually proceeds.

The empirically grounded model is **co-evolution.** Kees Dorst and Nigel Cross, studying experienced industrial designers at work, found that problem and solution develop *together*, each reshaping the other. [High] Their protocol studies — watching nine senior designers think aloud — produced a now-standard vocabulary: designers move between a **problem space** and a **solution space**, and the interesting work happens when a tentative move in the solution space provokes a *surprise* that forces a reframing of the problem, which in turn opens a different region of the solution space. The two spaces ratchet against each other. Dorst and Cross distinguish a "default" problem-solution pairing — the obvious framing and its obvious answer — from a "surprise" that shifts both. Expertise lives in provoking and exploiting the surprise.

![A problem space and a solution space side by side; a default pairing links P-zero to S-zero, then a red surprise arrow in the solution space forces a red reframe arrow back to a reframed problem.](images/06-problem-formulation-part-1-fig-02.png)

*Figure 6.2 — Problem and solution ratchet against each other: a surprise in the solution space forces a reframe of the problem, which opens a new region of solutions.*

The reason this matters for AI supervision is severe and underappreciated. If problem and solution co-evolve, then **handing the problem to the AI surrenders the steering wheel.** This is the line worth pinning to the wall: handing problem definition to a model is an *abdication, not a delegation.* (That phrasing is this book's claim, supported by the co-evolution model — not a finding lifted from Dorst and Cross.) When you delegate a solution, you keep the problem and judge the result against it. When you hand over the problem, you have given away the very thing that lets you judge whether the result is to the point. The AI will then co-evolve a tidy solution to *its* default framing, and present it with full fluency, and you will have no independent problem-formulation left to audit it against. You will have lost the steering wheel without feeling the wheel leave your hands.

Donald Schön, in *The Reflective Practitioner* (1983), gives the move its sharpest name. "Problem setting," he writes, "is a process in which, interactively, we name the things to which we will attend and frame the context in which we will attend to them." [High] And, crucially: "problems do not present themselves as givens; they must be constructed from problematic situations." Semmelweis was handed a *problematic situation* — two mismatched numbers. The *problem* — "what do the doctors do that the midwives don't?" — he constructed. Naming and framing is the work. It is the work an AI will eagerly do for you, in its modal way, the instant you let it.

## Primary Generators: The Anchors You Don't Know You're Using

If problem-setting is so consequential, how does a practitioner actually start? You cannot reason about a problem from nowhere; you need a foothold. Jane Darke, interviewing British architects who designed public housing, found that they did not begin by systematically enumerating constraints. They latched, early, onto a small number of constraints — often subjective, sometimes a single guiding idea — and used that anchor to generate a first candidate design, which they then tested and refined. Darke called this anchor the **primary generator.** [High] Her model: generator → conjecture → analysis. The generator comes first and silently shapes everything after it.

The architects' primary generators were things like "I want this to be a place where neighbors can keep an eye on each other's children." That is not a deduction from the brief. It is a value, an anchor, a way of carving the problem — and once chosen, it made certain solutions visible and others invisible. A different generator ("minimize cost per unit") would have produced a different building from the same brief.

Two things make primary generators dangerous in AI-supervised work. First, **they are usually tacit** — the practitioner doesn't know they're using one, which means they don't know it could be otherwise. Second — and here is the misconception to crush early — **primary generators are not biases to be eliminated.** Darke's point is the opposite: you *cannot* start without an anchor. The blank-slate, assumption-free formulation is a fiction. The supervisory skill is not to purge your generators but to *surface* them — to know which anchor you've grabbed, so you can ask whether it's the right one and what it's making invisible.

This is precisely where an AI both helps and harms. Ask a model to frame your problem and it supplies *its* primary generator — the modal anchor from its distribution — and supplies it invisibly, dressed as neutral analysis. If you do not already know what generator *you* would have chosen, you cannot even see that the model has chosen one for you. Surfacing your own generator before you engage the tool is what keeps the model's anchor from becoming yours by default.

## Why Formulation Precedes — and Cannot Be Recovered After — Engagement

Put the three ideas together and the timing rule follows necessarily. Because problem and solution co-evolve (Dorst and Cross), because the framing is constructed rather than given (Schön), and because the framing rides on a tacit anchor (Darke), the formulation is not a step you can perform *after* the tool runs and the solution exists. By then the solution embodies a framing, the framing embodies a generator, and all of it arrives wrapped in fluency that reads as inevitability. You can audit the output — Chapters 4 and 5 taught you how — but you will be auditing it against the framing it already assumes, which is the one thing the audit most needs to be independent of.

This is the deepest reason the capacities are ordered as they are in this book. Plausibility auditing checks whether the answer is grounded. Problem formulation checks whether it was ever the right question. The second is logically prior, and it has to happen *before* engagement or it cannot happen at all. Reframe before you engage. Not as a slogan — as a structural necessity.

## Worked Example: Semmelweis Formulated Two Ways

Lay the Vienna case out as two formulations of one problematic situation, and make the consequence of each explicit.

**The tractable framing:** *The First Clinic's mortality is noise, or a property of its sicker patients.* This framing is conventional, requires no novel mechanism, sits comfortably in the distribution of available medical explanations of 1847, and demands nothing of the physician. Its solution space contains: accept the variance; perhaps adjust admission criteria; wait for better patients. Its consequence: the dying continues. The framing is *answerable* and *worthless*.

**The salient framing:** *What do the physicians do that the midwives do not — and could it be carried on the body?* This framing is unconventional, points at a mechanism no theory yet supported, and demands that the physician implicate his own hands. Its solution space contains: identify the differential practice (autopsies), interrupt the transfer (chlorinated lime), measure the result. Its consequence: mortality from over eighteen percent in the worst month to roughly two. The framing is *harder*, *less tractable at the time*, and *correct about what mattered.*

The data did not choose between these framings. Both are consistent with the same mortality differential. The choice was a judgment about which difference between the wards to treat as *signal* — and that judgment required a grounded sense of what was worth attending to, exactly the thing the modal framing optimizes away. Semmelweis's tragedy completes the lesson: he chose the salient framing, was right about the intervention, was incomplete about the mechanism, and was rejected anyway. The reframe is necessary and not sufficient. But without it, nothing else was even possible.

---

> ### AI Wayback Machine: Einstein and Infeld on Formulating the Problem (1938)
>
> **Albert Einstein and Leopold Infeld, *The Evolution of Physics* (1938), p. 92.** "The formulation of a problem is often more essential than its solution, which may be merely a matter of mathematical or experimental skill. To raise new questions, new possibilities, to regard old problems from a new angle, requires creative imagination and marks real advances in science."
>
> Cite *both* authors — the quotation is routinely shortened to Einstein alone, and Infeld co-wrote the book and the line. The Wayback lesson is the chapter in one sentence. Solution is "mathematical or experimental skill" — exactly the kind of skill an AI now supplies in abundance, fast and tireless. Formulation is "creative imagination," the regarding of old problems from a new angle. That is the move an AI cannot originate, because originating it requires a grounded judgment about which new angle is *salient* rather than merely *available*. As the cost of solution collapses toward zero, the relative value of formulation rises. The conductor's most consequential act may be choosing which piece is worth performing at all.

---

## Exercises

These constitute the basis of **Reading Response #4 (30 pts)**. Each names a judgment call the Assessment Spine requires you to surface.

**Exercise 6.1 — Explain co-evolution from your domain (Understand).** Using a real problem from your own field, explain the co-evolutionary model: show one concrete place where a tentative move toward a solution *changed your understanding of the problem*. Then state why a static restatement of the original brief would not count as formulation. Deliverable: roughly 250 words with the co-evolution moment identified. *The judgment call to name: what did probing the solution space teach you about the problem that you could not have known by defining the problem first?*

**Exercise 6.2 — Surface the primary generators (Analyze).** For a provided brief, name the primary generator(s) — the tacit anchors that would silently shape how a practitioner first approaches it. Then re-approach the same brief from a *different* generator and show that it yields a different problem. Deliverable: the brief, two generators named, and the two problems they produce. *The judgment call to name: which generator would you have grabbed by default, and what would it have made invisible?*

**Exercise 6.3 — AI-default versus situation-required formulation (Evaluate). [Track 2]** For your capstone problem, write the formulation an AI would optimize toward (the common/likely/modal framing — generate it by actually asking a model to "frame the problem" and recording what it produces) and contrast it with the formulation the situation actually requires (the salient/important one). Make the difference between them explicit. Deliverable: both formulations, the model's actual output, and the contrast. *The judgment call to name: identifying the salient framing required knowledge or values the model did not have — name exactly what, and why it could not be supplied by a prompt.*

## Chapter Closing / Bridge

You can now see the framings — the tractable one the data and the tool both reach for, and the salient one the situation actually requires. You can name the co-evolution that makes handing over the problem an abdication, surface the primary generator riding underneath your first approach, and understand why all of this has to happen before engagement rather than after.

Seeing two framings, though, is not the same as generating several and choosing well among them under constraint. The application week that follows demands more and harder work: not one alternative reframe but *three genuinely distinct* ones — distinct enough that each would require a different solution even to test — evaluated against an explicit constraint set, with one selected and defended on both analytical and values grounds. And it forces into the open the thing this chapter has only gestured at: that every reframing centers some interests and decenters others, which makes formulation an irreducibly *values-laden* act long before any solution is computed.

## Sources

- Einstein, Albert, and Leopold Infeld. *The Evolution of Physics.* Simon & Schuster (1938), p. 92.
- Semmelweis, Ignaz. Work at Vienna General Hospital, 1847. Scholarly review: "Semmelweis and the aetiology of puerperal sepsis 160 years on: an historical review." PMC2870773. First Clinic mortality averaged ~10% (above 18% in the worst months, e.g., 18.3% in April 1847) versus the midwife-staffed Second Clinic at under 4%; after chlorinated-lime handwashing instituted mid-May 1847, the First Clinic rate fell to 2.2% in June 1847.
- Dorst, Kees, and Nigel Cross. "Creativity in the design process: co-evolution of problem–solution." *Design Studies* 22(5), 425–437 (2001).
- Darke, Jane. "The primary generator and the design process." *Design Studies* 1(1), 36–44 (1979). DOI: 10.1016/0142-694X(79)90027-9.
- Schön, Donald A. *The Reflective Practitioner: How Professionals Think in Action.* Basic Books (1983). Source for "problem setting," the naming-and-framing definition, and "problems do not present themselves as givens; they must be constructed from problematic situations."
