---
name: distill-concepts
description: Extract atomic concept notes from one or more source notes and wire them into the graph. Use when the user wants to distill concepts, create concept notes, or connect ideas across papers.
disable-model-invocation: true
---

# Distill concepts

Turn sources into `concepts/` notes — the connective tissue of the brain. A concept is **one
idea that connects ≥2 sources**, not a summary of one paper.

## Workflow

```
- [ ] 1. Read the target source(s)
- [ ] 2. Identify atomic, reusable ideas (one idea each)
- [ ] 3. For each: check if a concept note already exists (update, don't duplicate)
- [ ] 4. Write/extend the concept note from the template
- [ ] 5. Add typed back-links between the concept and its sources
- [ ] 6. Report the concepts created/updated and links added
```

## What makes a good concept note

- **Atomic**: one idea. "Probabilistic VAE vs count autoencoder" is a concept; "scVI" is a source.
- **Connective**: `distilled_from` lists ≥2 sources; `## Related` links them with typed verbs.
- **Reusable**: the title is a general idea other future papers could also link to.

Split a note the moment it starts covering two ideas.

## Write

Copy `docs/00-system/templates/concept-note.md` to
`docs/concepts/{kebab-slug}.md`. Fill `distilled_from` with source wikilinks. Write the
one-line definition, "Why it matters", and "Details". In `## Related`, link each source with a
verb (`introduces`, `contrasts`, `benchmarks`, …).

## Then

Update the source notes to link back to the new concept, and add the concept to the relevant
topic MOC. Report which concepts were created vs updated. Do not commit to git.
