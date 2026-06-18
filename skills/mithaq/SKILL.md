---
name: mithaq
description: Apply mithaq conventions when working in any MiaoDX repo (roboharness, verse-driven, robowbc, LIP, docfit, etc.) and the user asks to (a) run or update a periodic deep-research ecosystem checkpoint, (b) create or update a research vectors card defining what a repo should track, or (c) archive an important AI-conversation dialogue. mithaq is the meta-repo that holds shared templates, per-repo vectors cards, and curated dialogues across all MiaoDX projects. Trigger words include "checkpoint", "调研", "deep research", "vectors", "存档对话", "ecosystem snapshot".
version: 0.1.0
license: MIT
---

# mithaq

The meta-repo for recording important AI-model conversations and using them to guide all MiaoDX projects.

Repository: https://github.com/MiaoDX/mithaq

## When to use this skill

Trigger this skill when the user is in any MiaoDX repo and asks for one of:

- **Run a checkpoint**: "跑一次月度 checkpoint" / "做一次 deep research 盘点" / "更新 ecosystem snapshot"
- **Create or update a vectors card**: "为 X repo 建一份 vectors 卡片" / "更新 roboharness 的调研方向" / "添加新的隐藏假设"
- **Archive a dialogue**: "把这次对话存档到 mithaq" / "这次讨论值得记下来" / "记一份 dialogue"

If the user just wants a one-off web search or a casual ecosystem question, **do not use this skill** — mithaq is for *structured, persistent, cross-session* artifacts only.

## What mithaq is (one paragraph)

mithaq holds three things: **Layer 1** — universal templates (currently `templates/checkpoint.md`, a 300+ line skeleton for periodic deep-research checkpoints); **Layer 2** — per-repo vectors cards (`vectors/<repo>.md`) that define which entities a specific repo must track, which sources to trust/blacklist, what cadence to follow, and what hidden assumptions to challenge; **Layer 3** — curated dialogues (`dialogues/YYYY-MM-DD-<slug>.md`) preserving important AI conversations. The Layer 1/2 separation is essential: Layer 1 stays repo-agnostic, Layer 2 carries all per-repo specifics. Without this separation, "universal prompts" devolve into asking the agent about empty placeholders.

Read `README.md` and `CHARTER.md` if more context is needed.

## Conventions — where things go

| Artifact | Lives in | Naming |
|----------|----------|--------|
| Universal templates | `mithaq/templates/` | descriptive name, e.g., `checkpoint.md` |
| Per-repo vectors cards | `mithaq/vectors/` | `<repo-short-name>.md` |
| Curated dialogues | `mithaq/dialogues/` | `YYYY-MM-DD-<slug>.md` |
| **Actual checkpoint instances** | **the consuming repo's `docs/research-checkpoints/`** | `YYYY-MM.md` |

The last row is critical: **checkpoint instances do NOT live in mithaq**. They live in each repo's own `docs/research-checkpoints/` directory. mithaq holds the *template* and the *vectors card*; the consuming repo holds its own *instances*. This keeps mithaq from being flooded by every repo's monthly checkpoints.

## Mode A — Run a checkpoint

Trigger: user wants a periodic ecosystem snapshot for a specific repo.

Steps:

1. **Identify the target repo** (e.g., roboharness). Confirm with the user if ambiguous.
2. **Read the vectors card** at `mithaq/vectors/<repo>.md`. This defines: which research vectors to track, each vector's coverage type (core / watch / trigger-only), which entities to track, source whitelist/blacklist, cadence, hidden assumptions to challenge, and triggers.
3. **Read `mithaq/templates/checkpoint.md`** as the structural skeleton.
4. **Read the previous checkpoint** at `<repo>/docs/research-checkpoints/<previous>.md` if any exists. This is the comparison anchor — new checkpoints note *what changed* against prior ones, they do not write from scratch.
5. **Run deep research against the fixed tracking surface, with flexible expansion depth**:
   - Core vectors: full update every routine checkpoint.
   - Watch vectors: light check every routine checkpoint; expand only when material evidence appears.
   - Trigger-only vectors: list in the coverage table; expand only when their explicit trigger fires.
   - Do not invent a new set of directions for the period. Vector count, classification, and scope change only during vectors-card self-audit or an explicit card update.
6. **Write the new checkpoint** at `<repo>/docs/research-checkpoints/YYYY-MM.md`, following the template structure. The most important sections are:
   - §1 Executive summary (3–5 most important changes this period)
   - §6 Recommendations (concrete actions for this repo)
   - §7 Open questions (carries forward to next checkpoint)
   - §8 Changelog (what changed vs prior checkpoint, with `[YYYY-MM 修正]` annotations preserving overruled prior judgments)
7. **Verify every hidden assumption**: for each H1..HN in the vectors card, explicitly answer "did this period produce evidence that should make us reconsider this assumption?" If the answer is "no" for all assumptions across two consecutive checkpoints, flag that vectors card may have blind spots.
8. **Source quality**: cite A-tier sources directly. B-tier needs cross-verification. Mark anything based only on C/D-tier (SEO content, awesome lists) as `[未充分验证]`. Never trust D-tier blacklist sources from the vectors card.

Output location: `<repo>/docs/research-checkpoints/YYYY-MM.md` in the consuming repo, **not** in mithaq.

## Mode B — Create or update a vectors card

Trigger: user wants to define (or revise) research direction tracking for a repo.

Steps:

1. **Read `mithaq/vectors/README.md`** for the design rationale and what each card must contain.
2. **Read `mithaq/vectors/roboharness.md`** as the baseline reference implementation. For richer evolved-card examples, also inspect `robowbc.md` or `roboclaws.md` when their domains are closer to the target repo.
3. **For a new card**: clone the structure from roboharness.md, then customize:
   - Project positioning paragraph (one-sentence definition)
   - Hidden assumptions table (H1..HN) — these are the things this repo is implicitly betting on; the vectors are designed to challenge them. **A vectors card without hidden assumptions is incomplete** — it will produce "what's new in field X" research rather than "should we change our mind about Y" research.
   - 3–8 research vectors, each with concrete entity lists (no abstract placeholders like "key projects in this area" — list actual names)
   - Coverage policy: classify each vector as core, watch, or trigger-only. Small repos should not be padded to match larger repos; large repos should not be compressed into an arbitrary shared count.
   - Source whitelist (A-tier) and blacklist (D-tier) specific to this domain
   - Cadence (monthly / bi-monthly / quarterly / event-driven)
   - Triggers for off-schedule research
4. **For an update**: preserve prior assumptions/vectors; add new ones with `[新增于 YYYY-MM]` annotation; revise stale entities with `[YYYY-MM 更新]` annotation. **Do not silently delete prior content** — vectors cards evolve visibly, like checkpoints.
5. **Audit cadence**: vectors cards themselves should be reviewed quarterly. If a card hasn't been audited in 90+ days, flag this when touching it.

Output location: `mithaq/vectors/<repo>.md`.

Aim for 150–250 lines per card. Longer suggests the card is doing too much; shorter suggests it's not specific enough.

## Mode C — Archive a dialogue

Trigger: user explicitly wants to preserve an important AI conversation (or recognizes a conversation in progress as worth preserving).

Steps:

1. **Verify it meets the inclusion criteria** (see `mithaq/CHARTER.md`, "收录原则" section). At least two of three must hold:
   - The conversation changed a decision.
   - It will be referenced again (likely re-consulted within 3 months).
   - It contains an abstractable structure (a reusable method/framework, not just situation-specific advice).
2. **Read `mithaq/dialogues/README.md`** for the recommended file structure.
3. **Read `mithaq/dialogues/2026-05-21-naming-mithaq.md`** as the reference implementation. It demonstrates the curated-not-verbatim style.
4. **Curate, don't transcribe**: a 30-round conversation should yield maybe 150–250 lines of archive. Preserve decision turns, key quotes from the user (especially direction shifts), and the *abstractable structures* section. Elide the verbose middle.
5. **Privacy**: scrub any API keys, tokens, secrets, or non-public commercial information before committing.
6. **Naming**: `YYYY-MM-DD-<slug>.md` where slug describes *what the conversation changed*, not *what the topic was*. Good: `2026-05-21-naming-mithaq.md` (describes outcome). Bad: `2026-05-21-talking-about-names.md` (describes topic).
7. **The "abstractable structures" section is the most important**: it's what makes a dialogue archive useful to future readers (including future-MiaoDX who has forgotten the context). Without it, the dialogue is just nostalgia.

Output location: `mithaq/dialogues/YYYY-MM-DD-<slug>.md`.

## Common mistakes to avoid

- **Treating SKILL.md as authoritative**: this file is a *router*, not the source of truth. When in doubt, the actual files in mithaq (`CHARTER.md`, `templates/checkpoint.md`, `vectors/README.md`, `dialogues/README.md`) win.
- **Writing checkpoint instances into mithaq**: they go into the *consuming repo*, never into mithaq.
- **Generic vectors without entity lists**: "track major projects in agent harnesses" is not a vector; "track Anthropic engineering blog, OpenAI Symphony, Cursor planner/worker, HumanLayer, Martin Fowler" is. Specific entity names are non-negotiable.
- **Vectors without hidden assumptions**: a card that only lists "what to read" without "what this repo is betting on" will produce shallow research forever.
- **Ad hoc vector selection during checkpoints**: checkpoints may vary coverage depth, but they must use the vectors card's stable tracking surface. Reclassify or resize the surface in a card update, not inside a routine checkpoint.
- **Verbatim dialogue dumps**: archive curated extracts with framing, not raw chat history. Discipline the volume — a dialogue archive is for re-reading, not for forensic completeness.
- **Silent revision**: when a prior judgment is overruled, annotate with `[YYYY-MM 修正]` and keep the original visible. The audit trail is the point.
- **Falling for SEO content**: D-tier sources (the "best AI tools of 2026" sites) almost never carry signal. If the only support for a claim is D-tier, mark it `[未充分验证]` and move on.

## Reference files

When this skill is loaded, also fetch (or have the user fetch) the following from mithaq:

- `README.md` — top-level orientation
- `CHARTER.md` — why this repo exists, why "mithaq", inclusion criteria
- `templates/checkpoint.md` — Layer 1 universal skeleton (Mode A)
- `vectors/README.md` — Layer 2 design rationale (Mode B)
- `vectors/roboharness.md` — Mode B reference implementation
- `dialogues/README.md` — Mode C conventions
- `dialogues/2026-05-21-naming-mithaq.md` — Mode C reference implementation

If working in another MiaoDX repo and these files are not locally available, fetch from `https://raw.githubusercontent.com/MiaoDX/mithaq/main/<path>`.

## Status

Skill v0.1.0, released 2026-05-21. This is an early version — revise after the first real checkpoint or dialogue archive is produced through this skill, to capture lessons that this draft cannot anticipate.
