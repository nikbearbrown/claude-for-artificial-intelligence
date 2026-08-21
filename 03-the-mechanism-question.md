# Chapter 3 — The Mechanism Question

> *Why correlation cannot tell you what intervention will do — and what Judea Pearl's framework adds to the unknown-unknowns problem.*

---

## Learning objectives

1. *(Understand)* State the three rungs of Pearl's ladder of causation in plain language and name a question each rung answers that the rung below cannot.
2. *(Analyze)* Read a causal diagram (a directed acyclic graph) and distinguish a *confounder* from a *collider* by their structural role, not just their position.
3. *(Apply)* Take a real-world causal claim and identify what kind of evidence — observation, intervention, counterfactual — would be required to defend it.
4. *(Evaluate)* Decide whether a given study's design supports a causal claim or only an associational one, and explain the difference structurally.

## Opening case — John Snow's pump handle

In late August 1854, a cholera outbreak in the Soho district of London killed approximately 600 people in two weeks. The dominant theory at the time was the *miasma theory* — that cholera was carried by foul air. Within the miasma framework, the data supported the theory: cholera struck densely-populated unsanitary areas where bad smells were thickest. The correlation was real.

John Snow (1813–1858), a physician with a different working hypothesis, walked the streets, mapped each death, and identified a cluster around the Broad Street water pump. He did not have a germ theory of disease — the microbial agent of cholera (*Vibrio cholerae*) was not isolated until Robert Koch's work in 1883–84. But Snow had something the miasma theorists did not: a model in which the *mechanism of transmission* was waterborne, and a prediction that intervening on the water supply would change the outcome.

On September 8, 1854, Snow persuaded the local Board of Guardians to remove the pump handle. The outbreak's continued decline cannot be cleanly attributed to the intervention — the outbreak was already declining when the handle was removed — but Snow's broader case, including the dual-water-company natural experiment he ran in 1855, established the waterborne mechanism years before the agent itself was identified.

This case is canonical in Pearl's framework because Snow had what the miasma theorists did not: an **intervention-level** understanding of cause. He did not just observe correlation. He proposed a structural model and made a falsifiable claim about what would happen if you broke a specific link in it. The cholera case is the prototype the rest of the chapter unpacks.

## The core concept — three rungs

Judea Pearl's *The Book of Why* (2018, with Dana Mackenzie) organizes causal reasoning into a three-rung ladder. Each rung answers a kind of question; each rung requires evidence the rung below cannot supply.

**Rung 1 — Association.** *What is correlated with what?* This is the rung statistics has traditionally lived on. Given a dataset, what patterns of co-occurrence exist? Most of the techniques taught in introductory statistics — correlation, regression, machine-learning predictions — operate here. The cholera death map is rung 1 data. So is every customer-behavior dataset, every clinical-trial-without-randomization, every credit-risk scoring system trained on observational data.

What rung 1 cannot tell you: what happens if you *intervene*.

**Rung 2 — Intervention.** *What happens if I change X?* This is the question randomized experiments are designed to answer. By assigning treatment randomly, the experimenter cuts every prior pathway through which X could be associated with the outcome — every confounder is broken by the random assignment — and the observed difference becomes attributable to the intervention.

Snow's pump-handle removal is a rung-2 act. He did not predict the outcome from association alone; he predicted it from his hypothesized mechanism. The miasma theorists' framework had no equivalent intervention prediction. Their model said "clean the air"; Snow's said "block the water." Both interventions could be tried; only one was specific to the mechanism.

**Rung 3 — Counterfactual.** *What would have happened to this specific patient, this specific firm, this specific election if the intervention had been different?* This is the rung policy and personal decision-making actually need. Did this drug cause this person's recovery? Did this hire decision cause this team's success? The data alone — observational or experimental — cannot answer rung-3 questions about individual cases. They require a model that lets you reason about parallel worlds.

The unknown-unknowns connection: the turkey lived on rung 1. The butcher lived on rungs 2 and 3 — he could simulate the counterfactual *if I delayed slaughter, what would the price be?* and act on it. Climbing the ladder requires knowledge that does not live in the data alone.

## The confounder, the collider, and the causal diagram

The chapter's most useful technical tool is the **directed acyclic graph** (DAG) — a diagram in which variables are nodes and arrows represent causal effects.

Consider three variables: X (a candidate cause), Y (an outcome), and Z (a third variable).

A **confounder** is a Z that causes both X and Y: `X ← Z → Y`. If you observe a correlation between X and Y without controlling for Z, you can be misled. Z is producing the correlation. The classic example: ice cream sales and drowning rates are correlated. Both are caused by warm weather. The fix: control for Z.

A **collider** is a Z that is caused by both X and Y: `X → Z ← Y`. Here the situation reverses. If you observe a correlation between X and Y *without* conditioning on Z, you see the true relationship (which may be zero). If you condition on Z, you *create* a spurious correlation. The classic example: among hospitalized patients, two unrelated diseases can appear correlated because being hospitalized for one of them increases the chance of being noticed for the other.

The structural identical-looking diagrams produce opposite conditioning rules. Pearl's contribution is the framework that tells you which is which from the diagram's structure.

For the unknown-unknowns problem this matters specifically: many post-mortems of organizational failures invoke "common cause" or "the system itself" as the explanation. Some of those invocations are accurate (a confounder was driving both the observed pattern and the failure). Some are not (a collider relationship makes the pattern look causal when it isn't). Distinguishing them is rung-2 work.

## Worked example — Simpson's paradox at a graduate school

In 1973, the University of California, Berkeley faced a sex-discrimination lawsuit over graduate-admission rates: 44% of male applicants were admitted vs. 35% of female applicants. The aggregate appeared discriminatory.

When P. J. Bickel, E. A. Hammel, and J. W. O'Connell investigated department-by-department (published *Science*, 1975), the pattern flipped. Most departments admitted women at *higher* rates than men. The aggregate-level discrimination was a **Simpson's paradox** (Simpson, *Journal of the Royal Statistical Society B*, 1951) — produced by the fact that women applied disproportionately to harder-to-enter departments. Department admission rate was the confounding variable.

The causal diagram: `Sex → Department → Admission`. The aggregate `Sex ↔ Admission` correlation is non-causal. Conditioning on Department reveals the within-department relationship.

What this case demonstrates: the same data supports opposite conclusions depending on which causal diagram you bring to it. The numbers do not select between diagrams. Domain knowledge does. The Berkeley investigators had to ask *why* women applied to harder departments — a separate causal question outside the admission data — to decide which diagram was more defensible.

**The lesson:** Aggregate correlations and within-stratum correlations can disagree. The correct conclusion depends on which causal structure produced the data. Rung 1 cannot resolve the disagreement; rung 2 reasoning can.

**The limit:** Even within rung 2, the right answer depends on whether the assumed DAG is correct. Pearl's framework is honest about this: it tells you what conclusions follow *given* a causal model, not what the correct model is. The work of selecting the right model is the irreducibly human part. The chapter returns to this in Chapter 10.

## Common misconceptions

**"Correlation does not imply causation — but it can support it."**
This is the standard teaching. It is true but incomplete. The Pearl framework's contribution is that correlation can be *consistent* with multiple causal structures (including ones with no direct causal effect at all), and that distinguishing among them requires reasoning the data cannot supply alone. The slogan needs the upgrade.

**"Randomized experiments solve causality."**
Randomization solves the rung-1-to-rung-2 problem under specific conditions: a population that doesn't change between treatment and outcome, no spillover between treated and untreated units, no non-compliance with assignment. Many real-world questions don't meet these conditions. The rung-2 toolkit extends well beyond random assignment.

**"Causality is unknowable without experiments."**
Wrong in both directions. Sometimes experiments are unethical or impossible (you cannot randomize sex, race, or country-of-birth) but causal claims can still be defended using natural experiments, instrumental variables, or structural reasoning. And sometimes experiments produce results that don't generalize because the experimental context differs from the deployment context.

**"DAGs are just diagrams."**
The diagrams are structurally constrained. Each arrow encodes a specific testable claim. Conditioning rules follow from the structure mechanically (Pearl, *Causality*, 2nd ed. 2009). The diagrams are not informal sketches; they are formal objects that produce specific predictions.

## Exercises

1. *(Understand)* Take a recent media article reporting a correlation as a cause (e.g., "people who eat breakfast are healthier"). Draw the simplest DAG consistent with both the reported finding and a plausible confounder. Name the confounder explicitly.

2. *(Apply)* Identify a study (academic, journalistic, or organizational) whose conclusion you have accepted. Determine which rung of Pearl's ladder its evidence supports. If the conclusion claims more than the evidence supports — which is common — articulate the gap.

3. *(Evaluate)* Take a current causal claim from your own work or domain. Specify what evidence at rung 2 (intervention) would be needed to defend it. Specify whether that evidence is obtainable in your context. If not, state honestly what the strongest defensible version of the claim would be.

## What would change my mind

If a large-scale meta-analysis of causal-inference applications showed that the rung-1 / rung-2 distinction did not improve outcomes — that practitioners who used Pearl's framework produced no more reliable causal conclusions than practitioners using standard statistical methods — the chapter's emphasis on Pearl's framework would weaken. The available evidence (Pearl & Mackenzie 2018; the broader causal-inference literature; Hernán & Robins, *Causal Inference: What If*, 2020) is supportive but not conclusive at the methodological-comparison level.

## Still puzzling

- The DAG approach assumes the analyst can write down the correct causal structure. In domains with sparse mechanism knowledge — much of social science, much of organizational decision-making — the DAG is itself the thing under dispute. The framework specifies what conclusions follow *given* a DAG; it does not specify how to find the right DAG. The chapter does not resolve this.
- Pearl's framework operates at the level of populations and counterfactuals about individuals. The bridge from population-level evidence to individual-level decisions remains technically delicate and theoretically contested.
- The relationship between Pearl's rung 2 and Goldratt's identified bottleneck (Chapter 4) is suggestive: both isolate a single point of intervention. Whether the two frameworks are formally compatible is an open question the synthesis chapter returns to.

---

*Pearl gives you the framework for asking *what is the mechanism*. The next chapter introduces a domain in which the mechanism is structural and almost always invisible to local actors. **Chapter 4 — The Constraint You Can't See (Goldratt).***
