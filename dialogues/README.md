# Dialogues — Archived Important Conversations

This directory holds the conversations between human and AI models that genuinely shaped judgment and deserve to be returned to.

## Inclusion criteria

See "Inclusion criteria" in [`../CHARTER.md`](../CHARTER.md). At least two of these must hold:

1. **A decision was changed by it.**
2. **It will be referenced** — there is a real chance of being re-consulted within three months when making a related decision.
3. **It contains an abstractable structure** — a method, framework, or decision pattern that emerged from one concrete discussion but applies to other situations.

## Naming convention

`YYYY-MM-DD-<short-slug>.md`

For example:

- `2026-05-21-naming-mithaq.md` — the conversation that named this repo
- `2026-04-30-checkpoint-mechanism-generalization.md` — the conversation that abstracted roboclaws' checkpoint mechanism into a cross-repo template

The slug should be a verb phrase or noun phrase describing **what this conversation caused to happen**, not merely **what it was about**.

## Suggested file structure

Each dialogue file follows roughly this structure (not strict — run two or three and converge on your own rhythm before solidifying):

```markdown
# {{short summary: what this conversation changed}}

## Metadata

- **Date**: YYYY-MM-DD
- **Model**: Claude Opus 4.7 / GPT-5.x / ...
- **Triggering question**: {{the initial question that started this conversation}}
- **Affected repos**: {{which repos' judgment shifted as a result}}
- **Status**: {{in progress / landed / abandoned}}

## Key conclusions

> Three to five bullets so a reader who has not read the body can still take away the core.

- ...

## Abstractable structures (if any)

> Methods, frameworks, or decision patterns that emerged from one concrete discussion but apply to other situations.

## Excerpted dialogue

> Do not paste the whole thing. Excerpt the turns that mattered.
> When context is too thick, use `[...]` to indicate elision and briefly summarize what was elided.

### User

...

### Claude

...

## Follow-up actions

- ☐ Landed as `<repo>` issue #N
- ☐ ...

## Revisions

> If a judgment is later found wrong or no longer holds, record it here. Do not delete the original — preserve the evolution.

- {{YYYY-MM-DD}}: {{...}}
```

## Privacy and safety

- **Do not archive any conversation containing non-public API keys, tokens, or secrets.** If they appear, scrub them first.
- **Do not archive any conversation containing non-public commercial sensitive information.**
- This directory is public, and so are the dialogues — treat each one as "will be published someday."

## Why not just use Claude.ai / ChatGPT's export feature

Platform exports have several problems:

1. Different formats across platforms — no unified search.
2. Platforms can change history visibility or delete old conversations.
3. Exports contain a lot of irrelevant data (system messages, raw tool-call details) — very noisy.
4. Most importantly: **export is mechanical; archiving requires judgment**. The value of `mithaq` is not "everything recorded" — it is "the part selected to be recorded."

## Status

Started 2026-05. One archived dialogue so far: `2026-05-21-naming-mithaq.md` — also serves as the reference implementation for the format.
