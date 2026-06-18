# Skills — mithaq

This directory contains the mithaq skill definition for AI agent cross-repo invocation.

## Contents

- [`mithaq/SKILL.md`](./mithaq/SKILL.md) — Core skill definition

## What is a SKILL.md?

A SKILL.md file is an open standard (released by Anthropic in late 2025, now adopted by Claude Code, Codex, Cursor, and others) that acts as a router for AI agents. It defines:

- **When to trigger** — the conditions under which the skill applies
- **What it does** — the skill's purpose and behavior
- **Where artifacts live** — the file locations and naming conventions
- **How to execute** — step-by-step instructions for the agent

## How mithaq's SKILL.md works

The mithaq skill routes agents into three modes:

| Mode | Trigger | What happens |
|------|---------|--------------|
| **A — Run a checkpoint** | "Run monthly checkpoint" / "做一次 deep research 盘点" | Reads vectors card + previous checkpoint, does incremental research, writes new checkpoint |
| **B — Create vectors card** | "为 X repo 建一份 vectors 卡片" | Creates or updates a per-repo research direction card |
| **C — Archive a dialogue** | "把这次对话存档到 mithaq" | Archives an important AI conversation to dialogues/ |

## For AI agents

When working in any MiaoDX repo and the task involves mithaq conventions:

1. **Fastest path**: Read [`../prompts/invoke.md`](../prompts/invoke.md), copy everything between dashed lines, paste to the agent
2. **Or**: the consuming repo's `CLAUDE.md` / `AGENTS.md` can point at this skill directly

## For human readers

See the main [README.md](../README.md) for project overview, or [CHARTER.md](../CHARTER.md) for the philosophical foundation.
