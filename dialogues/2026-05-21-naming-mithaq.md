> **Language**: Current · [中文（原始对话语言）](./2026-05-21-naming-mithaq.zh.md)

# The conversation that named this repo — why Mithaq

> **Editor's note**
>
> This is the **genesis archive** of the `mithaq` repository. The original was a single long session with Claude Opus 4.7 (2026-05-21), conducted in Chinese, around one concrete question: can the periodic deep-research mechanism in `roboclaws` be abstracted into a cross-repo template, and if so, the meta-repo that holds the abstraction needs a name — what should it be?
>
> This file is an **edited version** — preserving the decision turns and key quotes, dropping the per-candidate detail (which exists in two deep-research artifacts). The original session ran about 30 round-trips; what is shown here is the skeleton.
>
> This is the first entry in `dialogues/` because it is itself the conversation that defines what `dialogues/` should contain — all three inclusion criteria are met.

## Metadata

- **Date**: 2026-05-21
- **Model**: Claude Opus 4.7 (with Anthropic deep research, two invocations)
- **Original language**: Chinese (a faithful Chinese version is preserved at `2026-05-21-naming-mithaq.zh.md`)
- **Triggering question**: can the periodic deep-research mechanism in `roboclaws` be abstracted into a cross-repo template
- **Affected repos**: mithaq (itself); indirectly all future MiaoDX repos via the Layer 1 template and Layer 2 vectors cards
- **Status**: landed — `mithaq` repository created, first commits pushed

## Key conclusions

1. **The name landed on `Mithaq`** (Arabic, *مِيثَاق*, "solemn covenant"). Reasons: precise hit on the *covenant* character of "important long conversations with top models"; the namespace is clean across GitHub, AI startups, and crypto tokens; deep cultural excavation potential (Quran 7:172, *Mithaq al-Alast*, the distinction from `'ahd`, Sufi interpretations).

2. **`Earthseed`** (Octavia Butler) is the strongest runner-up; reserved as a possible name for a future English-facing sister repo. **`Primer`** (Neal Stephenson, *The Diamond Age*) had the most precise functional fit but `github.com/primer` is GitHub's own design system — the discovery that the perfect name is unusable is itself worth recording.

3. **The Layer 1 / Layer 2 / Layer 3 three-tier separation** is the core structural product of this conversation:
   - **Layer 1**: a universal checkpoint meta-template (structure + methodology), reusable across repos, lives in mithaq.
   - **Layer 2**: per-repo research-direction cards (which entities to track, source whitelist/blacklist, cadence), one per repo, lives in mithaq.
   - **Layer 3**: the actual periodic checkpoint for a specific month, lives in each repo's own `docs/research-checkpoints/`.
   The instinct "write one set of generic prompts and any repo can run them" **is wrong** — it produces answers to no-content placeholders across the board.

4. **Confirmation is also a research outcome.** Two rounds of deep research (the first across language/religious traditions, the second focused on science fiction) both pointed to Mithaq. The second round did not change the conclusion, but **established the robustness of the choice** — having seriously compared Primer / VALIS / Wallfacer / Earthseed / Fuligin / Ekumen and most alternatives has independent value.

## Abstractable structures

This conversation surfaced several methods that apply beyond naming:

### 1. Three-tier abstraction: universal meta-structure / per-instance card / concrete instance

Not unique to naming. Any situation where "I want to abstract one project's successful mechanism for use by other projects" hits the same layering problem. Taking the full set of practices from a successful project and treating them as a universal template fails, because:

- What looks like a "process" is, at a deeper level, an "entity list + cadence + source judgment" — the latter has to be per-instance.
- The cost of forced universalization is that **every user has to translate** — and that translation step is what the per-instance card should be doing. It cannot be skipped.

**How to decide which layer something belongs to**: ask "if I swapped to a different project, would the specific content change a lot?" If yes, it belongs in Layer 2.

### 2. "Excavation depth" as a name-evaluation criterion

Short-term, a name is judged on memorability. Long-term, it is judged on whether it can sustain repeated use without becoming hollow. To assess excavation depth:

- How many layers can be drawn out? (literal / mythic / mathematical / literary / modern resonance)
- Is each layer self-contained? (i.e., when discussing one layer with the reader, can it stand alone without unpacking the others)
- Three years from now, will there still be new material to mine?

Memex dug all the way down lands on Bush 1945 — and that's the bottom. Mithaq can be excavated at least four or five times without repetition (Quran 7:172 / al-Alast / the `'ahd`-`mithaq` distinction / Sufi internalization / comparison with the Sinai covenant / contractarian framings in modern AI alignment discussion…).

### 3. "What has already been claimed by AI" as a measure of ecosystem density

Running a naming search in May 2026, the most striking finding was not "which names are available" but **which names have already been claimed**:

- Primer → GitHub itself (the design system) + Primer.ai (defense AI)
- VALIS → VALIS Systems (an "AI output verification layer" startup)
- Wallfacer / 面壁 → ModelBest / 面壁智能 (MiniCPM's maintainer) + wallfacer.ai
- Sophon / 智子 → Sophon Network L2 (Binance Labs backed, $70M+)
- Musubi → Musubi Labs (VC-backed AI content moderation)
- Telos → Daniel Miessler's LLM context framework, plus several other AI products
- Sutra → TWO AI's multilingual LLM

This is, in itself, **a 2026 snapshot of the Chinese-and-English AI naming space being consumed**. The list has independent archival value — it tells future readers: "this year, every beautiful sci-fi or mythological word got mined out."

### 4. When deep research produces an uncertain answer, run a focused follow-up round

The first deep-research round handled science fiction shallowly (covering only six or seven Le Guin / Asimov / Lem concepts). The user noticed. The second round was scoped narrowly to SF and produced 28 candidates, the discovery being that **the perfect candidates were almost all already claimed by AI companies** — which *strengthened* confidence in Mithaq, something the first round could not have produced alone.

Lesson: when the first deep-research round leaves you uncertain, **do not concede on the conclusion** — open a focused supplementary round. The cost of focus is far lower than the cost of a wrong decision.

## Excerpted dialogue

> Quotes from the user are translated from Chinese; direct Chinese versions are in the `.zh.md` sibling.

### Starting point: abstract roboclaws' mechanism into a universal template?

The user described `roboclaws/docs/research-checkpoints/2026-04.md` — a 1221-line monthly ecosystem snapshot with a detailed update procedure, a four-tier source quality system, and triggers for off-schedule research — and asked whether it could be abstracted into a set of prompts reusable across all repos.

My first response was to push back:

> Building "a single set of universal prompts" runs three risks:
>
> 1. Universalized research directions become "asking the air." Rewriting "OpenClaw strict-family increments" as "project core-dependency increments" makes the prompt universal but the deep-research agent will turn around and ask "what are your core dependencies, specifically?" — which is asking nothing.
>
> 2. The "adjacent perspectives" for each repo are structurally different, not superficially so. roboharness's adjacent perspectives are MuJoCo / Isaac Lab / LeRobot; verse-driven's are Claude Code Skills ecosystem / classical-text digitization; LIP's are site generators / PKM tools — these differences cannot be folded into a single set of prompts.
>
> 3. "Monthly" is too heavy for small projects. A docfit-class tool might have only one notable change every two or three months. Forcing a monthly cadence produces empty ceremony.

I proposed the three-layer scheme: Layer 1 universal meta-template / Layer 2 per-repo vectors cards / Layer 3 the actual monthly checkpoint.

The user said "Hm, the suggestion doesn't seem to have major issues." Then turned to an unexpected question — **what should this meta-repo be called**.

### First batch of candidates: covenant / long-term dependency

The user framed the question with a specific angle:

> Basically every suggestion I take comes from talking with you — Claude or GPT. Maybe the name should contain that — our compact, our long-term relationship of mutual dependence.

That raised the naming question from "name a meta-repo" to "name a relationship."

I offered candidates across several frames:

- Covenant / long-term dependency: **compact**, accord, covenant, pact
- Long-term memory / archive: **ledger**, codex, atlas
- Continuing the harness metaphor: yoke, reins, tether
- Aligned with MiaoDX naming style: coharness, **LLMpact**, handshake

I recommended **compact** — the "compactness + covenant" pun, fitting the existing MiaoDX naming rhythm.

### Pivot: sci-fi, religion, Daodejing

The user: "Find some terms from sci-fi movies, or the Bible, or the Quran, or Daoist classics, or the Daodejing."

This was the key widening. I offered a batch:

- Sci-fi: **Ansible** (Le Guin), Sophon (Three-Body), **Memex** (Bush), Mentat (Dune)
- Bible / Quran: **Logos**, Aleph, Ark
- Daodejing: 朴 (Pu), 玄 (Xuan)

Recommended Logos first — it is **simultaneously** the Christian "Word", the Greek "logos" of philosophy, and the standard Chinese translation of "道" in the Daodejing — one word spanning three traditions. But too common in tech use.

### Narrowing to memex / aleph

User: "memex / aleph — say more about these two words."

This round I did a deep comparison of the two:

- **Memex**: Bush 1945, *As We May Think*. Memory extender, external memory + associative trails — the conceptual ancestor of hypertext and the web.
- **Aleph**: a three-layer compound — Hebrew letter א (infinite source) + Cantor ℵ (the symbol for ordering levels of infinite sets) + Borges 1945, *El Aleph* (a point two or three centimeters across through which one can see everything in the universe).

I recommended Aleph: **the metaphor is more precise** (Memex corresponds to the checkpoint mechanism itself; Aleph corresponds to the Layer 1 → Layer 2 → Layer 3 layered abstraction itself); **the excavation density is deeper** (Memex bottoms out at Bush's paper; Aleph can be excavated three times without repetition); **continuity with verse-driven** (the line of "putting computers in contact with humanistic density").

### Widening again: deep research opens

User: "Now that we've mentioned Hebrew — what about other languages? I'd like to widen the search. I'm enabling deep research. Take a look from different angles. This name feels really important."

And a clarification:

> This is a Meta Repo that records the most important conversations I have with these top models, and uses them to guide all my projects.

That sentence shifted the naming center of gravity from "container for a meta-template" to "archive of long-running conversations + direction-setter for projects." Two threads stacked: **covenant relationship** + **long-conversation archive** + **direction for future projects**.

The first deep-research round covered Hebrew, Arabic, Sanskrit, classical Greek, Latin, classical Chinese, Japanese, Old Norse, Egyptian, Sumerian, and more. The results were unexpected:

- **Aleph is not as clean as it looks**: `Aleph-Alpha` (the German 30-repo sovereign AI company, with an explicit LLM Intelligence Layer SDK) + `Aleph Zero` (the privacy L1 blockchain) have split the namespace.
- **Several seemingly perfect names were already claimed by AI companies**: Sutra (TWO AI's multilingual LLM), Yuanqi 元气 (Tencent's agent platform), Musubi (VC-backed AI content moderation), Telos (Daniel Miessler's LLM context framework), Ansible (Red Hat).
- **A few genuinely clean candidates surfaced**: Mithaq (Arabic, "primordial covenant"), Bijaksara (Sanskrit, "seed-syllable"), Foedus (Latin, "covenant" — the etymological root of "federal"), Yesod (Hebrew, "foundation," the ninth sefirah of the Kabbalah), Ma'at (Egyptian, "truth/order").

I recommended **Mithaq**. The reasons, ranked:

> 1. It precisely hits the core of your phrasing. "My most important conversations with these top models" — that is a **covenant relationship**. Mithaq in Arabic is "solemn covenant," and specifically refers to **the primordial covenant before all existence** (Quran 7:172, *Mithaq al-Alast*).
>
> 2. The namespace is genuinely clean. Only one Saudi family office called Mithaq Capital, with zero developer-world contact.
>
> 3. Excavation depth is deep. Your earlier worry about Memex bottoming out at Bush 1945 — Mithaq doesn't; there are at least four or five distinct essays inside it.
>
> 4. Doesn't conflict with your existing naming style. verse-driven, roboharness, LIP, docfit — your naming aesthetic accepts foreign words.

### The user caught a gap

User: "Did the deep research above actually research sci-fi movies?"

— a critical moment in this conversation. **The user performed independent review on Claude's output**, noticed that the first round had handled sci-fi shallowly with six or seven names breezed through.

I conceded: the original prompt had asked for broader coverage, but the deep research had concentrated on linguistic / religious traditions and underweighted the sci-fi line. I listed what hadn't been covered (Le Guin's other concepts, the full Stephenson catalogue, Lem, Egan, Banks's Culture, the full Cixin Liu set, Borges, Calvino, Ted Chiang, PKD…).

User: "OK, let's go."

### Focused SF deep-research round 2

28 candidates from sci-fi specifically. The result overturned the naive assumption "sci-fi must contain a good name":

- **Primer** (Stephenson, *The Diamond Age* — a book that grows a person up by adaptive instruction): the most precise functional fit. But `github.com/primer` is **GitHub's own** official design system. Unusable.
- **VALIS** (PKD): VALIS Systems is "an AI output verification layer" startup — squarely in this problem space.
- **Wallfacer / 面壁** (Cixin Liu): ModelBest / 面壁智能 is a major Chinese LLM lab (the MiniCPM maintainer). For the Chinese AI space, this name is permanently welded shut.
- **Sophon / 智子**: Sophon Network (a ZK Stack Validium L2, Binance Labs invested, $70M+ funding).
- **Droplet / 水滴**: WaterDrop Inc. (NYSE: WDH).

**The Cixin Liu coinages were almost entirely defeated** — the Chinese tech scene has been mining the Three-Body lexicon since 2022.

Only three genuinely clean sci-fi candidates remained: **Earthseed** (Butler), **Fuligin** (Wolfe), **Ekumen** (Le Guin, but `github.com/Ekumen-OS` is an Argentine robotics company — namespace collision with roboharness).

### Mithaq confirmed

The second round did not change the conclusion. It strengthened it. My final judgment:

> Mithaq still wins. The three clean SF candidates each have one structural weakness: Earthseed's political coloration / Fuligin's awkward Chinese transliteration / Ekumen's namespace collision with the robotics repo. Mithaq has no such structural weakness.
>
> Your key phrasing — "my most important conversations with these top models" — centers on *relationship*, not archive. Earthseed / Fuligin are archive concepts; Ekumen is a federation concept; Mithaq is a **covenant** concept. Covenant is the core of that phrasing.

By-product suggestions:

- **Reserve Earthseed for a future sister-repo name** — the structure parallels Butler's setup: Mithaq is the primordial covenant; Earthseed would be a propagable distilled-verses derivative.
- **The first essay should be titled "Why this repo is not named Primer"** — the contrast frames mithaq more sharply than a direct explanation could.
- Future essay material: Hylaean Theoric World (the Platonic realm and LLMs) / the Demon of the Second Kind (Lem's "filter for relevance" — RAG's prehistory) / The Telling (Le Guin: "telling is not explaining") / Severian's brown book (unreliable perfect memory).

### Landing

User: "I created MiaoDX/mithaq. Push an initial commit or two as needed."

I pushed two commits:

- `8f6e1f3` — `docs: add README and CHARTER`
- `e4894ff` — `feat: establish templates, vectors, and dialogues structure`

Containing README, CHARTER (with the case for Mithaq, the case against alternatives, inclusion criteria, relationship to other repos), the Layer 1 universal checkpoint meta-template (336 lines), and `vectors/` and `dialogues/` directories with their respective READMEs.

## Follow-up actions

- ☐ Write the WeChat essay "Why this repo is not named Primer" (first essay)
- ☑ Lay down the first vectors card — `roboharness` (to validate whether the Layer 1 template actually works across scenarios). Completed 2026-05-21; `robowbc` and `roboclaws` cards were added next.
- ☐ Run the Layer 1 template against an actual repo (roboharness or verse-driven) for a first-period checkpoint, to validate usability
- ☐ Follow-up essay candidates: the Aleph Alpha squat phenomenon / how Chinese AI mined out Cixin Liu's lexicon / Primer as "the perfect-but-unusable name"
- ☐ Monitoring: if an AI startup named Mithaq appears in the next 12 months, re-evaluate

## Revisions

- 2026-06-18: Updated follow-up status for the vectors-card milestone; the archive now has three cards (`roboharness`, `robowbc`, `roboclaws`).
