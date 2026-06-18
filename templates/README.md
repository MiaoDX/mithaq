# Templates

Reusable structural skeletons for mithaq artifacts. Templates are Layer 1 documents — they define the *how* (structure, methodology, quality bar) but carry no repo-specific content.

## Contents

| Template | Purpose |
|----------|---------|
| [`checkpoint.md`](./checkpoint.md) | Universal checkpoint skeleton (300+ lines) |

## How templates work

### The two-layer architecture

```
Layer 1: templates/checkpoint.md    →   The skeleton (how to write)
                ↓
Layer 2: vectors/<repo-name>.md     →   The substance (what to track)
```

Templates combine with per-repo vectors cards to produce actual checkpoints. The separation is essential: Layer 1 stays repo-agnostic, Layer 2 carries all per-repo specifics.

### Creating a checkpoint

1. **Read the vectors card** at `mithaq/vectors/<repo-name>.md` — defines research vectors, coverage policy, entities, sources, cadence
2. **Read this template** as the structural skeleton
3. **Read the previous checkpoint** at `<repo>/docs/research-checkpoints/<previous>.md` for comparison
4. **Fill in** using `{{...}}` placeholders; delete `>` instruction blocks before publishing

### Placeholder syntax

- `{{...}}` — must be replaced with actual content
- `> ...` lines — author instructions (delete before publishing)
- `(optional)` sections — delete entirely when not applicable

## Where checkpoints live

**Checkpoint instances live in the consuming repo**, not in mithaq:

```
mithaq/templates/checkpoint.md          ← the template (here)
roboharness/docs/research-checkpoints/  ← roboharness instances
robowbc/docs/research-checkpoints/      ← robowbc instances
roboclaws/docs/research-checkpoints/    ← roboclaws instances
```

This keeps mithaq from being flooded by every repo's monthly updates.

## Related

- [`../vectors/`](../vectors/) — Layer 2: per-repo research direction cards
- [`../skills/mithaq/SKILL.md`](../skills/mithaq/SKILL.md) — AI agent routing logic
- [`../INDEX.md`](../INDEX.md) — Complete documentation index
