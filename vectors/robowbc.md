# robowbc Research Vectors

> Layer 2 card: defines what `MiaoDX/robowbc` must track, which sources to use, and on what cadence.
> Used together with [`mithaq/templates/checkpoint.md`](../templates/checkpoint.md).
>
> **First written:** 2026-05-21
> **Next self-audit:** 2026-08-21 (the card itself is audited quarterly — vectors cards also go stale)

## Current project positioning (one sentence)

> "Linux-first embedded runtime for humanoid whole-body-control policy inference: one caller-facing contract, multiple policy backends."
>
> Core wedge: `Observation → WbcPolicy.predict → JointPositionTargets`, with TOML-config-driven backend selection.
> Primary stack: Rust core + PyO3 + ONNX Runtime, MuJoCo for hardware-free execution, CycloneDDS / in-memory transport, Rerun for visualization, Unitree G1 as the integration target.
> Project-specific vocabulary and policy status table: see [`robowbc/ARCHITECTURE.md`](https://github.com/MiaoDX/robowbc/blob/main/ARCHITECTURE.md) and [`robowbc/README.md`](https://github.com/MiaoDX/robowbc/blob/main/README.md).

## Hidden assumptions (the vectors exist to detect when these stop holding)

The following are bets the project's current architecture is making **without writing them down explicitly**. If a deep-research pass produces evidence that the support for any of these is weakening, immediately log it as an item in §7 Open Questions of the corresponding checkpoint.

| # | Hidden assumption | Vector that challenges it |
|---|------------------|--------------------------|
| H1 | The `Observation → predict → JointPositionTargets` contract is the right abstraction across all WBC policy families; one contract really can cover gear_sonic / decoupled / wbc_agile / bfm_zero / future families | Vector 1 (WBC policy upstream); Vector 6 (interface peers) |
| H2 | Rust core + PyO3 + ONNX Runtime is the right runtime stack; pure-Python, native-PyTorch-only, or TensorRT-only are not | Vector 2 (inference backends) |
| H3 | Linux-first with fail-fast on unsupported platforms is the right deployment posture; cross-platform with partial fallbacks is not | Vector 3 (hardware SDK ecosystem) |
| H4 | Joint position targets as the policy output boundary is the right safety stance; direct torque output is not | Vector 1 (policy upstream); Vector 3 (hardware control interfaces) |
| H5 | Multiple WBC policy families should coexist under one registry; picking one family and going deep is not the answer | Vector 1 (policy upstream) |
| H6 | A static reports site (HTML policy cards + proof packs + NVIDIA benchmark page) is the right primary proof surface; interactive dashboards and on-platform leaderboards are not the priority | Vector 5 (sim substrate for proof) |
| H7 | Unitree G1 + unitree_sdk2 + CycloneDDS is the right hardware integration target; ROS 2 native customer API is correctly in the parking lot | Vector 3 (hardware); Vector 4 (middleware) |
| H8 | LeRobot is the right Python-first distribution channel; standalone packaging or framework-of-its-own is not | Vector 6 (distribution + standards) |

Every checkpoint must answer: did this period produce evidence that any of the above assumptions needs to be reconsidered?

---

## Research vectors

### Vector 1: Humanoid WBC policy upstream

> The set of "things being wrapped." New policy families directly drive new wrapper work and may stress-test H1 (one-contract abstraction) and H4 (joint-position output).

**Entities to track**:

- **Currently wrapped (live)**: GEAR-SONIC (NVIDIA GEAR); DECOUPLED-WBC; WBC-AGILE; BFM-Zero
- **Currently wrapped (blocked / experimental)**: HOVER (CMU); WholeBodyVLA; user-supplied via `py_model` / PyO3
- **NVIDIA line**: GR00T N1.7 / N2 (and any successor); GR00T-WholeBodyControl; SONIC successors; Cosmos Policy / Cosmos Reason; MimicGen-derived WBC checkpoints
- **Academic / open humanoid policy line**: HumanPlus (Stanford); OmniH2O / H2O; ExBody / ExBody2 (Tsinghua/UCSD line); ASAP; OKAMI; AgileGR; unitree_rl_gym first-party checkpoints
- **Physical Intelligence**: π₀ / π₀.₅ / π₁ (currently single-arm manipulation; watch for whole-body extensions); openpi releases
- **Closed but observable**: Figure Helix; Apptronik Apollo policy line; Tesla Optimus
- **Counter-evidence to H1**: any policy family that fundamentally does not fit `Observation → predict → JointPositionTargets` (e.g., direct torque-out policies, hierarchical multi-step prediction interfaces, model-predictive policies that expect to own the transport loop)

**Expected changes**:

- New open-source humanoid whole-body VLAs continue arriving (likely quarterly through 2026)
- Increasing pressure on the joint-position-target convention as agile / contact-rich policies appear
- Possible appearance of a "competing one-contract runtime" from NVIDIA, HuggingFace, or a Chinese humanoid vendor

**Relevance to robowbc**: H1, H4, H5 — this vector carries the central architectural bets. A new policy family that doesn't fit is the most consequential event for the project.

---

### Vector 2: Robot ML inference runtime stack

> robowbc bets on Rust + PyO3 + ONNX Runtime. Movement in the inference-runtime layer directly affects H2 and the project's deployment-cost story.

**Entities to track**:

- **Current core dependency**: onnxruntime (releases, CUDA EP, TensorRT EP, CPU performance work); `ort-rs` (Rust bindings used by `robowbc-ort`)
- **NVIDIA inference stack**: TensorRT (versions, humanoid-relevant op coverage); Triton Inference Server
- **Cross-vendor alternatives**: PyTorch ExecuTorch (mobile-first, expanding to edge); Apple MLX; Intel OpenVINO; Alibaba MNN; Tencent ncnn
- **Rust ML ecosystem (could substitute or complement ort-rs)**: candle (HuggingFace); burn; tract (Sonos); wonnx; dfdx
- **Graph compiler line**: torch.compile; OpenAI Triton; MLIR / IREE; Apache TVM; JAX/XLA
- **Compute fabric**: CUDA (versions); ROCm; Metal; Vulkan / wgpu (for cross-vendor inference)

**Expected changes**:

- ExecuTorch reaching production maturity for robotics workloads
- Rust ML inference libraries either consolidating or remaining niche
- Possible release of a humanoid-tuned inference engine from NVIDIA / a Chinese vendor

**Relevance to robowbc**: H2. If ONNX Runtime perf stalls or ExecuTorch passes it for robotics workloads, the primary backend choice needs reconsidering. If Rust ML libs mature, `robowbc-ort` could expand to multiple Rust backends.

---

### Vector 3: Humanoid hardware + SDK ecosystem

> robowbc integrates with Unitree G1 today. Hardware platform maturity (Linux SDK, documented joint specs, deterministic transport) is the constraint on which platforms become viable integration targets.

**Entities to track**:

- **Unitree (current target)**: G1 (firmware revisions, unitree_sdk2 releases); H1; H2 (new); unitree_mujoco; unitree_rl_gym
- **Chinese humanoid wave**: AgiBot (智元) G2 and successors; Booster T1; Fourier GR-series; XPeng IRON; EngineAI; UBTECH (优必选) Walker series; Galbot; Robotera
- **US humanoid wave**: Figure 02 / 03 (closed-source); Boston Dynamics Atlas (commercialization, SDK status); Apptronik Apollo; 1X NEO; Sanctuary Phoenix; Tesla Optimus
- **Research humanoids**: HumanPlus body (Stanford); HRP series; smaller bipeds (Cassie, Digit from Agility)

**SDK quality criteria worth scoring per platform**:

- Linux supported
- Documented joint topology + URDF/MJCF
- Deterministic transport (DDS or equivalent)
- Sim parity to a public substrate (MuJoCo / Isaac)

**Expected changes**:

- More Chinese humanoids ship usable Linux SDKs through 2026
- One or two US humanoid vendors may open a customer API
- AgiBot / Booster / Fourier potentially becoming serious alternatives to G1 for the integration story

**Relevance to robowbc**: H3, H7. A second-platform integration target with mature SDK is the most realistic challenger to the G1-only story. If a major platform ships ROS 2 native as its only customer API, H7 needs revisiting.

---

### Vector 4: Robot middleware (DDS / ROS 2 / alternatives)

> Transport is where policy output meets the robot. robowbc bets on CycloneDDS / in-memory and explicitly parks ROS 2 native customer API. Middleware-layer shifts directly affect H7.

**Entities to track**:

- **DDS implementations**: CycloneDDS (current choice); Fast DDS; Connext DDS; OpenDDS
- **Eclipse Zenoh**: zenoh-rs; ROS 2 zenoh-bridge; zenoh-pico (embedded)
- **ROS 2 releases**: humble (LTS), iron, jazzy, kilted; ros2_control; rosbag2
- **Visualization / observability transports**: rerun-io (current); Foxglove Studio; PlotJuggler
- **Non-DDS alternatives in robotics**: NATS; MQTT; raw gRPC

**Expected changes**:

- Zenoh adoption trajectory in 2026 (ROS 2 default bridge maturity, embedded uptake)
- Whether ROS 2 Jazzy / Kilted reduces the friction that motivated robowbc's parking-lot stance
- Unitree's transport choices in newer SDK versions

**Relevance to robowbc**: H7. If a future Unitree SDK drops CycloneDDS or if ROS 2 native becomes the unavoidable customer expectation, the parking-lot decision needs reconsidering.

---

### Vector 5: Sim substrate for inference proof artifacts

> robowbc's primary proof surface is the static reports site driven by MuJoCo-based sim runs. Substrate-layer shifts affect what proof artifacts can be produced and how cheaply.

**Entities to track**:

- **MuJoCo line**: MuJoCo (DeepMind/Google, latest releases); mujoco-mjx (JAX); mujoco_playground; mujoco-warp; mjlab; mujoco_menagerie
- **NVIDIA sim**: Isaac Sim; Isaac Lab (note 2.x → 3.x restructuring); Cosmos
- **Newcomers / challengers**: Genesis (Genesis-Embodied-AI, claimed perf advantages); MolmoSpaces (Allen AI, 2026-02 release); ManiSkill3 (HF team); Habitat 3.0 (Meta); RoboCasa
- **Robot description tooling**: robot_descriptions.py (Stéphane Caron); unitree_ros; URDF / MJCF tooling chain

**Expected changes**:

- mujoco-mjx and mujoco-warp expanding usable GPU paths for humanoid scenarios
- Isaac Lab 3.x landing and what it breaks in existing integrations
- Genesis 1.0 release and whether an actual ecosystem coalesces
- Whether sim2real for humanoid converges around one substrate or stays fragmented

**Relevance to robowbc**: H6. The proof-pack credibility scales with substrate fidelity; a major substrate event (new GPU MuJoCo path, Isaac Lab 3.x reset) is worth a focused checkpoint section.

---

### Vector 6: Python-first robotics distribution + policy interface peers

> robowbc bets on LeRobot as the primary user surface (roadmap item #41). This vector tracks both LeRobot's evolution and any peer effort that might constitute a competing "one-contract" runtime.

**Entities to track**:

- **Primary distribution channel**: LeRobot (HuggingFace) — releases, policy schema evolution, adapter-relevant breaking changes
- **Peer Python robotics frameworks**: gymnasium; robosuite; ManiSkill3 baselines API; mujoco_playground policy interface; Isaac Lab Python API
- **Standards / interface peers (the H1 competition watch)**: any project shipping a similar `Policy.predict(obs) → targets` abstraction at framework or community-standard scope — to watch: LeRobot's `Policy` API; NVIDIA Cosmos Policy interface; OpenVLA reference interface; ROS 2 humanoid control interface proposals
- **RL ecosystem (interface, not delivery)**: Stable Baselines 3; CleanRL; SKRL; SKRL-style training-side patterns that may dictate observation/action shapes

**Expected changes**:

- LeRobot policy schema changes that may break or require adapter updates for `robowbc-py`
- Possible appearance of a "WbcPolicy"-equivalent open standard from LeRobot, NVIDIA, or the ROS 2 control community
- New entrants competing for Python-first robotics mindshare

**Relevance to robowbc**: H1 (competing interface watch), H8 (distribution-channel bet).

---

## Sources

### Whitelist (A-tier, cite directly)

- **Official primary**: nvidia.com/blog (robotics, GEAR, Isaac); physicalintelligence.company/blog; deepmind.google/blog; anthropic.com/news (for inference-relevant items); huggingface.co/blog (LeRobot); allenai.org/blog; figure.ai; bostondynamics.com/news
- **Project repos (primary)**: GitHub MiaoDX/robowbc itself; google-deepmind/mujoco; google-deepmind/mujoco_playground; NVIDIA/Isaac-GR00T; Physical-Intelligence/openpi; huggingface/lerobot; unitreerobotics/unitree_sdk2; unitreerobotics/unitree_rl_gym; Genesis-Embodied-AI/Genesis; isaac-sim/IsaacLab; pykeio/ort (ort-rs); microsoft/onnxruntime; pytorch/executorch; ml-explore/mlx
- **Academic**: arXiv (cs.RO, cs.LG, cs.AI); priority subscribe keywords "humanoid", "whole-body control", "WBC", "loco-manipulation", "VLA humanoid", "policy distillation humanoid"
- **Conferences**: Humanoids, ICRA, IROS, RSS, CoRL (robotics); NeurIPS, ICLR, ICML (academic AI); ICRA Humanoid Workshop, RSS Humanoid Workshop when relevant
- **Vendor SDK docs**: support.unitree.com; Unitree GitHub release notes; AgiBot, Booster, Fourier official docs as they appear

### Grey list (B-tier, requires cross-verification)

- IEEE Spectrum, The Robot Report, IEEE Robotics & Automation Magazine, ZDNet robotics coverage
- 量子位, 机器之心, 智东西, 极客公园 — especially humanoid product launch coverage
- HackerNews, Reddit r/robotics, r/MachineLearning; Zhihu highly-upvoted technical answers with citations
- Substacks: Two Cents on Embodied AI; Last Week in AI (robotics segments); Import AI (robotics weeks)

### Blacklist (D-tier, actively ignore)

- "Top N humanoid robots of 2026" SEO buying guides
- Investment-pitch-style writeups from undisclosed humanoid startups without published technical content
- Tech Insider / Business Insider humanoid clickbait
- AI-generated awesome-humanoid / awesome-WBC GitHub lists (use only as discovery surfaces, never as citation)
- Marketing-flavored medium/dev.to posts without primary-source citations

---

## Cadence

- **Routine checkpoint**: monthly, in the last week of the month.
- **Coverage policy**: fixed tracking surface, flexible expansion depth.
  - **Core vectors**: Vectors 1 and 2 receive a full update every routine checkpoint.
  - **Watch vectors**: Vectors 3-6 receive a light check every routine checkpoint and may be marked "no significant change" rather than padded if no material evidence appeared.
  - **Tracking-surface changes**: vector count, classification, and scope change only during card self-audit or an explicit card update, not ad hoc inside an ordinary checkpoint.
- **Card self-audit**: quarterly (after every 3 checkpoints), audit this vectors file itself — is the entity list stale? do the hidden assumptions need to be added to or pruned? has any platform / policy family / runtime been wrapped or wholly removed since last audit?

---

## Triggers for off-schedule research (do not wait for the next cycle)

Any one of these triggers an ad-hoc deep research pass:

- **New WBC policy family released**: a new open-source humanoid whole-body VLA or learned WBC checkpoint becomes available (affects H1, H5; potentially Vector 1 expansion)
- **Counter-evidence to H1 surfaces**: a credible new policy family that fundamentally does not fit `Observation → predict → JointPositionTargets`, or someone publishes a structured comparison showing direct-torque output dominates joint-target output for humanoid agility tasks (affects H1, H4)
- **Competing one-contract runtime appears**: NVIDIA, HuggingFace, ROS 2 humanoid control WG, or a Chinese humanoid vendor ships a `WbcPolicy`-equivalent open abstraction at framework scope (affects H1, H8)
- **Inference-backend major release**: ONNX Runtime, TensorRT, ExecuTorch, or candle/burn ship a release with material humanoid-workload performance change (affects H2)
- **Humanoid SDK major event**: AgiBot / Booster / Fourier / Figure / Apptronik / 1X opens or significantly upgrades a Linux SDK; or Unitree changes the SDK/transport story (affects H3, H7)
- **Middleware shift**: zenoh becomes the ROS 2 default bridge officially, or a major humanoid vendor commits to ROS 2 native as the only customer API (affects H7)
- **Substrate major change**: Isaac Lab 3.x lands; Genesis 1.0 ships; mujoco-warp becomes the default GPU path (affects H6)
- **LeRobot breaking change**: LeRobot ships a policy-schema-level breaking change that affects the `robowbc-py` adapter shape (affects H8)
- **Key-dependency event**: MuJoCo, onnxruntime, ort-rs, unitree_sdk2, Pinocchio, or Rerun undergoes license change, end of maintenance, or serious security event

---

## Status

- 2026-05-21: first written, immediately after roboharness.md. **No checkpoints have been run yet** — this card's usability has not been validated.
- When running the first checkpoint, verify two things: (1) all 6 vectors produce useful, distinct output (no two vectors collapsing into the same content); (2) the hidden assumptions actually get challenged — if two consecutive checkpoints leave all assumptions unchallenged, the vectors design has blind spots and needs revision.
- Entity lists in §Research vectors are seeded from current MiaoDX ecosystem knowledge as of writing; the first monthly checkpoint should surface and add entities that were missed at card-writing time.
