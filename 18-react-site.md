# Chapter 18 — The React Site: .mdx + .tsx

*One Python command makes the scaffold. Everything after that is someone else's job — and being honest about that boundary is the point.*

---

It is Thursday morning. You have a finished book: forty-one chapter and appendix files in `chapters/`, clean builds, a Kindle edition live on KDP. You also have a collaborator — a developer friend, a hired contractor, a student TA who knows React — who asked, two weeks ago, what it would take to put the book online. "Send me a Next.js app," she said, "and I can have it deployed in an afternoon."

You have been putting off the answer because you assumed the answer was complicated. It turns out the answer is one command:

```
python3 build-react-site.py
```

You run it from your book's root directory. It takes a few seconds. When the terminal settles, a new folder called `site/` exists alongside your `chapters/` folder. Inside it: 89 files. Forty-one `.mdx` files, one per chapter. Forty-one `.tsx` route components. A table-of-contents home page. A shared layout. A component called `AskAI.tsx` that is not wired to a model yet but knows exactly where it needs to go. Valid JSON configs for Next.js and TypeScript.

You compress `site/` into a zip file and send it to your developer. She unpacks it, types `npm install && next build`, and the book is on the web.

That is this chapter. What the script does, what the scaffold gives your student, what to hand your developer, and where the boundary is between what you can finish alone and what you cannot. This is, of all the Part 2 chapters, the most honest one about hand-offs. The web surface is the most flexible and most public surface the pipeline produces. It is also the only one you cannot fully ship alone.

---

## What the scaffold is — and what it is not

Before the mechanism, a frame. Every output this pipeline produces starts from the same source: your `chapters/*.md` files. That is the single source of truth. The EPUB and PDF in Chapter 12 are build artifacts. The Canvas course package in Chapter 17 is a build artifact. The Anki deck in Chapter 16 is a build artifact. The React site is a build artifact. You do not maintain seven parallel versions of your book. You maintain one source and run scripts.

The React site build introduces one new file type on each side of the boundary.

On the content side: `.mdx`. MDX is Markdown with a JSX superset — it can contain React component tags inline with prose. Your chapters are plain Markdown; the script converts them to MDX. The result is a file your developer can enhance with interactive components without you ever touching the syntax. You wrote `.md`. The script produced `.mdx`. The distinction matters to the build toolchain. It does not require a new writing practice.

On the app side: `.tsx`. TypeScript with JSX syntax — what React developers write when they want type safety. Each `.tsx` file is a *page component*: a small module that imports the corresponding `.mdx` file and renders it as a route. The script generates them from a template. They have valid TypeScript types, valid default exports, valid metadata. A developer can open any of them and immediately understand the structure. You did not write any of them.

This is the contract: **source stays `.md`. Build outputs are `.mdx` and `.tsx`. The author runs one command and never hand-writes either format.**

---

## How the script works

`build-react-site.py` is pure Python standard library — no dependencies to install, no virtual environment to manage. Run it with Python 3 from your book's root directory. It reads `chapters/*.md` and `metadata.yaml`. It writes everything into `--out` (default `./site`). Full script in Appendix 95.

What the script actually does, in the order it does it:

It reads every `.md` file in `chapters/`, sorted alphabetically, and skips empty files. For each chapter it extracts the slug from the filename and scrapes the first `# Heading` as the display title.

It runs an MDX-escape pass on each chapter's content. MDX parses curly braces as JSX template expressions — prose that contains a literal `{` or `}` would break the build. The script walks each line outside of code fences and replaces bare braces with their HTML entities. Your code examples are left alone. Your prose is made safe.

For each chapter it writes two files: `content/<slug>.mdx` (the escaped chapter body) and `app/<slug>/page.tsx` (the route component). The route component imports the MDX file and the `AskAI` placeholder, sets the TypeScript metadata export, and renders the chapter inside an `<article className="prose">` wrapper with the `AskAI` panel below it.

Then it writes the shared files: `app/page.tsx` (the home page, a linked table of contents), `app/layout.tsx` (the root HTML shell), `components/AskAI.tsx` (the placeholder — more on this), `mdx-components.tsx` (required by the Next.js MDX integration), `next.config.mjs`, `tsconfig.json`, and `package.json`.

The script does not run `npm`. It does not start a dev server. It does not deploy anything. When it finishes it prints a one-line summary and a next-steps reminder:

```
Scaffolded: site
  book        : AI+1: AI Native Personalized Textbooks
  chapters    : 41
  files       : 89
  next steps  : cd site && npm install && npm run dev  (developer's step)
```

That last line is the boundary. Everything before it is yours. Everything after it is your developer's.

---

## The tested run: 41 chapters, 89 files

When the script ran against the AI+1 source, the numbers were exact: 41 chapter and appendix files in, 89 files out.

The breakdown:
- 41 `content/<slug>.mdx` files — one per chapter
- 41 `app/<slug>/page.tsx` route files — one per chapter
- `app/page.tsx` — the table of contents home page
- `app/layout.tsx` — the shared HTML shell
- `components/AskAI.tsx` — the Ask-AI placeholder
- `mdx-components.tsx` — the MDX component bridge
- `next.config.mjs` — Next.js configuration
- `tsconfig.json` — TypeScript configuration
- `package.json` — dependencies and build scripts

Total: 41 + 41 + 7 = 89. Every generated `.tsx` file has a valid default export. The JSON config files are valid. `next.config.mjs` correctly registers the `@next/mdx` plugin and adds `"mdx"` to the allowed page extensions. The `tsconfig.json` includes the `@/*` path alias so imports like `@/content/01-chapter.mdx` resolve correctly.

A developer who unpacks this folder and runs `npm install && next build` gets a working site — assuming no Node version conflicts and the package versions in `package.json` are still current. That last caveat is the one aging risk in the script: the pinned dependency versions (`next: "^14.2.0"`, `react: "^18.3.0"`) will drift. The script's dependency versions are current as of mid-2026; re-verify before a student developer picks this up a year from now. [verify — confirm dependency versions against npm before the next teaching run]

---

## What the site gives your students

A React site serves different needs than an EPUB, a Canvas course, or an Anki deck. The comparison is worth holding clearly because each surface is a deliberate choice, not a default.

The EPUB and PDF are the finished-object surfaces: self-contained, readable offline, no accounts required. They are appropriate for deep reading, reference reading, and the Kindle ecosystem. They cannot be updated interactively, cannot embed live components, and cannot run code in the reader's browser.

The Canvas course is the institutional surface: it lives inside an LMS, carries quizzes and case studies and grade-tracked assignments, integrates with the learning management infrastructure the institution already runs. It is the right surface for a formal course with enrollment, grading, and institutional support. It is opaque to the open web and locked behind account access.

The React site is the public surface: searchable by Google, linkable, shareable, accessible without an account, readable on any device. A student who finds a chapter via search reads it immediately. A collaborator who wants to share a specific section sends a URL. The table of contents is a navigable web page. Each chapter is a web page. The book is on the internet.

The trade-off is explicit: the React site is the most flexible surface and the only one that needs a developer and a hosting account. Unlike the `.imscc` package or the `.apkg` deck, you cannot finish it alone. You can scaffold it alone — that is what the script does — but you cannot run it without `npm install`, and you cannot deploy it without a hosting provider. If you have no developer collaborator and no Node.js installation and no Vercel account, the site folder sits on your disk and does nothing. That is not a bug. It is the honest account of what this surface costs.

The author's question before running the script is not "how do I build a React site?" It is: "do I have a developer to hand this to?" If yes, run the script. If no, skip this chapter and return to it when the collaboration exists.

---

## The AskAI placeholder

Every generated chapter route includes this at the bottom of the page:

```tsx
<AskAI chapter="01-the-fluency-trap" />
```

The component itself, in `components/AskAI.tsx`, is a placeholder. It renders a labeled input field and holds its state, but it does not call a model. The comments in the file are explicit:

```
// Placeholder for the embedded Ask-AI loop (Chapter 20).
// Wire this to your model endpoint; keep it a human+AI loop, not a
// one-shot answer box. The system prompt spec lives in Appendix 97.
```

This matters pedagogically. The web surface is the one surface that can embed a live model — not as a link to an external chatbot, but as a component within the chapter page itself. The student reads the chapter and, at the bottom of the page, asks a question about what they just read. The model's response appears in context. The chapter is still there. The question and the chapter are in the same view.

Chapter 20 is where the Ask-AI loop gets wired. The placeholder exists here because the architecture is already in place: every chapter page already includes the component, already passes the chapter slug, already knows where the panel goes. When your developer wires the endpoint in Chapter 20, the change is in one file — `components/AskAI.tsx` — and all 41 chapter pages get the live panel simultaneously. The scaffold is already built for what Chapter 20 delivers.

This is the web surface's version of the enrichment loop: the model is embedded in the reading experience, not adjacent to it. The student cannot close the book and the model at the same time. That proximity is deliberate and is worth explaining to your developer when you hand the folder over.

---

## What to hand your developer

The hand-off is a folder and a short conversation. Not a long technical brief. The developer will read the code; what she needs from you is intent and constraints.

What to include in the hand-off conversation:

**The purpose.** This is a textbook, not a blog. The reading experience should prioritize typography and line length over visual complexity. A `prose` CSS class (Tailwind Typography, or the developer's equivalent) handles this well. The chapters are long-form text with code blocks, tables, figures, and footnotes; all of those need readable rendering.

**The `AskAI` component.** Point to Chapter 20 and Appendix 97. The placeholder is already in every page route. The developer should not redesign its placement until you have discussed the Chapter 20 architecture. The system prompt spec is in Appendix 97; share that file when the conversation reaches the model endpoint.

**The source of truth.** The `content/*.mdx` files were generated from `chapters/*.md`. If you revise a chapter — fix an error, add a section, update a figure — you run the script again and the `.mdx` files regenerate. The developer should not edit `.mdx` files directly. Any structural changes to the site (new pages, custom components, styling) belong in the `.tsx` files and components, which will not be overwritten by a script re-run. Draw that line clearly.

**Hosting.** Vercel and Netlify both support Next.js app-router sites with zero configuration against the generated `package.json` and `next.config.mjs`. The developer connects the output directory to a GitHub repository, pushes, and deploys. The domain is her choice. The certificate is handled by the hosting provider. None of this requires your involvement — but it does require your blessing on where the public site lives.

What you do not need to specify: the CSS framework, the component library, the font choices, the color scheme, the responsive breakpoint strategy. These are design decisions the developer makes. Your book is the content. The site is the container. Hand the container decisions to the developer.

---

## The trade-off, named plainly

This is a rare chapter in the AI+1 series because the thing it teaches ends in a hand-off rather than a finished artifact. Every other Part 2 chapter ends with a file you can use immediately: the EPUB loads on your Kindle, the `.imscc` imports into Canvas, the `.apkg` installs in Anki. The React site ends with a folder that needs a developer to become a site.

That asymmetry is worth naming rather than softening. The pipeline is designed around the principle that the author should be able to finish each artifact independently. The React site is the honest exception. It is the most capable surface and the most dependent one.

Three things the script cannot do, by design:

It does not run `npm install` or `npm run dev`. The Python standard library has no Node.js bridge, and even if it did, running arbitrary package installation in a book-author's environment is not something a script should do. The developer runs `npm install`. The author runs `python3 build-react-site.py`.

It does not deploy. Deployment requires a hosting account, a domain decision, and configuration choices that belong to the project, not the script. Vercel's one-click deploy requires a GitHub repository and an account. None of that is scriptable in a generic way.

It does not wire the `AskAI` component to a model endpoint. That requires API credentials, a system prompt, a rate-limiting strategy, and a cost model. Chapter 20 addresses all of this. The placeholder is already in the scaffold, waiting.

The script's job is to remove the scaffolding cost from the hand-off. Without it, you would hand your developer a folder of `.md` files and ask her to build the site from scratch. With it, you hand her a folder of `.mdx` files, `.tsx` route components, and valid configs, and ask her to run `npm install` and style it. That is a materially different starting point. The scaffold does not finish the site. It makes the site startable.

---

## What comes next

Chapter 19 covers Medhavy: the AI-tutor layer that sits on top of Canvas via LTI. Like this chapter, it ends in a hand-off — Medhavy requires institutional registration, a Canvas sandbox, and an IT approval sequence. Chapter 18 and Chapter 19 are the two chapters in this book that are honest about needing a collaborator to finish. That honesty is part of the AI+1 design.

Chapter 20 closes the loop. Ask AI Everywhere is the capstone: the same embedded AI question-and-answer surface showing up across the web site (the `AskAI` component wired here), the Canvas course (through the Ignite integration from Chapter 17), Medhavy's tutor layer, and the parallel-LLM companion for the EPUB reader. Chapter 20 returns to the question Chapter 1 opened: the fluency trap, now on the student's side of the desk. The `AskAI` placeholder in the React scaffold is a promise. Chapter 20 is where it gets kept.

---

## AI Wayback Machine — Tim Berners-Lee

> **Prompt to run in Claude or ChatGPT:**
>
> "Read the Wikipedia article on Tim Berners-Lee and his 1989 proposal 'Information Management: A Proposal.' The original web was designed to allow physicists to share documents across a network without coordinating on a central system. What does Berners-Lee's separation of document structure (HTML) from presentation (CSS, applied later) have to do with the AI+1 separation of source truth (.md) from build artifacts (.mdx, .tsx, .epub, .imscc, .apkg)? Where does the analogy hold and where does it break down?"

The question Berners-Lee was solving in 1989 was not "how do we make beautiful web pages." It was "how do we make documents that survive being passed between systems that were not designed to talk to each other." The answer was separation: structure in one layer, presentation in another, linking in a third. The AI+1 pipeline applies the same logic to a textbook: content in one layer (`.md`), format in another (EPUB, Canvas, React), pedagogy in a third (quizzes, cases, glimmers, Ask-AI). Each layer is independently maintainable. The source does not change when the format changes. The format does not constrain the content.

Where the analogy breaks: Berners-Lee's web was stateless — documents do not know about the browsers rendering them. The AI+1 enriched layer is not stateless. The `AskAI` component in the React site is a live connection to a model. The Anki deck remembers your answer history. The Canvas course tracks your quiz scores. The enriched layer is not just a formatted document. It is a document that responds to its reader. That is the AI in AI+1.

---

## Exercises

**Exercise 18.1 (Apply).** Run `build-react-site.py` against your book directory. Confirm the script completes without errors. Open `site/` and verify: (a) the file count matches `(2 × number of chapters) + 7`; (b) `app/page.tsx` contains a link for every chapter in your `chapters/` directory; (c) at least two `app/<slug>/page.tsx` files have valid default exports; (d) `components/AskAI.tsx` contains the placeholder comment pointing to Chapter 20 and Appendix 97.

**Deliverable:** A one-paragraph note listing the chapter count, file count, and the result of each spot check.

**Exercise 18.2 (Analyze).** Open `content/<slug>.mdx` for one of your chapters that contains code blocks and one that contains curly braces in prose. Verify that: (a) curly braces in prose are escaped as `&#123;` and `&#125;`; (b) curly braces inside code fences are not escaped. Then open the corresponding `app/<slug>/page.tsx` and identify where the chapter slug is passed to the `AskAI` component.

**Deliverable:** A two-paragraph analysis — one paragraph on the MDX-escape behavior, one on the AskAI component prop.

**Exercise 18.3 (Evaluate).** You are preparing the hand-off to a developer. Write a short brief (one page, plain text or markdown) covering: (a) what the `site/` folder contains and how it was generated; (b) the source-of-truth rule (edit `.md` files, not `.mdx` files); (c) the `AskAI` placeholder and the pointer to Chapter 20; (d) the hosting recommendation (Vercel or Netlify, zero-config); (e) the one decision you are deliberately leaving to the developer.

**Deliverable:** The one-page hand-off brief.

**Exercise 18.4 (Evaluate — harder).** The script pins specific package versions in `package.json` (Next.js `^14.2.0`, React `^18.3.0`). Look up the current stable versions of `next`, `react`, and `@next/mdx` on npmjs.com. If any of the pinned versions are more than one major version behind, write the update in your copy of `site/package.json`. Note any breaking changes in the Next.js changelog that might affect the generated `.tsx` files. [verify — dependency versions current as of mid-2026; re-check before each teaching run]

**Deliverable:** A list of version comparisons and any changelog notes relevant to the generated scaffold.

---

## Bridge — Chapter 19

The `site/` folder is ready to hand off. A developer can take it from here.

Two chapters left.

Chapter 19 is the other hand-off chapter: Medhavy, the AI-tutor layer that integrates with Canvas via LTI 1.3. Like the React site, it requires a collaborator — in this case, not a front-end developer but an institutional IT contact and a Canvas administrator. The architecture is different and the approval sequence is longer. The chapter is shorter, because the hand-off is even cleaner: the system design document is Sri's, the LTI configuration is IT's, and your job is to understand what Medhavy gives your students and what information to send to get the integration live.

Chapter 20 is where the `AskAI` placeholder in every React page gets wired to a real model. It is also where the fluency trap comes back around — not as a warning about what the model generates for the author, but as a design constraint on what the model does for the student. A student who can make the AI explain the chapter without understanding it themselves has not learned the chapter. Chapter 20 is about building Ask-AI surfaces that keep the human thinking. The placeholder is already in the scaffold. The design question is still open.

---

## References

1. Next.js App Router documentation. nextjs.org/docs/app
2. MDX documentation. mdxjs.com/docs/
3. `@next/mdx` integration guide. nextjs.org/docs/app/guides/mdx
4. Vercel deployment documentation. vercel.com/docs
5. Netlify Next.js deployment guide. docs.netlify.com/frameworks/next-js/
6. Appendix 95 — `build-react-site.py` full script and reference. (This volume.)
7. Appendix 97 — Ask-AI system prompt specification. (This volume.)
