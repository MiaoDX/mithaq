# mithaq invoke prompt

Copy everything between the dashed lines below and paste it to an agent working in any MiaoDX repo.

---

You are working in a MiaoDX repository. The user wants to perform a task governed by mithaq, the meta-repo that holds shared templates and conventions across all MiaoDX projects.

Before doing anything else, fetch and read the mithaq skill:

https://raw.githubusercontent.com/MiaoDX/mithaq/main/skills/mithaq/SKILL.md

The skill defines three modes:

- Mode A — run or update a periodic deep-research checkpoint for the current repo
- Mode B — create or update a research vectors card defining what a repo should track
- Mode C — archive an important AI-conversation dialogue

After loading the skill, ask the user which mode applies, then follow the skill's instructions for that mode. The skill itself points to several reference files (CHARTER.md, templates/checkpoint.md, vectors/README.md, vectors/roboharness.md, dialogues/README.md, dialogues/2026-05-21-naming-mithaq.md). Fetch those from `https://raw.githubusercontent.com/MiaoDX/mithaq/main/<path>` as needed for the chosen mode — not all at once, only the ones that mode requires.

Do not skip the skill-loading step. The skill encodes design discipline (where checkpoint instances go, what counts as a valid vectors card, what makes a dialogue worth archiving, common mistakes to avoid) that this prompt deliberately does not duplicate.

Begin by fetching the skill and confirming you have it loaded. Then ask which mode applies.

---

## Notes (do not copy this part)

- A single universal prompt covering all three modes. After loading the skill, the agent asks "which mode?" and then proceeds.
- If one specific mode (say, Mode A checkpoint) becomes frequent enough that saving the mode-selection turn matters, add a dedicated prompt like `run-checkpoint.md` later without breaking this one.
- This prompt deliberately duplicates nothing from SKILL.md — it only "delivers the agent to the skill."
