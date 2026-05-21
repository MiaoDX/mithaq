# Vectors —— Per-Repo 调研方向卡片

本目录存放每个 MiaoDX repo 的**调研方向卡片**。每个卡片定义"这个 repo 该盯哪些方向"。

## 为什么需要这一层

[`templates/checkpoint.md`](../templates/checkpoint.md) 是 Layer 1——通用的 checkpoint 写作骨架，跨 repo 复用。

但是骨架本身不告诉你"该盯哪些方向"——这是 per-repo 的，结构性不同：

- `roboharness` 该盯：MuJoCo / Isaac Lab / LeRobot / VLM 评估 / robotics benchmark
- `verse-driven` 该盯：Claude Code Skills 生态 / 经典文本数字化 / agent 反思框架 / 人文 × LLM 学术圈
- `LIP` 该盯：站点生成器 / 个人知识管理工具 / 文档 site 同行
- ……

强行揉成一组通用 prompt 会让每个 repo 都拿到"问空气"的答案。所以每个 repo 自己有一份卡片。

## 一份 vectors 卡片应该包含什么

至少这些：

1. **3-7 个调研方向**，每个方向写清楚：
   - 方向名（如"Agent SDK / Harness 层动态"）
   - 具体的 entity 清单（人 / 项目 / 标准 / 论文系列）—— 没有具体 entity，prompt 会问空气
   - 这一年的关键变化预期
2. **信源白名单**：本领域哪些 A 档站点值得直接信
3. **信源黑名单**：本领域哪些 D 档站点应主动忽略
4. **调研节奏**：月度 / 双月 / 季度 / 事件驱动
5. **触发临时调研的条件**：什么事件发生时不等节奏到就要跑

## 文件命名

`<repo-short-name>.md`，例如：

- `roboharness.md`
- `verse-driven.md`
- `lip.md`

## 与 checkpoint 文件的关系

vectors 卡片留在 mithaq；具体期次的 checkpoint 文件（`YYYY-MM.md`）放在各自 repo 的 `docs/research-checkpoints/`。

理由：

- vectors 是元数据，跨期不变（变了就是 vectors 自己升级，独立 commit）。
- checkpoint 是实例数据，每期一份，跟该 repo 的代码 history 在一起更自然。
- 这样 mithaq 不会被各 repo 的月度 checkpoint 灌爆。

## 状态

2026-05 启用，**尚无具体卡片**。第一份会是 roboharness 或 verse-driven。
