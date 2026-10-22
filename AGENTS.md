# AGENTS.md

## Explanation style

The point of this wiki is learning: take something complex and explain it simply.

**Match the model to the topic and its complexity.** There is no fixed menu and no required set of models. The names below are examples, not a closed list. Choose whatever lens makes this particular subject clearest, and combine lenses when useful.

| Lens                                          | What it means                                                                                                                                                                                                                                                                                            | Use when                                                             |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Pareto 80/20**                              | A small share of causes often drives most of the result. It is a heuristic, not a law; real ratios vary (e.g. 90/10 or 70/30).                                                                                                                                                                           | Many factors compete and priorities are unclear.                     |
| **ASD-STE100 (Simplified Technical English)** | Controlled technical English: one idea per sentence, active voice, common words, short sentences. Issue 9 (2025) has 53 rules and about 900 approved words, with limits of 20 words per procedural sentence and 25 per descriptive sentence. Borrow the principles, not necessarily the full dictionary. | Procedures and dense technical text.                                 |
| **First principles**                          | Strip the topic to its basic truths, then rebuild the explanation from there.                                                                                                                                                                                                                            | A mechanism is confusing or conventional explanations are hand-wavy. |
| **Analogy**                                   | Map the unfamiliar onto something the reader already knows, and say where the comparison breaks.                                                                                                                                                                                                         | The idea is unfamiliar or abstract.                                  |
| **Inversion**                                 | Explain by showing what fails, what the thing is not, or how it goes wrong.                                                                                                                                                                                                                              | Reasoning forward is hard, or hidden assumptions need exposing.      |
| **Feynman technique**                         | Explain in plain language as if teaching a beginner; gaps in the explanation reveal what to relearn.                                                                                                                                                                                                     | Checking understanding or building intuition.                        |
| **Worked example**                            | Show one concrete case solved step by step.                                                                                                                                                                                                                                                              | Rules feel abstract and the reader needs to see them applied.        |
| **Progressive disclosure**                    | Start with the minimum needed, then add detail in layers.                                                                                                                                                                                                                                                | The topic is too large to absorb at once.                            |
| **Contrast**                                  | Compare the idea with a close neighbour (e.g. Git vs GitHub).                                                                                                                                                                                                                                            | Two concepts are easily confused.                                    |

This table is illustrative, not exhaustive. If another lens fits better — systems thinking, 5 Whys, diagrams, storytelling, decision tables, or any other model not listed here — use it. Do not limit yourself to this table: pick whichever lens is best for the topic, even if it is not listed, and combine lenses when useful.

**Selection guide**

- Many parts, unclear priorities → Pareto.
- Dense instructions or error-prone steps → ASD-STE100.
- A confusing mechanism → first principles.
- An unfamiliar abstract idea → analogy.
- A problem that is hard to reason forward → inversion.
- Passive understanding, no intuition → worked example or Feynman.
- Overwhelming scope → progressive disclosure.

**Rules that always apply**

- Identify the core idea and the likely source of confusion before writing, then pick the model that removes that confusion.
- Simplicity is clarity, not terseness. Never drop a fact, condition, or caveat to sound simple; split the sentence or add an example instead.
- Length follows complexity. Simple topic → short note. Complex topic → as long as needed, but structured with headings, examples, and a short summary.
- Define jargon on first use; prefer concrete examples over abstractions.
- Do not force a model. A plain explanation is better than a stretched analogy.
- **Do not assume anything.** Search the web for factual information — facts, numbers, dates, quotes, and current information — before writing it. Do not rely on memory. If a claim cannot be verified, say so or omit it.
- Separate fact from analogy or opinion, and flag uncertainty.
- End a complex explanation with a brief "the gist" summary.

## Wiki organization rules

Content lives in `content/`. The site is built with Quartz; run `npx quartz build --serve` to preview (`npm run docs` builds the bundled help docs, not this wiki).

Structure emerges just-in-time from what is actually written. There is no predefined taxonomy and no empty folders; folders are created only when notes earn them.

### Current state

Everything is flat at the root of `content/`: `git.md`, `github.md`, `tailscale.md`, `index.md`.

### Promotion rules

- **Flat by default** — new notes go at the `content/` root.
- **Promote at 3** — when a theme has 3+ related notes, create one folder and move them in. Not before.
- **Subdivide at 7+** — if one category grows past 7 notes, split it along the clearest axis. Keep 3–6 subfolders.
- **Flatten at 1–2** — if a folder drops to 1–2 notes, move them back up.
- **Cap at 10** — no more than 10 top-level categories. Adding an 11th means merging two existing ones.
- **Max depth 3** — `category/subfolder/note.md`. Deeper relationships belong in links and tags, not folders.

### Tags as a staging area

Hierarchical tags (`tools/version-control`, `systems/linux`) encode a tentative category without committing to a folder, and Quartz renders a page for every tag. When a tag collects roughly 5–7 notes, that is the signal to promote it into a folder.

### Explanation model tags

Every note also records the lens or lenses used to explain it, under `explanation/`:

- `explanation/pareto`
- `explanation/asd-ste100`
- `explanation/first-principles`
- `explanation/analogy`
- `explanation/inversion`
- `explanation/feynman`
- `explanation/worked-example`
- `explanation/progressive-disclosure`
- `explanation/contrast`

Use one to three primary lenses, not every technique that appears in the note. For any other model, use `explanation/<model-name>`. These tags create tag pages, so notes can be browsed by explanation style.

### Creating a note

1. Pick the lens that fits the topic and complexity (see the table above).
2. Add frontmatter with `title`, one category tag, and one to three `explanation/` tags.
3. Put the note at the `content/` root; link it from `index.md` or a related note.
4. Check the result. With `npx quartz build --serve` running, the page rebuilds on save. Run a full `npx quartz build` after a move, rename, new folder, or before publishing.

Do not leave a note without an `explanation/` tag. If no single lens dominates, tag the one that shaped the explanation most.

### Mechanics

- Keep shortest `[[Note]]` links. They survive file moves as long as filenames stay unique. Do not rename `git.md` or `github.md`; that would break existing links.
- Every folder gets an `index.md` with a `title` and a one-line description; otherwise Quartz generates a plain folder listing.
- Filenames are lowercase kebab-case (`git-rebase.md`); display names come from the `title` frontmatter.
- After any move, verify with `npx quartz build` (without `-d docs`) and check the explorer and folder page.

### Git

Do not commit unless explicitly asked.
