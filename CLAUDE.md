# CLAUDE.md

Instructions for working in Project Alexandria. The README defines the rules; this file defines how to apply them. Read both before touching any note.

## Clarity Is the Prime Directive

Notes must be **clear and accessible** to a smart undergraduate who has the prerequisites listed in the note's frontmatter — no more, no less. Length is not the enemy; *opacity* is. A note can be long and excellent if every sentence is understandable. A note can be short and broken if it leans on unexplained jargon.

Operationally:
- **Keep callouts and Property statements at full length.** They are reference material. "Concise" there means *no filler*, not *fewer facts*. Formulas, headline numbers, citations, edge cases all stay.
- **Condense Intuition sections.** One or two tight paragraphs are usually enough. Cut narrative loops, repeated framings, and meta-commentary about the field.
- **Simplify vocabulary.** Replace insider phrasing with plain English wherever it does not lose technical content. Avoid filler-jargon like "directionally agnostic," "post-academic-discovery era," "self-reinforcing flow dynamics," "ICAPM specifications," "data mining of post-publication samples."
- **Inline-gloss unavoidable jargon.** When a technical term is genuinely needed, define it in the same sentence the first time it appears: *"ex-ante volatility (the volatility forecast made before the position is held)."*
- **Cut filler hedges:** "essentially," "fundamentally," "approximately" used as filler, "it is important to note that," "as we have seen."
- **Examples can stay long** — they teach by being concrete. Just keep the prose plain.

Clarity and completeness are both non-negotiable. The discipline is "every necessary thing said once, in plain language" — not "as short as possible."

## Core Mandate

Project Alexandria is an open-source knowledge base. Every note serves two readers at once:

1. **The learner** — a motivated stranger who doesn't share Mihail's course context. They read top-to-bottom to understand the concept for the first time.
2. **The returner** — someone (often Mihail himself) who already understands the concept and wants to grab a formula, refresh a definition, or verify a detail at a glance.

These two readers have opposite needs. Serving both is the whole point of the vault's structure. If a note only serves one, it's broken.

Before writing anything, ask: *who am I serving with this sentence?* If the answer is "the returner," it belongs in the opening `>[!note]` callout. If the answer is "the learner," it belongs in `# Intuition` or `# Examples`. Nothing belongs in both.

## How to Think Before Writing

Writing a note starts long before the first character. Work through this sequence:

**Identify the concept, precisely.** One note covers one concept. If the working title is "Eigenvalues and Eigenvectors," stop — that's two notes. If it's "Nash Equilibrium," that's one. When in doubt, ask: can the intuition be explained in a single coherent paragraph? If yes, it's one note. If the paragraph keeps branching, split it.

**Locate it in the hierarchy.** Find the folder it belongs in. If no obvious home exists, that's a signal the hierarchy is missing a subfolder — raise it before creating the note. Never create orphans that live loose in a primary folder.

**Map the prerequisites.** List every concept a reader would need to understand this one. Check that each prerequisite has its own note. If it doesn't, either (a) create the prerequisite note first, or (b) add it to `_backlog/` and link forward to the backlog entry. The `prerequisites` frontmatter field is populated from this list.

**Map the dependents.** Ask: what future notes will link *to* this one? This shapes what goes in the opening callout. A heavily-depended-upon concept needs a denser cheat sheet because many future notes will rely on it as a reference.

**Decide the level.** Who is the concept for? First-semester freshmen (`level/intro`)? Upper-division (`level/intermediate`)? Graduate (`level/advanced`)? The level shapes tone, assumed background, and depth of derivation.

Only after all five steps is the note ready to be written.

## Writing the `>[!note]` Callout

The opening callout is the single most important part of any note. It is the cheat sheet. Treat it like a contract: if a returning reader reads only this block, they must walk away with a correct, complete, and actionable understanding of the concept.

A good opening callout contains:

- **The formal definition**, stated with full rigor and every quantifier in place.
- **The key formula or formulas**, written as block math with all variables defined.
- **The domain of applicability** — when does this apply, and when does it not?
- **Canonical assumptions** — what conditions must hold?
- **Headline results** — existence, uniqueness, convergence, complexity, whatever applies.
- **Relationships to neighbors** — "every X is a Y, but not vice versa" is often the most useful line in the entire note.

A bad opening callout is one line that just restates the title. If the callout is under five lines, it isn't doing its job.

The callout is written *last*, not first. Write the Intuition and Derivation first — they help you figure out what actually matters. Then distill the cheat sheet from what you've written. This is counterintuitive but important: the callout is a summary, and summaries require the full thing to exist first.

## Writing the `# Intuition` Section

The intuition section is where learning happens. It is prose, not bullets. It assumes the reader knows the prerequisites but knows nothing about this specific concept. Its job is to build the mental model that the rest of the note assumes.

Principles for good intuition:

- **Start with the "why."** Why does this concept exist? What problem does it solve? What goes wrong without it? A reader who doesn't know why a concept exists can't remember it.
- **Use concrete imagery.** Abstract math becomes memorable when tied to something physical or visual: "zooming in on the world where A happened," "rotating the coordinate system until the matrix becomes diagonal," "finding the direction of steepest descent."
- **Name the central tension.** Most interesting concepts exist because two things are in tension. Identify it.
- **One or two paragraphs is the target.** If the intuition runs longer than three paragraphs, it probably contains content that should be in Properties or Examples.
- **Never repeat the formal definition.** The reader already saw it in the callout. Restating it in prose wastes their time.

Do not begin the intuition with "Intuitively, ..." — it's filler. Just start explaining.

## Writing Examples

Examples are where understanding gets tested. A note without examples is incomplete, even if the intuition is airtight.

Rules for examples:

- **Ground them in reality.** Pharmaceutical trials, card games, Monty Hall, robot arms, coin flips, physical setups — always prefer a scenario over "Let $f$ be a function..." framings. Abstract examples don't build memory.
- **Vary the difficulty.** If a concept has multiple layers, include examples at multiple levels. Physics already labels these (Easy/Medium/Hard) — extend this practice.
- **Show the full solution, collapsed.** Use `>[!example]-` to hide solutions so the reader can attempt the problem first. This matters more than it seems — passive examples teach less than interactive ones.
- **Pick examples that exercise the non-obvious.** If an example can be solved by plugging into the formula mechanically, it isn't a good example. Good examples force the reader to think about *which* property applies, *when* to use it, or *why* it works.
- **One worked example minimum.** Three is ideal. More than five is usually too many — examples should be curated, not exhaustive.

## Visual Aids and TikZ Diagrams

TikZ diagrams are one of the vault's most underused levers. A good diagram frequently teaches more than a paragraph of prose, and concepts like Convex Sets, Convex Optimization, Eigenvectors, Gram-Schmidt, and Bayes' Rule become dramatically clearer with the right visual. Be aggressive about adding TikZ wherever it would serve a visual learner, even when retrofitting a note that currently has none.

**Concepts that almost always benefit from a diagram:**

- **Geometric objects.** Convex sets, half-spaces, polytopes, hyperplanes, affine subspaces, conic sections, manifolds — anything defined by a shape in space.
- **Transformations and mappings.** Linear maps, rotations, projections, coordinate changes, feature maps, graph morphisms. Show the before and after.
- **Vector and matrix operations.** Gram-Schmidt orthogonalization, SVD decomposition, eigendecomposition, change of basis. These are geometric at heart even when they're usually presented algebraically.
- **Functions and their properties.** Convex vs. non-convex functions, Lipschitz continuity, fixed points, critical points, saddle points, level sets, gradient fields.
- **Probability and information.** Venn diagrams for events, sample spaces, probability trees, distribution plots, decision boundaries, entropy visualizations.
- **Dynamics and equilibria.** Phase portraits, best-response correspondences, game matrices, stability regions, vector fields.
- **Circuits and signals.** Circuit schematics (via CircuiTikZ), signal waveforms, block diagrams, stem plots, Bode plots.
- **Physical setups.** Free-body diagrams, coordinate systems with labeled axes, trajectories, fluid flows, collision geometries.
- **Algorithmic and architectural structures.** Neural network layers, data structures (trees, graphs, heaps), state machines, pipeline diagrams.

**Where diagrams belong inside a note:**

- **In the `# Intuition` section** to build the initial mental model. Place the diagram before or immediately after the paragraph that introduces the geometric/visual framing.
- **Inside a property** to illustrate a specific fact. A property like "*the intersection of convex sets is convex*" is nearly free to diagram and far more memorable with one.
- **Inside an example** to set up the scenario. A worked problem about a pulley system, a game matrix, or a probability tree almost always wants a diagram before the algebra starts.

**Where diagrams do *not* belong:**

- In the opening `>[!note]` callout. The callout is a dense reference — diagrams bloat it. Exceptions are rare and should be genuinely tiny.
- In the `# Derivation` section, unless the derivation is itself geometric. Derivations are symbolic; diagrams compete with the steps.
- As decoration. If removing the diagram does not hurt the reader's understanding, delete it.

**Principles for good TikZ:**

- **Label everything.** Unlabeled axes, unnamed points, and anonymous vectors teach nothing. Every object in the diagram has a name the reader can refer to.
- **Use color with purpose, not for decoration.** Color distinguishes categories (feasible vs. infeasible region, positive vs. negative eigenvalue, input vs. output) — it does not just prettify. Three colors is usually the maximum.
- **Minimize what's on the canvas.** A diagram with one idea beats a diagram with five. If a concept has multiple visual aspects, make multiple diagrams rather than one cluttered one.
- **Match the prose.** Variables in the diagram use the same symbols as the prose. If the text says $\vec{v}_1$, the diagram does not say $\mathbf{a}$.
- **Reproduce, don't scan.** A hand-drawn diagram from a lecture slide should be rebuilt in TikZ, not screenshotted. TikZ is version-controllable, editable, and consistent with the rest of the vault.

**When retrofitting a note that has no diagrams:**

Ask: *is there a geometric or visual interpretation the reader would benefit from seeing?* If yes, and the concept is in the "almost always benefit" list above, add a diagram. The bar is low — a simple two-color plot of a convex function with a chord drawn across it is already a better note than one with no visual at all. Flag the note in commit notes as "added TikZ" so the improvement is traceable.

Do not, however, add diagrams to notes that are fundamentally symbolic or computational. A note on modular exponentiation or asymptotic notation does not need a picture. If in doubt, ask Mihail before spending time on TikZ.

## Writing Properties

Properties are the meat of the reference layer. They sit between the cheat-sheet callout and the learning-oriented intuition, and they are structured as named facts the reader can scan.

- **Format: three layers — short title, one-sentence statement, explanation paragraph.**
  ```
  #### *(Short Title)* One-sentence statement that captures the essence.

  Explanation paragraph carrying the full statement, conditions, formulas, and edge cases.
  ```
  Layer 1 (title) lets the reader scan. Layer 2 (one-sentence, on the same line as the heading) gives the gist. Layer 3 (explanation paragraph, after a blank line) carries the full reference detail. The title is a $1$–$4$-word italicized phrase. The one-sentence statement lives on the same `####` line, immediately after the italicized title.
- **No repetition across layers.** The explanation paragraph must not restate what the title or one-sentence already said. Each layer adds new information; do not paraphrase the one-sentence as the opening of the paragraph.
- **No repetition between Properties and the callout.** The `>[!note]` callout is the cheat sheet. Properties go *beyond* the callout — mechanism, implementation, edge cases, robustness checks, failure modes. A property that just restates a line from the callout in longer form should be cut, not rewritten. The Properties section should make the note *more useful* than reading the callout alone; if a property does not, it is dead weight.
- **Positive checklist — what counts as "going beyond" the callout.** Every surviving property should fall into at least one of the following buckets. If a candidate fits none of them, it is almost certainly restating the callout and should be cut.
    1. *Mechanism / why-it-works.* The internal causal story that produces the headline result.
    2. *Implementation detail.* Practical steps the cheat sheet omits — overlapping portfolios, volatility scaling, parameter conventions, value-weighted variants.
    3. *Hidden compositional shift.* The headline statistic averages over states that look different inside (loser-leg becoming high-beta survivors; unconditional $\beta \approx 0$ hiding $\beta \approx -2$ in panics).
    4. *Robustness pattern.* Why the result is not a fluke — cell-by-cell evidence across a parameter grid, replication across asset classes, stability across non-overlapping subsamples.
    5. *Why the deeper rebuttal also fails.* The callout says "static factor models fail"; the property explains that the conditional or state-dependent generalizations also fail.
    6. *Failure mode / regime shift.* When and how the headline result breaks — correlation breakdown, two-phase crashes, beta flips mid-rebound.
    7. *Joint test across siblings.* Constraints a complete account must satisfy across multiple related notes (continuation-and-reversal must appear in both cross-section and time-series).
    8. *How to read the headline number.* Reframing what the average return *means* — small wins punctuated by rare catastrophic losses, not a steady cash flow.
- Long proofs go in a collapsible `>[!example]-` block or get extracted to their own note.
- Order properties from most-used to least-used, not in the order they were discovered or proved.
- Long proofs go in collapsible `>[!example]-` blocks or get extracted to their own notes. Inline proofs longer than five lines break the flow.

If the Properties section grows beyond 8–10 items, the note is probably covering too much and should be split.

## Writing the Derivation

A derivation is optional. Include it when the concept is *derived* from more primitive ideas and the derivation itself teaches something the reader should know. Do not include derivations that are mechanical bookkeeping — link to them as a separate note or collapse them.

A good derivation:

- Starts from a named prerequisite (link it).
- States the goal upfront: "We want to show that..."
- Justifies each step in a short phrase. "By linearity of expectation...", "Substituting the Taylor expansion...", "Applying Cauchy-Schwarz...".
- Ends with the headline result that already appeared in the callout. This closes the loop.

## Cross-Linking While Writing

Links are written as the prose goes, not bolted on afterward. If a sentence mentions a concept that has its own note, link it on the spot. Three links is the floor, not the target.

- Link the first mention of a named concept, not every mention.
- Use display-text aliasing whenever the bare filename reads awkwardly in the sentence: `[[1.3 Conditional Probability|conditional probability]]`.
- Link across domains aggressively. A Machine Learning note that uses gradient descent should link to the Multivariable Calculus note on gradients. This cross-domain weaving is the single biggest thing that elevates the vault from "organized notes" to "knowledge base."
- If a concept doesn't yet have a note, create a stub entry in `_backlog/` and link forward to it. Dead links are worse than forward-links — they leave no trace of the intended connection.

## Handling Incomplete Knowledge

When writing a note on a topic where the available information is incomplete — whether because Mihail's course only covered part of it, because the concept is genuinely open, or because the source material is ambiguous — be explicit about the boundary. Do not fabricate.

- If a property is known but the proof was not covered, state the property and omit the proof with a note: `*(Proof omitted; see [source] for a full treatment.)*`
- If a concept has alternative formulations and only one was taught, prefer the taught version and mention the alternatives in a `>[!warning]` callout.
- Never invent examples. If no good example comes to mind, flag the note with `status/needs-examples` and move on — a real example written later is worth more than a fabricated one written now.
- Never invent citations or references. If the source is unknown, omit the citation.

## Voice and Prose Discipline

The writing voice is textbook-formal but alive. These are hard rules:

- **No first person in substantive notes.** No "I," "my," "we'll see." The README is the only place for Mihail's personal voice. Substantive notes use either "we" (for collaborative exposition: "we define," "consider") or the passive/declarative voice.
- **No casual asides.** "Pretty weird, right?" and "this is kind of the key insight" belong in a blog post, not a reference.
- **No filler transitions.** "As we have seen," "it is important to note that," "recall that" — all banned. If a reference is needed, link it.
- **Bold means defined.** Every bolded term in a note is either (a) the subject term on first mention, or (b) a new term being defined in passing. Bold for emphasis is not allowed — that's what italics are for.
- **Italics mean property name or emphasis.** `#### *(Nash's Theorem)*`, or a single italicized word for stress. Nothing else.
- **Short sentences beat long ones.** Mathematical prose rewards brevity. If a sentence runs longer than two lines, it should probably be two sentences.

## Metadata Discipline

Frontmatter is not optional. Every substantive note has, at minimum:

- `title`, `aliases`, `course`, `created`, `updated` — bookkeeping.
- A `domain/` tag (one and only one, following the taxonomy in README §4.2).
- A `type/` tag (one and only one).
- A `level/` tag (one and only one).
- A `status/` tag (one and only one).
- A populated `prerequisites` list.

If any of these are missing, the note is not ready to ship. When retrofitting old notes, frontmatter is added before the note is considered done.

Tags are never freeform. If a tag would fit none of the namespaces in the README, it doesn't exist. Do not invent new namespaces without updating the README first.

## Comparison-Hub Notes

Some concepts are best understood *against each other*. Activation functions, optimizers, normalization layers, attention variants, loss functions, proof techniques, regression metrics, classification metrics — in each of these, the reader's question is rarely "what is ReLU?" and almost always "which of these should I use, and how do they differ?" A single note that lumps them together loses the depth the returner needs; a bare set of sibling notes loses the comparison the learner needs. The answer is a **comparison hub**.

A comparison hub is a first-class note type, alongside concept notes and index notes. It has a parent note whose body is dedicated to side-by-side comparison, and a set of sibling notes — one per variant — where the full details live.

**Structure of the parent hub:**

- **`>[!note]` callout.** States the *family* (e.g., "Activation functions introduce non-linearity into neural networks"), the *shared interface* (signature, domain, codomain), and — most importantly — the **decision rule**: one or two sentences telling the returning reader which variant to reach for by default and under what conditions to deviate. This decision rule is the whole reason the hub exists.
- **`# Intuition`.** Explains what the family has in common and what dimension the variants trade off along (smoothness vs. sparsity, bias vs. variance, compute vs. accuracy, etc.). Name the tension.
- **`# Comparison Table.`** A Markdown table with one row per variant. Columns are the dimensions that matter for choosing between them. For activation functions that might be: formula, derivative, range, monotonic, saturating, zero-centered, default use-case, failure mode. For optimizers: update rule, memory cost, hyperparameters, typical use. Every row links to its sibling note.
- **`# When to Use Which.`** A short prose section that walks through the decision tree: "use X by default; switch to Y when saturating gradients are a concern; switch to Z when memory is tight." This is what a returner actually reads.
- **`# See Also.`** Links to every sibling and to the closest concept-note neighbors.

**Structure of each sibling:**

- A normal concept note with the full CLAUDE.md treatment — dense callout, intuition, properties, derivation (if relevant), examples, TikZ where applicable.
- Its `>[!note]` callout should include **one line** about where it sits relative to its siblings ("ReLU is the default activation in CNNs; GELU replaces it in transformers for smoother gradients"). This is the only place where the sibling references the comparison.
- The sibling does not repeat the comparison table. It links back to the hub.

**When to build a comparison hub:**

- Three or more variants share a signature or interface.
- A reader choosing between them needs the same information about each one.
- The variants exist *because* they trade off along a known axis.

**When not to build one:**

- Only two variants exist — use a single concept note with a `# Variants` subsection and a short comparison paragraph.
- The variants don't share an interface (e.g., "algorithms for sorting" is too broad to hub; a hub for "O(n log n) comparison sorts" is reasonable).
- The variants are so context-dependent that no general decision rule can be written. If the "When to Use Which" section can only say "it depends," skip the hub.

**Splitting an existing lump-sum note into a hub:**

When retrofitting a note like "Activation Functions" that currently covers five variants in one file:

1. Extract each variant into a sibling note using the normal note-writing workflow. The variant's opening callout gets the full treatment; its properties and examples move with it.
2. Keep the original file as the hub. Its title and numeric prefix stay the same.
3. Rewrite the hub's callout around the decision rule, not around any individual variant.
4. Build the comparison table. Row order matches sibling order in the folder.
5. Write the "When to Use Which" prose.
6. Add a `See Also` section linking every sibling.
7. Update every wiki-link that used to point at the lumped note. Most will now point at a specific sibling; the ones that meant "the comparison" stay pointed at the hub.

Do not retrofit a lump-sum note into a hub without Mihail's approval — some concepts are deliberately lumped because the course presented them that way, and the comparison-hub pattern is a structural change, not a formatting fix.

## Splitting and Merging Notes

A note that tries to cover two concepts is worse than two short notes. Signs a note should be split:

- The intuition section branches into "on the other hand..." or "another way to think about this..."
- The Properties section exceeds 10 items.
- The file exceeds 250 lines.
- Two distinct formulas appear in the opening callout.
- The title contains "and" or a comma.

When splitting, the original note usually becomes either (a) an index-style hub that links to the new pieces, or (b) one of the new pieces with a See Also pointing to its siblings. Preserve the numeric prefix on whichever piece is the natural "main" one.

Merging is rarer. Notes should only be merged when they cannot be reasonably understood independently — e.g., two halves of a definition that depend on each other circularly.

## Retrofitting Existing Notes

Most of the vault predates these rules. When asked to retrofit or refactor an old note, work in this order of priority:

1. **Add or densify the `>[!note]` callout.** If the note has no callout, add one. If it has a one-liner, expand it into a full cheat sheet using the rest of the note's content as source material.
2. **Add `# Intuition`.** Many old notes jump straight from definition to properties. Write an intuition section from scratch if needed.
3. **Add at least one example** if none exists, or improve the existing examples to meet the grounded-and-curated standard.
4. **Add wiki-links.** Aim for three minimum. Cross-domain links are extra valuable.
5. **Add frontmatter.** Tags, aliases, prerequisites, dates.

Do not let the perfect be the enemy of the good. A note that goes from "broken" to "step 3 complete" is a win. Log what was done and move on.

## When Asked to Create a New Note

Default workflow for a new-note request:

1. Confirm the concept, the folder, and the level with Mihail before writing. Use `AskUserQuestion` if any of these are unclear — do not guess folder placement.
2. Check whether a related note already exists that should be linked or expanded instead of duplicated.
3. Check whether the prerequisites already have notes. Flag any gaps.
4. Draft the Intuition, Derivation, Examples, and Properties sections first.
5. Distill the `>[!note]` callout from the draft.
6. Add cross-links throughout.
7. Populate frontmatter.
8. Update the parent folder's index note to reference the new file.
9. Report what was created, what was linked, and what prerequisites are still missing.

## When Asked to Analyze or Refactor

- Never modify a substantive note without first reading it fully.
- When refactoring, preserve Mihail's wording wherever it already meets the rules. The goal is not to rewrite in Claude's voice; the goal is to make the vault self-consistent.
- When in doubt about whether a change is desired, ask before committing to it.
- Keep edits surgical. A note that already has good intuition does not need its intuition rewritten.

## When Given Slides or Lecture Materials

Mihail frequently uploads slide decks (`.pptx`, `.pdf`) and other lecture materials from his Berkeley courses. These materials are **sources, not content**. They never get imported into the vault directly. Their role is to seed and guide note creation — the notes themselves are written from scratch in the vault's voice.

The material sets the *floor* for what a note must cover, not the *ceiling*. A note may go further than the lecture, but it must honor the lecture's scope, notation, and level as its starting point.

### What to Extract

- **Concepts and definitions.** Every named concept the lecture introduces is a candidate for a note.
- **Formulas and notation.** Treat the material's notation as the canonical convention for that course and domain. If a lecture writes $\hat{\theta}_{\text{MLE}}$, match that in the note. Consistency with what Mihail was taught matters more than matching any external textbook.
- **Theorems, lemmas, and named results.** These become Properties in the relevant notes, with their original names preserved.
- **Scope signals.** What the lecture chose to cover — and what it chose to skip — tells you what `level/` the note should be pitched at and how deep the derivation should go.
- **Worked examples.** These can inspire examples but must be rewritten in the vault's example format. Never copy a slide's worked example verbatim.

### What NOT to Extract

- **Slide layouts, bullet lists, or section dividers.** These belong to the presentation format, not the knowledge base.
- **Speaker-specific phrasing, anecdotes, or jokes.**
- **Slide images**, unless they are genuinely irreplaceable (a photograph, a published figure, or a diagram too complex to recreate). A slide's hand-drawn diagram should be rebuilt in TikZ.
- **Slide numbers, lecture numbers, or "as we saw last time" references.** The note must stand alone.
- **Course codes inside the note body.** Course provenance lives in the `course` frontmatter field. The body reads as if the reader has never seen the lecture.

### Workflow for a New Lecture Upload

1. **Read the material fully** using the appropriate skill (`pdf` for PDFs, `pptx` for slide decks). Do not skim. The last slide or two often contains the summary that makes the earlier slides cohere.
2. **Inventory every named concept** the lecture introduces. For each, grep the vault to check whether a note already exists.
3. **Classify each concept:**
   - *New concept, no existing note* → candidate for a new note.
   - *Existing note, material adds depth* → candidate for a refactor.
   - *Existing note, material matches* → no action needed.
   - *Mentioned but not developed in the lecture* → add to `_backlog/` with a one-line description.
4. **Report the inventory to Mihail before writing anything.** Present the classification as a list and let him choose which concepts to act on. Never start creating or refactoring notes unilaterally from a lecture upload.
5. **For each approved concept, apply the normal note-writing workflow** from "When Asked to Create a New Note" or "When Asked to Analyze or Refactor," using the material as the source.
6. **Record the source in the `course` frontmatter field only.** The note body does not mention the lecture.

### Using the Material as a Style Guide

The material is not just a source of content — it is also a calibration tool for how to write the note.

- **Notation.** Match the material's variable names, symbol conventions, and formula structure exactly. If the material uses $p(x \mid \theta)$ and the vault's Probability section already uses $\mathbb{P}[X \mid \theta]$, stop and raise the inconsistency to Mihail rather than silently picking one.
- **Level.** A lecture's depth of derivation indicates the note's `level/` tag. A lecture that derives everything from first principles is `level/intermediate` or `level/advanced`. A lecture that only states results is `level/intro`.
- **Wording.** If the material uses a specific English phrasing for a concept ("fixed point," "steady state," "stationary distribution"), prefer that phrasing as the primary term and list the alternates in `aliases`.
- **Scope.** The set of concepts the lecture covers defines the neighborhood of notes that should exist. If the lecture mentions a concept but doesn't develop it, that concept belongs in `_backlog/`, not absent from the vault.

### Expanding Beyond the Material

The material is a seed, not a cage. Good notes frequently go further than the lecture:

- Add intuition the lecture glossed over.
- Add counterexamples or edge cases that weren't in scope.
- Add worked examples at difficulty levels the lecture didn't reach.
- Link to cross-domain connections the lecture wouldn't have mentioned.
- Add standard properties or results the lecture skipped for time.

But expansion has hard limits:

- Do not add content that contradicts the lecture's treatment without flagging the disagreement in a `>[!warning]` callout.
- Do not add advanced material that requires prerequisites beyond the lecture's level without linking those prerequisites.
- Do not invent examples, properties, or citations just to pad the note. The "never fabricate" rule from "Handling Incomplete Knowledge" applies with full force.
- Do not rewrite the lecture's definition in a form that loses information the lecture included.

### Handling Ambiguity in the Material

Slides are condensed. They often omit quantifiers, drop assumptions, or use shorthand that only makes sense with a live speaker. When the material is ambiguous:

- **Ask Mihail before guessing.** If a slide says "the estimator is unbiased" without specifying under which assumptions, do not fabricate the assumptions from plausible-sounding defaults.
- **Prefer the most conservative reading.** When two interpretations are possible, pick the one with the strongest hypotheses.
- **Flag the ambiguity in the note.** A `>[!warning]` callout noting that the lecture's treatment was incomplete is more valuable than a confident-but-possibly-wrong statement.

## Things to Never Do

- Never write in first person in a substantive note.
- Never leave an opening `>[!note]` callout at one line.
- Never create an empty stub in the main tree. Use `_backlog/`.
- Never invent examples, citations, or properties you are unsure about.
- Never add freeform tags outside the five namespaces.
- Never duplicate a note across domains. Link instead.
- Never use casual asides, filler transitions, or rhetorical questions in substantive notes.
- Never rename a file without updating every link pointing to it.
- Never modify the README's rules without an explicit request from Mihail.
