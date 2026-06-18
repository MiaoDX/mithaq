# Mithaq Documentation Index

> A comprehensive guide to all documentation in this repository.

## Core Documents

| Document | Purpose | Location |
|----------|---------|----------|
| [README.md](./README.md) | Main entry point (English) - project overview | `/README.md` |
| [README.zh.md](./README.zh.md) | Main entry point (Chinese) | `/README.zh.md` |
| [CHARTER.md](./CHARTER.md) | Why this repo exists, the name origin | `/CHARTER.md` |
| [CHARTER.zh.md](./CHARTER.zh.md) | Chinese charter | `/CHARTER.zh.md` |

## Directory Index

### `/skills/` — AI Agent Skills

| File | Purpose |
|------|---------|
| [mithaq/SKILL.md](./skills/mithaq/SKILL.md) | Core mithaq skill definition for AI agents across repos |

### `/prompts/` — Ready-to-Paste Invocation Prompts

| File | Purpose |
|------|---------|
| [invoke.md](./prompts/invoke.md) | Universal prompt covering all three mithaq modes |

### `/templates/` — Reusable Structures

| File | Purpose |
|------|---------|
| [checkpoint.md](./templates/checkpoint.md) | Layer 1: Universal checkpoint skeleton |

### `/vectors/` — Research Direction Cards

| File | Purpose |
|------|---------|
| [roboclaws.md](./vectors/roboclaws.md) | Roboclaws research vectors (robotics AI coding agent) |
| [robowbc.md](./vectors/robowbc.md) | Robowbc research vectors (whole-body-control runtime) |
| [roboharness.md](./vectors/roboharness.md) | Roharness research vectors (coding agent on code) |
| [README.md](./vectors/README.md) | Vectors directory overview |

### `/dialogues/` — Archived Important Conversations

| File | Purpose |
|------|---------|
| [2026-05-21-naming-mithaq.md](./dialogues/2026-05-21-naming-mithaq.md) | Conversation that named this repository (English) |
| [2026-05-21-naming-mithaq.zh.md](./dialogues/2026-05-21-naming-mithaq.zh.md) | Chinese translation of naming conversation |
| [README.md](./dialogues/README.md) | Dialogues directory overview with inclusion criteria |

## Layer Architecture

This repository implements a two-layer research structure:

```
┌─────────────────────────────────────────────────────────────┐
│                    Layer 1: The How                          │
│                                                              │
│  templates/checkpoint.md ─────────────────────────────────┐  │
│  (Universal skeleton: method, structure, quality bar)      │  │
│                                                              │
├─────────────────────────────────────────────────────────────┤
│                    Layer 2: The What                         │
│                                                              │
│  vectors/roboclaws.md  (per-repo: what to track, where)  │  │
│  vectors/robowbc.md                                         │  │
│  vectors/roboharness.md                                     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

## How to Use This Documentation

### For AI Agents
1. **Fastest path**: Read [`prompts/invoke.md`](./prompts/invoke.md), copy everything between dashed lines, paste to agent
2. **Deep reference**: Read [`skills/mithaq/SKILL.md`](./skills/mithaq/SKILL.md) for full routing logic

### For Human Readers
1. **Start here**: [README.md](./README.md) — project overview and purpose
2. **Understand the "why"**: [CHARTER.md](./CHARTER.md) — philosophical foundation
3. **Navigate content**: This index → specific directory README → actual content

## Conventions

### File Naming
- `YYYY-MM-DD-<slug>.md` for dialogues (date-prefixed, verb-phrase slugs)
- Lowercase with hyphens for all other files
- Bilingual: `.md` for English, `.zh.md` for Chinese variants

### Language
- Primary language: English
- Chinese translations exist for core documents (README, CHARTER, dialogues)
- All new content should be written in English; Chinese translations can follow

### Link Convention
- Use relative paths for internal links (`../templates/checkpoint.md`)
- Use full GitHub URLs for cross-repository references (`https://github.com/MiaoDX/mithaq/blob/main/...`)
