# Chapter 2 — Known Unknowns and Why They're the Easy Part

> *The Rumsfeld taxonomy decomposed. Why organizations convert unknown unknowns into known unknowns too slowly — and what would accelerate the conversion.*

---

## Learning objectives

1. *(Remember)* State the four cells of the Rumsfeld / Johari window taxonomy and the kind of risk-management work appropriate to each.
2. *(Understand)* Explain why **known unknowns** are tractable with standard methods and **unknown unknowns** are not — naming the specific structural difference, not just the labels.
3. *(Analyze)* Diagnose an organization's risk register and identify which entries are known unknowns dressed up as managed and which are unknown unknowns the register cannot reach.
4. *(Evaluate)* Assess whether a specific reported risk represents a quantification failure (a known unknown not yet measured) or a representation failure (an unknown unknown not yet conceptualized).

## Opening case — Lehman Brothers and the model that did not see itself

In September 2008, Lehman Brothers filed the largest bankruptcy in U.S. history — approximately $639 billion in assets. The court-appointed Examiner's Report (Valukas, 2010, ~2,200 pages) documents an internal risk-management apparatus that, by 2007 standards, was sophisticated. Lehman had Value-at-Risk models, stress tests, scenario analyses, an enterprise risk committee. The committee held known unknowns: the size of its repo financing exposure, the haircuts the firm could absorb, the timing of credit-line drawdowns under stress. Each was tracked. Each had a number.

What the apparatus did not have: an exposure category for *the collapse of the short-term repo financing market itself*. The model assumed that liquidity would always be available at *some* price; the price was the variable being managed. The unknown unknown was the simultaneous disappearance of liquidity at every price. By the time the apparatus saw the event, the event had eaten the firm.

This chapter is about the asymmetry between those two failures. Tracking the price of an identified risk and missing the existence of an unidentified one are not the same problem. They require different kinds of work. Most organizations do the first; very few do the second; and the second is what the rest of the book is about.

## The core concept — the four cells, decomposed

The Rumsfeld taxonomy as commonly cited contains three quadrants: known knowns, known unknowns, unknown unknowns. The Johari window (Luft & Ingham, 1955) is structurally identical but with a fourth quadrant — **unknown knowns** — that the public Rumsfeld framing leaves out. The fourth quadrant matters. We will need it.

| | **Known to us** | **Not known to us** |
|---|---|---|
| **Identified as relevant** | *Known knowns:* the data and concepts we operate with. | *Known unknowns:* risks we've named but not yet quantified. |
| **Not yet identified as relevant** | *Unknown knowns:* facts we know but have not connected to the question. | *Unknown unknowns:* the structural surprises. |

Each cell is a different kind of work.

**Known knowns** are operational. The work is application: deploy the knowledge, monitor the system, repair when it breaks.

**Known unknowns** are managerial. The work is quantification: assign probabilities, estimate magnitudes, hedge or insure or accept. The standard risk-management literature (Power, *The Risk Management of Everything*, 2004) is built around this cell. It works. Most enterprise risk frameworks deliver real value here.

**Unknown knowns** are organizational. The work is connection: somebody in the company knows the thing; the question is whether the knowledge reaches the decision-maker who needs it. Slack channels full of warnings before deployments. Engineers who flagged the Challenger O-rings. The Boeing 737 MAX MCAS documentation that did not reach the pilots ([House Transportation Committee Report, September 2020](https://transportation.house.gov)). These are not unknown unknowns; they are unconnected knowns.

**Unknown unknowns** are epistemic. The work is conceptualization: nobody has yet formulated the question whose answer would be the risk. The mechanism is invisible because no one has drawn the diagram. The 2008 liquidity case sits here for the firms that genuinely had not represented "the repo market itself disappears" as a node in the model.

This chapter's central claim: *most "unknown unknowns" cited in post-mortems were actually unknown knowns or unmanaged known unknowns*. The genuinely unknown unknown — the structural surprise no one in the system had — is rarer than the management literature suggests. The first practical step is honest classification.

## Worked example — the Challenger O-rings as unknown known

On January 28, 1986, the Space Shuttle Challenger broke apart 73 seconds after launch. Seven crew members were killed. The cause was identified as the failure of the O-rings sealing the joints of the solid rocket boosters at the unusually low temperature of the launch (29°F at launch time).

The Presidential Commission (Rogers Commission, 1986) and later Diane Vaughan's *The Challenger Launch Decision* (1996) established that the O-ring vulnerability to cold was **known**. Engineers at Morton Thiokol had been documenting O-ring blow-by since at least 1985 and had argued, the night before launch, that the cold-weather conditions exceeded the qualified flight envelope. NASA management overruled them.

This is not an unknown unknown. The risk had a name, a documented history, and an internal advocate. What it didn't have: a structural pathway from the engineers' knowledge to the launch-decision authority that respected the warning. The information existed in the system; it did not reach the cell that could act on it. Vaughan's diagnosis is harder than "communication failure" — she argues that the *normalization of deviance* turned recurring out-of-spec events into evidence of robustness rather than evidence of vulnerability. The cognitive frame inside which the data was interpreted converted the warning into reassurance.

**The lesson:** When a post-mortem reports "we didn't know," ask whether nobody knew or whether the knower could not reach the decider. The work to fix each is different. For unknown knowns: structural changes in how information flows. For unknown unknowns: practices that surface what no one has yet formulated.

**The limit:** The two cells can co-occur. Some Challenger-class failures combine an unknown known (the engineer's warning) with an unknown unknown (the broader operational frame that made the warning legible only as exception). Disentangling them in real-time is harder than in retrospect.

## Common misconceptions

**"Unknown unknowns are mostly tail events."**
The Knightian distinction between risk and uncertainty (1921) does not map cleanly onto tail-event probability. A high-frequency mechanism can be an unknown unknown if nobody has represented it. The 2008 case was structural before it was tail. The chapter resists the conflation: tail events are about probability distributions; unknown unknowns are about model coverage.

**"Smart organizations don't have unknown unknowns."**
Kahneman's *Thinking, Fast and Slow* (2011) compiles the literature on how intelligence often functions as *post-hoc justification* of decisions made by faster cognitive systems [verify quotation]. Smart organizations are particularly prone to defensive reasoning (the subject of Chapter 5) — the smart story for why the absent variable was reasonable to omit becomes the story that closes the conversation. Smart can make the problem worse.

**"Unknown unknowns are just black swans."**
Taleb's Black Swan is observer-relative — an event the *observer's model* did not contain. This makes Black Swans a specific kind of unknown unknown: the kind that ruptures retrospectively obvious mechanisms. Many unknown unknowns are not catastrophic; they are slow-moving and visible only with the right reframe. The book's framework is broader than the Black Swan framework.

**"The fix is to add more items to the risk register."**
Risk registers operate in the *known unknown* cell. They cannot add an item whose category does not yet exist. Adding items to the register accelerates the conversion of known unknowns to managed risks. It does nothing for unknown unknowns. The two practices are not substitutes.

## Exercises

1. *(Apply)* Pull your organization's most recent risk register (or your team's most recent retrospective document). Classify each entry: known unknown (the risk has a name and a number), unknown known (someone in the organization knew this and the document is now reaching the decision-maker), or unknown unknown (the entry came from outside the prior conceptual map). Note the counts. The shape of the distribution is diagnostic.

2. *(Analyze)* Pick a recent organizational failure — yours or one in the public record. From the post-mortem, distinguish (a) the unknown knowns (signals that existed in the organization but did not reach the deciders), (b) the unmanaged known unknowns (named risks no one quantified), and (c) the unknown unknowns (the structural features genuinely absent from anyone's model). Quantify the rough proportions. Most failures are not what they look like in summary.

3. *(Create)* Draft a one-paragraph addition to your team's risk register designed to address *unknown knowns specifically*. The paragraph should specify a practice (not a list) that would let the unconnected knowledge in the organization reach the decision-maker. Test it against the Challenger case: would the practice you describe have changed the launch decision?

## What would change my mind

If the management literature on enterprise risk reliably converted unknown unknowns into managed risks at a higher rate than the unstructured baseline — i.e., if firms with formal risk frameworks were measurably less prone to structural failures than peers without them — the chapter's emphasis on the inadequacy of standard risk management for unknown unknowns would weaken. The available evidence (Power 2004; the post-2008 risk-management literature) is more skeptical than supportive, but a high-quality study showing the opposite would shift the chapter's framing toward *better risk frameworks* rather than *frameworks complementary to risk management*. As of writing the evidence does not support this revision.

## Still puzzling

- The line between *unknown known* and *unknown unknown* depends on what counts as "the organization knowing" something. If one engineer flagged the O-ring issue and was overruled, did the organization "know"? The cell boundary is not crisp in practice.
- The Rumsfeld taxonomy is famously asymmetric: there is no public articulation of the unknown-known cell from him. That asymmetry may be politically generative (it positions failures as epistemic rather than organizational). The Johari window's fourth cell is the more honest version.
- The book's downstream chapters lean on the unknown-knowns / unknown-unknowns distinction. Whether the distinction holds operationally — whether practitioners can reliably sort cases into the right cell — is an empirical question the chapter does not resolve.

---

*The taxonomy gives you the map. The next chapter introduces the formal tool for thinking about what makes one cell convert to another. **Chapter 3 — The Mechanism Question (Pearl).***
