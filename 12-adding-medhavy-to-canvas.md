# Chapter 12 — Adding Medhavy to Canvas: What Actually Changes

*The vendor demo shows the easy part. This chapter shows the rest.*

---

Every vendor demo of an LTI integration follows the same script. Click the button. The tool appears in Canvas. Students appear in the system. The demo ends. The audience nods. The proposal gets signed.

What the demo does not show is the six weeks of faculty time that make the tool do anything worth measuring. The LTI handshake — the technical integration between Canvas and Medhavy — takes two days of IT work. The curriculum design layer that makes the loop close takes ten to twelve weeks of institutional effort, most of it from people whose time is the most constrained resource the institution has. The demo inverts the actual cost structure, which is why this chapter exists.

The chapter's thesis in one sentence: the technology is the easy part, and the institutional work is what determines whether the loop closes or the dashboard sits unopened.

---

## What LTI actually does

LTI stands for Learning Tools Interoperability. It is a specification maintained by a nonprofit called 1EdTech that lets Canvas talk to an external tool like Medhavy securely and consistently. You do not need to understand the protocol to make a budget decision. You need to understand what it does, which is four things.

**Single sign-on.** When a student clicks the Medhavy link in Canvas, she does not log in again. Canvas signs a token that says *this is Maria, she is a student in Pharmacology 401, section 2*, Medhavy verifies the signature, and Maria lands inside Medhavy already authenticated. One click. No second password. No second account.

**Roster sync.** Medhavy receives the class list from Canvas automatically. When a student adds or drops the course, Medhavy knows within hours. The instructor does not maintain a parallel roster.

**Grade passback.** When Medhavy completes a graded interaction — a Quiz Me session that counts, a Glimmer assignment with a faculty-reviewed score — the grade flows into the Canvas gradebook automatically. The student sees a unified gradebook. The instructor does not transcribe scores between systems.

**Role awareness.** Canvas tells Medhavy whether the person clicking the link is a student, a teaching assistant, or an instructor. Medhavy shows the appropriate interface: students get the four modes; instructors get the GLP dashboard. Nothing is exposed to the wrong person.

The technical setup takes days. Your IT shop installs Medhavy as an LTI 1.3 external tool at the Canvas account level, configures the cryptographic handshake — a key exchange your IT staff has done many times for other tools — and the integration is functionally live. The principle is simple: Canvas vouches for the user, Medhavy trusts the vouch, grades flow back the same way.

That is the easy part.

Running in parallel with the IT install is the institutional approval process, which takes six to sixteen weeks depending on institution size and review backlog. The variation is real: a small private institution with a nimble IT governance structure can move in four to six weeks; a large public system with layered review committees runs eight to fourteen. The approval touches four gates: security review, which asks whether the vendor passes the institution's vendor questionnaire; data privacy review, which checks FERPA compliance plus whatever state laws apply to the student population; accessibility review, which verifies WCAG 2.1 AA compliance; and contract review, which is the standard legal pass through institutional counsel. Your IT shop has done this for every LTI tool in your Canvas instance — Top Hat, Lumen, OpenStax, Cengage MindTap. The process for Medhavy is identical. What is different about Medhavy is not the integration. It is what gets built on top of it.

<!-- → [TABLE: LTI integration timeline — two parallel tracks: IT install track (days 1–10, showing handshake, testing, live), Institutional review track (weeks 1–16, showing security, privacy, accessibility, contract gates, with typical durations and the note that these run in parallel not in sequence); reader should see that the bottleneck is institutional review, not technical setup] -->

---

## What changes for students

The student-facing change is the four-mode interface sitting inside Canvas where a textbook link used to be. It does not look like a revolution. It looks like a different button. What is different is what the button does.

Before Medhavy, a student in the pharmacology course reads the AI+1 chapter on Kindle, takes a Canvas quiz at the end of the module, and submits a written assignment. After Medhavy, she encounters the same concepts through a different shape. Ask AI is her first encounter with anything she has no schema for yet — beta blockade, before she knows what receptor blockade is. The session is not a chatbot conversation. It is a guided question-back that pushes her to articulate what she already knows before she receives anything new. The mechanism is the same Socratic forcing function that the best tutors use; the scale is the difference.

Quiz Me becomes a daily habit rather than an end-of-module event. Twelve minutes a morning. Spaced repetition scheduled by the FSRS algorithm, due-count counter visible at the top of the screen. The habit is the architecture; the algorithm is what makes the habit produce durable retention rather than just familiarity. By the second week, the student opens Quiz Me the way she opens her email — not because she decided to, but because it is now part of the morning pattern.

Case Study is the assignment that looks different from anything she has encountered before. A pre-written, faculty-reviewed clinical scenario: a forty-three-year-old patient presenting with symptoms consistent with three possible diagnoses, two of which contraindicate beta blockade. The AI facilitates discussion and never gives the answer. The student walks in with her concepts and walks out having deployed them under ambiguity, or aware that she couldn't. The distinction matters. The Case Study does not let her proceed without discovering which one is true.

Glimmer is the open-ended assignment with no single correct answer: design a clinical protocol for beta blockade in a novel patient context, defend every decision. The student does not know in week three that her Glimmer work will compile into a term project. The emergent structure is deliberate, and the reason it is deliberate is in Chapter 6.

The student does not need to understand any of this architecture. She experiences four buttons. The first day she gets a fifteen-minute orientation. By the second week she is using it without thinking about it, which is the goal. What does not change for her: she still logs into Canvas, still sees her gradebook there, still submits Canvas assignments for non-Medhavy work. Medhavy is added to her experience, not substituted for the LMS.

---

## What changes for instructors

The instructor-facing change is the GLP dashboard, and the change it requires is more cognitive than technical.

The Canvas gradebook tells the instructor four things per assignment: who submitted, when, what they scored, and whether the score meets the cutoff. The GLP dashboard tells her something different. For each student, for each concept, it shows the trajectory of the seven friction signals: temporal engagement, error trajectory coherence, cross-context transfer, uncertainty calibration, social knowledge texture, retrieval strength decay, and scaffolding response curve. The instructor does not need to remember all seven signals or track them manually. The dashboard summarizes them into a per-concept GLP score and flags the students whose behavioral pattern looks like borrowed certainty rather than genuine learning.

Here is the specific case the dashboard is built to surface. Maria scored 88% on the Canvas quiz. The GLP dashboard shows her temporal engagement collapsed on the second pass through the module, her retrieval strength is decaying steeply at seven days, and her scaffolding response curve looks more like full-answer dependency than partial-hint activation. The Canvas score looks fine. The learning trace does not.

What the instructor does with that divergence is the meta-modeling step. She is not asked to trust the GLP score over the Canvas grade. She is asked to combine them — the score from the artifact, the signal from the behavior, her own professional judgment from teaching and conversation — into a richer picture of where Maria actually is. The dashboard is not making the call. The instructor is. The dashboard surfaces the question.

This is where the cognitive change lives. An instructor who has spent a career treating the gradebook as the source of truth now has a parallel source that sometimes disagrees. The first time the two diverge it is uncomfortable. The third or fourth time it stops being uncomfortable and starts being useful — the instructor learns to read the divergence as information about the student rather than as a malfunction of one of the systems. That transition is not guaranteed. Educause surveys consistently find that thirty to fifty percent of newly-licensed edtech tools are used minimally or not at all. The binding constraint on willingness to act is not whether the institution can in principle act — it is whether the specific instructor whose section the data points to will open the dashboard in the first place.

---

## What the institution must actually provide

The institution provides three things, in roughly this order of difficulty.

The first is the concept map. Medhavy needs to know what concepts are in the course, in what order they are taught, which concepts are prerequisites for which, and which concepts get which modes. This is the institutional analog of what Wiggins and McTighe called backward design: you specify what counts as learned before you build the loop that measures whether it was learned. For a one-semester pharmacology course covering roughly two hundred concepts, the map typically requires three sessions of three hours each between the lead course instructor and an instructional designer, plus another five to ten hours of asynchronous revision. The instructor is the only person who can name what counts as a concept in her course. The designer's job is to structure her tacit knowledge into a graph Medhavy can use.

A note on AI-assisted map drafting: an AI can draft a concept map from a syllabus, and vendors sometimes suggest this as a labor-saving shortcut. Instructional designers who have tried it report that the review burden — going through the draft line by line, correcting the concept granularity, adjusting the prerequisite structure — runs roughly seventy percent of what from-scratch authoring would have taken. Useful. Not the labor-saver implied.

The second is faculty review for Case Study scenarios. Case Studies cannot be generated by AI without faculty review, because a plausible-sounding wrong clinical claim in a case scenario is a patient safety risk. The starter set is four to eight scenarios per term per course; each scenario takes a faculty author roughly four to six hours to draft and a second faculty reviewer one to two hours to audit. The numbers are not large. The constraint is calendar: getting two faculty members to commit four to eight hours each, before the term begins, is harder than it looks. Pharmacology programs that have done case-based learning before know this rhythm. Programs that have not done it before underestimate it the first time and estimate it correctly the second time.

The third is willingness to act with a named owner and budgeted time. Chapter 11 named this as the Q3 condition. Here it looks like a specific person — the department chair, the curriculum committee chair, the program director — whose calendar time is reserved for the redesign step that happens when the dashboard flags a section or a concept as underperforming. The willingness has to exist before the data does. Institutions that buy Medhavy and figure out the redesign owner later are the institutions that produce dashboards nobody opens.

<!-- → [TABLE: Three institutional requirements — columns: What it is, Who provides it, Typical time investment, What happens if it is missing — rows: concept map, case study faculty review, willingness to act — reader should see the time investment stacked against the LTI install time and understand where the real cost lives] -->

---

## What the institution does not need to provide

Equal in importance to what the institution must provide is what it does not. Institutions that understand both spend their energy correctly.

The institution does not need to understand the contextual bandit. The algorithm is the vendor's responsibility; the institution's responsibility is the inputs and the interpretation of outputs. The math is invisible to the user the same way the math behind Canvas's enrollment management is invisible to the registrar.

The institution does not need to retrain its faculty in pedagogy. The four modes are pedagogical instruments built on retrieval theory, transfer research, and clinical reasoning education. The instructor benefits from that theory without being asked to become an expert in it. She uses the dashboard. The dashboard is built on the pedagogy.

The institution does not need to replace Canvas. Medhavy lives inside Canvas. The gradebook is still Canvas's gradebook. Course administration — announcements, modules, discussion boards, calendar, grade exports — is still Canvas. Medhavy adds a layer on top of one component of the course experience and touches nothing else.

And the institution does not need to commit to program-wide adoption before piloting one course. The technology supports per-course adoption. The right shape for most institutions is one course, one term, real measurement, then expand if the measurement justifies it. Start where Q1 through Q3 are most clearly yes. Prove the loop closes. Then scale.

---

## One deployment, week by week

The pharmacology chair from Chapter 11's three-yes deployment is the worked example. She has decided to pilot Medhavy in one of her four sections — eighty students, her own section, deliberately, because she wanted the early adoption friction to land on her calendar before her two colleagues had to absorb it.

**Week zero.** She signs the proposal and sends the standard procurement packet to the institutional review office: HECVAT response from Medhavy, FERPA addendum, state data-privacy attestations, WCAG 2.1 AA documentation, contract draft.

**Weeks one through two — IT track.** Her IT shop installs Medhavy as an LTI 1.3 external tool at the Canvas account level. The cryptographic handshake takes one afternoon. The integration is technically live by end of week two, though no students will use it for another ten weeks.

**Weeks one through ten — institutional review track.** Security review, privacy review, accessibility review, contract review — running in parallel, not in sequence. Her institution is a mid-size public university. Security review takes six weeks. Privacy review takes four weeks, plus one extra for a data-residency question about out-of-state students. Accessibility review takes three weeks. Contract review takes two weeks. Security review is the pacing item. By week ten, all gates are cleared.

**Weeks three through eight — concept map.** Three sessions of three hours each, plus four hours of asynchronous revision. The chair maps the first six weeks of the pharmacology curriculum to roughly seventy-five concepts, names the prerequisite graph — receptor pharmacology before drug class behavior, pharmacokinetics before dosing decisions — and assigns modes. Ask AI as the entry mode for unfamiliar concepts. Quiz Me as the daily habit for receptor names and drug classifications. Case Study and Glimmer reserved for the second half of the term, when students have built enough schema to deploy under ambiguity.

**Weeks six through eight — case study authoring.** The chair drafts four starter Case Studies, four hours each. Her most senior colleague reviews each one, two hours each. Two of the four come back with revisions — one for a slightly outdated dosing range, one for a scenario that was ambiguous in the wrong way. Revised cases finalized by end of week eight.

**Week eleven — student onboarding.** The term began the week before in Canvas. Medhavy is activated for students in week eleven. The chair spends fifteen minutes in the first lab walking students through the four modes. Students leave with access. Quiz Me daily habits begin forming by end of the week.

**Week twelve — first data.** Two weeks of student use produces enough signal for the GLP dashboard to populate. The chair sees per-student trajectories for the first set of concepts. She sees patterns the Canvas gradebook had not shown her: one student with high quiz scores but rapidly decaying retrieval strength, three students whose temporal engagement looks like genuine processing on harder concepts and like skimming on easier ones, one student whose scaffolding response curve suggests genuine partial understanding — a partial hint activates a complete answer, which is the Chapter 8 signal for a learner who is almost there.

She did not know any of this was visible until the end of week twelve. The Canvas gradebook had told her these students were performing between 84 and 92 percent. The dashboard told her something different. Whether she acts on the difference is what the next twelve weeks will test.

<!-- → [INFOGRAPHIC: Week-by-week timeline for the pharmacology pilot — two swim lanes (IT/institutional review track and curriculum design track) running in parallel from week 0 to week 12, with milestones marked: LTI live (week 2), review cleared (week 10), concept map finalized (week 8), cases finalized (week 8), students onboarded (week 11), first GLP data (week 12) — reader should see the total time from decision to first data and understand which track determines the pacing] -->

Total institutional investment across all tracks: roughly eighty hours of faculty time, thirty hours of instructional designer time, six hours of IT time, twenty hours of institutional review across security, privacy, accessibility, and legal. The license fee is the smallest line. The faculty time is the largest. The willingness to act has no line item and is the gating condition on everything that follows.

---

## What would change my mind

Two conditions would shift the chapter's estimates enough to matter.

If AI-assisted concept-map drafting improved to the point where faculty review took twenty percent of authoring time rather than seventy, the concept-map step would shrink from three sessions of three hours to roughly one session of two hours with revisions. Total institutional time would drop by a third, and the Q1 scale threshold from Chapter 11 might soften — smaller deployments could become viable earlier. Whether AI tools can reach that quality threshold is an empirical question the experienced instructional designers whose work I have read remain skeptical about. The question is not settled.

If institutional review processes for AI-enabled tools became standardized across higher education — a shared AI-specific vendor questionnaire, common state-law compliance frameworks, shared accessibility attestations — the eight-to-sixteen-week parallel review track could compress to four weeks. Educause is working in that direction. If it succeeds, the chapter's pacing changes in ways that matter for deployment planning. Neither has happened yet. Either could. If either does, this chapter gets rewritten first.

---

## LLM Exercises

**Exercise 1 (Apply) — Identify your most likely early adopter.** Pick the single faculty member in your program most likely to volunteer for a Medhavy pilot. Write three sentences describing why — what about her course, her teaching style, or her institutional position makes her the right first volunteer. Then write what she would need from you: the calendar time you would need to clear, the instructional designer support you would need to staff, the political cover you would need to provide. If you cannot name a specific person, that is information about Q3.

**Exercise 2 (Apply) — Map your institutional approval process.** Sketch the approval gates a new LTI tool would go through at your institution. Who runs security review, and what is their typical turnaround? Who runs privacy review, and which state laws apply to your student population? Who runs accessibility review? Who signs the contract? What does each gate's queue look like right now? The output is a timeline estimate from "decision to add" to "approval complete." Compare it to the pharmacology worked example's ten-week pacing.

**Exercise 3 (Evaluate) — Is the realistic timeline acceptable?** Take your timeline from Exercise 2 and add the parallel curriculum-design timeline — six to ten weeks for the concept map and case authoring, depending on your faculty's case-based learning experience. From the day the decision is made to the day the first student is in the loop, what is the realistic total? If the deployment is accreditation-driven and the next review is nine months away, twelve weeks of setup is fine. If the problem needs solving by the end of this term, the timeline may not fit — and the right move is to start the institutional review now and adopt next term rather than to compress a process that does not compress.
