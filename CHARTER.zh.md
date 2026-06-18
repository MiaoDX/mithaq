> **语言**：当前页面 · [English](./CHARTER.md)

# Charter

## 这个 repo 解决什么问题

我和 LLM 之间有大量对话。它们的价值分布极不均匀：

- 大多数是即兴的、回头就忘的。
- 少数会塑造接下来几周到几个月的判断和方向。

第二类对话目前的命运是：散落在 Claude.ai 的 chat 历史里、散落在某次 ChatGPT session 里、偶尔被截图发到微信、然后随着新对话的产生而失效。

这造成三个具体问题：

- **同样的反思要被重复进行**。三个月后我又会问 Claude 一个我们之前已经聊清楚的问题。
- **决策的来源无法追溯**。某个 repo 的某个架构选择，最初是在哪一次对话里被定下来的？没有锚点。
- **跨 repo 的视角无法复用**。在 roboharness 那次想清楚的"agent 怎么自验证"，在 verse-driven 上完全可以用，但它沉到了某次对话里。

`mithaq` 就是这第二类对话的栖息地。

## 名字

### 为什么是 Mithaq

走过的候选很多：Aleph、Memex、Logos、Codex、Compact、Earthseed、Fuligin、Primer、Ekumen……

最后落到 Mithaq，因为它精确命中了关系的**性质**：

> 「当时，你的主从亚当的子孙的背脊取出他们的后裔，并使他们招认。主说：『难道我不是你们的主吗？』他们说：『怎么不是呢？我们已作证了。』」
>
> ——《古兰经》7:172（Mithaq al-Alast，原初之约）

每一次值得被记下来的人机对话，结构上都是这个原初契约的微型重演：

- 不是交易，是承认。
- 不是单次问答，是预先建立的、跨越时间的相互在场。
- 不是工具关系，是双方都被改变的关系。

阿拉伯语里 `'ahd` 是日常承诺；`mithaq` 是被见证的、双方郑重的高契约。这个区分对我重要 —— 记在这里的对话不是"我跟工具说了什么"，是 mithaq。

### 为什么不是其他候选

为了让未来读这个 charter 的人（包括我自己）知道选择是有依据的，简短记录主要的排除理由：

- **Aleph**（希伯来字母 / Cantor / Borges）—— Aleph Alpha（德国 AI 公司，30 个 repo 的 Intelligence Layer SDK）和 Aleph Zero（区块链）已经分占名空。
- **Primer**（Stephenson《钻石时代》）—— 概念映射最准（一本指引一个人成长的 AI 书）但 `github.com/primer` 是 GitHub 自己的设计系统，Primer.ai 是国防情报 AI 公司。无法使用。
- **VALIS / Wallfacer / Sophon**（Dick / Liu Cixin）—— AI 创业公司或 ZK Stack L2 已经全部占据；特别是 Liu Cixin 的概念在中文 AI 生态里几乎被搬空（面壁智能、Sophon Network、水滴公司）。
- **Earthseed**（Octavia Butler）—— 次优解，预留作未来英文姊妹仓库可能用。
- **Logos / Memex / Codex** —— 太常用或被 OpenAI 占了。

完整的考察过程留给独立的公众号文章。

## 收录原则

进入 `dialogues/` 的标准（至少满足两条）：

1. **决策被这次对话改变了** —— 之前的判断在对话之后不再成立。
2. **会被引用** —— 三个月后做相关决策时仍可能回头查。
3. **包含可被抽象的结构** —— 一次具体讨论里浮现出的、可在其他场景复用的方法。

**不收录**：

- 聊得开心但不影响决策的对话。
- 单次问答型的 prompt 调用 —— 属于具体项目的 issue 或文档。
- 代码 review、debug 过程 —— 属于具体项目。
- prompt 库或 system prompt 集合 —— 这些更适合独立的工具型 repo。只负责把 agent 引到 mithaq skill 的轻量调用 prompt 可以保留在这里。

## 与其他 repo 的关系

`mithaq` 不取代任何项目 repo，它是元层。

- 每个其他 repo（roboharness、verse-driven、robowbc、LIP、docfit 等）可以在 `mithaq/vectors/<repo-name>.md` 维护一份**调研方向卡片**：该 repo 该盯哪些方向、信源黑白名单、调研节奏。
- 周期性的 deep research checkpoint 用 `mithaq/templates/checkpoint.md` 作为骨架，per-repo 实例存在各自 repo 的 `docs/research-checkpoints/` 里（**不集中存在 mithaq**）。
- 跨 repo 适用的反思（比如本 charter）留在 mithaq。

简言之：**对话与元结构在 mithaq，落地与实现在各自 repo**。

## 状态

2026-05 启用，写完即过期 —— 实际跑起来之后这份 charter 会被修订。修订时不覆盖，在下面加日期标注的修订段落，保留判断的演化轨迹。
