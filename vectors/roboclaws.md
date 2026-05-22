# roboclaws Research Vectors

> Layer 2 card: defines what `MiaoDX/roboclaws` must track, which sources to use, and on what cadence.
> Used together with [`mithaq/templates/checkpoint.md`](../templates/checkpoint.md).
>
> **First written:** 2026-05-22
> **Next self-audit:** 2026-08-22 (the card itself is audited quarterly — vectors cards also go stale)

## Current project positioning (one sentence)

> "Visible robotics demos driven by VLM policies, OpenClaw, and AI coding agents."
>
> Core wedge: `open-ended goal → agent skill → composite action → semantic capability → environment primitive → execution backend`
> (the canonical 6-layer abstraction ladder from `roboclaws/README.md` and `roboclaws/ARCHITECTURE.md`),
> with reviewable HTML reports as the proof artifact derived from execution (not itself a layer),
> with public/private evaluation truth separation as a first-class architectural concern.
> Primary stack: AI2-THOR (navigation/territory/coverage) + MolmoSpaces & MuJoCo (cleanup/manipulation) +
> MCP semantic profiles + multi-LLM providers (Anthropic / OpenAI / Kimi / MiMo / NVIDIA / Mock) +
> RBY1M/CuRobo for planner-proof, with Nav2-shaped map bundles as the real-robot bridge.
> Four operating modes coexist: direct VLM games, OpenClaw Gateway, coding-agent-over-MCP, and the Railway appliance.
> Project-specific vocabulary and the canonical capability surface:
> see [`roboclaws/ARCHITECTURE.md`](https://github.com/MiaoDX/roboclaws/blob/main/ARCHITECTURE.md)
> and [`roboclaws/README.md`](https://github.com/MiaoDX/roboclaws/blob/main/README.md).

## Hidden assumptions (the vectors exist to detect when these stop holding)

The following are bets the project's current architecture is making **without writing them down explicitly**. If a deep-research pass produces evidence that the support for any of these is weakening, immediately log it as an item in §7 Open Questions of the corresponding checkpoint.

| # | Hidden assumption | Vector that challenges it |
|---|------------------|--------------------------|
| H1 | The same coding-agent / VLM that drives the robot can also do the visual review of its own behavior; a separate VLM-judge is not needed at this scope | Vector 5 (multimodal model capabilities) |
| H2 | AI2-THOR + MolmoSpaces is the right dual substrate (navigation+territory on AI2-THOR, cleanup+manipulation on MolmoSpaces); other substrates are watchlist | Vector 3 (simulator substrate) |
| H3 | MCP semantic profiles + Anthropic Skills (SKILL.md) is the right packaging for both VLM-direct mode and coding-agent-over-MCP mode; per-framework custom interfaces are not | Vector 1 (harness upstream); Vector 4 (MCP + skill standards) |
| H4 | Four-mode coexistence with Mode 3 (coding-agent-over-MCP) as architectural center is right; collapsing to one mode is not | Vector 1 (harness upstream); Vector 2 (OpenClaw ecosystem) |
| H5 | Public-vs-private evaluation truth separation (privileged tools, hidden mess sets, semantic profile metadata) is the right way to expose capability without leaking ground truth | Vector 4 (MCP + skill standards); Vector 7 (real-robot bridge) |
| H6 | Static HTML reports (frames + maps + traces + scores + proof bundles) are the right primary proof surface; interactive dashboards and live leaderboards are not the priority | Vector 3 (simulator substrate) |
| H7 | Per-agent SOUL + multi-LLM provider mix (Anthropic / OpenAI / Kimi / MiMo / NVIDIA / Mock) is the right experimental design; provider monogamy is not | Vector 5 (multimodal model capabilities) |
| H8 | Multiple coding-agents driving multiple robots simultaneously is the right new territory worth pioneering; sticking to single-agent harness loops is not | Vector 1 (harness upstream); Vector 6 (multi-agent embodied AI) |

Every checkpoint must answer: did this period produce evidence that any of the above assumptions needs to be reconsidered?

---

## Research vectors

### Vector 1: Harness engineering upstream + driver SDKs

> Source of Mode 3's design philosophy and the set of SDKs that could plug into it. A paradigm shift here directly affects the architectural-center claim (H4) and the multi-agent extension bet (H8).

**Entities to track**:

- **Conceptual mainline**: Mitchell Hashimoto ("My AI Adoption Journey", "Engineer the Harness"); Anthropic engineering blog ("Effective harnesses for long-running agents", "Harness design for long-running application development", Managed Agents); OpenAI ("Harness engineering: leveraging Codex", Symphony, "Unlocking the Codex harness", Agents SDK harness/sandbox decoupling); Cursor ("Scaling long-running autonomous coding", "Towards self-driving codebases", "Best practices for coding with agents"); HumanLayer ("Skill Issue: Harness Engineering for Coding Agents"); Martin Fowler ("Harness Engineering" memo); TheNewStack "harness is the product" coverage
- **Driver SDKs that could plug into Mode 3**: Smolagents (HuggingFace, ~1k LoC, code-as-action); Anthropic Claude Agent SDK + Claude Code CLI; OpenAI Agents SDK + Codex CLI; OpenHands (All-Hands-AI, stateless event-sourced); Aider; Goose (Block); LangGraph
- **Closest multi-agent precedent**: Cursor's recursive Planner / sub-Planner / Worker / Judge architecture (multi-coding-agent driving one codebase — informs multi-agent driving N robots)
- **Counter-evidence to watch**: any publication showing a single-agent harness systematically beats a multi-agent recursive design at long-horizon embodied tasks (counter-evidence to H8)

**Expected changes**:

- Managed Agents pricing/availability evolution at Anthropic, Symphony 2.x at OpenAI, similar managed offers from Cursor
- New entrants in the "agent SDK" category specifically aimed at robotics or simulated worlds (currently absent)
- Approval-pack / proof-pack vocabulary either consolidating or fragmenting across vendors
- Smolagents code-as-action vs JSON tool-call benchmarks in embodied settings (Q1 from 2026-04 checkpoint)

**Relevance to roboclaws**: H3, H4, H8 — three of the core assumptions live here. Any change to "harness/" semantics or Mode 3 driver ecology re-prioritizes the entire roadmap.

---

### Vector 2: OpenClaw / personal-agent ecosystem

> Mode 2 specifically rides OpenClaw Gateway. This vector tracks OpenClaw itself, the variants that could replace it, and the governance/security signals that affect its strategic weight.

**Entities to track**:

- **Core + kernel**: OpenClaw (openclaw/openclaw, Linux Foundation governance after 2026-Q1 transfer); pi-mono (OpenClaw kernel SDK, badlogic/pi-mono); OpenClaw releases
- **Python variants worth tracking** (potential Mode 2 alternatives or watchlist): Hermes Agent (NousResearch, `hermes claw migrate`); Nanobot (HKUDS); OpenHarness (HKUDS, 2026-04 new); AstrBot; CoPaw / QwenPaw (AgentScope/Alibaba)
- **Security/isolation variants**: ZeroClaw (Rust); IronClaw (NEAR AI, TEE); NanoClaw (qwibitai)
- **Persona tooling**: soul.md (aaronjmars)
- **Governance signals**: foundation transitions, CVE bulletins, trademark disputes, founder moves (Steinberger → OpenAI), Anthropic-OpenClaw relationship status

**Expected changes**:

- OpenClaw foundation governance maturity (or stall) in 2026
- Whether Hermes / Nanobot / OpenHarness coalesce into a coherent "post-OpenClaw Python line" or stay fragmented single-user agents
- Security event cadence (CVE-2026-25253 was a wake-up; expect more)
- Whether any variant adds the multi-session simulation orchestration that Mode 2 actually needs (currently none do)

**Relevance to roboclaws**: H4. If OpenClaw's governance becomes hostile to Mode 2's needs, or if a Python variant gains true gateway semantics, the four-mode coexistence claim changes shape. Cadence can be relaxed if no governance signals fire.

---

### Vector 3: Simulator substrate ecosystem

> roboclaws bets on AI2-THOR (current) + MolmoSpaces (next-gen for manipulation). A substrate-layer change directly affects both Phase 2 capacity and Phase 3 plans.

**Entities to track**:

- **Currently used**: AI2-THOR (allenai/ai2thor, including the multi-agent ProcTHOR limitations — issue #1169); MolmoSpaces (allenai/molmospaces, 2026-02 release, 230K+ scenes, 42M+ grasps, USD export); MuJoCo (DeepMind, latest); MolmoBot (zero-shot sim-to-real reference)
- **Watchlist (not investing yet)**: ManiSkill3 (HF team, GPU-parallel + PettingZoo multi-agent + room-scale); Habitat 3.0 + PARTNR (Meta, most mature multi-agent LLM evaluation benchmark); Isaac Sim + Isaac Lab (NVIDIA, note 2.x → 3.x restructuring); Genesis (pre-1.0, performance claims unverified); RoboCasa; mujoco_playground; mujoco-mjx; mujoco-warp; mjlab
- **Robot description tooling**: robot_descriptions.py (Stéphane Caron); URDF / MJCF / USD conversion paths
- **Counter-evidence**: any substrate that natively ships an "approval pack" or proof-bundle abstraction comparable to roboclaws's HTML report design (counter-evidence to H6)

**Expected changes**:

- MolmoSpaces multi-agent maturity (Q14 from 2026-04 checkpoint) — currently single-agent only
- Habitat 3.0 PARTNR baseline updates (multi-agent LLM eval reference)
- Isaac Lab 3.x landing and what it breaks
- Whether Genesis 1.0 ships and grows an ecosystem
- USD-as-portable-asset convention reaching across MolmoSpaces / Isaac / ManiSkill

**Relevance to roboclaws**: H2, H6. If MolmoSpaces multi-agent support arrives or fails to arrive, Phase 3 planning changes. If a substrate ships native proof-bundle semantics, H6's "static HTML reports are the right primary surface" needs revisiting.

---

### Vector 4: MCP protocol + agent skill standards + robotics MCP peers

> roboclaws's public capability surface is MCP. Protocol-layer changes affect every mode. Skill-format changes affect cross-driver portability.

**Entities to track**:

- **Protocol mainline**: MCP (Anthropic / Linux Foundation AAIF since 2025-12; 2026-03-09 roadmap covering transport scalability, agent communication, governance, enterprise-readiness); A2A; ACP variants (IBM REST, arXiv:2602.15055 federated discovery + zero-trust DID, commercial ACP/UCP)
- **Agent skill standards**: Anthropic Skills (agentskills.io, open standard published 2025-12-18, anthropics/skills); SKILL.md instances in robotics (roboclaws's own `skills/ai2thor-navigator/SKILL.md` and `skills/capture-object-photo/SKILL.md`); SOUL.md / MEMORY.md conventions; mitsuhiko/agent-stuff `skills/tmux/SKILL.md` as a reference tmux-skill
- **Robotics MCP peers**: isaacsim-mcp (whats2000); ros-mcp-server (robotmcp); mujoco-mcp (if it appears); whether LeRobot ships an official MCP server
- **Semantic profile peers**: any project shipping a similar "public canonical tool surface + privileged opt-in helpers + private evaluation truth excluded from metadata" pattern (roboclaws's `ai2thor_navigation_v1` / `molmospaces_cleanup_v1` / `real_robot_cleanup_v1`)
- **Counter-evidence to H3**: any per-framework custom interface that demonstrably outperforms MCP+SKILL.md on a robotics benchmark

**Expected changes**:

- MCP spec evolution post-AAIF transfer (next version is overdue as of 2026-05; spec was 2025-11-25)
- Whether a de facto "standard robotics MCP server" emerges
- Anthropic Skills uptake outside Anthropic's own products
- Whether semantic profiles get standardized as a pattern (currently only roboclaws does this explicitly)

**Relevance to roboclaws**: H3, H5. MCP and skill standards are the substrate H3 depends on; semantic profile pattern is H5's load-bearing structure. Both deserve every-period coverage.

---

### Vector 5: Multimodal model & VLM capabilities

> roboclaws routes work through multiple LLM/VLM providers. Visual-reasoning capability directly affects H1 (same-agent visual review); provider diversity affects H7 (multi-provider experimental design).

**Entities to track**:

- **Currently wired providers**: Claude (Anthropic, especially latest Sonnet/Opus vision capability and tool-use reliability); GPT / o-series (OpenAI, vision improvements); Gemini Pro (visual reasoning); Kimi (especially K2.x, integrated for smoke and live); MiMo (v2 Omni, v2.5 Pro currently in MolmoSpaces live reports); NVIDIA models; Mock provider
- **Other multimodal candidates to track**: Qwen-VL (Alibaba); Reka; xAI Grok vision; DeepSeek-V series; Yi-VL
- **Capability axes that matter for H1**: long-context image reasoning (handling N FPV + overhead + chase across a long episode); multi-image simultaneous reasoning; visual chain-of-thought; tool-call reliability under image load; cost-per-step for long-horizon runs
- **Academic VLM-as-judge line**: arXiv papers on "VLM judge", "visual evaluation", "image reasoning benchmark in robotics scenarios"
- **Counter-evidence to H1**: any benchmark showing same-agent visual review systematically underperforms an independent VLM judge on robotics tasks
- **Counter-evidence to H7**: provider-monogamy designs that demonstrably outperform multi-provider on the experimental questions roboclaws actually asks

**Expected changes**:

- Long-context image reasoning maturity (one model handling 10–20 images per turn at production cost)
- Robotics-specific visual reasoning benchmarks emerging
- Chinese provider (Kimi / MiMo / Qwen-VL / DeepSeek) capability convergence with frontier US providers on visual tool-use
- Vendor-specific harness pricing affecting which provider is economic for `harness/` long runs

**Relevance to roboclaws**: H1, H7. Mode 1 and Mode 3 both load this vector. If a model-generation jump materially changes the same-agent vs separate-judge gap, H1 needs updating.

---

### Vector 6: Multi-agent embodied AI + multi-agent harness research

> H8 is the riskiest bet on the card: "multiple coding-agents driving multiple robots is the right new territory with no public precedent." This vector tracks every precedent that could either validate or refute that bet.

**Entities to track**:

- **AI2-THOR multi-agent line**: TBONE (arXiv:1904.05879); MAP-THOR; Smart-LLM; GoalVLM
- **Multi-agent LLM evaluation benchmarks**: PARTNR (Meta + Habitat 3.0, arXiv:2411.00081, facebookresearch/partnr-planner — most mature multi-agent LLM eval baseline with privileged-world-model and no-privileged-world-model variants)
- **Generative agent / memory research**: Generative Agents (joonspk-research/generative_agents — memory stream + reflection design)
- **Multi-coding-agent precedent in code (not embodied)**: Cursor recursive Planner/Worker/Judge (architectural ancestor of multi-agent harness)
- **Watchlist (the gap that makes H8 risky)**: any paper, blog, or repo describing multiple coding-agents simultaneously driving multiple simulated robots; until something appears, H8's "no public precedent" remains true and roboclaws is at the frontier
- **Academic surveys**: LLM Agent survey (Preprints 2025); LLM-based Agentic Reasoning survey (arXiv:2508.17692)

**Expected changes**:

- A multi-coding-agent-multi-robot publication could appear any month (would invalidate the "first instance" framing in 2026-04 checkpoint §1)
- PARTNR baseline updates or successor benchmark
- Whether multi-agent harness emerges as a named subdiscipline of harness engineering or stays niche

**Relevance to roboclaws**: H8. Two consecutive checkpoints with no movement here would be evidence the "frontier position" framing is real and worth investing in.

---

### Vector 7: Real-robot bridge — Nav2, LeRobot, VLA, planner-proof stack

> The real-robot Nav2 cleanup pilot (currently on draft PR #112 per STATUS.md) extends the public/private evaluation contract from sim into hardware. This vector tracks the pieces that bridge across.

**Entities to track**:

- **Real-robot navigation stack**: Nav2 (ROS 2 navigation); ROS 2 (Jazzy, Kilted); CycloneDDS; Nav2-shaped map bundles as a portable artifact format
- **Manipulation planner-proof**: RBY1M (current planner-probe target); CuRobo (NVIDIA, motion generation); MimicGen-derived checkpoints; grasp-cache validity tooling
- **Data format standards**: LeRobotDataset (v3.0+, watch for schema changes); Open X-Embodiment; Bridge-V2; Droid
- **VLA candidates for future Phase** (selection deliberately postponed in 2026-04 checkpoint until substrate settles, tracked at survey level): GR00T N1.7 / N2 + GR00T-WholeBodyControl (NVIDIA, G1-aligned); π₀ / π₀.₅ / π₁ (Physical Intelligence, openpi); WholeBodyVLA (ICLR 2026, +21.3% over GR00T baseline); MEM (Physical Intelligence 2026-03, 15-min kitchen tasks); ICLR 2026 architecture wave (Cosmos Policy, dVLA, DIVA, FASTer, OmniSAT, XR-1, FLOWER)
- **Sibling project (own ecosystem)**: MiaoDX/robowbc (whole-body-control runtime — potential consumer of cleanup proof bundles for humanoid integration); MiaoDX/roboharness (visual harness for coding-agent on its own code — shared review philosophy)
- **Counter-evidence to H5**: any project that exposes raw ground truth to public agent-facing metadata and still produces clean evaluation (would refute the "private separation is necessary" stance)

**Expected changes**:

- Nav2 cleanup pilot promotion from draft PR #112 to merged + repeatable (near-term within 1–2 checkpoints)
- VLA selection unblocking once substrate decision settles (2026-04 checkpoint deferred this)
- LeRobotDataset breaking changes (LeRobot ships fast; schema-level changes affect rollout archive design)
- RBY1M / CuRobo licensing or maintenance signals

**Relevance to roboclaws**: H5, H8. The real-robot path is where evaluation-truth separation either holds up or collapses under hardware noise. It is also the second instance of "multi-agent + harness" if Nav2 pilot generalizes.

---

## Sources

### Whitelist (A-tier, cite directly)

- **Official primary**: anthropic.com/engineering; anthropic.com/news; openai.com/index; cursor.com/blog; deepmind.google/blog; allenai.org/blog (especially MolmoSpaces, MolmoBot); nvidia.com/blog (robotics, GEAR, Isaac); huggingface.co/blog (LeRobot, Smolagents); physicalintelligence.company/blog; agentskills.io
- **Project repos (primary)**: GitHub MiaoDX/roboclaws itself; allenai/ai2thor; allenai/molmospaces; openclaw/openclaw; badlogic/pi-mono; huggingface/smolagents; openai/symphony; openai/openai-agents-python; openai/codex; All-Hands-AI/OpenHands; anthropics/skills; NVIDIA/Isaac-GR00T; Physical-Intelligence/openpi; huggingface/lerobot; facebookresearch/partnr-planner; mitsuhiko/agent-stuff; joonspk-research/generative_agents; MiaoDX/roboharness; MiaoDX/robowbc
- **Maintainer blogs**: mitchellh.com; Martin Fowler ("Exploring Gen AI"); Pete Warden; Anthropic engineering blog (independent subdomain); Simon Willison's blog (for harness-adjacent commentary)
- **Academic**: arXiv (cs.RO, cs.AI, cs.LG, cs.MA); priority subscribe keywords "embodied multi-agent LLM", "VLA", "agent harness", "VLM judge", "MCP robotics", "agent skill", "household cleanup benchmark"
- **Conferences**: CoRL, ICRA, IROS, RSS (robotics); NeurIPS, ICLR, ICML (academic AI); ICSE, FSE (software engineering, source of approval-testing concepts)

### Grey list (B-tier, requires cross-verification)

- TheNewStack, InfoQ, IEEE Spectrum, The Robot Report, ZDNet, VentureBeat, 量子位, 机器之心, 智东西, 极客公园
- HackerNews; Reddit r/MachineLearning, r/robotics; Zhihu highly-upvoted answers with citations
- Substacks: Last Week in AI; Import AI; Two Cents on Embodied AI

### Blacklist (D-tier, actively ignore)

- "Best agent framework of 2026" / "Top OpenClaw alternatives" SEO buying guides (vellum.ai, qubittool.com, composio.dev, scriptbyai.com, aimagicx.com, skywork.ai, and similar)
- Marketing-flavored medium/dev.to posts without primary-source citations
- AI-generated awesome-agents / awesome-MCP / awesome-claw GitHub lists (use only as discovery surfaces, never as citation sources)
- Star-count-based ranking content without GitHub API verification (the 2026-04 checkpoint flagged this as Q13)

---

## Cadence

- **Routine checkpoint**: monthly, in the last week of the month. A single deep-research session covers all 7 vectors. Vectors 1, 3, 5, 6 must be written every period (they carry the highest-stakes assumptions). Vectors 2, 4, 7 may be marked "no significant change" rather than padded.
- **Card self-audit**: quarterly (after every 3 checkpoints), audit this VECTORS file itself — is the entity list stale? do the hidden assumptions need to be added to or pruned? has Phase 3 changed shape since the last audit?

---

## Triggers for off-schedule research (do not wait for the next cycle)

Any one of these triggers an ad-hoc deep research pass:

- **Multi-agent-multi-robot precedent appears**: any paper, blog, or repo demonstrating multiple coding-agents simultaneously driving multiple simulated robots (affects H8 directly — currently "no public precedent" is the load-bearing claim)
- **Model-generation jump with vision impact**: a flagship multimodal model (Claude Opus 5, GPT-6, Gemini 3, Kimi K3, MiMo v3) ships with materially improved visual reasoning or long-context image capability (affects H1, H7)
- **MolmoSpaces multi-agent support landing or failing**: Allen AI ships (or publicly commits to) multi-agent in MolmoSpaces, or publishes a position against it (affects H2 and Phase 3 planning)
- **Substrate major event**: Isaac Lab 3.x lands; Genesis 1.0 ships; Habitat 4 / PARTNR-2 announced; mujoco-warp becomes default GPU path (affects H2, H6)
- **MCP / Skill standard major version**: MCP spec next-version published; A2A or ACP gains material adoption; Anthropic Skills extended into robotics scenarios (affects H3, H5)
- **OpenClaw governance shift**: foundation announces a direction change; CVE of CVE-2026-25253 severity hits an unpatched window; a Python variant gains genuine multi-session gateway semantics (affects H4)
- **Counter-evidence to H1**: a robotics benchmark shows separate-VLM-judge significantly outperforms same-agent visual review (affects H1)
- **Real-robot signal**: the Nav2 cleanup pilot (draft PR #112) merges or stalls; an upstream Nav2 / ROS 2 release breaks the bundle format; RBY1M / CuRobo licensing event (affects H5, H8 and the §STATUS.md "current focus" framing)
- **Peer / upstream change**: Anthropic, OpenAI, or Cursor ships a major harness-engineering release (Managed Agents 2.x, Symphony 2.0, Cursor multi-agent GA); Smolagents publishes a robotics benchmark (affects H3, H4, H8)
- **Key-dependency event**: AI2-THOR, MolmoSpaces, MuJoCo, LeRobot, RBY1M SDK, or CuRobo undergoes license change, end of maintenance, or serious security event

---

## Status

- 2026-05-22: first written. Material drawn from `roboclaws/docs/research-checkpoints/2026-04.md` (1221 lines, v1+v2 published 2026-04-28/29), `roboclaws/README.md`, `roboclaws/ARCHITECTURE.md`, and `roboclaws/STATUS.md` (2026-05-19, real-robot Nav2 cleanup pilot on draft PR #112).
- 2026-05-22 (post-write correction): two factual fixes against the first-written version. (a) Anthropic Skills open-standard publication date corrected from 2026-03-14 to 2025-12-18 (verified against TheNewStack 2025-12-18 coverage and Anthropic's anthropics/skills GitHub timeline). (b) Project-positioning abstraction ladder restored to the canonical 6-layer form from `roboclaws/README.md` and `roboclaws/ARCHITECTURE.md` (`goal → skill → composite action → semantic capability → environment primitive → execution backend`); the first-written 5-layer version conflated `composite action` with `semantic capability` and `environment primitive` with `execution backend`, and treated the HTML report as a layer rather than as a proof artifact derived from execution.
- This card formalizes a vectors structure for a repo that already produced one large ad-hoc checkpoint. The first checkpoint written *under* this card (2026-05) should verify: (1) all 7 vectors produce useful, distinct output; (2) the 8 hidden assumptions each actually get challenged; (3) the 2026-04 → 2026-05 delta is visible across OpenClaw governance, MolmoSpaces multi-agent, Nav2 pilot status, and multi-agent-multi-robot precedent.
- If two consecutive checkpoints leave all assumptions unchallenged, the vectors design has blind spots and needs revision. Entity lists are seeded from the 2026-04 checkpoint's Appendix A.1–A.12 plus current architecture state; the first monthly checkpoint should surface and add entities missed at card-writing time.
