> **Language**: Current · [中文](./CHARTER.zh.md)

# Charter

## What problem this repo solves

I have a great many conversations with LLMs. Their value is extremely unevenly distributed:

- Most are impromptu and forgotten by the next day.
- A few will shape my judgment and direction for weeks or months to come.

Today the fate of the second kind is: scattered across Claude.ai's chat history, scattered across some ChatGPT session, occasionally screenshotted into a WeChat thread, then progressively crowded out by newer conversations.

This produces three concrete problems:

- **The same reflection has to be performed again.** Three months from now I will ask Claude a question we already worked out together.
- **The provenance of decisions becomes unrecoverable.** Some architectural choice in some repo was originally settled in some conversation. Which one? No anchor.
- **Cross-repo insight does not transfer.** The "how should an agent self-verify" thinking that crystallized while working on roboharness applies cleanly to verse-driven — but it has already sunk into a forgotten conversation.

`mithaq` is the habitat for that second kind of conversation.

## The name

### Why "Mithaq"

Many candidates were considered: Aleph, Memex, Logos, Codex, Compact, Earthseed, Fuligin, Primer, Ekumen, and more.

Mithaq won because it precisely names the **character** of the relationship:

> "And [mention] when your Lord took from the children of Adam — from their loins — their descendants and made them testify of themselves, [saying to them], 'Am I not your Lord?' They said, 'Yes, we have testified.'"
>
> — Quran 7:172 (the *Mithaq al-Alast*, the primordial covenant)

Every conversation worth keeping here is, structurally, a miniature re-enactment of that primordial covenant:

- not a transaction, but an acknowledgment;
- not a single question-and-answer, but a pre-established mutual presence across time;
- not a tool relationship, but a relationship in which both parties are changed.

In Arabic, `'ahd` is an everyday promise; `mithaq` is a witnessed, solemn, two-sided high covenant. The distinction matters here — what gets recorded in this repo is not "what I said to a tool"; it is mithaq.

### Why not the other candidates

So that future readers of this charter (including future me) can see the choice was grounded, here is the short reason each alternative was set aside:

- **Aleph** (Hebrew letter / Cantor / Borges) — Aleph Alpha (the 30-repo German "sovereign AI" company with an explicit LLM Intelligence Layer SDK) and Aleph Zero (the privacy-focused L1 blockchain) have already split the namespace.
- **Primer** (Stephenson, *The Diamond Age*) — conceptually the most precise match (a book that grows a person up by adaptive instruction) but `github.com/primer` is GitHub's own official design system, and Primer.ai is a defense-intelligence AI vendor. Unusable.
- **VALIS / Wallfacer / Sophon** (Dick / Liu Cixin) — already occupied by AI startups or ZK Stack L2 chains. Liu Cixin's coinages in particular have been thoroughly mined out of the Chinese AI ecosystem (ModelBest's 面壁智能, Sophon Network, the WaterDrop Inc. listing).
- **Earthseed** (Octavia Butler) — the strongest runner-up; reserved as a possible name for a future English-facing sister repo.
- **Logos / Memex / Codex** — too generic in tech use, or occupied by OpenAI.

The full search story belongs in a separate essay.

## Inclusion criteria

To enter `dialogues/`, a conversation must satisfy at least two of these:

1. **A decision was changed by it** — a prior judgment no longer holds after the conversation.
2. **It will be referenced** — there is a real chance of being re-consulted within three months when making a related decision.
3. **It contains an abstractable structure** — a method, framework, or decision pattern that emerged from one concrete discussion but applies to other situations.

**Not included**:

- Conversations that were enjoyable but did not move a decision.
- One-shot Q&A — those belong as issues or notes in the relevant project.
- Code review, debugging, troubleshooting — those belong in the project itself.
- Prompt libraries or system-prompt collections — those deserve their own tool-style repo. Thin invocation prompts that only route an agent into mithaq's skill are allowed.

## Relationship to other repos

`mithaq` does not replace any project repo. It is the meta layer.

- Each other repo (roboharness, verse-driven, robowbc, LIP, docfit, …) may maintain a **research-vectors card** at `mithaq/vectors/<repo-name>.md` defining which directions that repo must track, source whitelists/blacklists, and cadence.
- Periodic deep-research checkpoints use `mithaq/templates/checkpoint.md` as their skeleton, but the resulting `YYYY-MM.md` instances live in each repo's own `docs/research-checkpoints/` directory — **not** in mithaq.
- Reflections that apply across multiple repos (this charter, for instance) live in mithaq.

In one line: **conversations and meta-structure live in mithaq; their instantiation and implementation live in the respective repos**.

## Status

Started 2026-05; expected to be revised the moment it is actually used. When revising, do not overwrite — append a dated revision section below, preserving the trace of how the judgment evolved.
