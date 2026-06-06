# 1. Rationale
I started this project during my sophomore fall, when I took CS 70. My good friend Rishab Bhatia introduced me to Obsidian, and I became fascinated by the platform's potential for note-taking. As I'm writing this, I'm in my junior spring. This means that it's been more than a year since I started to use Obsidian. Below I provide some guidelines on how to interpret everything in this hidden treasure of EECS. I also provide note-taking rules that I decided to set for myself when I realized that this vault is becoming too big, and that all notes are structured a tad bit differently, depending on my semesterly whims.

This vault is being prepared as an **open-source knowledge base**. That shapes everything that follows. A stranger landing on a random note should be able to (a) understand the concept from the intuition, (b) treat the opening callout as a complete cheat sheet they can return to, and (c) navigate outward through metadata and links to related ideas. The rules below exist to make that experience consistent across ~1,200 notes.

# 2. Structure
## 2.1 Macrocosm
- Primary (subject) folders are structured generally. They are sorted in order of creation.
- Secondary (field) folders are structured based on my interests, with a weight on importance.
- Every folder represents a single coherent topic. A subfolder with fewer than three notes and no meaningful sub-hierarchy gets flattened into its parent.
- Folder nesting does not exceed five levels below a primary folder. Deeper structure is a sign the hierarchy needs rethinking, not extending.
- Each folder contains an *index note* sharing the folder's name (e.g., `5. Linear Algebra.md` inside `5. Linear Algebra/`). Index notes are not placeholders — see §4.3.

## 2.2 Microcosm
- File names begin with a numeric prefix matching the folder hierarchy. Dots separate levels (e.g., `2.2.1 Mean Function.md`). A lowercase letter is appended only when a concept naturally splits into siblings at the same level (e.g., `2.5a Mixed Strategies.md`, `2.5b Pure Strategies.md`).
- Styles do not mix within a folder. The preferred vault-wide form is **no period after the number** (`2.1 Topic.md`, not `2.1. Topic.md`).
- Filenames use Title Case. Abbreviations are avoided unless the abbreviation is the canonical name of the concept (e.g., `SVD`, `LTI`, `KCL`, `NLP`).
- Every substantive note covers exactly one concept. A note that starts describing two things gets split — one concept per file, linked via §3.7. The one exception is the *comparison hub* — a note whose purpose is to compare a family of siblings against each other. See §3.3.
- A note is either *substantive* (contains content) or an *index note*. Empty stubs are not allowed in the main tree. Planned notes live in `_backlog/` until they are real.

# 3. Note Formatting
## 3.1 The Core Principle
**Clarity is the prime directive.** Every note must be readable by a smart undergraduate who has the prerequisites listed in the frontmatter and no more. The enemy is not length — it is *opacity*. A long, plainly-worded note is fine; a short note that leans on insider jargon is broken.

Three operational rules follow: (i) keep the `>[!note]` callout and Properties at their full reference detail — formulas, headline numbers, citations, and edge cases all stay; (ii) keep Intuition sections condensed to one or two tight paragraphs of plain prose; (iii) replace insider phrasing with plain English wherever it does not lose technical content, and inline-gloss unavoidable jargon the first time it appears. Filler hedges ("essentially," "fundamentally," "as we have seen") and meta-asides about the field get cut on sight.

Every substantive note serves two readers simultaneously:

- **The learner** reads it top-to-bottom to understand the concept. They need the intuition, the derivation, and the examples.
- **The returner** scans it to refresh their memory or grab a formula. They need the opening `>[!note]` callout to function as a complete, self-contained cheat sheet.

These two readers have opposite needs. The rules below are designed to serve both without compromising either. The short version: **the opening callout holds all concrete details; the body holds all understanding**.

## 3.2 The Canonical Template
Every substantive note follows this structure. Sections may be omitted only when they genuinely do not apply, but the order is fixed.

**Opening `>[!note]` callout — the cheat sheet.** The note begins with a `>[!note]` callout containing the formal definition and every concrete detail a returning reader would want at a glance: formulas, key notation, domain of applicability, assumptions, and canonical results. The subject term is **bolded** on first mention. No H1 heading precedes the callout. This section should be *dense*; if a reader only ever reads this block, they should still walk away with a correct and complete reference.

```
>[!note] Nash Equilibrium
>The **Nash equilibrium** of a strategic-form game $G = (N, (S_i), (u_i))$
>is a strategy profile $s^* \in \prod_i S_i$ such that for every player $i$,
>$$u_i(s_i^*, s_{-i}^*) \geq u_i(s_i, s_{-i}^*) \quad \forall s_i \in S_i.$$
>**Existence:** Every finite game has at least one Nash equilibrium in mixed strategies (*Nash's Theorem*).
>**Relation:** Every dominant-strategy equilibrium is a Nash equilibrium; the converse does not hold.
```

**`# Intuition` — the understanding.** A plain-English explanation of why the concept matters and how to think about it. Full sentences, not bullets. This is where the learning happens. The intuition section builds the mental model that the cheat sheet in the callout assumes.

**`# Properties`** — Named facts, theorems, and lemmas. Each property has three layers: a short italicized title, a one-sentence statement on the same line, and an explanation paragraph below.

```
#### *(Short Title)* One-sentence statement that captures the essence.

Explanation paragraph with the full statement, conditions, formulas, and edge cases.
```

The title is a $1$–$4$-word handle the reader uses to scan; the one-sentence is the gist; the paragraph below carries the full reference detail. **No layer repeats what an earlier layer already said** — each layer adds new content, so the paragraph never paraphrases the one-sentence. **And Properties never repeat the `>[!note]` callout** — the callout is the cheat sheet, and Properties exist to go beyond it. A surviving property should fall into at least one of these buckets: *mechanism* (the causal story behind the headline result); *implementation detail* (practical steps the cheat sheet omits); *hidden compositional shift* (the average hides regimes that look different inside); *robustness pattern* (cell-by-cell evidence the result is not a fluke); *why the deeper rebuttal also fails* (when the cheat sheet says "static models fail," the property explains that the conditional generalizations also fail); *failure mode or regime shift* (when and how the result breaks); *joint test across siblings* (constraints a complete account must satisfy across related notes); *how to read the headline number* (reframing what the average actually means). If a candidate property fits none of these buckets, it is almost certainly restating the callout and should be cut. Long proofs go inside a collapsible `>[!example]-` or get linked out to their own note.

**`# Derivation`** *(optional)* — Step-by-step mathematical reasoning for results that are derived from more primitive pieces.

**`# Examples`** — At least one worked example, each in a `>[!example]` callout. Solutions that would disrupt reading flow live in nested `>[!example]-` (collapsible) callouts. Examples are grounded: prefer concrete scenarios (cards, coins, robot arms, pharmaceutical trials) over abstract "Let $f$ be a function..." framings.

**`# See Also`** *(optional)* — A short bullet list of related notes as wiki-links. Used when a note has peer concepts that aren't naturally mentioned in the body.

## 3.3 Comparison Hubs
Some concepts exist *in families*. Activation functions (ReLU, GELU, Sigmoid, Softmax), optimizers (SGD, Momentum, Adam, AdamW), normalization layers (BatchNorm, LayerNorm, RMSNorm, GroupNorm), proof techniques, loss functions, regression metrics, classification metrics, op-amp configurations, matrix factorizations — in all of these, the reader's question is almost never "what is ReLU?" and almost always "which of these should I use, and how do they differ?" A single lumped note loses the depth the returner needs on any individual variant; a bare set of sibling notes loses the comparison the learner came for. The answer is a **comparison hub**.

A comparison hub is a first-class note type alongside concept notes and index notes. It has a parent *hub note* dedicated to side-by-side comparison, and a set of *sibling notes* — one per variant — where the full details live.

**The hub note structure.**

- **`>[!note]` callout.** States the family ("Activation functions introduce non-linearity into neural networks"), the shared interface (signature, domain, codomain), and — most importantly — the **decision rule**: one or two sentences telling the returning reader which variant to reach for by default and when to deviate. The decision rule is the whole reason the hub exists.
- **`# Intuition`** explains what the family has in common and what axis the variants trade off along (smoothness vs. sparsity, bias vs. variance, compute vs. accuracy). Name the tension.
- **`# Comparison Table`** is a Markdown table with one row per variant. Columns are the dimensions that matter for choosing between them — for activation functions: formula, derivative, range, monotonic, saturating, zero-centered, default use, failure mode. Every row links to its sibling.
- **`# When to Use Which`** is a short prose section walking through the decision tree: "use X by default; switch to Y when saturating gradients are a concern; switch to Z when memory is tight."
- **`# See Also`** links to every sibling and to the closest concept-note neighbors.

**The sibling note structure.**

- A sibling is a normal concept note following §3.2 in full — dense callout, intuition, properties, derivation (if applicable), examples, diagrams.
- Its `>[!note]` callout contains one additional line placing it relative to its siblings: "ReLU is the default activation in CNNs; GELU replaces it in transformers for smoother gradients." This is the only place the sibling references the comparison.
- The sibling does not repeat the comparison table. It links back to the hub.

**When to build a hub.**

- Three or more variants share a signature or interface.
- A reader choosing between them needs the same information about each one.
- The variants exist *because* they trade off along a known axis.

**When not to build a hub.**

- Only two variants exist — use a single concept note with a short `# Variants` subsection.
- The variants don't share an interface. "Sorting algorithms" is too broad; "O(n log n) comparison sorts" is narrow enough.
- No general decision rule can be written. If the "When to Use Which" section can only say "it depends," skip the hub.

**Retrofit workflow.** Some notes in the vault started life as a single lumped file precisely *because* the comparison was the point. Turning one of those into a hub means: extract each variant into its own sibling note with the full §3.2 treatment, keep the original file as the hub (same title and numeric prefix), rewrite the hub's callout around the decision rule, build the comparison table, write "When to Use Which," add the See Also, and update every wiki-link that used to point at the lumped note.

## 3.4 Callouts
- `>[!note]` is reserved for the opening cheat-sheet callout. It does not appear mid-note.
- `>[!warning]` marks common misconceptions, edge cases, and notational caveats. Every warning gets a descriptive title (e.g., `>[!warning] Fictitious Forces`, not just `>[!warning]`).
- `>[!example]` marks worked problems. `>[!example]-` (collapsible) hides the solution when it would otherwise overwhelm the note.
- No custom callout types. If `note`, `warning`, and `example` aren't enough, the content belongs in a different section.

## 3.5 Mathematics
- Inline math uses `$...$`. Block math uses `$$...$$`. Multi-line equations use `\begin{align}...\end{align}` inside a block.
- Notation is consistent within a domain. Probability uses `\mathbb{P}[...]` and `\mathbb{E}[...]`. Physics uses vector arrows `\vec{v}`. Linear algebra uses `\mathbf{v}` for vectors and capital letters for matrices. Sets use `\mathbb{R}`, `\mathbb{Z}`, `\mathbb{N}`.
- Every symbol introduced in an equation is defined in prose, either right before or right after it. No floating variables.
- Orphaned math fragments (e.g., a lone `$$\hat{X}$$` left over from editing) get deleted on sight.

## 3.6 Diagrams & Images
- TikZ is preferred for any diagram that is geometric, algebraic, or schematic. TikZ blocks live in fenced ` ```tikz ` code blocks. TikZ is version-controllable and reviewable, which matters for an open-source knowledge base.
- Screenshots are used only when the content is genuinely visual and cannot be reproduced in TikZ (photographs, figures from papers).
- Screenshots live in `/attachments/<domain>/`, not the flat root. They are renamed descriptively at import time (`sigmoid-curve.png`, not `Screenshot 2025-10-20 at 2.21.10.png`).
- Every embedded image has alt text: `![[sigmoid-curve.png|Sigmoid activation]]`.

## 3.7 Cross-Linking
- Every substantive note contains **at least three** wiki-links. If three can't be found, the note is too isolated and is probably missing context.
- Links use display-text aliasing when the filename would read awkwardly: `[[1.3 Conditional Probability|conditional probability]]`, not `[[1.3 Conditional Probability]]` mid-sentence.
- Links go in three directions: *upward* to prerequisite concepts, *sideways* to peer concepts, and *downward* to dependent concepts (in the See Also section).
- Cross-domain links are strongly encouraged. Linking Probability ↔ Statistics, Linear Algebra ↔ Machine Learning, and Multivariable Calculus ↔ Physics is exactly what the graph view is for, and it's what makes the vault valuable as a cross-disciplinary reference.
- If a concept belongs under one domain but is used in another, it lives in its native domain and is linked from the other. No duplicate notes.

## 3.8 Writing Voice
- The voice is textbook-formal but not dry. Definitions are precise; intuition sections are conversational. "We" and "Consider..." are fine. Casual asides are not.
- Bold is reserved for the subject term on first mention and for key terms being defined in passing. Italics are reserved for `*(property names)*` inside `####` headers and for emphasis.
- No filler. Every sentence either defines, explains, or exemplifies. Transitions like "As we have seen..." and "It is important to note that..." get cut.
- First-person ("I", "my") does not appear in substantive notes. The README is the only place for personal voice.
- Assume the reader is a motivated stranger. They are smart and curious, but they don't share your course context, your semester, or your inside references.

## 3.9 File Length
- Target length for a substantive note is **60–150 lines**. Below 30 lines, the note is probably missing Intuition or Examples. Above 250 lines, it probably needs to be split.
- The opening `>[!note]` callout is typically 5–15 lines. If it's one line, the cheat-sheet principle isn't being honored.

# 4. Metadata
The metadata layer is what turns a folder of markdown files into a queryable, navigable knowledge base. For an open-source vault, it's also the primary way strangers discover and filter content. Metadata discipline is not optional.

## 4.1 Frontmatter Schema
Every substantive note begins with YAML frontmatter. The full schema is:

```yaml
---
title: Nash Equilibrium
aliases: [Nash equilibrium, NE]
tags:
  - math/game-theory
  - type/definition
  - topic/equilibrium
  - level/intermediate
  - status/complete
course: CS70
created: 2024-10-15
updated: 2025-03-02
prerequisites:
  - "[[2.1 Strategic Form Game]]"
  - "[[2.2 Best Responses]]"
---
```

Field definitions:

- `title` — Human-readable name of the concept, without the numeric prefix. Used by Dataview and by external tools that ingest the vault.
- `aliases` — Alternate names so wiki-links resolve without display-text tricks. Include common abbreviations, alternate spellings, and historical names.
- `tags` — Structured tags following the taxonomy in §4.2. Always include at least one `domain/`, one `type/`, and one `status/` tag.
- `course` — The Berkeley course code where the concept was first encountered (e.g., `CS70`, `EE120`, `MATH110`). This preserves the historical trail and lets readers filter by course.
- `created` — ISO date (`YYYY-MM-DD`) the note was first written.
- `updated` — ISO date of the most recent substantive revision. Omit if equal to `created`.
- `prerequisites` — Explicit list of notes the reader should already understand. Written as wiki-links in quotes. This is the single most valuable field for a learning-oriented knowledge base: it makes the dependency graph explicit rather than implicit.

Index notes use a reduced schema (`title`, `tags`, `updated`) — see §4.3.

## 4.2 Tag Taxonomy
Tags are structured, not freeform. Every tag belongs to one of a fixed set of namespaces, and each namespace answers a specific question about the note.

**`domain/` — What field is this?**
One per note. Values: `math`, `cs`, `stats`, `econ`, `ee`, `physics`. Subdomains are encoded as nested paths:
`math/probability`, `math/linear-algebra`, `math/game-theory`, `cs/machine-learning`, `cs/deep-learning`, `cs/computer-vision`, `cs/nlp`, `cs/robotics`, `cs/architecture`, `cs/algorithms`, `ee/circuits`, `ee/signals`, `physics/mechanics`, `stats/inference`, `stats/time-series`, `stats/bayesian`, `econ/finance`, `econ/money`, `econ/markets`.

**`type/` — What kind of note is this?**
One per note. Values: `definition`, `theorem`, `lemma`, `identity`, `algorithm`, `model`, `method`, `framework`, `principle`, `technique`.

**`topic/` — What conceptual theme does it belong to?**
Zero or more. Cross-cuts domains. Examples: `topic/optimization`, `topic/equilibrium`, `topic/duality`, `topic/symmetry`, `topic/convergence`, `topic/transformation`, `topic/uncertainty`. Use sparingly — if a topic tag only ever applies to one note, delete it.

**`level/` — How advanced is this?**
One per note. Values: `intro` (first-semester freshman level), `intermediate` (upper-division), `advanced` (graduate level). This is essential for open-source readers coming in without the Berkeley course context.

**`status/` — Is this ready for public consumption?**
One per note. Values: `complete` (ready to ship), `draft` (has content but needs review), `stub` (placeholder, lives in `_backlog/`), `needs-examples`, `needs-intuition`. The `needs-*` statuses make it easy to generate to-do lists with Dataview.

Tags that don't fit one of these namespaces are not allowed. The vault does not use flat hashtags like `#important` or `#review`.

## 4.3 Index Notes
Index notes are the backbone of navigation. Every folder has one, and it is the first thing a stranger sees when entering that folder. Their schema and structure are different from substantive notes.

Index note frontmatter:

```yaml
---
title: Linear Algebra
tags:
  - math/linear-algebra
  - type/index
updated: 2026-04-06
---
```

Index note body contains:

- A 2–4 sentence overview explaining what the folder covers and why a reader might care.
- A **Prerequisites** section with wiki-links to notes in other folders needed to understand this section.
- A **Contents** section listing every child note as a wiki-link, in reading order, with a one-line gloss after each. This is the table of contents.
- A **Recommended path** section (optional) suggesting which notes to read first if the reader only has time for three.

Index notes do not use the `>[!note]` callout, do not contain concept definitions, and do not have a `# Intuition` section. If an index note starts looking like a regular note, the content gets moved out.

## 4.4 Dataview-Friendliness
The metadata schema above is designed to work cleanly with the Dataview plugin, so that readers (and the maintainer) can run queries like:

- `FROM #domain/math/probability WHERE status = "complete"`
- `LIST FROM #level/intro SORT course`
- `TABLE prerequisites FROM #type/theorem WHERE contains(course, "CS70")`

Fields are always written as YAML lists (not comma-separated strings) so Dataview parses them correctly. Wiki-links inside YAML values are always wrapped in quotes.

# 5. File Naming
- Filenames match the `[number] [Title].md` pattern exactly.
- No typos. `Classifcation.md` → `Classification.md`. Fixed on sight.
- No duplicate titles across the vault. The numeric prefix disambiguates if needed.
- Renaming a note requires updating every wiki-link that points to it. Obsidian's rename tool does this automatically; manual renames via the filesystem do not, and are forbidden.

# 6. Maintenance
- **Stub policy.** Empty files are forbidden in the main tree. Planned notes live in `_backlog/` with a one-line description of eventual content. When a note gets written, it is pulled out of `_backlog/` and into its permanent home.
- **`.trash/` is temporary.** Files in `.trash/` older than one semester are permanently deleted. The vault's git history is the long-term record, not `.trash/`.
- **Cross-link audit.** Once a semester, the graph view is checked for orphans. Every note should be reachable from at least one index note and from at least one peer note.
- **Metadata audit.** Once a semester, all notes get grepped for missing frontmatter fields. Any note without `domain/`, `type/`, `status/`, and `level/` tags is flagged.
- **Template refactor.** When retrofitting old notes, the priority order is: (1) populate the `>[!note]` callout with concrete cheat-sheet content, (2) add `# Intuition`, (3) add at least one `# Examples` entry, (4) add wiki-links, (5) add frontmatter. A partially-retrofitted note is better than a pristine one that never ships.
- **Rule changes.** When the rules in this README change, git commit messages start with `rules:`. No silent drift.

# 7. Quick Reference
When creating a new note:

1. Decide the folder. Use the numeric prefix of the parent.
2. Create the file with the full `[number] [Title].md` name.
3. Add frontmatter: `title`, `aliases`, `tags` (domain + type + level + status), `course`, `created`, `prerequisites`.
4. Write the `>[!note]` callout as a dense, self-contained cheat sheet.
5. Write `# Intuition`.
6. Write `# Properties` (if applicable).
7. Write `# Derivation` (if applicable).
8. Write `# Examples` with at least one worked problem.
9. Add at least three wiki-links throughout the body.
10. Update the parent folder's index note to reference the new file.
