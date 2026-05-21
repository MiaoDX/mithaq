# roboharness Research Vectors

> Layer 2 卡片：定义 `MiaoDX/roboharness` 该盯哪些方向、用哪些信源、什么节奏。
> 配合 [`mithaq/templates/checkpoint.md`](../templates/checkpoint.md) 使用。
>
> **首次铺设：** 2026-05-21
> **下次自审：** 2026-08-21（每季度审一次卡片本身——vectors 也会过期）

## 项目当前定位（一句话）

> "Approval/evidence harness for unattended robot code changes."
>
> 核心 wedge：`long unattended agent run → one proof pack → short human review`。
> 主栈：MuJoCo + Meshcat + LeRobot + Unitree G1 + GR00T/SONIC + Pinocchio/Pink。
> 关键术语自定义见 [`roboharness/CONTEXT.md`](https://github.com/MiaoDX/roboharness/blob/main/CONTEXT.md)。

## 隐藏假设（vectors 的存在就是为了发现这些假设何时过期）

以下是 roboharness 当前架构里**没被显式写出来**但实际在被押注的判断。如果某次 deep research 发现某个假设的支撑变弱，应立刻进入 §7 公开问题。

| # | 隐藏假设 | 对应的挑战 vector |
|---|---------|------------------|
| H1 | "同一个 coding agent 做视觉 review"是对的，独立 VLM judge 是反模式 | Vector 3（agent 视觉能力） |
| H2 | MuJoCo 是对的主 substrate，Isaac Lab / Genesis / MolmoSpaces 是 watchlist | Vector 2（仿真生态） |
| H3 | 合同优先的 Python authoring（`HarnessContract`）是对的，YAML/DSL/prompt-only 不是 | Vector 1（harness 上游） |
| H4 | LeRobot 是对的数据格式，Open X-Embodiment 等不构成替代 | Vector 4（VLA / 数据） |
| H5 | G1 + GR00T + SONIC 是对的人形 demo 栈，Figure/Helix/π₀ 不构成立即替代 | Vector 5（人形硬件） |
| H6 | "人审在 agent run 结束时"是对的循环，连续 review / 无人审都不是 | Vector 1（harness 上游） |
| H7 | 视觉 + 数值双通道、metric-first-with-visual-fallback 是对的策略 | Vector 1（harness 上游） |

每期 checkpoint 应该回答：这一期有没有证据让上面任何一条假设需要被重新审视？

---

## 调研方向

### Vector 1：Harness Engineering 上游

> 这是 roboharness 命名和定位的源头。这条线如果发生范式转变，整个项目的设计哲学需要重审。

**要盯的 entity**：

- **核心人物 / 项目**：Mitchell Hashimoto（mitchellh.com，"Engineer the Harness"）、Anthropic engineering blog（"Effective harnesses for long-running agents"、"Harness design for long-running application development"、Managed Agents 系列）、OpenAI（Symphony、"Harness engineering: leveraging Codex"、"Unlocking the Codex harness"、"Unrolling the Codex agent loop"）、Cursor（"Towards self-driving codebases"、"Scaling long-running autonomous coding"）、Martin Fowler（"Harness Engineering" essay）
- **二线但活跃**：HumanLayer（"Skill Issue: Harness Engineering for Coding Agents"、五杠杆）、LangChain blog（"The Anatomy of an Agent Harness"、"Improving Deep Agents with Harness Engineering"）、Epsilla、InfoQ 关于 harness 的报道
- **新兴值得追踪**：每月扫一遍 arXiv 是否出现 "agent harness" / "approval testing for LLM agents" 类的论文

**关键变化预期**：

- 12 个月内可能出现的：agent harness 的 spec 标准化、"approval pack" 这个术语本身的传播或被替换、unattended 长跑的 SLA 模式
- 已经在发生：harness 组件随模型代际淘汰（Anthropic 在 Opus 4.5→4.6→4.7 之间逐一移除旧组件）

**对 roboharness 的相关性**：H3、H6、H7 三条假设全部来自这条线。任何"approval"语义的变化都直接影响 roboharness 的 proof pack 设计。

---

### Vector 2：机器人仿真 Substrate 生态

> roboharness 坐在 MuJoCo 之上。substrate 层换代会直接影响项目的工作面。

**要盯的 entity**：

- **主流**：MuJoCo（DeepMind/Google，最新 release）、mujoco_playground（Google DeepMind 2025）、mjlab/mujocolab（MuJoCo-Warp 后端的 Isaac Lab API 复刻）、Isaac Sim、Isaac Lab（NVIDIA，注意 2.x→3.x 的重构）、Meshcat
- **新晋 / 挑战者**：MolmoSpaces（Allen AI，2026-02 发布，23 万+ 场景、4200 万抓取，USD 出口）、Genesis（2024-12，号称比 MuJoCo 快 80×）、ManiSkill3（HF 团队）、Habitat 3.0（Meta + PARTNR）
- **特殊角色**：mujoco_mpc、DiffPhys / 可微分仿真（如 Brax、warp-sim）

**关键变化预期**：

- Genesis 在 2025-2026 期间会决定是真长出生态还是只是一次性发布
- MolmoSpaces 的多 agent 支持成熟度（目前是单 agent）
- Isaac Lab 3.x 重构会否打破现有集成
- MuJoCo 加 GPU 后端（mujoco-warp）改变性能格局

**对 roboharness 的相关性**：H2 假设的支撑。MuJoCo 失势或者某个 substrate 出现"原生 approval pack"能力，roboharness 主栈需要重审。

---

### Vector 3：Agent 视觉 Review 能力

> roboharness 押注"coding agent 自己看图就够了，不需要独立 VLM judge"。这条假设依赖于多模态模型的图像理解长上下文能力持续提升。

**要盯的 entity**：

- **主流多模态模型版本**：Claude（最新版本的视觉能力、长上下文图像推理能力、多张图同时推理）、GPT 系列（含 vision 改进）、Gemini 系列（特别是 Pro 的视觉推理）、Qwen-VL 系列、Kimi 视觉能力
- **VLM-as-judge 学术线**：arXiv 上关于"VLM judge"、"visual evaluation"、"image reasoning benchmark" 的新论文（特别是机器人场景）
- **专门的视觉评估工具**：Anthropic 的 vision agent 能力 release notes、OpenAI o-series 视觉推理、Reka、xAI Grok vision
- **反向证据**：是否有研究表明 same-agent visual review 系统性地不如独立 VLM judge

**关键变化预期**：

- 长上下文图像推理（一次看 10-20 张图）的能力曲线
- 机器人视觉推理专门 benchmark 的出现
- "visual chain-of-thought" 这条线的成熟度

**对 roboharness 的相关性**：H1 假设的支撑。如果某次新模型发布显著缩小或扩大 same-agent 与独立 judge 的差距，H1 需要更新。

---

### Vector 4：VLA / 机器人策略模型生态

> 这些是 roboharness 评估的对象。新 VLA 改变需要被 review 的东西。

**要盯的 entity**：

- **当前主流**：GR00T N1.7 / N2（NVIDIA，及 WholeBodyVLA、GR00T-WholeBodyControl）、Physical Intelligence π₀ / π₀.₅ / π₁（openpi）、SONIC（NVIDIA GEAR）、Helix（Figure，闭源但可观察）
- **学术线**：OpenVLA + OpenVLA-OFT、CogACT、Cosmos Policy、dVLA、DIVA、FASTer、OmniSAT、XR-1、FLOWER、MEM（Physical Intelligence 2026-03，15 分钟厨房任务）
- **数据 / 格式标准**：LeRobotDataset（v3.0 已发布，关注后续）、Open X-Embodiment、Bridge-V2、Droid

**关键变化预期**：

- 通用 humanoid VLA（双臂 + 全身）的开源版本（目前 G1 集成主要走 GR00T，π₀.₅ 是潜在替代）
- 数据格式收敛到 LeRobotDataset 还是分裂
- 新增需要 review 的维度（如双手协同、长程任务、自然语言指令）

**对 roboharness 的相关性**：H4 和 H5 假设的支撑。新 VLA 出来即所谓"评估目标"扩大，proof pack 设计可能需要新维度。

---

### Vector 5：人形硬件 + WBC 栈

> roboharness 具体集成 Unitree G1 + Pinocchio + Pink。硬件平台或 WBC 栈换代会影响集成工作。

**要盯的 entity**：

- **硬件**：Unitree G1 / H1（固件、新 SDK 版本）、Figure（02/03）、Boston Dynamics（Atlas 商业化进展）、Apptronik Apollo、Tesla Optimus、1X NEO、Sanctuary Phoenix、RBY1M、AGIbot G2
- **WBC 栈**：Pinocchio、Pink（IK）、MuJoCo MPC、generative WBC 论文（如 GMP / Trajectory Diffusion for WBC）
- **新兴**：humanoid-gym、unitree_mujoco、unitree_rl_gym

**关键变化预期**：

- Figure 或 Boston Dynamics 是否会发布开放 SDK（如发布即新集成目标候选）
- 国内人形（智元、宇树）固件和 SDK 升级节奏
- 单臂 → 双臂 → 全身这条复杂度阶梯上 roboharness 提供的 proof pack 是否需要重做

**对 roboharness 的相关性**：H5 假设的支撑。这条线慢于 Vector 1-4，节奏可以放宽。

---

### Vector 6：MCP / Agent 工具协议（含机器人 MCP server）

> roboharness 提供可选的 MCP tools。协议层变化会影响集成方式。

**要盯的 entity**：

- **协议主线**：MCP（Anthropic / Linux Foundation AAIF）规范版本变更、A2A、ACP
- **机器人 MCP server**：isaacsim-mcp、ros-mcp-server、mujoco-mcp（如存在）、LeRobot 是否出官方 MCP server
- **agent skill 标准**：Anthropic Skills（agentskills.io，2026-03-14 发布的开放标准）、SKILL.md 在机器人领域的实例
- **agent-to-robot 通用框架**：是否有项目尝试把 ROS / DDS 包成 MCP

**关键变化预期**：

- MCP 2026 路线图的落地节奏（传输可扩展性、agent 通信、治理、企业就绪）
- 机器人 MCP server 是否会出现"事实标准"
- Anthropic Skills 在机器人场景的扩展

**对 roboharness 的相关性**：技术债 + 集成路径决策。节奏可以放宽。

---

## 信源

### 白名单（A 档，直接引用）

- **官方一手**：anthropic.com/news、anthropic.com/research、openai.com/index、cursor.com/blog、deepmind.google/blog、nvidia.com/blog（特别是 robotics 板块）、huggingface.co/blog、allenai.org/blog、physicalintelligence.company/blog
- **项目 repo 一手**：GitHub MiaoDX/roboharness 自己、google-deepmind/mujoco、google-deepmind/mujoco_playground、isaac-sim/IsaacLab、NVIDIA/Isaac-GR00T、Physical-Intelligence/openpi、huggingface/lerobot、allenai/molmospaces、Genesis-Embodied-AI/Genesis
- **学术**：arXiv（cs.RO、cs.AI、cs.LG），重点订阅"robot policy"、"VLA"、"agent harness"、"approval testing"、"VLM judge" 关键词
- **维护者博客**：mitchellh.com、Martin Fowler、Pete Warden、Anthropic engineering blog（独立子域）
- **会议**：CoRL、ICRA、IROS、RSS（机器人）；NeurIPS、ICLR、ICML（学术 AI）；ICSE、FSE（软件工程，approval testing 来源）

### 灰名单（B 档，需交叉验证）

- TheNewStack、InfoQ、IEEE Spectrum、The Robot Report、ZDNet、VentureBeat、量子位、机器之心
- HackerNews、Reddit r/MachineLearning、知乎技术回答（高赞且有引用）

### 黑名单（D 档，主动忽略）

- "2026 年最佳 X" 导购站（vellum.ai、qubittool.com、composio.dev、scriptbyai.com、aimagicx.com、skywork.ai 等典型 SEO 站）
- 大量未引用一手信源的 medium/dev.to 营销文
- AI 生成的 GitHub awesome-* 列表（仅作为"发现工具"使用，不作为引用源）

---

## 节奏

- **常规 checkpoint**：每月一次，月底最后一周。一次 deep research session 覆盖全部 6 个 vector。Vector 1-4 每期都要写；Vector 5-6 如果当期没有显著变化可以注明"无更新"而不强求填充。
- **卡片自审**：每季度（每 3 个 checkpoint 后）重审一次本 VECTORS 文件——entity 清单是否过期？隐藏假设是否需要增删？

---

## 触发临时调研的条件（不等月底）

任一条触发即开一次 ad-hoc deep research：

- **模型代际跃迁**：Claude Opus 5、GPT-6 等旗舰模型发布；视觉能力显著进步的版本（影响 H1）
- **VLA 重大发布**：GR00T N2、π₁、新开源 humanoid VLA（影响 H4、H5）
- **Substrate 重大变化**：Genesis 1.0 release、Isaac Lab 3.x 完成、MolmoSpaces 增加多 agent 支持（影响 H2）
- **关键依赖事件**：MuJoCo、LeRobot、GR00T、Pinocchio 任一发生 license 变更、停维护、严重安全事件
- **同行 / 上游变化**：Anthropic、OpenAI、Cursor 在 harness engineering 方向出大型 release（如 Managed Agents GA、Symphony 2.0 等）（影响 H3、H6、H7）
- **概念竞争**："approval pack" / "harness contract" 等术语被某个大厂用不同方式重新定义，或出现明确的反范式（如有 paper 证明 separate VLM judge 显著优于 same-agent review）

---

## 状态

- 2026-05-21：首次铺设。**尚未跑过任何 checkpoint**——这份卡片的可用性需要在第一次实际跑过之后才能验证。
- 第一次跑 checkpoint 时重点验证两件事：(1) 6 个 vector 是否都能产出有用结果；(2) 隐藏假设是否真的能被 deep research 挑战到（如果连续两期都"全部假设未受挑战"，说明 vectors 设计有盲点，需要修订）。
