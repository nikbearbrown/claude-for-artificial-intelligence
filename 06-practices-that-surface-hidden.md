# Chapter 6 — Practices That Surface What's Hidden

> *The practical toolkit — pre-mortem, red teaming, scenario planning, five whys — examined for what each can surface, and honestly named for what each cannot.*

---

## Learning objectives

1. *(Remember)* Name the central move of each of the four practices and the class of unknown unknown each is designed to surface.
2. *(Understand)* Explain why each practice has a structural limit — what it cannot reach — and why combining practices is not the same as having more of any one of them.
3. *(Apply)* Run a one-hour pre-mortem on a project you control and produce a list of named risk factors the original plan did not include.
4. *(Evaluate)* Decide which of the four practices is the right fit for a specific unknown-unknown problem and defend the choice with reference to the practice's known limits.

## Opening case — Shell, 1972

In 1972, Pierre Wack and his team at Royal Dutch Shell ran an exercise that, by industry standards, was strange. They constructed scenarios — not forecasts — of what might happen to global oil markets over the following decade. One of the scenarios involved a coordinated supply shock from OPEC producers and a sharp, sustained rise in oil prices.

The scenario was not a prediction. Wack's articulation of his own method was precise: *scenarios are not predictions. They are mental-model rehearsals* ([Wack, "Scenarios: Uncharted Waters Ahead," *Harvard Business Review*, 1985](https://hbr.org/1985/09/scenarios-uncharted-waters-ahead)). The scenarios' purpose was to prepare Shell's executives to think *about* a world in which their operating model — built on cheap, abundant, stable Middle East oil — was suddenly obsolete.

In October 1973, the OPEC oil embargo produced precisely the kind of shock Wack's team had rehearsed. Shell's response was, by industry consensus, faster and more coherent than its peers'. The company shifted refining capacity, hedged forward, and repositioned strategically within months while competitors took years.

The case is canonical in the scenario-planning literature. It is also widely *over-claimed* in the popular literature. Wack himself was careful: scenario planning did not predict the 1973 embargo. It made Shell's executives *able to think* about a discontinuity their forecasting models did not contain. The unknown unknown — *the structure of cheap-oil-forever is itself the assumption* — was surfaced. Wack and his successors are explicit that the value lived in the prior conversations, not in the post-hoc forecast accuracy.

This chapter examines four practices that, like Wack's, are designed to surface what the standard models cannot reach. It is also honest about what each practice does not do.

## The core practices — four moves

**Pre-mortem.** A meeting held *before* a project launches, in which participants are asked to imagine the project has failed catastrophically and to write down why. Originated in Gary Klein's research on naturalistic decision-making; the canonical published statement is Klein, "Performing a Project Premortem," *Harvard Business Review*, 2007.

The structural move: shift the conversational frame from *the project will succeed* to *the project failed*. The shift relaxes commitment-to-the-plan defensiveness (Chapter 5) and lets participants surface concerns that the "let's-launch" frame suppresses.

What it surfaces: failure modes participants can *imagine*. Pre-mortems are particularly good at surfacing risks that someone in the room knew but had not raised. Unknown knowns (Chapter 2) become known unknowns.

What it does not surface: failure modes no one in the room can imagine. The pre-mortem is bounded by the participants' collective imagination. If the failure mode is genuinely outside the room's experience, the pre-mortem cannot reach it.

**Red teaming.** A practice — originating in military planning, adopted into intelligence analysis, business strategy, and AI safety — in which a designated group is empowered to argue against the plan as if they were adversaries or competitors.

The structural move: institutionalize the role of *the person who is against the plan*. Without the structural authority of the red-team role, opposition gets read as obstruction; with it, opposition becomes a legitimate part of the planning process.

What it surfaces: failure modes that depend on adversarial action — competitor moves, attacker strategies, opposition tactics — and structural weaknesses that a friendly review would miss.

What it does not surface: failure modes that depend on no one being adversarial, or that emerge from system dynamics rather than from any actor's intention. Red teaming also has a documented failure mode: when the red team becomes *performative* (e.g., to satisfy a checkbox requirement) without structural authority to change the plan, it produces theater rather than information.

**Scenario planning.** Constructing multiple distinct futures — typically two to four, distinguished by load-bearing uncertainties — and stress-testing strategic decisions against each. Originated in military planning (Herman Kahn at RAND, 1950s; *Thinking the Unthinkable*, 1962) and made famous in corporate strategy by Wack at Shell.

The structural move: replace single-point forecasts with a small set of structurally distinct worlds. The point is not to assign probabilities to the worlds. The point is to rehearse decision-making *in each*, so that the strategy in the actual world becomes more flexible.

What it surfaces: structural assumptions in the current strategy that are visible only when contrasted against alternatives. The Shell case is the canonical demonstration.

What it does not surface: futures the scenario designers cannot conceive. If the relevant discontinuity is outside the imaginative range of the planning team, no scenario set will contain it. The 1973 oil shock was within Wack's imaginative range because Wack had cultivated a broad view of geopolitical possibility; for a planning team without that cultivation, the same exercise would have produced different (and probably less useful) scenarios.

**Five whys.** Ask "why?" five times, working from a presented problem backward to a root cause. Originated at Toyota under Sakichi Toyoda and was systematized by Taiichi Ohno (*Toyota Production System*, 1978). Widely adopted in lean and Six Sigma contexts.

The structural move: refuse to stop at the first plausible answer. The discipline forces the inquirer past surface symptoms into the chain of causation that produced the symptom.

What it surfaces: structural causes that lie upstream of the immediate failure — typically two or three causal links back from the surface problem, where the operational fix actually lives.

What it does not surface: causes outside the questioner's mental model. The five whys terminate at *the asker's edge of competence*. A skilled diagnostician in domain X can reach mechanism with five whys; a novice in domain X will hit a plausible-sounding but shallow root cause and stop.

## Worked example — the Challenger and the five whys

Apply the five whys to the Challenger O-ring case (Chapter 2 introduced the case as an unknown known; here we use it to examine a practice's limits).

*Why did Challenger fail?* The O-rings did not seal at low temperature.
*Why did the O-rings not seal?* They had lost elasticity in cold weather and could not perform their function under the operating conditions.
*Why were they operating outside the qualified temperature envelope?* Because management approved a launch at 29°F when the qualification envelope was higher.
*Why did management approve a launch outside the qualified envelope?* Because the engineers' concerns were reviewed and overruled.
*Why were the engineers' concerns overruled?* Because the normalization-of-deviance pattern (Vaughan 1996) had reclassified out-of-spec performance as evidence of robustness, and the schedule pressure created a frame in which postponement required more justification than launch.

The five whys reached a sophisticated answer — but only because the analyst (a reader of Vaughan or the Rogers Commission) brought a sophisticated model. A naive five-whys analysis would have stopped at "management approved a launch outside the qualified envelope" and concluded "improve approval procedures." That conclusion is not wrong; it is operationally insufficient. The deeper cause — the normalization-of-deviance pattern — is invisible to the practice on its own. The practice's reach depends on the asker's existing knowledge.

**The lesson:** Each practice surfaces what its structure can surface. None substitutes for the cultivated knowledge of the practitioner running it. The practices amplify; they do not replace.

**The limit:** The chapter's most uncomfortable claim — practices that promise to surface unknown unknowns are bounded by the practitioner's prior mental-model coverage. A pre-mortem run by people who have never seen a relevant failure mode will not surface that failure mode. The practices accelerate the conversion of unknown unknowns to known unknowns *for people who already have enough mental-model coverage to make the conversion possible*. They do not produce coverage where none existed.

## Common misconceptions

**"Pre-mortems prevent failure."**
Pre-mortems prevent the subset of failures whose patterns are within the room's collective imagination. They do not prevent failures whose patterns are outside it. The Klein 2007 *HBR* article is explicit about this; the popular adoption often is not.

**"More practices = more coverage."**
Each practice has a different reach. Combining them produces real coverage gains where the reaches overlap and where they complement. Combining them does not produce *coverage of what none of them reaches*. The Challenger case illustrates: red-team-plus-pre-mortem-plus-five-whys-plus-scenario-planning, run by people without Vaughan's organizational-sociology framework, would still not have surfaced the normalization-of-deviance pattern. Coverage is bounded by the practitioners' knowledge.

**"Red teaming works whenever you do it."**
Red teaming works when the red team has structural authority to change the plan. Red teams without authority become consultation theater. The Department of Defense's institutional red teaming has a documented mix of effective and performative implementations (multiple after-action reports; the literature on "red cell" effectiveness is uneven).

**"Scenario planning is about predicting the future."**
Wack's clearest articulation, repeated in his successors' work (van der Heijden, *Scenarios: The Art of Strategic Conversation*, 1996), is that scenarios are *not* predictions. Treating them as predictions defeats the purpose; the rehearsal value lives in considering futures the participants do not yet have a probability on.

## Exercises

1. *(Apply)* Run a 45-minute pre-mortem on a current project. Time-box: 10 minutes of silent writing ("the project failed; here's why"), 25 minutes of structured surfacing (each participant reads one item; group classifies as in-scope/out-of-scope/needs-investigation), 10 minutes of action assignment. Produce a written list of named risk factors. Compare against the project's prior risk register. Count what was new.

2. *(Analyze)* Take an organizational failure post-mortem (yours or in the public record). Run a counterfactual five-whys: at which point would the practice have surfaced the actual root cause, and at which point would it have stopped at a plausible-sounding shallow answer? The diagnosis is about the practice's reach, not about whether the answer is findable in hindsight.

3. *(Evaluate)* Pick a planned organizational decision in the next 90 days. Decide which of the four practices is the best fit for surfacing the kinds of unknown unknowns the decision is most exposed to. Defend the choice in three sentences. Run the practice. Note whether it surfaced anything; note whether the practice's limits (named in this chapter) bit.

## What would change my mind

If empirical work demonstrated that pre-mortem or red-team interventions reliably prevent failures of the kind the practitioners had not previously seen — i.e., that the practices surface unknown unknowns *outside* the participants' prior knowledge at meaningful rates — the chapter's central claim about practitioner-knowledge bounding the practices' reach would weaken. The current evidence (Mitchell, Russo & Pennington 1989 [verify]; Klein's later work; the broader naturalistic-decision-making literature) is more consistent with the chapter's claim than against it. A high-quality study to the contrary would shift the framing toward *practice as substitute* rather than *practice as amplifier*.

## Still puzzling

- The chapter argues that practices amplify but do not substitute for practitioner knowledge. The line between "amplification" and "substitution" is fuzzy in practice — some skilled practitioners credit pre-mortem for catching things they would have missed without the practice. The honest position: the practice helps; the help is bounded; the boundary is the practitioner's prior coverage.
- Several practices in current circulation (e.g., adversarial collaboration, structured analytic techniques from intelligence analysis) are adjacent to the four covered here. Whether they belong on the list is a curatorial question the chapter does not resolve.
- The Wack/Shell case's reputation is partly a function of the dramatic 1973 outcome. The same practice run in years where no dramatic discontinuity occurred is harder to evaluate. The chapter's epistemic humility: the evidence base for any of these practices is weaker than the practice-promotion literature claims.

---

*The practices are tools. The next chapter turns the analytic lens on one of the most famous theorists of unknown unknowns and asks the uncomfortable question: did he apply his own framework to himself? **Chapter 7 — Badly Priced Risk: The Taleb Case Study.***
