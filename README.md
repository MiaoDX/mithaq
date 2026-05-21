> **Language**: Current · [中文](./README.zh.md)

# Mithaq

> *Mithaq* (مِيثَاق, "solemn covenant") — a meta-repository for long-running conversations between one human and a handful of top AI models, kept so they do not dissipate, and used to guide every other project this human runs.

## What this is

A meta-repo doing two things:

1. **Archive** — preserve the actually-decision-shaping conversations with Claude / GPT and other top models. One-shot, impulsive, forget-it-by-tomorrow exchanges do not enter. Only the ones that **changed a downstream decision**.
2. **Direct** — extract reusable structures from those conversations (a universal periodic deep-research template, per-repo research-vectors cards, etc.) so other repos (roboharness, verse-driven, robowbc, LIP, docfit, …) can borrow them.

No code, no draft documents, no prompt libraries — those belong elsewhere.

## The name

See [`CHARTER.md`](./CHARTER.md). Short version: `Mithaq` is the Arabic word for "solemn covenant," referring specifically to the Quran 7:172 *Mithaq al-Alast* — the **primordial covenant before all existence**. Every conversation worth keeping here is, structurally, a miniature re-enactment of that primordial covenant.

## Why this repo might be worth copying

If you also work with top AI models on a long timeline, and find that:

- The genuinely important conversations keep dissolving into chat history;
- Decisions get made in conversation and three months later you can no longer reconstruct *why*;
- Insights from one project never seem to find their way into the next;

then a meta-repo like this might serve you. The structure here is reusable across people and projects. Fork freely, or just borrow the patterns.

## Layout

```
mithaq/
├── README.md          # this file (entry, English)
├── README.zh.md       # Chinese entry
├── CHARTER.md         # why this repo exists, why the name "Mithaq"
├── CHARTER.zh.md      # Chinese charter
├── skills/            # SKILL.md for AI agents (cross-repo invocation)
├── prompts/           # ready-to-paste invocation prompts
├── templates/         # reusable structures (e.g. the checkpoint meta-template)
├── vectors/           # per-repo research direction cards (Layer 2)
└── dialogues/         # curated archive of important conversations
```

## For AI agents

When working inside any MiaoDX repo and the task involves mithaq's conventions (running an ecosystem checkpoint, writing a research-vectors card, archiving a dialogue):

**Fastest path**: open [`prompts/invoke.md`](./prompts/invoke.md), copy the content between the dashed lines, paste it to the agent.

**Mechanism**: the prompt above instructs the agent to load [`skills/mithaq/SKILL.md`](./skills/mithaq/SKILL.md) — an open-standard SKILL.md (the format Anthropic released in late 2025, now adopted by Claude Code, Codex, Cursor, and others) that acts as a router: telling the agent when mithaq applies, where each artifact should live, and which canonical files to consult. The agent can also fetch the raw URL directly:

```
https://raw.githubusercontent.com/MiaoDX/mithaq/main/skills/mithaq/SKILL.md
```

Or the consuming repo's `CLAUDE.md` / `AGENTS.md` can point at the skill once and benefit from it on every subsequent session.

## Status

Started 2026-05. The structure will evolve as it is actually used.
