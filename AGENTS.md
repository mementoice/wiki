# AGENTS.md

## Explanation style

The point of this wiki is learning: take something complex and explain it simply.

A **lens** is a model or framework used to explain a topic. **Two lenses are mandatory in every content note: Pareto 80/20 and ASD-STE100.** Pareto decides what matters; ASD-STE100 decides how to say it. Extra lenses are optional; add them only when they help. The names below are examples, not a closed list.

| Lens                                          | What it means                                                                                                                                                                                                                                                                                            | Use when                                                             |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Pareto 80/20**                              | A small share of causes often drives most of the result. It is a heuristic, not a law; real ratios vary (e.g. 90/10 or 70/30).                                                                                                                                                                           | Always. Decide what to explain first and what to leave out.          |
| **ASD-STE100 (Simplified Technical English)** | Controlled technical English: one idea per sentence, active voice, common words, short sentences. Issue 9 (2025) has 53 rules and about 900 approved words, with limits of 20 words per procedural sentence and 25 per descriptive sentence. Borrow the principles, not necessarily the full dictionary. | Always. Keep sentences short and clear, with one idea each.          |
| **First principles**                          | Strip the topic to its basic truths, then rebuild the explanation from there.                                                                                                                                                                                                                            | A mechanism is confusing or conventional explanations are hand-wavy. |
| **Analogy**                                   | Map the unfamiliar onto something the reader already knows, and say where the comparison breaks.                                                                                                                                                                                                         | The idea is unfamiliar or abstract.                                  |
| **Inversion**                                 | Explain by showing what fails, what the thing is not, or how it goes wrong.                                                                                                                                                                                                                              | Reasoning forward is hard, or hidden assumptions need exposing.      |
| **Feynman technique**                         | Explain in plain language as if teaching a beginner; gaps in the explanation reveal what to relearn.                                                                                                                                                                                                     | Checking understanding or building intuition.                        |
| **Worked example**                            | Show one concrete case solved step by step.                                                                                                                                                                                                                                                              | Rules feel abstract and the reader needs to see them applied.        |
| **Progressive disclosure**                    | Start with the minimum needed, then add detail in layers.                                                                                                                                                                                                                                                | The topic is too large to absorb at once.                            |
| **Contrast**                                  | Compare the idea with a close neighbour                                                                                                                                                                                                                                                                  | Two concepts are easily confused.                                    |

Pareto and ASD-STE100 always apply. This table is illustrative, not exhaustive. If another lens fits better — systems thinking, 5 Whys, diagrams, storytelling, decision tables, or any other model not listed here — use it. Do not limit yourself to this table: pick whichever lens is best for the topic, even if it is not listed, and combine lenses when useful. Keep this table short: add a row only for a lens that is used repeatedly.

**Selection guide**

- Pareto and ASD-STE100 → every content note, as the baseline.
- A confusing mechanism → first principles.
- An unfamiliar abstract idea → analogy.
- A problem that is hard to reason forward → inversion.
- Passive understanding, no intuition → worked example or Feynman.
- Overwhelming scope → progressive disclosure.

**Rules that always apply**

- Apply Pareto first: find the vital few ideas that explain most of the topic. Use it to choose scope and depth, never to drop a required fact or caveat.
- Apply ASD-STE100 to the prose: one idea per sentence, active voice, short sentences.
- Identify the core idea and the likely source of confusion before writing, then pick any extra lens that removes that confusion.
- Simplicity is clarity, not terseness. Never drop a fact, condition, or caveat to sound simple; split the sentence or add an example instead.
- Length follows complexity. Simple topic → short note. Complex topic → as long as needed, but structured with headings, examples, and a short summary.
- Define jargon on first use; prefer concrete examples over abstractions.
- Do not force an optional lens. The two baseline lenses always apply, but a plain explanation is better than a stretched analogy.
- **Do not assume anything.** Search the web for factual information — facts, numbers, dates, quotes, and current information — before writing it. Do not rely on memory. If a claim cannot be verified, say so or omit it.
- Separate fact from analogy or opinion, and flag uncertainty.

### Pareto summary

Start every content note with a fenced code block. Inside it, write 3–6 short bullet points that give the vital 20%: the core ideas, facts, names, and distinctions a reader must remember. Keep it conceptual; procedures and configuration details belong in the body. Avoid vague lines that could describe any note or merely restate the title. A reader should be able to recall the concept from the block alone. Do not use it for a full outline.

## Wiki organization rules

Content lives in `content/`. The site is built with Quartz; run `npm run serve` (or `npx quartz build --serve`) to preview (`npm run docs` builds the bundled help docs, not this wiki). Use `--serve` for local preview; do not serve `public/` directly at the server root. The production `baseUrl` includes `/wiki`, so a non-serve build links to `/wiki/...` and those links return 404 locally.

Structure emerges just-in-time from what is actually written. There is no predefined taxonomy and no empty folders; folders are created only when notes earn them.

### Promotion rules

- **Flat by default** — new notes go at the `content/` root.
- **Promote at 3** — when a theme has 3+ related notes, create one folder and move them in. Not before.
- **Subdivide at 9+** — when one category has 9 or more notes, split it into 2–3 subfolders, each with at least 3 notes.
- **Flatten at 1–2** — if a folder drops to 1–2 notes, move them back up.
- **Cap at 10** — no more than 10 top-level categories. Adding an 11th means merging two existing ones.
- **Max depth 3** — `category/subfolder/note.md`. Deeper relationships belong in links and tags, not folders.

### Tags as a staging area

Tags are lowercase kebab-case under a namespace, such as `tools/version-control` or `systems/linux`. They encode a tentative category without committing to a folder, and Quartz renders a page for every tag.

A tag is a staging area, not a second folder system. Three notes that clearly belong together become a folder now. A tag that keeps appearing across 5–7 otherwise unrelated notes is a signal to consider a folder — but only if it names a stable category. Cross-cutting tags stay tags.

### Creating a note

1. Apply Pareto to choose the vital few ideas. Start the note with a fenced code block of bullet points that gives the vital 20%.
2. Apply ASD-STE100 to the prose.
3. Add frontmatter with `title` and one category tag.
4. Put the note at the `content/` root; link it from `index.md` or a related note.
5. Check the result. With `npx quartz build --serve` running, the page rebuilds on save. Run a full `npx quartz build` after a move, rename, new folder, or before publishing.

Every content note starts with the Pareto summary block. Home, folder, and tag index pages are exempt.

### Mechanics

- Keep shortest `[[Note]]` links. They survive file moves as long as filenames stay unique.
- Every folder gets an `index.md` with a `title` and a one-line description; otherwise Quartz generates a plain folder listing.
- Filenames are lowercase kebab-case (`git-rebase.md`); display names come from the `title` frontmatter.
- After any move, verify with `npx quartz build` (without `-d docs`) and check the explorer and folder page.

### Git

Do not commit unless explicitly asked.
