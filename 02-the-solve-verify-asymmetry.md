# Chapter 2: The Solve-Verify Asymmetry

## A claim, stated before it is defended

Here is the claim the whole book rests on. I am going to state it plainly, then spend the chapter arguing for it and — this is the part that matters — telling you exactly where the argument stops being airtight.

> Solving a problem and verifying a solution are different cognitive operations. AI automates the first. The second remains human, not because today's models are weak, but because verification requires something statistical pattern-matching does not contain. And because faster solving produces more output needing verification, the gap *deepens* as capability scales rather than closing.

If you are a skeptical engineer, you should already be suspicious of two things in that paragraph: the word "structural" lurking behind "remains human," and the implied permanence of "does not contain." Good. Hold the suspicion. A claim this strong earns its keep only by surviving the strongest version of the objection, and I intend to give you the strongest version myself.

Let me start with the misconception the chapter exists to detonate. Most people, asked whether AI will eventually verify its own work, reason like this: *verifying is just solving again, more carefully. If the model can solve, then with enough scale it can solve the checking problem too. Verification is a harder instance of generation.* This feels obviously true. It is the intuition behind every "the next model will fix it." And it is wrong — not because verification is harder, but because it is a *different kind of operation*, requiring inputs the solver structurally lacks.

## Two operations, not one harder one

Start with a place where the distinction is formally precise and beautifully clean, then we will leave it before it overstays its welcome.

In 1971, Stephen Cook published "The Complexity of Theorem-Proving Procedures" and, with Leonid Levin working independently in the USSR, gave the world the concept of NP-completeness and the question we now call **P versus NP** [High]. Strip it to its pedagogical core. There is a class of problems — call it NP — for which a candidate answer can be *checked* quickly, in polynomial time. The open question is whether every such problem can also be *solved* quickly. The widespread belief, unproven, is that the answer is no: P ≠ NP, meaning for many problems, *finding* a solution is genuinely harder than *checking* one [High].

The examples are intuitive. A route through fifty cities: handed a proposed tour, you can verify its length in a glance; *finding* the shortest is brutal. A satisfying assignment for a logical formula: trivial to check, hard to discover. A mathematical proof: easier to verify line by line than to originate. In each, *checking and finding are different problems, and the gap between them is not an artifact of weak tools.* That is the deepest formal expression we have of the idea that verification and solution are distinct operations.

Now the honesty, because this is the chapter where the book's credibility is made or lost. **This is an analogy, and it is bounded twice over.** First, P versus NP is an *open conjecture*, not a theorem — nobody has proven P ≠ NP; it is one of the Clay Millennium Prize problems precisely because it remains unresolved [High]. So even the formal statement is a belief, not a proof. Second, and more important: *large language models are not subject to P versus NP in any literal way.* P versus NP is about worst-case algorithmic complexity for exact problems. An LLM is not running an exact algorithm against a worst-case instance; it is doing something better described as approximate retrieval from a learned distribution. Subbarao Kambhampati makes exactly this point, and it cuts against the naive use of the analogy: the intuition that verification should be easier than generation "should be irrelevant to LLMs to the extent that what they are doing is approximate retrieval" [Contested].

So Cook does not *prove* anything about AI. What Cook earns us is narrower and still valuable: the *conceptual respectability* of the claim that checking and finding can be genuinely different operations, with a structural rather than incidental gap between them. Computer science has a whole mature theory in which this is taken seriously. That licenses us to take it seriously about AI — but the argument *about AI* has to be made on its own terms, which is what we do next. If you ever hear someone say "P vs NP proves AI can't verify itself," they have overreached, and you should be able to say why. Teaching the limit of your own analogy is the move that lets a skeptic trust the rest.

> **AI Wayback Machine — Stephen Cook, "The Complexity of Theorem-Proving Procedures" (1971).** Cook, with Levin, formalized the deepest idea we have that *finding* and *checking* are different problems — a gap that lives in the structure of the problems, not in the strength of our machines. He won the Turing Award for it in 1982; the P-versus-NP question it raises is still open. We borrow the *idea* and refuse the *overreach*: this is a conjecture about exact algorithms, not a theorem about language models. What it gives us is permission to treat "solving ≠ verifying" as a serious structural possibility rather than a temporary complaint. The argument that it holds for AI we have to make ourselves.

## The argument that holds for AI

So make it. Forget complexity classes; reason about what a language model actually does when it answers, and what it does when asked to check.

When a model generates, it samples from a learned distribution — it produces the continuation that is, in the statistical landscape of its training, *common and likely* given the prompt. This is what makes it fluent, and it is also why fabricated case citations look exactly like real ones: a citation that fits the *form* and *frequency* of real citations is, distributionally, a likely continuation, whether or not the case exists. The model is not lying. It has no access to a fact-of-the-matter about the case's existence; it has access to what citation-shaped text usually looks like.

Now ask that same model to verify its answer. What does it do? It samples again — from the same distribution that produced the answer in the first place. Self-verification is *more retrieval against the same landscape that contained the error.* If the original mistake was a likely-looking fabrication, the verification pass finds it likely-looking too. This is not a flaw in a particular model; it is what self-verification *is* for a system of this kind. The retrieval loop closes on its own blind spot.

This is not armchair reasoning. Stechly, Valmeekam, and Kambhampati tested it directly — GPT-4 self-critiquing on Game of 24, graph coloring, and STRIPS planning — and found that iterative self-verification does *not* reliably improve output; the apparent gains are often misattributed to the verification step when they come from elsewhere [Medium]. Their conclusion: these systems are better deployed as idea generators than as their own critics [Medium]. You can reproduce the core demonstration in a classroom in five minutes: get a model to commit to a wrong Game-of-24 solution, then ask it to verify; watch it confirm its own error with confidence.

Here is the load-bearing step. *What verification actually requires* — in the lawyer's room, the physician's, the analyst's — is grounding in the *specific domain reality*: does this case exist in the actual corpus of law, does this package exist in the actual registry, does this match actual pathology, do these sources actually exist. That grounding is exactly what statistical generation does not contain. It is not a more careful version of generation; it is an appeal to something *outside* the distribution — the world the distribution is a blurry photograph of. The solver cannot supply it because the solver only has the photograph.

That is the version of the structural claim I will defend: not "P vs NP proves it," but "verification that matters requires grounded, situated, accountable domain judgment, and that is categorically outside what approximate retrieval contains" [Medium].

## Why it deepens instead of closing

Grant the argument for a moment and watch what scaling does. A faster, cheaper, more fluent model increases the *volume* and *velocity* of solved output. More briefs drafted, more code generated, more reports produced, per hour. But each piece of that output carries the same need — grounding against specific reality — and that need is met only by the human operation the model lacks. So the solving throughput climbs while the verification gate stays the same size, because the thing it requires was never in the machine.

Picture it as two channels. The SOLVE channel widens every year: broad, fast, scaling, optimized for the common and the likely. The VERIFY channel is a narrow gate: situated, accountable, attending to the salient and the important, human-sized. More water through the wide channel does not widen the gate. It just means more is arriving at it, faster, looking more finished than ever — which is precisely the condition under which a tired or trusting human waves it through. The asymmetry deepens. That is the structural prediction, and it is the opposite of the comfortable one.

![Chart with capability scaling on the horizontal axis; a steeply rising shaded SOLVE channel represents growing output volume, while a flat red line marks the human-sized VERIFY gate, the vertical distance between them widening into a labeled gap.](images/02-the-solve-verify-asymmetry-fig-01.png)

*Figure 2.1 — As capability scales, the solve channel widens but the verification gate stays human-sized — so the gap between output produced and output grounded widens rather than closing.*

## Removing the comfort and the threat

Two stories follow people around when they think about AI and their own work. The asymmetry dissolves both, and for the same reason.

**The comfort:** *relax — the next model will check its own work.* This is the misconception, dressed for the future. It assumes verification is a solving problem that scale will reach. But self-verification is more retrieval against the same distribution (the empirical finding), and the verification that matters needs grounding the model does not contain (the structural argument). A better solver produces better-looking output that needs the *same* external verification — arguably more urgently, because it is harder to spot as wrong. The comfort is not just false; it points the wrong way.

**The threat:** *verification is the leftover, diminished work — you'll be a rubber stamp.* This inverts what verification is. Verification is where the grounding happens, where the output meets the specific reality, where accountability attaches. The solver faces no court, no patient, no refund; the verifier signs. Far from being the residue of the process, verification is the part with consequence in it. In a high-velocity AI workflow, the human who verifies is doing the *consequential* work — not despite the AI's speed but because of it. The faster the solving, the more the whole enterprise depends on the one operation that cannot be sped up by the same means.

I want to be scrupulous about status here, because the chapter that overstates this is the chapter a sharp reader dismisses. The sentence "these are not limitations better models will close; they are features of what statistical pattern matching *is*" is the book's boldest, and it is a **wager**, not a theorem [Contested]. It is defensible via the retrieval argument. It is contested by anyone who believes tool-augmented and reasoning models change the picture. Which brings us to the live counter-case, because pretending it does not exist would be the worst kind of dishonesty in a 2026 book.

## The live counter-case: reasoning models

Since 2024, "reasoning" models — systems that spend inference-time compute generating extended intermediate steps, and frontier systems that verify against external tools — have plainly *verified more*, and verified better, than the models the original critique was written against. A model that runs code to check its own arithmetic, or searches a real database to confirm a citation exists, is doing something the pure-retrieval picture does not describe. Any honest treatment has to concede: the gap is *narrower* in 2026 than the simplest version of the argument implies.

Two things to say, and the second is the one that holds.

First, even within the model: extended reasoning chains verify primarily against *internal consistency* and against the *training distribution* — they check whether the answer hangs together and matches what is typical. That is a real improvement and it catches a real class of errors. But internal consistency is not the same as grounding in *this situation's* specific reality, and Kambhampati's 2025 follow-on work argues the gains from reasoning models are narrower than marketed and do not constitute genuine self-verification of the kind that would close the gap [Contested].

Second — and this is the move that survives even if you are generous to the models — notice *where the grounding comes from when it works.* When a reasoning model verifies a citation by querying a real legal database, the verification is grounded not by the model but by *the tool the model was pointed at* — a tool that someone, with domain judgment, decided was the right authority for this kind of check. When it runs code to confirm a result, the grounding lives in the *executable specification*, which a human wrote with intent the model does not hold. The model is increasingly good at *orchestrating* grounded checks. It is not the source of the grounding, or of the judgment about which check is the right one for *this* situation, or of the accountability for being wrong. Tool use does not refute the asymmetry; it *relocates the verification into tools whose selection and trust are themselves supervisory judgments* — which is, not coincidentally, the entire subject of Chapter 8. The conductor does not disappear when the orchestra gets better instruments. The conductor's job moves up a level.

So the claim survives, suitably bounded: the verification that matters — grounded in specific reality, attentive to the salient and important, accountable for consequence — is not something a statistical solver supplies, whether it solves in one pass or ten thousand. The five capacities are the *content* of that verification, and they are what the rest of the book builds.

## Worked example: solved correctly, still wrong

Return to the lawyer's room and apply the distinction with precision. Ask: was the AI's output *solved* correctly? By every internal measure, astonishingly so. The citations were well-formed. The case names followed real conventions. The quotations had the cadence of real holdings. The reasoning connected to the brief's argument. As a *generation* task — produce text that fits the form and frequency of supporting case law — it was a near-perfect solve.

And it was catastrophically wrong, because the operation the situation required was not a better solve. It was a different operation entirely: *do these cases exist in the actual corpus of law?* That question cannot be answered from the distribution of citation-shaped text. It can only be answered by appeal to the real corpus — a database, a reporter, a librarian — which is to say, by grounding outside the model. The attorney's fatal move was to treat verification as a solving problem: confronted, he re-prompted, asking the solver to solve the checking question. The solver solved it the only way it could — by producing more likely-looking text — and confirmed the fabrication. Solving was flawless. Verification, the *different* operation, never happened. That is the asymmetry, lived.

## Exercises

Graduated and increasingly demanding. Together they constitute **Reading Response #2 (30 points)**.

**Exercise 2.1 — State the asymmetry for a skeptic (Understand).** In one paragraph, state the solve-verify asymmetry in terms a skeptical engineer would accept — meaning: no hand-waving about "AI can't really think," and an honest flag on what is argued versus proven. *Deliverable:* one paragraph. *The judgment this surfaces:* whether you can hold a strong claim and its limits at once — the intellectual honesty the rest of the course demands of every finding you make. (10 pts)

**Exercise 2.2 — Refute the comfort, structurally (Evaluate).** Respond to: "But the next model will be able to check its own work." Your refutation must use the *structural* argument (retrieval against the same distribution; verification needs grounding the solver lacks), not an appeal to current weakness ("models still make mistakes"), and must engage reasoning models as the live counter-case rather than ignoring them. *Deliverable:* a half-page argued response. *The judgment this surfaces:* your ability to defend a position against its strongest objection, conceding ground where honesty requires and holding it where the argument does. (12 pts)

**Exercise 2.3 — Map the boundary (Analyze).** Take one AI-assisted task you ran this week. Mark precisely where *solving* ended and *verification* began. Then state what the verification required that the solver could not supply — naming the specific reality the answer had to be grounded against. *Deliverable:* one annotated task with the solve/verify boundary and the grounding named. *The judgment this surfaces:* your accountability for a real output you trusted, and whether the grounding you relied on was yours or borrowed. (8 pts)

## Closing: from whether to what kind

If verification is the work — irreducible, consequential, deepening as the tools improve — then the next question is not *whether* to verify but *what kind* of verification a given use demands. Because not all AI use makes the same demand. Fixing a typo is not co-authoring an argument. The supervision a glance can supply is not the supervision a co-reasoned analysis requires, and the most dangerous error is not using AI at a high level — it is supervising high-level use as if it were low. The next chapter gives you the diagnostic: three levels of AI usage, three levels of supervisory demand, and the specific, persistent failure that appears when the two fall out of step.

---

## Sources

- Cook, Stephen A. "The Complexity of Theorem-Proving Procedures." *Proceedings of the Third Annual ACM Symposium on Theory of Computing* (STOC '71), 1971, pp. 151–158. DOI 10.1145/800157.805047.
- Levin, Leonid A. "Universal Sequential Search Problems." *Problems of Information Transmission* 9, no. 3 (1973) — the independent half of the Cook–Levin theorem.
- Stechly, Kaya, Karthik Valmeekam, and Subbarao Kambhampati. "On the Self-Verification Limitations of Large Language Models on Reasoning and Planning Tasks." arXiv:2402.08115, 2024 (ICLR 2025).
- Kambhampati, Subbarao, et al. "(How) Do Reasoning Models Reason?" *Annals of the New York Academy of Sciences*, 2025.
- Clay Mathematics Institute, statement of the P versus NP Millennium Prize Problem.
- *Mata v. Avianca, Inc.*, 678 F. Supp. 3d 443 (S.D.N.Y. 2023) — the re-examined case.
