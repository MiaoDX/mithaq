# Vectors — Per-Repo Research Direction Cards

This directory holds a **research-direction card** for each MiaoDX repo. Each card defines "what this repo must track."

## Why this layer exists

[`templates/checkpoint.md`](../templates/checkpoint.md) is Layer 1 — the universal skeleton for writing a checkpoint, reusable across repos.

But the skeleton itself doesn't tell you "which directions to watch" — that part is per-repo, and structurally different from repo to repo:

- `roboharness` watches: MuJoCo / Isaac Lab / LeRobot / VLM evaluation / robotics benchmarks
- `verse-driven` watches: Claude Code Skills ecosystem / classical-text digitization / agent reflection frameworks / humanities-meets-LLM academia
- `LIP` watches: site generators / personal-knowledge-management tools / documentation-site peers
- …

Trying to compress these into a single set of generic prompts would make every repo receive "asking-the-air" answers. So each repo keeps its own card.

## What a vectors card must contain

At minimum:

1. **3-7 research directions**, each one specifying:
   - The direction's name (e.g., "Agent SDK / harness-layer dynamics")
   - A concrete list of entities (people / projects / standards / paper series) — without specific entities, the prompt is asking the air
   - Expected major changes over the next year
2. **Source whitelist** — which A-tier sites in this domain can be cited directly
3. **Source blacklist** — which D-tier sites in this domain should be actively ignored
4. **Cadence** — monthly / bi-monthly / quarterly / event-driven
5. **Triggers for off-schedule research** — what events warrant breaking the cycle

## File naming

`<repo-short-name>.md`, e.g.:

- `roboharness.md`
- `robowbc.md`
- `roboclaws.md`

Planned or future examples:

- `verse-driven.md`
- `lip.md`

## Relationship to checkpoint files

Vectors cards stay in mithaq; the actual periodic checkpoint files (`YYYY-MM.md`) live in each consuming repo's `docs/research-checkpoints/` directory.

Rationale:

- Vectors cards are metadata — they don't change every period. When they do, the change is a deliberate Layer 2 upgrade and gets its own commit.
- Checkpoints are instance data — one per period, and they live alongside the code history of the repo they describe.
- This way mithaq does not get flooded by every repo's monthly snapshots.

## Status

Started 2026-05. Current cards:

| Card | Repo | Focus |
|------|------|-------|
| [`roboharness.md`](./roboclaws.md) | roboclaws | VLM robotics demo / multi-agent embodied AI |
| [`robowbc.md`](./robowbc.md) | robowbc | Whole-body-control runtime |
| [`roboharness.md`](./roboharness.md) | roboharness | Visual coding-agent harness |

Start from `roboharness.md` when writing a new card, then check the newer cards for examples of how to evolve assumptions and triggers as a repo's research surface becomes more specific.

## Related

- [`../templates/checkpoint.md`](../templates/checkpoint.md) — Layer 1 checkpoint skeleton
- [`../INDEX.md`](../INDEX.md) — Complete documentation index
- [`../skills/mithaq/SKILL.md`](../skills/mithaq/SKILL.md) — AI agent routing logic
