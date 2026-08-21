# Chapter 16 — Spaced Repetition: Anki and the Forgetting Curve

*You cannot learn what you cannot remember — and rereading is a comfortable lie about how memory works.*

---

Wednesday, 10 p.m. The exam is Friday. You open the textbook to chapter seven and read it again. The words are familiar. The concepts feel clear. Each pass through the material confirms the feeling: you know this. The sentences land with the pleasant weight of recognition.

Thursday morning, you close the book. You sit down to write from memory and discover that recognition is not recall. You can identify the right answer when you see it. You cannot produce it when the prompt is blank. The chapter you read twice has left an impression — a sense of knowing — but not a durable trace. You cram. The exam goes fine. Three weeks later, you remember almost nothing.

This is the forgetting curve doing what it always does. And it is where the AI+1 enrichment layer has something direct to offer.

---

## The Forgetting Curve and Why Rereading Fails

Hermann Ebbinghaus, a German psychologist working in the 1880s, was the first researcher to measure what happens to memory over time in a systematic way. He used himself as his only subject, memorized lists of nonsense syllables, and then tested his ability to relearn them at different intervals. What he found — and what has since been replicated in many forms — is that forgetting follows a decay curve: steep at first, then flattening. Most of what you learn in a single study session is gone within hours or days if you do not return to it. Retention decays toward a baseline that is above zero (something always lingers) but well below mastery.

Rereading feels effective because it activates recognition rather than retrieval. Recognition is the ability to confirm that something is familiar when you encounter it again — the warm sense of "yes, I've seen this." Retrieval is the ability to reconstruct the information from scratch when you need it. These are different cognitive operations, and they do not track together. A student who rereads a chapter three times can achieve near-perfect recognition without building the kind of durable retrieval trace the material requires. The test catches this. The client meeting catches this. The blank prompt catches this.

The problem with massed practice — reading and rereading in concentrated bursts — is not just the recognition/retrieval confusion. It is that the brain allocates attention based on perceived novelty. When material is new, the brain attends to it. When material is already processed and recently encountered, the brain attends less. Massed repetition encounters diminishing marginal returns quickly: the third consecutive pass through a chapter produces far less encoding than the first.

This is the forgetting curve's practical implication. The question is not "how many times did you study this?" but "when did you study it — and was the retrieval hard enough to matter when you did?"

---

## The Spacing Effect and What It Changes

The spacing effect reverses the massed-practice intuition. Practice distributed over time produces stronger, more durable memory than the same total practice massed together. The reason is related to the forgetting curve itself: when you return to material just as you are beginning to forget it, the act of retrieving it is effortful. That effort — the mental strain of reaching for something that has partially decayed — is not an obstacle to learning. It is the mechanism of learning.

Cognitive psychologists call this "desirable difficulty." The difficulty of retrieving a fading memory is desirable precisely because it drives deeper encoding. Each successful retrieval from the edge of forgetting strengthens the memory trace more than a retrieval from confident familiarity would. The spacing effect is not just about distributing practice in time — it is about engineering the retrieval to be effortful at exactly the right moment.

The right moment is when the forgetting curve has brought retention down to the edge of loss — far enough that retrieval is hard, close enough that retrieval is still possible. Review too early and you get an easy retrieval from confident familiarity, which strengthens the trace less. Review too late and the information is gone, which produces learning (relearning, technically) but at the cost of the time you already invested. The optimal window is narrow, and it shifts as the memory strengthens with each successful retrieval: each successful spaced review lengthens the interval before the next review is needed.

This is why "study schedule" and "flashcard stack" are the wrong mental models for spaced repetition. The right model is a forgetting curve per card, updated with each review, with the next review scheduled at the curve's edge. No human can track this across hundreds of cards manually. A spaced repetition algorithm can.

---

## What Anki Does

Anki is a flashcard application built on a spaced repetition scheduling algorithm called SM-2, developed by Piotr Wozniak in the late 1980s. The algorithm maintains a per-card record: how many times has this card been reviewed, how difficult was the last review, what is the current interval between reviews. After each review, the student rates their recall (from complete blackout to effortless) and SM-2 updates the next review date accordingly. Easy cards get pushed further into the future. Hard cards come back sooner. Lapses — cards answered wrong — get reset and start the schedule over.

What this produces over weeks and months is a review load that grows as knowledge grows. A new deck arrives as a burst of unfamiliar cards. Six months in, the same deck requires only occasional maintenance reviews as most cards settle into long intervals. The cognitive load is highest when retention is lowest and falls off as retention solidifies. This is the opposite of a lecture course, where the cognitive load peaks at the start of the semester and decays toward finals.

The mechanism Anki is exploiting is well-documented. Testing oneself on material — forcing recall from a blank prompt — produces better long-term retention than studying the same material passively. This effect is large enough to have its own name in the cognitive psychology literature: the testing effect, or retrieval practice effect. The act of retrieval is not just a measurement of memory; it is a consolidation of memory. Each review is both a test and a teaching event.

Anki is free, available on every major platform, and synchronizes across devices through AnkiWeb. The file format it imports is `.apkg` — a zip archive containing a SQLite database and a media manifest. And this is where the AI+1 pipeline connects.

---

## The Recall Layer in the AI+1 Pipeline

The AI+1 book source already produces the EPUB, the Canvas course, and the React site from the same markdown files. The recall layer adds one more artifact from the same source: an Anki deck.

Cards are authored as simple Q:/A: pairs in plain markdown. They live in one of two places: a dedicated `recall/` directory at the book root (one `.md` file per chapter or topic cluster), or a `## Recall` section at the end of any chapter file. The format is the same in both cases:

```
Q: What is the testing effect?
A: The finding that retrieving information from memory strengthens the memory
   trace more effectively than passive review of the same material.

Q: What does the SM-2 algorithm update after each review?
A: The interval before the next review, based on the student's self-rated
   recall difficulty.

Q: What file format does Anki import?
A: .apkg — a ZIP archive containing a SQLite database (collection.anki2)
   and a media manifest.
```

A blank line separates each card pair. Multi-line answers are fine — the parser accumulates continuation lines until it sees a new Q:, a new A:, or a blank line that ends the pair.

The discipline this authoring format enforces matters as much as the format itself. Good spaced repetition cards are atomic: one fact per card. A card that asks "what is the testing effect and why does spacing matter?" is a bad card — it is two facts, which means one will often be recalled and one missed, which means the card's review schedule will be wrong for both. The rule is: one question, one answer, the smallest testable unit. Writing cards in this format is an editorial act. It forces the author to decide what the durable facts of the chapter are, separate from what the prose needs to explain.

This is a trade-off worth naming directly: spaced repetition is not a substitute for the rest of the enrichment layer. Cards encode discrete recall. They do not encode argument, synthesis, or judgment. A student who knows every term in the deck has not necessarily understood the chapter. That is what glimmers (Chapter 15) and case studies (Chapter 14) are for — the reasoning-under-pressure layer that tests whether a student can use the knowledge, not just name it. The recall layer trains the substrate. The case studies and glimmers train the application.

---

## How build-anki.py Works

`build-anki.py` is the script that compiles the recall layer into a `.apkg` file the student double-clicks to import into Anki. It is pure Python — standard library only, no dependencies to install. The two libraries it uses are `sqlite3` and `zipfile`, both part of Python's standard distribution.

The script does three things in sequence.

**First, it reads cards.** It scans `recall/*.md` for Q:/A: pairs using `parse_qa()`. It also scans `chapters/*.md` for any `## Recall` or `## Spaced Repetition` section and extracts Q:/A: pairs from those sections. Both sources can be present at once; cards from both are combined into a single deck.

**Second, it builds a SQLite database conforming to Anki schema 11.** The schema is a specific table structure Anki expects: a `col` table (one row per collection, storing the deck configuration, model definition, and global settings as JSON blobs); a `notes` table (one row per card, storing the front and back fields separated by the ASCII 0x1f character, plus a checksum of the front field for deduplication); a `cards` table (one row per note in the basic case, linking to the deck and the note, with scheduling fields initialized to zero since no reviews have happened yet); a `revlog` table (review history, empty for a new deck); and a `graves` table (deletion records, also empty). The note type is "Basic" — two fields, Front and Back — which is the simplest Anki note type and the only one the script uses. Fields are stored joined by the 0x1f separator (a unit separator character Anki uses internally to delimit fields within a single `flds` column).

**Third, it writes the `.apkg`.** It zips the SQLite database as `collection.anki2` and adds a `media` file containing the string `{}` — an empty JSON object, signaling no media attachments. That is the complete `.apkg` format for a text-only deck.

In testing with three sample cards, the script produced a structurally valid package: one collection row, notes and cards present with no dangling references, fields correctly separated by the 0x1f character. The resulting `.apkg` passes Anki's internal validation on import.

What the script does not do — deliberately — is confirm the import. It produces the file. The student double-clicks it in Anki. This is exactly the same boundary the Canvas export in Chapter 17 draws: the build step produces the artifact; the import step is the reader's action. The pipeline hands you the file. You hand it to Anki.

The default output path is `output/[book-slug].apkg`, derived from the title in `metadata.yaml`. Run it with:

```
python3 build-anki.py
```

Or with explicit paths:

```
python3 build-anki.py \
  --cards-dir recall \
  --chapters-dir chapters \
  --out output/my-book.apkg
```

The error message when no cards are found is explicit: "error: no recall cards found. Add recall/*.md (Q:/A: pairs) or a '## Recall' section to a chapter." The script will not write an empty deck.

---

## Worked Example: Three Cards Through the Pipeline

Suppose a chapter on the forgetting curve has a `## Recall` section containing these three cards:

```markdown
## Recall

Q: Who first measured the forgetting curve experimentally?
A: Hermann Ebbinghaus, working in the 1880s using nonsense syllables.

Q: What is the difference between recognition and retrieval?
A: Recognition is confirming that something is familiar when you encounter it.
   Retrieval is reconstructing the information from scratch without seeing it first.

Q: What does "desirable difficulty" mean in spaced repetition?
A: The effortfulness of retrieving a fading memory — hard enough to drive
   deeper encoding, close enough to not be lost.
```

The build-anki.py script reads the section, parses three Q:/A: pairs, and writes `output/deck.apkg`. The terminal reports:

```
Built: output/deck.apkg
  deck  : [Book Title]
  cards : 3
  note  : Basic (Front/Back), Anki schema 11
```

The student opens Finder or File Explorer, double-clicks `deck.apkg`, and Anki loads: three new cards waiting in the queue. The first day they see all three. SM-2 schedules the next review based on how they rated each one. Cards they answered easily are deferred a few days. Cards they blanked on come back tomorrow.

Three weeks later, they are still reviewing those cards — but less often. Three months later, the cards have stabilized into long intervals. The material from that chapter is available at the edge of forgetting when they need it, not lost in the decay curve.

---

## Named Trade-offs

**Cards are only as good as their authoring.** A deck full of compound cards — cards that ask two things at once — will train the wrong schedule. A deck of trivially easy cards (Q: "What is Anki?" A: "A flashcard app") will produce false confidence without genuine encoding. Writing good recall cards is a skill, and it is where the time goes in this layer. The Spaced-Repetition Card Generator prompt in Appendix — covers this.

**Decks rot when the source changes and is not rebuilt.** If you rewrite a chapter's explanation of a concept and forget to update `recall/`, the cards encode the old explanation. This is the same problem as stale pantry notes, stale canvas quizzes, stale anything: a build pipeline only keeps artifacts fresh if the source stays fresh. The fix is to rebuild the `.apkg` whenever you rebuild the EPUB — they are both products of the same source.

**The recall layer rewards facts; it does not reward synthesis.** A student with perfect recall of the spacing effect's mechanism may still fail to apply it to a new scenario. That application layer is what the case studies, glimmers, and LLM exercises in the rest of the enrichment layer are built for. Anki trains the substrate — the vocabulary and the explicit propositions — on which synthesis and judgment are built. The layers are designed to be used together.

---

## What You Author vs. What the Script Produces

| Author | Script |
|---|---|
| Q:/A: card pairs in `recall/*.md` or `## Recall` sections | SQLite schema-11 collection with `col`, `notes`, `cards` tables |
| Book title in `metadata.yaml` | Deck name in the Anki collection JSON |
| Chapter prose that the recall cards summarize | `collection.anki2` + `media` manifest in `.apkg` |
| Nothing (no media files required for text decks) | `media` file containing `{}` (empty JSON object) |

The author writes cards. The script writes the format. The student double-clicks the result.

---

## AI Wayback Machine — Piotr Wozniak

Piotr Wozniak developed the SM-2 algorithm in 1987 while studying biochemistry at the Adam Mickiewicz University in Poland. He was trying to learn English vocabulary and anatomy systematically, and he found that standard flashcard practice wasted time — reviewing cards that were still fresh, missing cards that had decayed. He built a spreadsheet to track intervals manually, derived the formula from his own data, and published it as a Turbo Pascal program. The program was called SuperMemo.

SM-2 is not the most sophisticated spaced repetition algorithm that exists. Later versions of SuperMemo (SM-15, SM-17, SM-18) use more complex models. Anki's implementation is based on SM-2 but modified. What Wozniak's work established — in 1987, before the modern web, before smartphones, before large-scale learning data — is that the forgetting curve is not a fate but an input. If you know the curve, you can schedule reviews to outrun it.

The relevant detail for an AI+1 author: the algorithm's parameters (initial factor 2500, initial intervals of 1 and 4 days, ease multiplier on correct answers) are stored in the `dconf` JSON blob in the collection's `col` row. They are editable. A textbook author who knows their material is highly technical and frequently reviewed might adjust these defaults. Most won't need to. Wozniak's defaults are well-calibrated starting points derived from decades of use.

> **Prompt to run in Claude or ChatGPT:**
>
> "Read the Wikipedia article on SuperMemo and on the SM-2 algorithm. Explain the SM-2 scheduling formula in plain language — what inputs does it take, what does it update, and what does the 'ease factor' represent? Then: what assumptions about memory does SM-2 make that might be wrong for some categories of learning, and where has the algorithm been criticized?"

The verification reflex: the Wikipedia articles on SuperMemo and SM-2 are detailed enough to test whether Claude's account of the algorithm matches the documented description. The criticism question is what makes this worth running — SM-2 was designed for vocabulary acquisition and has known limitations for procedural knowledge, concepts requiring elaboration, and skills that require application rather than recall. That limitation is the direct reason this chapter exists alongside glimmers and case studies rather than instead of them.

---

## Exercises

**Exercise 16.1 (Apply).** Open one chapter of your book in progress. Write a `## Recall` section at the bottom of the file with at least eight Q:/A: pairs covering the chapter's core concepts. Apply the atomic card rule: each card should test exactly one fact. Check your work by asking: could any card be split into two? If yes, split it. Deliver the section.

**Exercise 16.2 (Apply).** Run `python3 build-anki.py` from your book root. Confirm that `output/[slug].apkg` was produced and that the terminal output shows the correct card count. If you get "no recall cards found," diagnose: either the `recall/` directory is missing, the `.md` files are not in Q:/A: format, or the chapter sections are not headed with `## Recall`. Fix and rerun. Deliver the terminal output.

**Exercise 16.3 (Apply).** Double-click the `.apkg` file in Anki (or drag it onto the Anki window). Confirm that the deck appears in your Anki deck list with the correct card count. Start a review session and complete at least one full pass through the deck. Take a screenshot of the deck list showing the card count and the first review session.

**Exercise 16.4 (Evaluate).** Use the Spaced-Repetition Card Generator prompt from Appendix — to generate a set of recall cards for a chapter you did not author the cards for manually. Compare the generated cards to your hand-authored cards from Exercise 16.1 on three criteria: atomicity (one fact per card), coverage (do the cards cover what matters?), and difficulty calibration (are any cards trivially easy or impossibly compound?). Write one paragraph assessing where the generator adds value and where it needs editorial correction.

**Exercise 16.5 (Synthesize).** Consider the chapter you used for Exercises 16.1–16.4 alongside the case study and glimmer you may have authored for Chapters 14 and 15. Identify one concept in the chapter where recall cards are necessary but not sufficient — where a student who could answer every card correctly might still fail to apply the concept. Write the glimmer or case scenario that covers that application gap. This exercise has no single correct answer. Deliver the scenario and a one-paragraph explanation of why the recall layer alone did not cover it.

---

## Bridge — Chapter 17

The `.apkg` is in `output/`. The reader double-clicks it and the deck loads in Anki. The same chapter source that produced the EPUB and the Anki deck also contains quizzes, cases, and glimmers. The next delivery surface is the Learning Management System — the Canvas course package that turns a chapter into a full online course in a single upload. That script is also tested and runs from the same project directory.

Chapter 17 is about why Canvas needs a `.imscc` file and how `build-imscc-standard.py` produces one.

---

## Prompts

### Figure 16.1 — The spacing effect versus massed practice
Build a dual-curve comparison chart as a single self-contained HTML file with inline CSS and D3 7.9.0 from the cdnjs CDN. Data: two schematic forgetting curves — one showing retention decay after massed study (steeper, lower floor), one showing retention maintained above a threshold line by spaced reviews (shallower, review events marked as upward recovery spikes). Marks: two continuous line paths and a series of small vertical tick marks on the spaced-review curve to indicate review events. Channels: x encodes time (days), y encodes retention (0 to 100%). Zero-baseline on y. Annotate the two curves with "massed practice" and "spaced review" labels, the threshold line as "review window," and individual tick marks as review events. No numbers on axes — schematic only. Deliverable: one HTML file, inline CSS, D3 7.9.0, responsive via ResizeObserver, role="img" with title and desc.

### Figure 16.2 — The AI+1 recall authoring and build pipeline
Build a horizontal left-to-right flow diagram as a single self-contained HTML file with inline CSS and D3 7.9.0 from the cdnjs CDN. Data: five sequential nodes — (1) author Q:/A: pairs in recall/*.md or ## Recall, (2) build-anki.py reads card pairs, (3) writes SQLite schema-11 collection, (4) zips as .apkg, (5) student double-clicks to import into Anki. Include a branch from node 1 showing both source paths (recall/ dir and ## Recall section) merging before node 2. Marks: five rectangular nodes connected by forward arrows; the two source paths as a fan-in before node 2. Channels: x-position encodes step order; the two source branches are stacked vertically before converging. Annotation: node labels; a note on node 5 reading "manual step / reader's action." Deliverable: one HTML file, inline CSS, D3 7.9.0, responsive via ResizeObserver, role="img" with title and desc.

---

## References

1. Ebbinghaus, H. (1885). *Über das Gedächtnis: Untersuchungen zur experimentellen Psychologie*. Duncker & Humblot. (English translation: Ruger, H. A., & Bussenius, C. E. (1913). *Memory: A Contribution to Experimental Psychology*. Teachers College, Columbia University.)
2. Cepeda, N. J., Pashler, H., Vul, E., Wixted, J. T., & Rohrer, D. (2006). Distributed practice in verbal recall tasks: A review and quantitative synthesis. *Psychological Bulletin*, 132(3), 354–380.
3. Karpicke, J. D., & Blunt, J. R. (2011). Retrieval practice produces more learning than elaborative studying with concept mapping. *Science*, 331(6018), 772–775.
4. Roediger, H. L., & Karpicke, J. D. (2006). The power of testing memory: Basic research and implications for educational practice. *Perspectives on Psychological Science*, 1(3), 181–210.
5. Wozniak, P. (1998–present). SuperMemo algorithm SM-2. supermemo.com/en/blog/application-of-a-computer-to-improve-the-results-achieved-in-working-with-the-super-memo-method
6. Bjork, R. A. (1994). Memory and metamemory considerations in the training of human beings. In J. Metcalfe & A. Shimamura (Eds.), *Metacognition: Knowing about Knowing* (pp. 185–205). MIT Press.
7. Anki documentation. Getting Started; .apkg format. docs.ankiweb.net
