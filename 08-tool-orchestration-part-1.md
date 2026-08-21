# Chapter 8 — Capacity 3: Tool Orchestration (Part 1: The Capability Stack)

A vascular surgeon does not reach for the instrument already in her hand. She reaches for the one the next step requires. Mid-procedure, the scrub nurse holds the tray; the surgeon names what she needs — a fine clamp here, a different suture there — and the instrument is chosen because the tissue in front of her demands it, not because it was convenient or because it worked last time. The tray is a menu of capabilities, each suited to some tasks and dangerous in others. The surgeon's skill is not in any single instrument. It is in the selection: knowing, at each step, which tool the procedure actually requires.

You already work this way with AI, whether or not you have named it. You have a chat window open, a retrieval system you trust for some questions, a code interpreter you reach for when arithmetic matters, an agent that can run a whole sequence while you watch. The difference between competent AI use and supervisory AI use is the difference between grabbing whatever is already open and choosing the instrument the step requires. This chapter gives that selection a discipline.

The discipline rests on two ideas. The first is a way of seeing AI capabilities as a layered stack, where each layer trades reliability for reach. The second is a design principle — *verifiability-first engineering* — that treats "can I check this?" as a first-class objective when selecting a tool, equal in weight to "can it produce an answer?" Together they convert tool choice from a convenience question into a supervisory one.

A caution before we begin. The five-layer stack you are about to learn is *a* useful decomposition, not an industry standard. [Medium] There is no canonical "AI capability stack" that vendors agree on. The layers are a teaching device — a way to organize what current systems are reliable and unreliable for, so you can route a step to the right one. Treat the *structure* as the author's pedagogical framing, and treat the *failure modes* within each layer as the durable content, because those failure modes are documented and they outlast any particular product name.

## The Five-Layer Capability Stack

Picture the instrument tray as five layers, ordered from the most constrained and inspectable at the bottom to the most autonomous and opaque at the top. The single most important property of this ordering: **as you climb, the system can do more on its own, and you can verify less of what it did.** Reliability degrades as autonomy rises, and the verification burden rises in lockstep. That trade-off is the whole chapter.

**Layer 1 — Language generation.** Free-form text: drafting, summarizing supplied material, rephrasing, brainstorming, transforming one format into another. This layer is reliable for *form* and unreliable for *truth*. [High] It will produce fluent prose, a clean summary of text you handed it, a plausible rewrite — and it will, with equal fluency, confabulate a fact, miscalculate a sum, and invent a citation. This is the plausibility trap from Chapters 4 and 5, now located precisely: the layer most reliable for the shape of an answer is least reliable for whether the answer is correct.

**Layer 2 — Structured extraction.** Function calling and schema-constrained output: pulling fields out of documents into typed, validated JSON. Modern "strict" structured-output modes enforce schema adherence and have sharply reduced *parsing* and *validity* errors relative to simply asking a model to "output JSON." In one 2025 benchmark, reinforcement learning using the schema as a training signal pushed valid-JSON rates to roughly 98.7% against an 82.3% baseline. [Medium] Treat that figure as illustrative magnitude, not a load-bearing number; it is single-benchmark. The teaching distinction that *is* durable: **schema enforcement guarantees the output is well-formed, not that it is correct.** Valid JSON containing the wrong value is the precise danger — a fabricated figure sitting in a perfectly typed field, which the next chapter will follow as it acquires false authority downstream.

**Layer 3 — Retrieval-augmented generation (RAG).** Grounding answers in a supplied, current, domain-specific corpus rather than in the model's parametric memory. It is settled that RAG *reduces* hallucination relative to parametric-only generation. [High] It is equally settled that RAG does not *eliminate* it. [High] The documented failure modes, drawn from multiple 2025 reviews: the model contradicts correctly-retrieved context anyway; bad retrieval feeds the model irrelevant or biased chunks that *mislead* generation; and the system hallucinates on top of a hallucinated retrieval. The honest framing is that RAG *moves* the failure rather than removing it — from "the model made it up" to "the model was fed the wrong thing, or ignored the right thing." The architecture around retrieval is itself in flux: "agentic RAG," where retrieval becomes a tool the system calls iteratively, is becoming common, and some practitioners argue that large context windows are eroding classic RAG's niche. [Contested] Do not anchor your understanding on the architecture, which is moving. Anchor it on the failure *types*, which are stable.

**Layer 4 — Multi-step reasoning.** Chain-of-thought, planning, tool-use loops: the model decomposes a problem and exposes its intermediate steps. The exposed chain is a genuine supervisory gift, because it gives you a surface to inspect. But the chain is unreliable for *faithfulness*. [High] The stated reasoning trace is not guaranteed to be the computation the model actually performed — the "unfaithful chain-of-thought" finding. A plausible-looking chain can reach a wrong answer, or reach a right answer for reasons it did not actually use, and an error in an early step propagates silently into every step that depends on it.

**Layer 5 — Agentic execution.** Autonomous multi-step action with tool calls: the system plans, acts, observes, and acts again, across many steps, with minimal human intervention. It is reliable for well-scoped, low-branching tasks that have verification gates built in. It is unreliable for long-horizon autonomy, and the headline result of 2025–2026 is **error compounding.** [High] A single mistake at step two propagates and amplifies across every dependent step; uncertainty poisons the trajectory so that an agent can hold high confidence in a wholly wrong final result; and traditional evaluation catches the step-two error only when step ten fails. This is the strongest empirical support the book has for its central thesis: *the more autonomous the layer, the more the human supervisory role matters, not less.* A vendor forecast that some large fraction of enterprise applications will embed agents by mid-2026 circulates widely [Low] — treat it as a forecast, not a fact; the durable point is the failure mode, not the adoption curve.

| Layer | What it is | Reliable for | Unreliable for | Verification move |
|---|---|---|---|---|
| 1. Generation | Free-form text | Form, fluency, summary of supplied text | Factual grounding, arithmetic, citations | Check against an external source |
| 2. Extraction | Schema-constrained output | Well-formed, typed output | Semantic correctness of values | Require each value to trace to a source |
| 3. RAG | Grounding in a corpus | Reducing hallucination | Eliminating it; retrieval quality | Inspect the retrieved chunks, not just the answer |
| 4. Reasoning | Exposed multi-step chains | Decomposition, an audit surface | Faithfulness of the stated chain | Check the answer independently of the chain |
| 5. Agentic | Autonomous action loops | Scoped, gated tasks | Long-horizon autonomy; errors compound | Gate each step; do not trust completion as correctness |

## Reliability Falls as Autonomy Rises

Read the table top to bottom and a single curve appears. Push from Layer 1 to Layer 5 and the system does more of the work for you — more steps, more decisions, more of the chain hidden inside one call. At the same time, per-step reliability falls and the work required to verify the result rises. This is not a flaw in the products. It is the solve-verify asymmetry from Chapter 2 showing up as a measurable property of the instrument you just selected.

Recall the asymmetry: AI solves faster than any human, but it cannot verify whether its output is grounded in the specific reality at hand — verification is the irreducibly human work. The capability stack instantiates that claim with unusual precision. **Higher layers solve more and verify worse.** Agentic execution solves the most — it acts autonomously across the longest horizon — and is the hardest to verify, because errors compound and confidence is miscalibrated against correctness. When you reach for the most general, most capable-feeling layer, you are not buying a more reliable answer. You are buying a less verifiable one, and importing the higher-variance failure modes that come with it.

![A five-layer stack from language generation at the bottom to agentic execution at the top, each labeled with what it is reliable and unreliable for; an ink arrow on the left shows autonomy rising and a red arrow on the right shows verifiability falling.](images/08-tool-orchestration-part-1-fig-01.png)

*Figure 8.1 — As autonomy rises up the stack, the system does more on its own and you can verify less of what it did — the trade-off the whole chapter turns on.*

This reframes a misconception worth naming directly: *"a more capable model is more reliable for every step."* It is not. Generality and verifiability trade off against each other. Climbing the stack for convenience imports avoidable failure modes — the confabulation of Layer 1, the valid-but-wrong values of Layer 2, the unfaithful chains of Layer 4, the compounding errors of Layer 5. The supervisory move is the opposite reflex.

## Verifiability-First Engineering

Here is the design principle the chapter is built to install. **Select the lowest-on-the-stack capability that the step actually requires.** Do not reach for the most general tool; reach for the most constrained one that still does the job, because the most constrained tool is the most verifiable.

This is the solve-verify asymmetry rendered as a rule you can apply at a workbench. If verification is the consequential human work, then a workflow should be engineered so that each step is *checkable* — not merely so that each step produces an answer. The capability stack is the menu; verifiability is the selection criterion. A step that produces a fluent answer you cannot check is worse, from a supervisory standpoint, than a narrower step that produces a plainer answer you can.

There is a sharper version of this reflex, and the best supervisors apply it instinctively: **ask which part of the task should not touch a stochastic model at all.** Arithmetic, exact lookups, deterministic transforms, schema validation — these belong outside the probabilistic layers entirely, routed to code or a spreadsheet or a database. The most reliable orchestration move is frequently to route a step *out* of the LLM. A model that "does the math" is borrowing Layer 1's confabulation risk to perform a task a calculator does without error. Take the calculation away from it.

Notice the lineage. McIlroy's Unix doctrine — make each program do one thing well, and expect the output of every program to become the input to another — is exactly "select the narrowest capability that suffices, and compose." Orchestration is composition with the trust decisions made explicit. The conductor frame holds: in selecting the instrument for the passage, the conductor produces no sound, writes no code, runs no model — but the performance collapses without the selection-and-sequencing judgment. This chapter is the *selection*; Chapter 9 is the *sequencing with documented handoffs*.

## Worked Example: One Task, Two Routings

Take a task an analyst meets constantly: *Extract every line item over $10,000 from these 200 invoices and total them.* Route it two ways and compare what you can verify.

**The convenient single-tool path.** Paste the invoices into a chat window and ask for the total. This runs the entire task through Layer 1. The model reads, filters, and sums — and the summation is arithmetic performed by a language model, which is exactly what Layer 1 is unreliable for. You receive a number. It is fluent, formatted, confident. You cannot check it without redoing the work, because nothing in the output traces to anything: no per-invoice breakdown you can audit, no arithmetic you can recompute. The output is unverifiable by construction. If it is wrong by one omitted invoice, you will not know.

**The requirement-driven multi-tool path.** Decompose the task by what each step requires. Extracting structured fields from each invoice is a Layer 2 job: run structured extraction per invoice, producing a typed record — vendor, line item, amount — for each. Filtering and summing are arithmetic and exact comparison; route them *out* of the stochastic stack entirely, into deterministic code or a spreadsheet formula. Now the workflow has a verification surface at every seam. You can inspect the extracted records against the source invoices. You can recompute the sum yourself, or have a second deterministic tool recompute it. The arithmetic has left the probabilistic layer, so it cannot confabulate; if the code is wrong it errors loudly rather than lying quietly.

The two routings produce a number either way. Only one produces a number you can stand behind. The legal version of this example is even sharper: ask a chat model to "summarize and cite the controlling cases" and Layer 1 will fabricate citations with the same fluency it drafts the prose [High] — a failure that has reached real courtrooms. Route it instead through Layer 3 retrieval against a real case database, Layer 2 extraction of citation fields, and Layer 1 only for the prose with citations carried verbatim from retrieval, and every citation traces to a retrieved source. Same task, same final artifact, radically different verifiability — and the difference was a selection decision a human made before any tool ran.

![Two routings of summing invoices over ten thousand dollars: the convenient path runs everything through Layer 1 to a single red unverifiable number; the requirement-driven path uses Layer 2 extraction plus deterministic code, opening a verification surface at every seam.](images/08-tool-orchestration-part-1-fig-02.png)

*Figure 8.2 — Routing the arithmetic out of the stochastic stack converts one unverifiable number into a chain you can check at every seam.*

> **AI Wayback Machine — Doug McIlroy and the Unix philosophy**
>
> The pipe — the mechanism that lets one program's output flow directly into another's input — was proposed by Doug McIlroy and implemented by Ken Thompson at Bell Labs in 1973. [High] The *written philosophy* came later: McIlroy's foreword to the *Bell System Technical Journal* special issue on the UNIX Time-Sharing System, 1978, where he set down the doctrine usually quoted in four points. The first two are the ones that matter here: *"Make each program do one thing well… Expect the output of every program to become the input to another, as yet unknown, program."* [High]
>
> Keep the two dates distinct: the pipe is 1973, the philosophy is 1978. McIlroy built the mechanism years before he wrote down the doctrine. The doctrine is precisely tool orchestration avant la lettre — build narrow, well-behaved tools, and compose them deliberately. What the AI era adds is that the seam between tools is now a *trust* decision, because one of the tools can lie fluently. Composition with the trust decisions made explicit: that is the whole capacity, and McIlroy named half of it in 1978.

## Exercises

These exercises ask you to make selection decisions and defend them. The Assessment Spine applies: each deliverable must name at least one judgment call that required your domain knowledge or values — a call an AI could not make on your behalf, because making it required knowing what your work actually demands.

**Exercise 8.1 — Build a capability-stack reference (Understand).** For your own domain, build a reference table mapping your three or four most recurring AI-assisted tasks to the capability layer each one actually requires. For each task, name what would go wrong if you routed it one layer too high. *Deliverable:* a one-page reference table. *Assessment Spine:* identify the one task where the "right" layer is genuinely contestable in your domain, and state the judgment — based on your knowledge of the stakes — that resolves it. *(25 points; Reading Response #5, 30 points.)*

**Exercise 8.2 — Diagnose a workflow (Analyze).** For a provided multi-step workflow, name the capability layer each step requires and state whether the tool currently assigned to that step supplies it. Flag every step routed too high on the stack. *Deliverable:* an annotated workflow with a layer label and a verifiability verdict per step. *Assessment Spine:* for the single most dangerous mis-routing, explain what specific failure mode it imports and what in your domain knowledge let you see it.

**Exercise 8.3 — Audit a habitual tool choice (Evaluate).** Take one tool choice you make reflexively in your own practice. Determine, honestly, whether you selected it for the step's requirement or out of convenience — because it was already open. If convenience, identify the lower, more verifiable layer the step actually needs, and the cost of the switch. *Deliverable:* a written audit of one habitual choice. *Assessment Spine:* name the judgment call — what the step *requires* in your work — that no tool could have made for you, because no tool knows what your output is for.

## Closing and Bridge

You can now choose the instrument for the step. You can see the stack as a trade-off curve, name what each layer is reliable and unreliable for, and apply the verifiability-first rule: the lowest capability that suffices, and route deterministic work out of the stochastic layers entirely.

But selecting the right tool for each step is only half of orchestration. The other half is the seam — the handoff where one tool's output becomes another's input *on trust*. A workflow of perfectly chosen tools can still launder a fabricated number from the first step into an authoritative-looking memo at the last, if no one verifies at the seams. Chapter 9 opens with a flawed workflow and asks you to find the undocumented handoffs and the silent trust decisions — and then to use one tool to audit another, with the one rule that makes cross-auditing more than theater: the audit tool must fail differently from the tool it checks.

## Sources

- McIlroy, M. D. Foreword to the special issue on the UNIX Time-Sharing System. *Bell System Technical Journal* 57(6), Part 2 (July–August 1978). [The Unix philosophy; "make each program do one thing well."]
- McIlroy, M. D. (proposer) and Thompson, K. (implementer). The Unix pipe, Bell Labs, 1973. [Pipe mechanism; distinct in date from the 1978 philosophy.]
- *PARSE: LLM-Driven Schema Optimization for Reliable Entity Extraction.* arXiv:2510.08623 (2025). [Structured-output validity figures; single-benchmark, illustrative.]
- *Hallucination Mitigation for Retrieval-Augmented LLMs: A Review.* MDPI *Mathematics* 13(5):856 (2025). [RAG reduces but does not eliminate hallucination; retrieval can mislead.]
- *Towards a Science of AI Agent Reliability.* arXiv:2602.16666 (2026); O'Reilly Radar, "The Hidden Cost of Agentic Failure" (2025). [Error compounding in agentic execution.]

## Tags

#conducting #ai #tool-orchestration #capability-stack #verifiability #McIlroy #unix-philosophy #judgment
