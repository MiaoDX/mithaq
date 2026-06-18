# Prompts

Ready-to-paste invocation prompts for routing agents into the mithaq skill.

## Contents

- [`invoke.md`](./invoke.md) — Universal single prompt covering all three mithaq modes (checkpoint, vectors card, dialogue archive). Copy everything between the dashed lines and paste to the agent.

## Why a separate prompts directory

These are thin routing prompts only. They carry no mithaq domain logic — that lives in `mithaq/skills/mithaq/SKILL.md`. A prompt just "delivers the agent to the skill."

If a particular mode becomes frequent enough that a dedicated prompt saves a turn, new single-mode prompts (e.g., `run-checkpoint.md`) can be added here without breaking the universal one.

## Related

- [`../skills/mithaq/SKILL.md`](../skills/mithaq/SKILL.md) — The skill definition that prompts route into
- [`../INDEX.md`](../INDEX.md) — Complete documentation index
