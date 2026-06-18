# Templates

Reusable structural skeletons for mithaq artifacts.

## Contents

- [`checkpoint.md`](./checkpoint.md) — Layer 1 universal checkpoint skeleton. Used as the starting point for writing periodic deep-research checkpoints. The companion Layer 2 (what to cover) lives in `mithaq/vectors/<repo-name>.md`.

## How templates work

Templates use `{{...}}` placeholders that must be replaced when filling in. Lines beginning with `>` are author instructions and should be deleted before the final document is published. Sections marked "optional" should be deleted entirely when they do not apply to the repo's ecosystem.

Checkpoint instances live in the consuming repo's `docs/research-checkpoints/YYYY-MM.md` — **not** in mithaq itself.
