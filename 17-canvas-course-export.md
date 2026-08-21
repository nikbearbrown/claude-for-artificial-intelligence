# Chapter 17 — Canvas Course Export: .imscc

*One file upload. A complete course appears.*

---

The professor is in Canvas Settings. She clicks Import Course Content. A file-picker opens and she selects `ai-for-designers.imscc` — a file she received from a colleague who ran a single Python command against a book's markdown source. She chooses "All Content." She clicks Import.

For about forty seconds, nothing visible happens. Then the import queue updates: Complete. She opens the course. Fifteen modules are listed in the left navigation. Module 1 is "Chapter 1 — The Fluency Trap." She opens it. A content page sits at the top — the chapter text, converted to HTML. Below it, an item titled "Chapter 1 — The Fluency Trap — Exercises." The assignments section shows shells named after every exercise section in the book. The syllabus page renders.

She has never opened a terminal. She has not touched the Canvas API. She has not written a line of XML.

This chapter works backward from that moment. What is in the file? How did a Python script produce it from markdown? What does Canvas do with it when it arrives? What happens after — what the import built correctly, what it left for the human to finish, and why that boundary is exactly right.

---

## What a `.imscc` Is

Rename the file. Change `.imscc` to `.zip` and your operating system will let you open it like any other archive. Inside you will find two things: a file called `imsmanifest.xml` sitting at the root, and a folder called `web_resources/` containing HTML pages.

That is the whole package. A ZIP archive with an XML index and a folder of content files.

The format is IMS Common Cartridge — a standard maintained by 1EdTech (formerly IMS Global), currently at version 1.3.[^1edtech] Common Cartridge defines what the archive must contain and what the manifest must say so that a learning management system can unpack the course from the file. Canvas supports it. Moodle supports it. Blackboard and Brightspace support it. A valid Common Cartridge 1.3 package is portable across all of them.

The `.imscc` extension is simply the file-type marker the LMS ecosystem agreed on to distinguish a Common Cartridge from a generic ZIP. Structurally, they are identical. The extension signals intent.

### The Manifest Is the Course Index

`imsmanifest.xml` is what makes the package a *course* rather than a loose folder of HTML pages. It tells the LMS three things.

First, metadata: what version of the Common Cartridge spec this package targets, and what the course is called.

```xml
<metadata>
  <schema>IMS Common Cartridge</schema>
  <schemaversion>1.3.0</schemaversion>
  <lomimscc:lom>
    <lomimscc:general>
      <lomimscc:title>
        <lomimscc:string>AI for Designers</lomimscc:string>
      </lomimscc:title>
    </lomimscc:general>
  </lomimscc:lom>
</metadata>
```

Second, the organization: the module hierarchy. Each module is an `<item>` element. Each content item inside the module is a child `<item>` that points to a resource by its identifier. This is where "fifteen modules" comes from — the manifest declares them, and Canvas reads the declaration to build the left-navigation structure.

Third, the resources: a flat list of every file the manifest references. Each resource gets an identifier, a type, and an href pointing to its location in the package. If the manifest references a resource that is not in the ZIP, the import will either skip it or error. If the ZIP contains a file the manifest does not reference, the file is invisible to the LMS — it exists in the archive but the course structure does not know about it.

This is the mechanism the teaching analogy captures: the `.imscc` is a moving box with a packing list. The HTML files are the objects. `imsmanifest.xml` is the packing list Canvas reads to rebuild the room. Without the packing list, Canvas cannot reconstruct the course. Without the objects, the packing list references things that are not there.

### Standard Common Cartridge vs. Canvas-Flavored Common Cartridge

Canvas reads two different kinds of Common Cartridge packages, and the difference matters.

A standard Common Cartridge — what the 1EdTech specification defines — contains modules, web content pages, assessment items, discussion shells, and the manifest. It imports cleanly into Canvas and into any other 1EdTech-compliant LMS. It is portable and unambiguous.

A Canvas-flavored Common Cartridge contains everything in the standard package *plus* two trigger files: `course_settings/syllabus.html` and `course_settings/course_settings.xml`. When Canvas sees those files, it reads them as course-level configuration — populating the syllabus page with the HTML content, applying course navigation settings, potentially setting module completion requirements and rubric structures through Canvas-specific XML that other LMS platforms do not recognize.

The two trigger files are the boundary between the portable path and the Canvas-specific path. `build-imscc-standard.py`, the script this chapter teaches, deliberately does not write them. That is not an oversight. A standard package that imports cleanly into Canvas, Moodle, Blackboard, and Brightspace is more durable than a Canvas-optimized package that imports richly into Canvas and fails or imports oddly everywhere else.

> **Sidebar: The Canvas-optimized path.** Instructure authored the `canvas_cc` Ruby gem for building Canvas-flavored Common Cartridge packages — rubric criteria, quiz shells, outcome alignments, module completion requirements. The most recent RubyGems release is 0.0.43 from August 2019.[^canvas_cc] If your institution runs Canvas and you need those features and you are comfortable maintaining a Ruby toolchain, the Canvas-optimized path exists. Appendix 91 covers it. This chapter teaches the standard path: pure Python, no external dependencies, portable across platforms.

---

## The Same Source, Two Outputs

Here is the single most useful framing for this chapter: `build-imscc-standard.py` reads the *same source files* that `./build.sh` reads to produce the EPUB and PDF.

`metadata.yaml` supplies the course title. `chapters/*.md` supply the content. The same markdown that became Kindle chapters becomes Canvas pages. The same exercise sections that became the "Exercises" headings in the book become assignment shell pages in the course. The TIKTOC.md chapter sequence becomes the module sequence.

This is what "single-source publishing" means in practice. The book and the course are not two separate production tasks. They are two compilation targets from one source tree. Fix a typo in a chapter file, rebuild, and both the EPUB and the `.imscc` are corrected.

The mapping is direct:

| Book source | Canvas course |
|---|---|
| One teaching chapter (`chapters/01-*.md`) | One module with one content page |
| `## Exercises` section in a chapter | An additional page titled "[Chapter] — Exercises" in the same module |
| Chapter sequence (01, 02, 03 ...) | Module sequence, preserving order |
| `00-*.md` front matter | "Start Here" module |
| `80-98-*.md` appendices | "Appendices" module |
| `99-*.md` back matter | "Back Matter" module |
| `metadata.yaml` title field | Course title in the manifest |

The mapping is not magic. It is a compiler. `build-imscc-standard.py` reads files, makes decisions based on file numbering conventions, converts markdown to HTML, and writes a ZIP. The intelligence is in the source structure the earlier chapters built — TIKTOC produced the chapter sequence, the scaffold created the file naming convention, the chapter writer populated the content. By Chapter 17 the source is already organized; the script is the final pass that packages it for a different delivery format.

---

## `build-imscc-standard.py` — What It Does

The script is pure Python. It imports nothing outside the standard library: `argparse`, `html`, `os`, `re`, `sys`, `uuid`, `zipfile`, and `xml.sax.saxutils`. No `pip install`. No virtual environment. Run it anywhere Python 3.6 or later is available.

```
python3 build-imscc-standard.py
```

That is the entire invocation for the default case. The script assumes the book root is the current directory, looks for `chapters/` and `metadata.yaml`, and writes the output to `output/<course-slug>.imscc`. Optional arguments:

```
python3 build-imscc-standard.py --source-dir /path/to/book \
                                 --out output/my-course.imscc
```

### What It Reads

**`metadata.yaml`** — a minimal flat YAML file, read without PyYAML using a line-by-line regex parser. The script extracts the `title` field and uses it as the course title in the manifest. If the file is missing, the script falls back to the directory name.

**`chapters/*.md`** — every `.md` file in the chapters directory, sorted by numeric prefix. The numbering convention this book uses (`00-`, `01-79`, `80-98`, `99-`) drives the grouping logic: front matter gets the "Start Here" module, teaching chapters 01–79 each get their own module, appendices 80–98 are collected into a single "Appendices" module, and back matter gets "Back Matter."

**TIKTOC.md (optional)** — accepted as a `--tiktoc` argument but used only for module-order confirmation. The definitive source of order is the file numbering in `chapters/`.

### What It Produces

For each chapter file, the script:

1. Reads the markdown and extracts the `# Title` heading as the module and page title.
2. Converts the full markdown to HTML using a stdlib-only renderer that covers the subset this book uses: headings, paragraphs, unordered and ordered lists, code fences, inline bold, italic, code, and links.
3. Writes the HTML to `web_resources/<slug>.html` inside the package.
4. Checks whether the file contains an exercises section (a heading matching `## Exercises` or `## Assessable Exercises`). If found, the exercises section gets its own HTML page at `web_resources/<slug>-exercises.html`.
5. Registers each page as a resource in the manifest and as an item in its module.

After all chapters are processed, the script builds `imsmanifest.xml` from the accumulated module and resource data, and writes the complete package as a ZIP file with the `.imscc` extension.

The terminal output when run against the AI+1 book's own source:

```
Built: output/ai+1-ai-native-personalized-textbooks.imscc
  course title : AI+1: AI Native Personalized Textbooks
  modules      : 15
  web pages    : 32
  manifest     : imsmanifest.xml (Common Cartridge 1.3.0)
```

Fifteen modules. Thirty-two web pages. A well-formed `imsmanifest.xml` — validated by Python's XML parser and by `xmllint`. Every resource href present in the ZIP. No dangling item references. The package imports into Canvas.

### The Manifest in Detail

`build_manifest()` is the heart of the script. It constructs the XML string that becomes `imsmanifest.xml`. Each module becomes an `<item>` element inside the `<organizations>` section. Each page within a module becomes a child `<item>` that carries an `identifierref` pointing to a resource. Every resource appears in the `<resources>` section with its identifier, type (`webcontent`), and href.

The identifiers are generated UUIDs — truncated to twelve hex characters for readability. The UUID generation uses Python's `uuid.uuid4()`, which produces a new random identifier each build. This means two builds of the same source produce manifests with different identifiers. That is expected behavior for a build system: the identifiers are internal references within one package, not stable external identifiers that need to persist across builds.

### What It Deliberately Omits

The script does not call the Canvas API. The professor uploads one file through the Canvas web interface. No API tokens, no Canvas admin rights, no integration setup.

The script does not write the Canvas-flavored trigger files. `course_settings/syllabus.html` and `course_settings/course_settings.xml` are absent by design. The package is standard Common Cartridge, not Canvas-specific XML.

The script does not grade or assess. The exercises pages are shells — they carry the exercise text, the prompts, the Bloom level headings from the chapter — but they are `webcontent` resources, not QTI assessment items. A professor who wants scored quizzes will configure them in Canvas after import. The script builds the structure; the pedagogy lives in the content.

The script does not do the live Canvas import. That step is yours. Mark it clearly in your workflow: the build produces the file, the professor uploads it. The chapter's last exercise is that upload.

---

## Inspecting the Package Before Import

Before uploading to Canvas, inspect the package. This step takes three minutes and saves the confusion of discovering a structural problem after a partially-complete import.

Rename `output/<course-slug>.imscc` to `output/<course-slug>.zip`. Open the archive with your file manager or `unzip -l`:

```
unzip -l output/ai+1.zip | head -40
```

Confirm three things:

1. `imsmanifest.xml` appears at the root of the archive — not inside a subdirectory. Some tools accidentally nest the manifest. Canvas requires it at the root.
2. `web_resources/` contains one HTML file per chapter and one HTML file per exercises section.
3. No chapter you expected is missing. If a chapter file was empty (a stub), the script skipped it. Empty stubs produce no module.

Now open `imsmanifest.xml` directly — it is a plain text file. Confirm the `<schemaversion>` reads `1.3.0`. Count the `<item>` elements in the `<organizations>` section and verify the count matches your expected module count. Spot-check one resource: find an `identifierref` in an `<item>` and confirm the matching resource in `<resources>` has an `href` that exists in the ZIP.

This is the diff-before-import habit. The manifest is the contract between the package and the LMS. Reading it takes two minutes and you will catch more problems here than Canvas's error messages will tell you after a failed import.

---

## Importing Into Canvas

*This step requires a Canvas sandbox. The following describes the documented Canvas workflow; verify against the current Canvas interface before proceeding — Canvas UI paths and option wording drift.* [verify — confirm against current Canvas import guide before publication]

The import path documented by Instructure is: Course Settings → Import Course Content → Common Cartridge 1.x Package → Choose File → select the `.imscc` file → All Content (or select specific content) → Import.[^canvas_import]

Canvas queues the import. For a book-sized package — fifteen modules, thirty-odd pages — the import completes in under a minute. The import status page shows a progress bar and a completion notice.

After import, open Modules. The module list should match the chapter sequence. Each module should contain the chapter content page and, for chapters with exercises, the exercises page.

Three things Canvas does not do automatically on import that you will need to configure:

**Dates.** The package carries no due dates. Assignment shells exist in the Assignments section but have no dates. You will set them manually or use Canvas's date-shift tool.

**Publication state.** Imported content lands in draft (unpublished) state. Nothing is visible to students until you publish modules and their items. This is correct behavior. Import is not publication.

**Links.** Internal cross-references in the markdown — `[see Chapter 3](#chapter-3-domain-research)` — become HTML anchor links in the page. They may not resolve correctly inside Canvas's page renderer, depending on how Canvas handles same-origin anchor links. External links work. Internal structural links may need manual correction.

---

## After Import: The Diff Review

Import success means the structure exists. It does not mean the course is ready.

The post-import diff review is the human gate. It has two parts.

### Part 1: Structural diff

Open the imported course. For each module, check:
- Module title matches the chapter title in the source file.
- Content page exists and renders the chapter text.
- Exercises page exists for chapters that have an exercises section.
- No modules are missing relative to the chapter file count.

For the AI+1 book's own source, a typical result: every module present, every content page rendering cleanly, exercises pages present for the chapters that had `## Exercises` sections. Common mismatches at this stage: a stub chapter that was empty in the source produces no module; a chapter whose heading used `##` instead of `#` has its module titled after the filename rather than the chapter title.

### Part 2: Content review

The structural diff confirms the scaffolding. The content review confirms the course makes sense as a course.

Open three modules at random. Read the content page. Ask four questions: Is this the chapter text — not placeholder content? Does the page render correctly — no broken markdown artifacts, no raw HTML showing through? Does the exercises page contain the actual exercises — not just a heading? Are any links in the page visibly broken?

Record what you find. The research file for this chapter frames it precisely: "list three exact matches and two human corrections." The corrections are not failures of the build script. They are the boundary between what a compiler can do — transforming structure — and what a human must do — confirming pedagogy, fixing dates, setting publication state, deciding what students see and when.

### IgniteAI as Refinement, Not Build

One clarification that matters: IgniteAI is the refinement tool after import, not the build tool.

The `.imscc` builds the baseline course in one upload. Fifteen modules, thirty-two pages, all the exercise shells — that is what the script produced and Canvas imported. IgniteAI, if your institution has it, is for refining the course after the baseline exists: reworking an assignment rubric, adding a quiz to a module, adjusting the syllabus narrative, personalizing the learning objectives for a specific cohort. IgniteAI is excellent at those tasks. It is not what you use to create the initial structure from the book source. That is the script's job.

The workflow is: script builds, Canvas imports, human reviews, IgniteAI refines. In that order. Skipping the review step — treating the import as ready-to-publish — is the same mistake as skipping the device read in Chapter 12. The pipeline does not guarantee pedagogical quality; it guarantees structure. The human gate is always the review.

---

## Trade-offs: Portable vs. Canvas-Rich

The standard path makes a deliberate bet. Name the trade-off clearly.

**Standard Common Cartridge — what you get:** A package that imports cleanly into Canvas, Moodle, Blackboard, and Brightspace without modification. A build process with no external dependencies beyond Python 3. A package you can rebuild from source whenever the content changes. A portable format that does not break when Canvas updates its internal XML expectations.

**Standard Common Cartridge — what you give up:** Canvas-native rubrics are not present in the imported shells. Module completion requirements — "students must view this page before moving to the next" — are not configured. Quiz items are not QTI-formatted; they are exercise shells, not gradeable assessments. The syllabus page is a blank Canvas default rather than the syllabus HTML from the book's front matter.

**Canvas-optimized path — what you gain:** Richer assignment structures with Canvas-specific rubric XML. Module prerequisites and completion requirements built into the manifest. A syllabus page populated from the package. Outcome alignment and quiz item structure for New Quizzes import.

**Canvas-optimized path — what you take on:** The `canvas_cc` gem's last RubyGems release is from 2019.[^canvas_cc] Maintaining a Ruby toolchain for a tool with a five-year-old release against an actively developed LMS platform is a maintenance liability. Canvas-specific XML structures can drift across institutional Canvas instances and Canvas version updates. A package optimized for one institution's Canvas configuration may import oddly at another.

For most instructors using this book, the standard path is the right path. The structure that matters most — modules, content pages, exercises — imports cleanly. The refinement that adds Canvas-specific features is done in Canvas, by a human who can see the actual course, or through IgniteAI. The parts that require human judgment should not be automated into a build script.

If you need the Canvas-optimized path, start from the standard package and add Canvas features in Canvas. Do not start from Canvas-specific XML and hope it stays compatible.

---

## Worked Example: The AI+1 Book as a Canvas Course

The worked example is the AI+1 book itself. The same source tree that produced the EPUB described in Chapter 12 also produced the `.imscc` package.

Run from the book root:

```
python3 build-imscc-standard.py
```

Output:

```
Built: output/ai+1-ai-native-personalized-textbooks.imscc
  course title : AI+1: AI Native Personalized Textbooks
  modules      : 15
  web pages    : 32
  manifest     : imsmanifest.xml (Common Cartridge 1.3.0)
```

Inspect the package:

```
unzip -l output/ai+1-ai-native-personalized-textbooks.imscc
```

The listing shows `imsmanifest.xml` at root, followed by `web_resources/` containing HTML for each chapter and each exercises section. Rename to `.zip`, open `imsmanifest.xml`, confirm `<schemaversion>1.3.0</schemaversion>`. Count `<item>` elements in `<organizations>`. Count `<resource>` elements in `<resources>`. Every resource referenced in the manifest exists in the archive.

Now the step that requires a Canvas sandbox — the reader's action, not the script's:

**Import into Canvas.** Course Settings → Import Course Content → Common Cartridge 1.x Package → Choose File → select the `.imscc` → All Content → Import. Wait for completion status.

After import, open Modules. You should see fifteen modules beginning with "Start Here" (front matter), proceeding through the teaching chapters in order, followed by "Appendices" and "Back Matter." Open Module 1. The content page "Chapter 1 — What AI+1 Is" should render the chapter text. Below it, "Chapter 1 — What AI+1 Is — Exercises" should render the exercises section.

The course structure exists. Due dates, publication state, and rubric details are yours to configure. The diff review is the next step.

---

## AI Wayback Machine — Tim Berners-Lee and the Web as a Format Decision

In 1989, Tim Berners-Lee wrote a proposal at CERN titled "Information Management: A Proposal." Its core argument was not about browsers or HTTP. It was about format: information should be stored in a universal format that allows any node to link to any other, independent of the software that created it.[^tbl]

The proposal that became the World Wide Web was, at its root, a portability argument. Don't lock content to one system's native format. Use a format any system can read. The links are what give it structure; the format neutrality is what gives it longevity.

Common Cartridge is the same argument applied to courses. A course locked inside one LMS's native database format is only as portable as that LMS's export tools and the next LMS's import compatibility. A course in a standard XML-in-ZIP format is movable. Not frictionlessly — the Canvas-flavored features remind us that portability always costs something. But movable in principle, and that matters when institutional contracts change, when a university migrates platforms, or when an instructor wants to teach the same course at two institutions that run different LMS platforms.

The standard path is the Berners-Lee bet. Not the richest single-platform feature set. The widest usable reach.

> **Prompt to run in Claude or ChatGPT:**
>
> "Read the Wikipedia article on IMS Global Learning Consortium and the history of the Common Cartridge standard. What problem was Common Cartridge designed to solve, and how does its approach compare to the approach of SCORM? What does Canvas support from the CC spec, and what does it extend beyond the spec with Canvas-specific XML? Note any claims Claude makes that you cannot verify from the Wikipedia source."

---

## Exercises

**Exercise 17.1 (Apply) — Inspect the package.** Run `build-imscc-standard.py` against your book's source directory. Confirm the output `.imscc` file is created. Rename it to `.zip` and open the archive. Find `imsmanifest.xml` at the archive root. Open the manifest and locate: (a) the `<schemaversion>` element confirming Common Cartridge 1.3.0; (b) one module's `<item>` element in `<organizations>` with its child item; (c) the matching `<resource>` element in `<resources>` with the `href` pointing to the HTML page. Confirm the `href` file exists in `web_resources/`. Write one sentence describing what you found.

**Deliverable:** Three excerpts from `imsmanifest.xml` — the schemaversion, one module item tree, and the matching resource — plus a one-sentence summary confirming the href file exists in the archive.

---

**Exercise 17.2 (Apply) — Import into Canvas.** *Requires a Canvas sandbox or institutional Canvas course shell with import permissions.* Import your `.imscc` package using Course Settings → Import Course Content → Common Cartridge 1.x Package → All Content → Import.[^canvas_import] Wait for the import queue to complete. Navigate to Modules. Capture a screenshot or written record of the module list. Confirm: (a) module count matches your chapter count; (b) at least one module contains both a content page and an exercises page; (c) the content page renders the chapter text without broken formatting.

**Deliverable:** Module list (screenshot or written list) with a note on module count and one specific observation about a content page rendering.

---

**Exercise 17.3 (Analyze) — Diff review.** After the Canvas import, conduct a diff review. Open three modules and for each record: the module title (does it match the chapter heading in the source?), the content page (does it render correctly?), whether an exercises page exists, and whether any links appear broken. Then identify two things the import built correctly and two things that need human correction before the course is publishable. Record the two corrections as specific action items.

**Deliverable:** A diff table with three modules, two confirmed matches, two required corrections, and two specific action items.

---

**Exercise 17.4 (Evaluate) — The portability trade-off.** Return to the trade-off section of this chapter. Your book has a specific audience and a specific deployment context. Answer three questions with evidence from your actual build and import: (1) Does the standard Common Cartridge output give you the structure you need for your course, or are there specific Canvas-native features your course design requires? (2) If you needed the Canvas-optimized path, what specific features would justify the Ruby/gem maintenance overhead? (3) If your institution migrated from Canvas to another LMS next year, what would survive from the standard package and what would be lost if you had used the Canvas-optimized path instead? Write one paragraph per question.

**Deliverable:** Three paragraphs with specific reference to your course structure and deployment context.

---

## Bridge — Chapter 18

The Canvas course exists. Fifteen modules, thirty-two pages, every exercise shell imported and waiting for due dates and rubrics.

One delivery format remains. A React site — the same source, again — compiled to a static site that runs in a browser without a canvas account, without a Kindle, without any LMS at all. Chapter 18 teaches the third compilation target from the single markdown source: the web.

---

## References

1. 1EdTech (IMS Global Learning Consortium). *IMS Common Cartridge Overview and Specification*. https://www.imsglobal.org/cc/index.html
2. 1EdTech. *Common Cartridge 1.4 Implementation Guide*. https://www.imsglobal.org/node/167531
3. Instructure. "How do I import content from Common Cartridge into Canvas?" Canvas Instructor Guide. https://community.instructure.com/en/kb/articles/660732-how-do-i-import-content-from-common-cartridge-into-canvas
4. Instructure. "How do I export a Canvas course?" Canvas Instructor Guide. https://community.canvaslms.com/t5/Instructor-Guide/How-do-I-export-a-Canvas-course/ta-p/785
5. RubyGems. `canvas_cc` gem, version 0.0.43 (released August 22, 2019). https://rubygems.org/gems/canvas_cc
6. RubyDoc. `canvas_cc` README. https://www.rubydoc.info/gems/canvas_cc/0.0.23
7. Berners-Lee, T. (1989). "Information Management: A Proposal." CERN. https://www.w3.org/History/1989/proposal.html
8. University of Wisconsin–Madison. "Importing a Pressbooks Book into Canvas via Common Cartridge." https://kb.wisc.edu/helpdesk/84559

[^1edtech]: 1EdTech (IMS Global Learning Consortium). *IMS Common Cartridge Overview and Specification*. https://www.imsglobal.org/cc/index.html
[^canvas_cc]: RubyGems. `canvas_cc` gem, version 0.0.43 (released August 22, 2019). https://rubygems.org/gems/canvas_cc
[^canvas_import]: Instructure. "How do I import content from Common Cartridge into Canvas?" Canvas Instructor Guide. https://community.instructure.com/en/kb/articles/660732-how-do-i-import-content-from-common-cartridge-into-canvas
[^tbl]: Berners-Lee, T. (1989). "Information Management: A Proposal." CERN. https://www.w3.org/History/1989/proposal.html
