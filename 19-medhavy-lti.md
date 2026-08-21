# Chapter 19 — Medhavy: the AI-Tutor Layer via LTI

*The Canvas course is the map. Medhavy is the conversation that happens when the student walks into the territory.*

---

Tuesday afternoon. A student in your course opens Canvas and navigates to the module for Chapter 4. The items in the module are familiar — a page, a quiz, a case study, a link labeled "Chapter 4 Tutor." She clicks the link. A new tab opens. She does not see a login screen. She does not see "create an account." She is already inside Medhavy, already authenticated, and the tutor already knows she is in your course, on Chapter 4, having completed Chapters 1 through 3. The tutor's first message is not "Hi! I'm an AI tutor. What would you like to learn today?" It is specific to where she is in the arc of the book.

That seamless entry — clicking a link in Canvas and landing inside a fully-contextualized AI tutoring session without a second login — is LTI 1.3 doing the work you cannot do by hand.

This chapter is different from Chapters 16, 17, and 18.

Say that again plainly, because it matters: this chapter describes the one deployment target in Part 2 that you cannot build and ship yourself. Chapter 16 asked you to run a script that produced an `.apkg` file. Chapter 17 asked you to run a script that produced a `.imscc` package you could upload to Canvas. Chapter 18 asked you to run a script that scaffolded a React site you could deploy to Vercel. Each of those chapters ended with you holding an artifact you made.

Chapter 19 ends with a conversation — a specification you hand to a developer and to your institution. Medhavy is a separately hosted system. LTI 1.3 is a protocol that requires registration with your institution's Canvas administrator. The connection between Canvas and Medhavy involves a FERPA review, an IT security review, and institutional approval that no script can automate. This chapter teaches you what is being built and why, so that you can specify it accurately and evaluate it honestly when it is done. You will not build it alone.

---

## What LTI 1.3 Actually Is

LTI stands for Learning Tools Interoperability. It is the standard protocol for connecting an external tool — Medhavy — to a learning management system — Canvas — in a way that is authenticated, authorized, and privacy-aware. Version 1.3, published by the IMS Global Learning Consortium (now 1EdTech), replaced the earlier shared-secret model with an OAuth 2.0-based OIDC flow. [^ims]

The mechanism matters enough to name even if you never touch the code. When the student clicks the Medhavy link in Canvas, Canvas does not simply redirect her to a URL. It initiates an OIDC login flow: Canvas passes a signed JWT — a JSON Web Token — to Medhavy's login endpoint, containing claims about who the user is, which course she is in, which assignment or module item she clicked, and what role she holds (student, instructor, TA). Medhavy verifies the JWT's signature against Canvas's published JWKS (JSON Web Key Set), then completes the handshake. The whole exchange takes less than a second. The student sees none of it. She just lands.

What this means for you as an author-instructor: no separate Medhavy account creation, no password for students to manage, no copy-paste of enrollment data. Canvas is the identity provider. Medhavy trusts it.

Three sub-protocols extend base LTI 1.3 and together make Medhavy's deeper integrations possible. These are called LTI Advantage services. You do not implement them; you specify that your deployment should use them.

**Names and Role Provisioning Services (NRPS)** lets Medhavy pull the current course roster from Canvas — names, roles, enrollment status — without you exporting a CSV. This is how the Medhavy analytics dashboard knows who is and is not engaging with the tutor, and how an instructor can see which students have completed which activities.

**Deep Linking** lets Medhavy offer a content picker inside Canvas's module editor. When you build a Canvas module and want to add a Medhavy chapter tutor, a Medhavy formative activity, or a Medhavy assessment, you click "Add External Tool," select Medhavy, and a picker opens. You choose the item. Canvas stores the link. Deep Linking is what makes it possible to add Medhavy items to Canvas without hard-coding URLs by hand.

**Assignment and Grade Services (AGS)** lets Medhavy write grade and completion data back to the Canvas gradebook. When a student finishes a Medhavy activity, Medhavy posts a score or a completion status to Canvas through AGS, and it appears in the gradebook as if the student had submitted a Canvas quiz. This is how the two systems share a record without duplicating it.

[^ims]: IMS Global Learning Consortium (now 1EdTech). *IMS LTI 1.3 and LTI Advantage Implementation Guide*, Version 1.0. 1edtech.org/activity/learning-tools-interoperability.

---

## The System-of-Record Split

Canvas and Medhavy are not competing records of the same thing. They are authoritative records of different things. Getting this split clear is the architectural decision that prevents future confusion.

**Canvas owns:** enrollment, the official gradebook, assignment deadlines, course communications, institutional identity.

**Medhavy owns:** AI-tutor interaction history, learning activity within the textbook, chapter-level reading progress, formative activity attempts, learning analytics at the session and course level.

When a student completes a Medhavy activity, AGS writes a line-item score to Canvas. Canvas stores the grade as a Canvas grade. Medhavy stores the full interaction — what the student asked, what the tutor said, how many attempts, where comprehension appeared to break down — in its own database, governed by its own privacy policy.

This split has a practical consequence for you as an instructor: you will look at Canvas for the gradebook picture and look at the Medhavy analytics dashboard for the learning picture. A student can have a complete gradebook record in Canvas and an empty interaction record in Medhavy (she submitted answers but never opened the tutor). A student can have a rich tutor interaction record in Medhavy and an incomplete gradebook record in Canvas (she spent three hours with the tutor but didn't finish the graded activity). Both views are true. Neither is the full picture alone.

The temptation to collapse this into one system — to build a custom Canvas API integration that reads Medhavy data into Canvas columns, or to route everything through Medhavy's database and abandon the Canvas gradebook — is real and worth resisting. The reason LTI 1.3 + LTI Advantage exists is precisely to let two well-maintained systems talk without either one becoming the whole system. The standard-path recommendation: use LTI 1.3 + LTI Advantage as the integration standard. Do not build a custom Canvas API integration first unless your institution's IT department refuses LTI registration. Custom integrations age badly; LTI registrations are maintained.

---

## What Medhavy Adds to the Canvas Course

The Canvas course you produced in Chapter 17 is a complete, self-contained learning environment. Quizzes run natively in Canvas. Pages carry the chapter content. Cases and glimmers live as Canvas assignments. That course works without Medhavy.

Medhavy adds a layer the Canvas `.imscc` package cannot carry: a tutor that knows the whole course and remembers the individual student across sessions.

Four specific additions, named at the level of specification rather than implementation:

**Course memory.** The AI tutor's context is not a single conversation. It is scoped to the course. When a student asks the tutor about a concept in Chapter 7, the tutor knows she struggled with the prerequisite in Chapter 4. When she returns to the tutor the following week, the conversation resumes with that history intact. The Canvas course has no mechanism for this — it can track completion states, not comprehension trajectories.

**Formative activities.** Beyond the quizzes the Canvas course carries, Medhavy can host tutor-led formative activities — Socratic prompts, structured problem-solving sequences, case interrogation sessions — that the AI facilitates and scores. These write their completions back to Canvas through AGS. They are not chat sessions. They are pedagogically structured interactions with defined outcomes.

**Learning analytics.** The Medhavy instructor dashboard shows engagement at a level the Canvas gradebook does not: time-on-tutor per chapter, which questions students ask most often, where conversations break down, which students have not interacted with the tutor at all. This is formative data for the instructor's next session, not just summative grades.

**Contextual launch.** Because every launch carries a signed JWT with course and chapter context, the tutor can open at the right place in the book for the student's current position. A student clicking the tutor link from the Chapter 9 module does not get a generic opening. The tutor has the Chapter 9 context loaded from the first message.

None of these are magic. Each one requires configuration — course materials imported into Medhavy's context, activity templates defined by you, analytics dashboards set up for the course. The Medhavy onboarding sequence (documented in Appendix 96 and in the Medhavy System Design Document, forthcoming) walks through this configuration. The point here is not the implementation. It is the capability: the Canvas course carries the structure; Medhavy carries the conversation.

---

## The Institutional Gate

Here is the honest accounting of what stands between you and a live Medhavy integration: not code, but process. Three gates, in order.

**LTI Registration.** To connect Medhavy to your institution's Canvas instance, someone with Canvas Administrator access must register Medhavy as a Developer Key in Canvas's administrative panel. This is not a step you can perform as an instructor. It requires your institution's LMS administrator or IT department. At Northeastern, this means the Canvas admin team and may involve a departmental request process. The registration requires: Medhavy's OIDC login URL, its redirect URI, its JWKS URL, its target link URI, and configuration of Deep Linking placement options. Appendix 96 carries the full checklist your developer and IT admin will need.

**FERPA and Privacy Review.** Student interaction data — what questions a student asks, which concepts they struggle with, their tutor conversation history — falls under FERPA. Before any student data flows into Medhavy, your institution's privacy office needs to review Medhavy's data processing agreement, confirm that Medhavy operates as a FERPA-covered School Official under the appropriate contractual conditions, and sign off on the integration. This is not optional or informal. It is a condition of any LTI integration that handles student personally identifiable information.

**Security Review.** Most institutional Canvas environments require a security review of any external LTI tool before registration. This typically includes a review of Medhavy's infrastructure (hosting environment, data residency, encryption at rest and in transit), an assessment of the OIDC flow and JWT handling, and confirmation of the institution's data deletion and retention policies. Timeline varies by institution; at many universities this process takes four to eight weeks. Plan accordingly.

The three gates are sequential in practice: security review often informs the privacy review, which must complete before the LTI registration goes live for student-facing use.

What this means for your timeline: if you want Medhavy in your next course section, initiate the institutional process this term, not the week before the course opens. The process is not hostile — it exists to protect your students — but it is not fast.

---

## What You Hand Off

The hand-off from author-instructor to developer and institution has two deliverables.

The first is a specification: what you want Medhavy to do in your course. Which chapters have tutor access points? Which activities should write grades back to Canvas? What completion criteria should AGS use? What should the analytics dashboard surface for you as an instructor? The Medhavy SDD (System Design Document, forthcoming) provides the template for this specification.

The second is Appendix 96: the developer-facing LTI 1.3 setup sequence. Hand this to the developer standing up the Medhavy integration. Hand the institutional-gate section to your Canvas admin and privacy office as the starting point for their review. Neither document replaces the Medhavy onboarding process; both make the handoff concrete enough to move.

One trade-off to name explicitly. LTI 1.3 is the right integration path because it is the standard, because Canvas supports it natively, because the IMS Learning Consortium maintains it, and because an LTI-registered tool can be reused across courses without repeating the security review. A custom Canvas API integration — using Canvas's REST API directly, bypassing LTI — seems faster at first. It is not. Canvas API tokens are scoped to individual users, not institutional tools. Token rotation, rate limiting, and Canvas API versioning all become your maintenance burden. LTI registration is a one-time institutional process. Custom API integration is an indefinite maintenance contract. The recommendation stands: LTI 1.3 + LTI Advantage first. Everything else only if that path is genuinely closed.

---

## The Student's Experience, End to End

Walk through the complete student experience once, concretely, so you can describe it to your developer.

The student is enrolled in your Canvas course. She opens the Chapter 4 module. She sees a Canvas module item with a custom icon and the label "Chapter 4 Tutor — Medhavy." She clicks it. Canvas initiates the OIDC launch in the background: it sends a signed JWT to Medhavy's login endpoint containing her Canvas user ID, her course ID, the LTI resource link ID of the item she clicked, her role (student), and the context title. Medhavy verifies the JWT signature against Canvas's JWKS, looks up or creates her Medhavy account using the Canvas sub claim as the stable identifier, and loads her tutor session with the Chapter 4 context. The new tab presents the Medhavy tutor interface with a contextual opening message. No login prompt. No account creation form.

She works with the tutor for twenty minutes. She completes a structured Medhavy activity. Medhavy posts a completion score to Canvas through AGS — the line item you configured appears in the Canvas gradebook as a submitted assignment. She closes the tab. She is back in Canvas.

Next week she clicks the same link again. Medhavy's session history means the tutor knows what she worked on last week. The conversation does not restart from zero.

The instructor opens the Medhavy analytics dashboard and sees which students have opened the Chapter 4 tutor, how long they spent, and which concepts generated the most questions. She does not need to export a report from Canvas. She logs into Medhavy directly (as an instructor, also via LTI) and reads the dashboard.

That is the complete system working. Every step in the sequence is named in the developer checklist in Appendix 96.

---

## What Would Change This Chapter

Two things could make a later edition of this chapter substantially different.

First: if 1EdTech releases LTI 2.0 or a significant revision to LTI Advantage, the protocol details here would need updating. The architecture — two well-maintained systems connected by a standard — would not change. The specific claim counts, token structures, and service endpoint contracts might. [verify — LTI Advantage specifications as of current 1EdTech release]

Second: if Medhavy develops a direct import path that does not require institutional LTI registration — for example, a standalone hosted mode where the author provides course context through an API rather than through Canvas LTI — then this chapter's gated status changes. That path does not exist as of this writing. If it does when you read this, treat the institutional gate section as a description of the full-integration path, not the only path.

The fluency trap the student faces in Chapter 20 — asking the AI to explain things rather than interrogating her own understanding — has a structural echo here. The author who reads this chapter and thinks "I'll just build something myself" is falling into the same trap: using the available tools rather than the right ones. LTI 1.3 is harder to stand up than a custom Canvas API script. It is the right tool. The difficulty is the cost of doing it properly, not evidence you should do it differently.

---

## AI Wayback Machine — Vint Cerf

> **Prompt to run in Claude or ChatGPT:**
>
> "Explain how Vint Cerf and Bob Kahn's 1974 paper 'A Protocol for Packet Network Intercommunication' established the principle that drove TCP/IP: two networks connected by a standard protocol do not need to know each other's internal architecture. Then apply that same principle to LTI 1.3: Canvas and Medhavy are both 'networks' in this sense. What does the analogy reveal about why a standard connection protocol is preferable to a custom integration? Where does the analogy break down?"

Cerf and Kahn's insight — that the protocol should sit between systems rather than inside either one — is the same insight that makes LTI 1.3 work. Canvas does not need to understand how Medhavy stores tutor interaction data. Medhavy does not need to understand how Canvas manages enrollment. The JWT at the boundary carries exactly what both sides need and nothing else. The systems remain independent; the standard connection is what coordinates them.

The analogy breaks down where it always does: TCP/IP is stateless; LTI launches carry state (the course context, the user identity, the resource link). But the architectural principle holds. Two systems, one standard, minimal coupling.

---

## Exercises

**Exercise 19.1 (Understand).** Write a one-paragraph plain-language description of what happens between the moment a student clicks a Medhavy link in Canvas and the moment she sees the tutor interface. Use no technical acronyms; explain the mechanism as if to a department chair who is deciding whether to approve the integration. The description should accurately name the three things Canvas sends to Medhavy (identity, course context, role) without using the words JWT, OIDC, or JWKS.

**Deliverable:** A one-paragraph description.

**Exercise 19.2 (Analyze).** Map the system-of-record split for your own course. Create a two-column table with the headers "Canvas owns" and "Medhavy owns." Populate it for a specific course you teach or plan to teach, going beyond the generic examples in this chapter — name the specific assignments, grade items, and analytics questions that belong on each side. Where the split is genuinely unclear, note it and explain why.

**Deliverable:** A two-column table with at least five items per column and a note for any ambiguous items.

**Exercise 19.3 (Apply).** Draft the institutional hand-off email for your course — the email you would send to your institution's Canvas administrator to initiate the LTI registration process. The email should name the three gates (LTI registration, FERPA review, security review) and ask the right opening questions: who owns each gate, what the expected timeline is, and what documentation the admin needs from the Medhavy side to begin. Do not invent the answers. Identify the questions.

**Deliverable:** A draft email of 200–300 words.

**Exercise 19.4 (Evaluate).** You are advising a colleague who wants to skip the institutional LTI registration and instead use Canvas's REST API to sync enrollment data into Medhavy manually every week. Identify three specific costs of that approach — one technical, one administrative, one related to student data governance — and compare them to the three gates of the LTI registration path. State which path you recommend for a two-semester pilot course and which for a permanent department-wide deployment, and explain why the answers might differ.

**Deliverable:** A 300-word comparative analysis with a clear recommendation for each scenario.

---

## Bridge — Chapter 20

Chapter 19 ends with a hand-off. Chapter 20 closes the loop that Chapter 1 opened.

The fluency trap is not only an author's problem. The student sitting across from the Medhavy tutor faces it too — the temptation to ask the AI to explain rather than to think, to extract rather than to interrogate. Chapter 20 is about what it means to deploy the Ask-AI loop everywhere the student encounters the book — in Medhavy, in Canvas, in the Kindle version, on the React site — and to design those encounters so that they resist the fluency trap rather than deepen it.

The student who clicks the Medhavy link in Chapter 4 and does the thinking the tutor structures has acquired something. The student who clicks it and reads the tutor's explanations without pushing back has acquired fluency. Chapter 1 named the difference. Chapter 20 is the designer's answer to it, on the student's side of the desk.

---

## References

1. IMS Global Learning Consortium (now 1EdTech). *IMS LTI 1.3 Core Specification*, Version 1.0 Final. https://www.imsglobal.org/spec/lti/v1p3/
2. 1EdTech. *LTI Advantage: Names and Role Provisioning Services (NRPS) Specification*, Version 2.0. https://www.imsglobal.org/spec/lti-nrps/v2p0
3. 1EdTech. *LTI Advantage: Assignment and Grade Services (AGS) Specification*, Version 2.0. https://www.imsglobal.org/spec/lti-ags/v2p0
4. 1EdTech. *LTI Advantage: Deep Linking Specification*, Version 2.0. https://www.imsglobal.org/spec/lti-dl/v2p0
5. IETF / OpenID Foundation. *OpenID Connect Core 1.0*. https://openid.net/specs/openid-connect-core-1_0.html
6. U.S. Department of Education. *Family Educational Rights and Privacy Act (FERPA)*. https://www.ed.gov/ferpa
7. Cerf, V., & Kahn, R. (1974). A protocol for packet network intercommunication. *IEEE Transactions on Communications*, 22(5), 637–648.
8. Appendix 96 — Medhavy LTI 1.3 Setup Guide. See `96-appendix-medhavy-lti.md`.
