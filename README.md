# Mithaq

> *Mithaq* (مِيثَاق, "庄严契约") —— 我与若干 top AI model 之间长期对话的元仓库。
> 它的存在是为了让这些对话不消散，并用它们指引我其他所有的项目。

## 这是什么

一个 meta-repo，做两件事：

1. **存档** —— 把我和 Claude / GPT 等模型之间真正重要的、塑造判断的对话保留下来。一次性的、即兴的、聊完就忘的不收；只收那些**改变后续决策**的对话。
2. **指引** —— 从这些对话里抽出可复用的结构（如周期性 deep research 的元模板、per-repo 的调研方向卡片），让我的其他 repo（roboharness、verse-driven、robowbc、LIP、docfit 等）能借力。

不收录代码，不收录文档草稿，不收录 prompt 库——这些有专门的项目。

## 名字

详见 [`CHARTER.md`](./CHARTER.md)。简短版：`Mithaq` 是阿拉伯语"庄严契约"，特指《古兰经》7:172 那个**先于一切存在的原始契约**（Mithaq al-Alast）。每一次值得被记下来的人机对话，结构上都是这个原初契约的微型重演。

## 目录

```
mithaq/
├── README.md          # 入口（你正在读的这个）
├── CHARTER.md         # 为什么取这个名字、为什么做这件事
├── skills/            # 给 AI agent 用的 SKILL.md（跨 repo 调用入口）
├── templates/         # 可复用结构（如 checkpoint 元模板）
├── vectors/           # 每个其他 repo 的调研方向卡片（Layer 2）
└── dialogues/         # 存档的关键对话
```

## 给 AI agent 用

在任何 MiaoDX repo 里工作时，如果要跑 checkpoint、写 vectors 卡片、或存档 dialogue，让 agent 加载 [`skills/mithaq/SKILL.md`](./skills/mithaq/SKILL.md) —— 它是 SKILL.md 开放标准格式（Anthropic 2025-12 发布、Claude Code / Codex / Cursor 等多家支持），起 router 作用，告诉 agent 何时该用 mithaq、各种产物放在哪。

让 agent 看 raw URL：

```
https://raw.githubusercontent.com/MiaoDX/mithaq/main/skills/mithaq/SKILL.md
```

或在 consuming repo 的 `CLAUDE.md` / `AGENTS.md` 里指向这个 skill。

## 状态

2026-05 启用。结构会随实际使用调整。
