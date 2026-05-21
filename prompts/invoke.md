# mithaq invoke prompt

把下面虚线之间的全部内容粘给任意 repo 里工作的 agent。

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

## 备注（不要复制这部分）

- 一份通用 prompt 覆盖三种 mode。agent 加载 skill 后会反问"你要做哪种"，再具体进入。
- 如果某天某种 mode 的触发足够频繁，要省掉"反问"那一步，再开专用 prompt（如 `run-checkpoint.md`）。
- 这个 prompt 故意不重复 SKILL.md 已经说过的话——它只负责"把 agent 送到 skill 面前"。
