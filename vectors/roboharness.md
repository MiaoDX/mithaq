# roboharness Research Vectors

> Layer 2 card: defines what `MiaoDX/roboharness` must track, which sources to use, and on what cadence.
> Used together with [`mithaq/templates/checkpoint.md`](../templates/checkpoint.md).
>
> **First written:** 2026-05-21
> **Next self-audit:** 2026-08-21 (the card itself is audited quarterly — vectors cards also go stale)

## Current project positioning (one sentence)

> "Approval/evidence harness for unattended robot code changes."
>
> Core wedge: `long unattended agent run → one proof pack → short human review`.
> Primary stack: MuJoCo + Meshcat + LeRobot + Unitree G1 + GR00T/SONIC + Pinocchio/Pink.
> Project-specific vocabulary: see [`roboharness/CONTEXT.md`](https://github.com/MiaoDX/roboharness/blob/main/CONTEXT.md).

## Hidden assumptions (the vectors exist to detect when these stop holding)

The following are bets the project's current architecture is making **without writing them down explicitly**. If a deep-research pass produces evidence that the support for any of these is weakening, immediately log it as an item in §7 Open Questions.

| # | Hidden assumption | Vector that challenges it |
|---|------------------|--------------------------|
| H1 | "The same coding agent should do visual review"; an independent VLM judge is the anti-pattern | Vector 3 (agent visual capabilities) |
| H2 | MuJoCo is the right primary substrate; Isaac Lab / Genesis / MolmoSpaces are watchlist | Vector 2 (simulator ecosystem) |
| H3 | Contract-first Python authoring (`HarnessContract`) is right; YAML / DSL / prompt-only are not | Vector 1 (harness upstream) |
| H4 | LeRobot is the right data format; Open X-Embodiment and others do not constitute a replacement | Vector 4 (VLA / data) |
| H5 | G1 + GR00T + SONIC is the right humanoid demo stack; Figure / Helix / π₀ do not constitute immediate replacements | Vector 5 (humanoid hardware) |
| H6 | "Human review at the end of an agent run" is the right loop; continuous review and no-human-in-loop are not | Vector 1 (harness upstream) |
| H7 | Visual-plus-numeric dual-channel, with metric-first and visual-fallback, is the right strategy | Vector 1 (harness upstream) |

Every checkpoint must answer: did this period produce evidence that any of the above assumptions needs to be reconsidered?

---

## Research vectors

### Vector 1: Harness engineering upstream

> Source of the project's name and positioning. If this line undergoes a paradigm shift, the project's entire design philosophy needs revisiting.

**Entities to track**:

- **Core people / projects**: Mitchell Hashimoto (mitchellh.com, "Engineer the Harness"); Anthropic engineering blog ("Effective harnesses for long-running agents", "Harness design for long-running application development", the Managed Agents series); OpenAI (Symphony, "Harness engineering: leveraging Codex", "Unlocking the Codex harness", "Unrolling the Codex agent loop"); Cursor ("Towards self-driving codebases", "Scaling long-running autonomous coding"); Martin Fowler ("Harness Engineering" essay)
- **Active second-tier**: HumanLayer ("Skill Issue: Harness Engineering for Coding Agents", the five levers); LangChain blog ("The Anatomy of an Agent Harness", "Improving Deep Agents with Harness Engineering"); Epsilla; InfoQ coverage of harness topics
- **Emerging, worth following**: monthly arXiv scan for new "agent harness" / "approval testing for LLM agents" papers

**Expected changes**:

- Within 12 months may emerge: standardization of agent-harness specs, the term "approval pack" spreading or being supplanted, SLA models for unattended long runs
- Already happening: harness components getting retired as models advance (Anthropic retired old components moving from Opus 4.5 → 4.6 → 4.7)

**Relevance to roboharness**: H3, H6, H7 — all three assumptions come from this line. Any change to the semantics of "approval" directly affects roboharness's proof-pack design.

---

### Vector 2: Robot simulator substrate ecosystem

> roboharness sits on top of MuJoCo. A substrate-layer change directly affects the project's working surface.

**Entities to track**:

- **Mainstream**: MuJoCo (DeepMind/Google, latest release); mujoco_playground (Google DeepMind 2025); mjlab/mujocolab (Isaac Lab API on a MuJoCo-Warp backend); Isaac Sim; Isaac Lab (NVIDIA, note the 2.x → 3.x restructuring); Meshcat
- **Newcomers / challengers**: MolmoSpaces (Allen AI, released 2026-02; 230K+ scenes, 42M+ grasps, USD export); Genesis (released 2024-12, claiming 80× faster than MuJoCo); ManiSkill3 (HF team); Habitat 3.0 (Meta + PARTNR)
- **Special cases**: mujoco_mpc; differentiable physics (Brax, warp-sim)

**Expected changes**:

- Will Genesis grow a real ecosystem in 2025-2026 or remain a one-off release?
- Multi-agent maturity in MolmoSpaces (currently single-agent only)
- Whether the Isaac Lab 3.x restructure breaks existing integrations
- MuJoCo gaining GPU backend (mujoco-warp) shifts the performance landscape

**Relevance to roboharness**: H2's support. If MuJoCo loses ground, or if some substrate gains native "approval pack" capability, roboharness's primary stack needs reconsideration.

---

### Vector 3: Agent visual review capabilities

> roboharness bets that "the coding agent's own eyes are enough; no separate VLM judge needed." This bet depends on multimodal models' image-reasoning and long-context capabilities continuing to improve.

**Entities to track**:

- **Mainstream multimodal model versions**: Claude (latest version's vision capability, long-context image reasoning, multi-image simultaneous reasoning); GPT series (including vision improvements); Gemini series (especially Pro's visual reasoning); Qwen-VL series; Kimi vision
- **VLM-as-judge academic line**: new arXiv papers on "VLM judge", "visual evaluation", "image reasoning benchmark" (especially in robotics scenarios)
- **Dedicated visual evaluation tools**: Anthropic vision-agent capability release notes; OpenAI o-series visual reasoning; Reka; xAI Grok vision
- **Counter-evidence**: research showing same-agent visual review systematically underperforms an independent VLM judge

**Expected changes**:

- Long-context image-reasoning capability curve (one model handling 10-20 images in a single pass)
- Emergence of robotics-specific visual reasoning benchmarks
- Maturity of "visual chain-of-thought" as a line of work

**Relevance to roboharness**: H1's support. If a new model release significantly widens or narrows the gap between same-agent review and a dedicated judge, H1 needs to be updated.

---

### Vector 4: VLA / robot-policy model ecosystem

> These are the things roboharness evaluates. New VLAs change what needs reviewing.

**Entities to track**:

- **Current mainstream**: GR00T N1.7 / N2 (NVIDIA, plus WholeBodyVLA and GR00T-WholeBodyControl); Physical Intelligence π₀ / π₀.₅ / π₁ (openpi); SONIC (NVIDIA GEAR); Helix (Figure, closed-source but observable)
- **Academic line**: OpenVLA + OpenVLA-OFT; CogACT; Cosmos Policy; dVLA; DIVA; FASTer; OmniSAT; XR-1; FLOWER; MEM (Physical Intelligence 2026-03, 15-minute kitchen tasks)
- **Data / format standards**: LeRobotDataset (v3.0 released, watch for what comes next); Open X-Embodiment; Bridge-V2; Droid

**Expected changes**:

- Emergence of open-source general humanoid VLA (dual-arm + whole-body): currently G1 integration goes through GR00T, π₀.₅ is a potential replacement
- Convergence on LeRobotDataset as the data format, or fragmentation
- New review dimensions appearing (dual-hand coordination, long-horizon tasks, natural-language instructions)

**Relevance to roboharness**: H4 and H5. As the set of "things to evaluate" expands with new VLAs, proof-pack design may need new dimensions.

---

### Vector 5: Humanoid hardware + WBC stack

> roboharness specifically integrates Unitree G1 + Pinocchio + Pink. A change in the hardware platform or WBC stack affects integration work.

**Entities to track**:

- **Hardware**: Unitree G1 / H1 (firmware, new SDK versions); Figure (02 / 03); Boston Dynamics (Atlas commercialization); Apptronik Apollo; Tesla Optimus; 1X NEO; Sanctuary Phoenix; RBY1M; AGIbot G2
- **WBC stack**: Pinocchio; Pink (IK); MuJoCo MPC; generative WBC papers (e.g., GMP / Trajectory Diffusion for WBC)
- **Emerging**: humanoid-gym; unitree_mujoco; unitree_rl_gym

**Expected changes**:

- Will Figure or Boston Dynamics release an open SDK (which would make them an integration target)
- Firmware and SDK release cadence for Chinese humanoids (智元, 宇树)
- Whether proof-pack design needs reworking for the single-arm → dual-arm → whole-body complexity ladder

**Relevance to roboharness**: H5. This line moves slower than Vectors 1-4; cadence can be relaxed.

---

### Vector 6: MCP / agent tool protocols (including robotics MCP servers)

> roboharness provides optional MCP tools. Protocol-layer changes affect integration approach.

**Entities to track**:

- **Protocol mainline**: MCP (Anthropic / Linux Foundation AAIF) spec version changes; A2A; ACP
- **Robotics MCP servers**: isaacsim-mcp; ros-mcp-server; mujoco-mcp (if it exists); whether LeRobot ships an official MCP server
- **Agent skill standards**: Anthropic Skills (agentskills.io, the open standard published 2026-03-14); SKILL.md instances in robotics
- **Agent-to-robot general frameworks**: whether any project tries to wrap ROS / DDS into MCP

**Expected changes**:

- The MCP 2026 roadmap's actual rollout (transport scalability, agent communication, governance, enterprise-readiness)
- Whether a de facto "standard robotics MCP server" emerges
- Anthropic Skills extending into robotics scenarios

**Relevance to roboharness**: Technical debt + integration-path decisions. Cadence can be relaxed.

---

## Sources

### Whitelist (A-tier, cite directly)

- **Official primary**: anthropic.com/news, anthropic.com/research, openai.com/index, cursor.com/blog, deepmind.google/blog, nvidia.com/blog (especially the robotics section), huggingface.co/blog, allenai.org/blog, physicalintelligence.company/blog
- **Project repos (primary)**: GitHub MiaoDX/roboharness itself; google-deepmind/mujoco; google-deepmind/mujoco_playground; isaac-sim/IsaacLab; NVIDIA/Isaac-GR00T; Physical-Intelligence/openpi; huggingface/lerobot; allenai/molmospaces; Genesis-Embodied-AI/Genesis
- **Academic**: arXiv (cs.RO, cs.AI, cs.LG); priority subscribe keywords "robot policy", "VLA", "agent harness", "approval testing", "VLM judge"
- **Maintainer blogs**: mitchellh.com; Martin Fowler; Pete Warden; Anthropic engineering blog (independent subdomain)
- **Conferences**: CoRL, ICRA, IROS, RSS (robotics); NeurIPS, ICLR, ICML (academic AI); ICSE, FSE (software engineering, the source of approval testing concepts)

### Grey list (B-tier, requires cross-verification)

- TheNewStack, InfoQ, IEEE Spectrum, The Robot Report, ZDNet, VentureBeat, 量子位, 机器之心
- HackerNews, Reddit r/MachineLearning, Zhihu highly-upvoted technical answers with citations

### Blacklist (D-tier, actively ignore)

- "Best X of 2026" buying guides (vellum.ai, qubittool.com, composio.dev, scriptbyai.com, aimagicx.com, skywork.ai, and similar SEO sites)
- Marketing-flavored medium/dev.to posts without primary-source citations
- AI-generated awesome-* lists on GitHub (use only as discovery tools, not as citation sources)

---

## Cadence

- **Routine checkpoint**: monthly, in the last week of the month. A single deep-research session covers all 6 vectors. Vectors 1-4 must be written every period; Vectors 5-6 may be marked "no update" rather than padded if no significant change happened this period.
- **Card self-audit**: quarterly (after every 3 checkpoints), audit this VECTORS file itself — is the entity list stale? do the hidden assumptions need to be added to or pruned?

---

## Triggers for off-schedule research (do not wait for the next cycle)

Any one of these triggers an ad-hoc deep research pass:

- **Model-generation jump**: a flagship model like Claude Opus 5 or GPT-6 is released; a version with significantly improved vision capabilities ships (affects H1)
- **Major VLA release**: GR00T N2, π₁, a new open-source humanoid VLA (affects H4, H5)
- **Substrate major change**: Genesis 1.0 release, Isaac Lab 3.x completion, MolmoSpaces adds multi-agent support (affects H2)
- **Key-dependency event**: MuJoCo, LeRobot, GR00T, or Pinocchio undergoes a license change, end of maintenance, or serious security event
- **Peer / upstream change**: Anthropic, OpenAI, or Cursor ships a major harness-engineering release (e.g., Managed Agents general availability, Symphony 2.0) (affects H3, H6, H7)
- **Conceptual competition**: terms like "approval pack" / "harness contract" get redefined differently by a major vendor; or a paper appears demonstrating that a separate VLM judge significantly outperforms same-agent review (counter-evidence to H1)

---

## Status

- 2026-05-21: first written. **No checkpoints have been run yet** — this card's usability has not been validated.
- When running the first checkpoint, verify two things: (1) all 6 vectors produce useful output; (2) the hidden assumptions actually get challenged by deep research (if two consecutive checkpoints leave "all assumptions unchallenged," the vectors design has blind spots and needs revision).
