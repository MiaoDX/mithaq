> **语言**：当前页面 · [English](./2026-05-21-naming-mithaq.md)

# 命名这个 repo 的对话——为什么是 Mithaq

> **编辑说明**
>
> 这是 `mithaq` 仓库的**创世存档**。原对话是一次单一长 session 与 Claude Opus 4.7 进行（2026-05-21），围绕一个具体问题：把 `roboclaws` 的周期性 deep research 机制抽象成跨 repo 模板，需要一个 meta-repo 来承载，那么这个 repo 该叫什么。
>
> 本文是**编辑后的版本**——保留判断转折和关键引用，剪掉每个候选名字的细节铺陈（那些都在两份 deep research artifact 里）。原对话约 30 轮往返，本文呈现的是骨架。
>
> 之所以这是 `dialogues/` 的第一份存档，因为它本身就是定义 `dialogues/` 该收什么的对话——三条收录标准它都满足。

## 元数据

- **日期**：2026-05-21
- **模型**：Claude Opus 4.7（含 Anthropic deep research 工具两次调用）
- **触发问题**：roboclaws 的周期性 deep research 机制能否抽象成通用模板，跨 repo 复用
- **影响的 repo**：mithaq（本身）、未来所有 MiaoDX repo（通过 Layer 1 模板和 Layer 2 vectors 卡片间接影响）
- **状态**：已落地——`mithaq` 仓库已创建，第一组 commit 已推送

## 关键结论

1. **命名最终落定 `Mithaq`**（阿拉伯语，*مِيثَاق*，"庄严契约"）。理由：精确命中"我和顶级模型之间长期对话"这一关系的契约性质；命名空间在 GitHub / AI 创业公司 / 加密 token 三个维度均未被占；可挖掘的人文层次深（Quran 7:172 / Mithaq al-Alast / 与 `'ahd` 的区别 / 苏菲传统解读）。

2. **Earthseed**（Octavia Butler）是次优解，预留作未来英文姊妹仓库可能用名。**Primer**（Neal Stephenson《钻石时代》）功能映射最准但 `github.com/primer` 是 GitHub 自己的设计系统，无法使用——这个发现本身是值得记下来的认知。

3. **Layer 1 / Layer 2 / Layer 3 三层分离**是这次讨论的核心结构性产出：
   - **Layer 1**：通用 checkpoint 元模板（结构 + 方法论），跨 repo 复用，住在 mithaq
   - **Layer 2**：per-repo 调研方向卡片（具体盯哪些 entity、信源黑白名单、节奏），每 repo 一份，住在 mithaq
   - **Layer 3**：具体某月的 checkpoint，住在各自 repo 的 `docs/research-checkpoints/`
   "做一组通用 prompt 让任何 repo 都能跑"这个直觉**是错的**——它会让每个 repo 都拿到"问空气"的答案。

4. **确认也是一种调研产出**。两轮 deep research（第一轮多语言/宗教传统、第二轮科幻）跑下来，Mithaq 始终是最优解。第二轮没有改变结论，但**建立了 Mithaq 选择的稳健性**——知道"已经认真比较过 Primer / VALIS / Wallfacer / Earthseed / Fuligin / Ekumen 等几乎所有可能的候选"本身有价值。

## 可抽象的结构

这次对话浮现了几个可在其他场景复用的方法：

### 1. 三层抽象：通用元结构 / per-instance 卡片 / 具体实例

这不是命名问题独有的。任何"想把一个项目的成功机制抽象给其他项目用"的场景都会遇到同一个分层问题。直接把成功项目的全套做法当通用模板会失败，因为：

- 表面看是"流程"，深处是"entity 清单 + 节奏 + 信源判断"，后者必须 per-instance。
- 强行通用化的代价是**每个使用者都得做翻译**——而翻译这一步就是 per-instance 卡片该做的事，省不掉。

**判断什么属于哪一层的方法**：问自己"换一个项目，这个东西的具体内容会不会大改"。会大改的就是 Layer 2。

### 2. 名字的"挖掘深度"作为评估维度

短期看好听易记的名字，长期看的是能不能撑起多次反复使用而不空洞。判断一个名字的挖掘深度：

- 能挖几层？（字面 / 神话 / 数学 / 文学 / 现代共鸣）
- 每一层是否独立成立？（即：跟读者讲第一层时，不需要把其他层都铺出来）
- 三年后还有没有新内容可挖？

Memex 一挖到底就是 Bush 1945 那一篇，挖完就到底。Mithaq 可以挖至少四五次而不重样（Quran 7:172 / al-Alast / `'ahd` 与 `mithaq` 的区分 / 苏菲传统的内在化解读 / 与西奈山立约的比较 / 现代 AI 对齐讨论中的契约论…）。

### 3. "已经被 AI 圈占了什么"作为生态密度的指标

2026 年 5 月做命名调研，最直接的发现不是"哪些名字可用"，而是**哪些名字已经被占了**：

- Primer → GitHub 自己（设计系统）+ Primer.ai（国防 AI）
- VALIS → VALIS Systems（"AI 输出验证层"创业公司）
- Wallfacer / 面壁 → 面壁智能 / ModelBest（MiniCPM 那家）+ wallfacer.ai
- Sophon / 智子 → Sophon Network L2（Binance Labs 投，$70M+）
- Musubi → Musubi Labs（VC backed，AI 内容审核）
- Telos → Daniel Miessler 的 LLM context framework 等多个 AI 产品
- Sutra → TWO AI 的多语言 LLM

这是一份**2026 年中文/英文 AI 命名空间被吞噬的快照**。这个清单本身就有独立的归档价值——它告诉未来的人："这一年所有美好的科幻/神话词都被矿走了。"

### 4. 当 deep research 给的答案让人犹豫时，再跑一轮聚焦的

第一轮 deep research 把科幻条目化处理得太浅（只覆盖了六七个 Le Guin / Asimov / Lem 的概念），用户察觉到了。第二轮专门只针对科幻挖了 28 个候选，发现**完美的候选几乎全被 AI 圈占了**，反而**强化了对 Mithaq 的信心**——这是第一轮做不到的。

教训：第一轮 deep research 不满意时，**不要在结论上让步**，而是开一轮聚焦的补充。聚焦的成本远低于做错决定的成本。

## 对话节录

### 起点：把 roboclaws 的机制抽象成通用模板？

用户描述了 `roboclaws/docs/research-checkpoints/2026-04.md` 这个机制——一份 1221 行的月度生态盘点文档，附带详细的更新流程、信源四档分级、触发临时调研的条件——希望抽象成所有 repo 通用的一组 prompt。

我的第一反应是先泼冷水：

> 直接做"一组通用 prompt"有三个风险：
>
> 1. 调研方向通用化之后会变成"问空气"。把"OpenClaw 严格家族增量"改写成"项目核心依赖增量"，prompt 通用了但 deep research agent 会问回来"你的核心依赖具体是哪些？"——等于没问。
>
> 2. 每个 repo 的"相邻视角"结构性不同，不是表面差异。roboharness 的相邻视角是 MuJoCo/Isaac Lab/LeRobot；verse-driven 是 Claude Code Skills 生态/经典文本数字化；LIP 是站点生成器/PKM 工具——这些差异没法揉进同一组 prompt。
>
> 3. "每月一次"对小项目过重。docfit 类工具可能两三个月才有一次值得记录的变化。

提出三层方案：Layer 1 通用元模板 / Layer 2 per-repo vectors 卡片 / Layer 3 具体某期 checkpoint。

用户："呃，我觉得这个建议没有太大问题。" 然后转向了一个出乎意料的问题——**这个 meta-repo 该叫什么**。

### 第一组候选：契约 / 长期依赖

用户特意提到一个 framing：

> 我基本上所有建议都是和你们不管是克劳德还是 GPT 来聊，也许这个名字就包含你这里，包含我们的契约，我们的长期依赖关系等等。

这把命名问题从"给一个 meta repo 起名"提升到了"命名一段关系"。

我给了几个视角下的候选：

- 契约 / 长期依赖：**compact**、accord、covenant、pact
- 长期记忆 / 档案：**ledger**、codex、atlas
- 延续 harness 隐喻：yoke、reins、tether
- 沿 MiaoDX 命名风格：coharness、**LLMpact**、handshake

我推荐 compact——"紧凑" + "契约" 双关，跟其他 MiaoDX repo 命名节奏一致。

### 转向：科幻、宗教、道德经

用户："找一些这种科幻电影里面的词，或者是《圣经》、《古兰经》里面的，或者说道教经典里面的，道德经里面的"

这是关键的拓宽。我给了一组：

- 科幻：**Ansible**（Le Guin）、Sophon（三体）、**Memex**（Bush）、Mentat（Dune）
- 圣经/古兰经：**Logos**、Aleph、Ark
- 道德经：朴（Pu）、玄（Xuan）

排序首推 Logos——它**同时**是基督教的"道"、希腊哲学的"言/理性"、以及《道德经》"道"的标准译名，一个词通三家传统。但它在 tech 圈太常用。

### 收窄到 memex / aleph

用户："memex / aleph，多介绍一下这两个词吧。"

这一轮我做了两个词的深度对比：

- **Memex**：Bush 1945《As We May Think》。Memory extender，外置记忆装置 + associative trails 概念，是 hypertext / web 的思想源头。
- **Aleph**：三层叠加——希伯来字母 א（无限源头）+ Cantor ℵ（无穷集合的级别符号）+ Borges 1945《El Aleph》（一个直径两三厘米的点，凝视它能看见宇宙中的一切）。

我推荐 Aleph，理由是**隐喻精度更高**（Memex 隐喻对应 checkpoint 机制本身，Aleph 隐喻对应 Layer 1→Layer 2→Layer 3 这个分层抽象本身），**挖掘密度更深**（Memex 一挖到底就是 Bush 那篇文章；Aleph 可以挖三次都不重样），**跟 verse-driven 形成精神延续**（让计算机接触人文密度这条线）。

### 拓宽再拓宽：开 deep research

用户："既然提到了希伯来语，那其他的语言呢？我觉得可以搜索面再大一些。我给你开了深度搜索，你从不同视角来再搜搜看吧。感觉这个名字还是很重要的。"

并补充关键的定位：

> 这是一个 Meta Repo 来记录我和这些 top model 的最重要的对话，用它们来指引我的所有的项目的开展。

这句话把命名重心从"meta-template 的载体"挪到了"长期对话的存档 + 项目指引"。两条线索叠加：**契约关系** + **长期对话档案** + **指引未来项目**。

第一轮 deep research 覆盖了希伯来 / 阿拉伯 / 梵语 / 古希腊 / 拉丁 / 古汉语 / 日语 / 古挪威 / 埃及 / 苏美尔等多个语言传统。返回的结果出乎意料：

- **Aleph 没有想象中干净**：`Aleph-Alpha`（德国 30-repo 主权 AI 公司，明确做 LLM Intelligence Layer SDK）+ `Aleph Zero`（隐私 L1 区块链）已经分占名空。
- **多个看似完美的名字已被 AI 公司占据**：Sutra（TWO AI 多语言 LLM）、Yuanqi 元气（腾讯 agent 平台）、Musubi（VC 投的 AI 内容审核）、Telos（Daniel Miessler 的 LLM context framework）、Ansible（Red Hat）。
- **几个真正干净的候选浮现**：Mithaq（阿拉伯，"原初契约"）、Bijaksara（梵语，"种子-字"）、Foedus（拉丁，"契约"，"federal"的词源）、Yesod（希伯来，"基础"，Kabbalah 的第九 sefirah）、Ma'at（埃及，"真理/秩序"）。

我推荐 **Mithaq**。理由按重要性排：

> 1. 它精确命中你那句话的核心。"我和这些 top model 之间最重要的对话"——这是一种**契约关系**。Mithaq 在阿拉伯语里就是"庄严契约"，而且专指**先于一切存在的那个原始契约**（Quran 7:172 的 Mithaq al-Alast）。
>
> 2. 命名空间真的干净。只有一家沙特家族办公室叫 Mithaq Capital，跟开发者世界零接触。
>
> 3. 挖掘深度极深。你之前担心 Memex 挖到底就到 Bush 1945——Mithaq 不会，至少能挖出四五篇不重样的文章。
>
> 4. 跟你已有命名风格不冲突。verse-driven、roboharness、LIP、docfit——你的命名审美里有外来词的接受度。

### 用户察觉到了缺漏

用户："上面 Deep Research 进行科幻电影的 Research 了吗"

——这是这次对话里非常关键的一刻。**用户对 Claude 的产出做了独立审查**，发现第一轮科幻部分只覆盖了六七个名字，敷衍带过。

我承认了：原本 prompt 里写了让覆盖更广，但 deep research 把重心全压到了语言学/宗教传统上，科幻这条线没认真挖。列了一份没覆盖的清单（Le Guin 其他概念、Stephenson 全系、Lem、Egan、Banks Culture、Cixin Liu 全套、Borges、Calvino、Ted Chiang、PKD…）。

用户："好的，开始吧"

### 第二轮聚焦 SF deep research

只针对科幻挖了 28 个候选。结果颠覆了"科幻就有好名字"的天真假设：

- **Primer**（Stephenson《钻石时代》——一本指引一个人成长的 AI 书）：功能映射最准。但 `github.com/primer` 是 **GitHub 自己**的官方设计系统。无法使用。
- **VALIS**（PKD）：VALIS Systems 是一家"AI 输出验证层"创业公司，正好踩在这个领域。
- **面壁者 / Wallfacer**（刘慈欣）：面壁智能 / ModelBest 是国内主要 LLM 实验室（MiniCPM 那家）。中文 AI 圈这个名字基本焊死。
- **智子 / Sophon**：Sophon Network（ZK Stack Validium L2，币安投，$70M+ 融资）。
- **水滴 / Droplet**：水滴公司（NYSE: WDH）。

**刘慈欣的概念几乎全军覆没**——中文科技圈从 2022 年开始把三体词汇当矿挖。

真正干净的科幻候选只剩三个：**Earthseed**（Butler）、**Fuligin**（Wolfe）、**Ekumen**（Le Guin，但 `github.com/Ekumen-OS` 是阿根廷一家机器人公司，跟 roboharness 命名空间冲突）。

### 确认 Mithaq

第二轮没有改变结论，反而强化了它。我给出最终判断：

> Mithaq 仍然最优。三个干净的科幻候选都各有一个无法消除的弱点：Earthseed 的政治色彩 / Fuligin 的中文读法 / Ekumen 跟机器人 repo 的命名空间冲突。Mithaq 没有这种结构性弱点。
>
> 关键描述——"我和这些 top model 之间最重要的对话"——重心在"关系"不在"档案"。Earthseed / Fuligin 是档案概念，Ekumen 是联合体概念，Mithaq 是**契约**概念。契约才是那句话的内核。

副产品建议：

- 把 **Earthseed 留作未来的姊妹仓库名**——结构上跟 Butler 的设置呼应：Mithaq 是原契约，Earthseed 是契约衍生出的、可传播的箴言集。
- **首篇文章可以直接写《为什么这个 repo 不叫 Primer》**——用对比来定义，张力比直接讲 Mithaq 是什么更强。
- 第二轮文章素材库：Hylaean Theoric World（柏拉图理念世界与 LLM）/ 第二种妖（Lem 笔下的"按需相关性过滤器"——RAG 的前史）/ The Telling（Le Guin："讲述不是解释"）/ Severian 的小棕书（不可靠完美记忆）。

### 落地

用户："我建了 miaodx/mithaq 这个仓库，然后你按需对它提一个最初的一个或者多个 commit 吧"

我推了两个 commit：

- `8f6e1f3` — `docs: add README and CHARTER`
- `e4894ff` — `feat: establish templates, vectors, and dialogues structure`

包含 README、CHARTER（含为什么是 Mithaq、为什么不是其他候选、收录原则、与其他 repo 的关系）、Layer 1 通用 checkpoint 元模板（336 行）、`vectors/` 和 `dialogues/` 两个目录及其 README。

## 后续行动

- ☐ 写《为什么这个 repo 不叫 Primer》公众号文章（首篇）
- ☑ 在 `vectors/` 下铺第一份卡片——roboharness（用来验证 Layer 1 模板是否真的能跨场景）。已于 2026-05-21 完成；之后又新增了 `robowbc` 和 `roboclaws` 两份卡片。
- ☐ 把 Layer 1 模板在某个真实 repo（roboharness 或 verse-driven）上跑一遍首期 checkpoint，验证可用性
- ☐ 后续素材文章池：Aleph Alpha 的占用现象 / Liu Cixin 词汇被中文 AI 圈挖空的现象 / Primer 作为"完美但不可用的名字"
- ☐ 监控：如果未来 12 个月内出现一家叫 Mithaq 的 AI 创业公司，重新评估是否需要换名

## 修订

- 2026-06-18：更新 vectors 卡片里程碑的后续状态；当前已有三份卡片（`roboharness`、`robowbc`、`roboclaws`）。
