# {{REPO_NAME}} Ecosystem Research — {{YYYY-MM}} Checkpoint

> A structured archive of `{{REPO_NAME}}`'s investigation into {{the surrounding ecosystem / relevant stack / adjacent technology domain}}.
>
> **This checkpoint:** {{Month D, YYYY}}
> **Next scheduled update:** {{end of Month YYYY / event-triggered}}
> **Maintenance mode:** {{monthly / bi-monthly / quarterly}} deep research + human review (see §0.2)

---

> **About this template**
>
> This file is the Layer 1 universal checkpoint skeleton provided by [`MiaoDX/mithaq`](https://github.com/MiaoDX/mithaq). Per-repo instances fill in this template; the resulting `YYYY-MM.md` file lives in each consuming repo's `docs/research-checkpoints/`, **not** in mithaq.
>
> **Companion:** mithaq holds a research-vectors card at `mithaq/vectors/<repo-name>.md` (Layer 2) defining "what to track." This template is the skeleton ("how to write"); the vectors card is the substance ("what to write about"). Both are needed.
>
> Three rules when filling in: (1) `{{...}}` markers are placeholders that must be replaced; (2) blockquote sections (`>`) are instructions to the author and should be deleted before publishing; (3) delete inapplicable sections entirely — do not leave empty headers.

---

## 0. About this document

### 0.1 Why this checkpoint exists

> Three to five paragraphs answering:
> - What is this repo's core positioning and what are its constraints?
> - Why does any "selection decision" in this domain have a short shelf life? (How fast is the ecosystem moving? What are the key variables?)
> - The two jobs of this checkpoint: freezing the current understanding + establishing a sustainable update mechanism.

{{Why this repo needs a periodic ecosystem snapshot. Cover: positioning, constraints, rate of change in the ecosystem, cost of not snapshotting.}}

### 0.2 Update method

Each update follows this loop:

**Step 1 — incremental research**

Run a targeted deep-research pass against the repo-specific tracking surface defined in the vectors card (see [`mithaq/vectors/{{repo-name}}.md`](https://github.com/MiaoDX/mithaq/blob/main/vectors/{{repo-name}}.md)). The vector set is stable across periods for comparability; the expansion depth is flexible:

| Vector | Type | This period coverage | Reason |
|--------|------|----------------------|--------|
| {{V1 name}} | core / watch / trigger-only | full update / light check / no significant change / not triggered | {{why this depth is sufficient this period}} |
| {{V2 name}} | core / watch / trigger-only | {{...}} | {{...}} |
| {{V3 name}} | core / watch / trigger-only | {{...}} | {{...}} |

Rules:

- **Fixed tracking surface, flexible expansion depth**: every checkpoint checks the same vectors card; it does not invent a new set of directions for the period.
- **Core vectors** receive a full update every routine checkpoint.
- **Watch vectors** receive a light check every routine checkpoint and expand only when a trigger fires or material evidence appears.
- **Trigger-only vectors** are listed in the coverage table but expand only when their explicit trigger fires.
- Vector count, classification, and scope change only during vectors-card self-audit or an explicit card update, not ad hoc inside an ordinary checkpoint.

**Step 2 — incremental update**

Compare the research output against the previous checkpoint and produce three categories of update:

- **New projects / concepts** — added to the relevant table with `(new in YYYY-MM)`.
- **Status changes** — original entry undergoes a significant change (a key metric ±30%, rename, end of maintenance, acquisition, key person leaving). Add `[updated YYYY-MM]` to the original entry.
- **Judgment revision** — if new evidence makes a prior recommendation no longer hold, **do not delete the prior recommendation**. Instead add a `[revised YYYY-MM]` block below it explaining why the judgment changed. This preserves the trail of how the thinking evolved.

**Step 3 — write the new checkpoint**

Copy the prior checkpoint as a template; update:

- File header date and next-update date;
- §1 Executive summary — rewritten to reflect the 3-5 most important changes this period;
- §3 / §4 / §5 / §6 sections — updated per Step 2 annotations;
- §7 Open questions — strike through any resolved this period, add new ones discovered this period;
- §8 Changelog — new section `## YYYY-MM-DD` listing all changes from this period.

**Step 4 — review and commit**

Manually review the whole document. Particularly check:

- Did we over-rely on any single source (especially SEO content sites)?
- Did we slack off by copy-pasting last period's content because "nothing changed this month"?
- Are the recommendations in §6 disconnected from the evidence in §3-§5?

After review, commit to the consuming repo's `docs/research-checkpoints/` directory.

**Triggers for an off-schedule research pass (do not wait for the next cycle):**

- {{trigger 1, e.g., "a model-generation jump occurred" — see the vectors card for specific triggers}}
- {{trigger 2}}
- {{trigger 3}}

### 0.3 Source-quality declaration

Sources encountered during research fall into four tiers, and the author must keep track of which tier they are citing:

**A-tier (primary, trustworthy)**: project official GitHub repos, official blogs (Anthropic, OpenAI, NVIDIA, HuggingFace, Allen AI, and similar majors), arXiv papers, Linux Foundation official announcements, technical blogs maintained by named individuals (e.g., mitchellh.com). These can be cited directly, though publication date still needs verification — an arXiv preprint is not the same as a published paper; a company blog may reflect PR framing.

**B-tier (secondary, requires cross-verification)**: technical press (The Information, TechCrunch, TheNewStack, InfoQ, SecurityWeek, VentureBeat, 量子位, 机器之心), comparison posts by independent engineers, highly-upvoted HackerNews / Reddit / Zhihu answers, industry consulting reports. Direction usually correct, but specific numbers and timelines must be checked against primary sources.

**C-tier (aggregators, use with care)**: `awesome-*` lists, comparison portals, ecosystem maps. Useful for **breadth of discovery** ("oh, this project also exists") but **any specific quantitative claim** (stars, market share) should be treated as ±20% and verified at the upstream repo.

**D-tier (SEO / content marketing, mostly not cited)**: sites whose hallmark is "best X alternatives of 2026" SEO content. Their **structural conclusions** (which tool fits which scenario) sometimes have value, but their **specific claims** (performance numbers, market judgments) are almost entirely SEO copy and should be **ignored in nearly all cases**. If a judgment is supported only by a D-tier source with no A/B-tier corroboration, mark it `[INSUFFICIENT VERIFICATION]`.

**Repo-specific source whitelists and blacklists**: see the "Sources" section of [`mithaq/vectors/{{repo-name}}.md`](https://github.com/MiaoDX/mithaq/blob/main/vectors/{{repo-name}}.md).

### 0.4 How to read this

The document may be long. Use these entry points based on what you need:

- **Quick conclusions only**: read §1 (executive summary) + §6 (recommendations).
- **Understand the ecosystem panorama**: read §3.
- **Make a selection decision**: read §6 + §7.
- **Prepare the next checkpoint**: read §0.2 + §8 (changelog) + §7 (open questions) — this tells you what needs filling in.

---

## 1. Executive summary

> Three to five most important ecosystem-level judgments from this period, each 1-3 sentences.
> First checkpoint: write "baseline established" and list the overall current understanding.
> Subsequent checkpoints: emphasize "what changed vs. last period."

**{{N}} ecosystem-level judgments:**

1. {{judgment 1}}
2. {{judgment 2}}
3. ...

**Specific recommendations for `{{REPO_NAME}}`:**

1. {{recommendation 1}}
2. {{recommendation 2}}
3. ...

**Still uncertain, requires next checkpoint to verify:**

- {{question 1}}
- {{question 2}}

---

## 2. Background: {{REPO_NAME}} current state and constraints

> So that this document reads without external context. If these change before the next checkpoint, update this section *first*.
> Cover: project positioning, current stack, roadmap phase, known technical constraints.

**Project positioning**: {{one-sentence definition: what this repo does, for whom, and what it does not do.}}

**Current stack ({{Month YYYY, actual state of the repo}})**:

- {{component 1}}
- {{component 2}}
- ...

**Roadmap**:

- **Phase 1** ({{done / in progress / planned}}): {{...}}
- **Phase 2**: {{...}}
- **Phase 3**: {{...}}

**Known technical constraints**:

- {{constraint 1, e.g., primary language, license restriction, performance threshold}}
- {{constraint 2}}

These constraints drive every judgment below.

---

## 3. Ecosystem panorama

> Main body of the checkpoint. Structure by what fits this repo — could be "list of peer projects," "upstream-downstream stack layers," "taxonomy," etc.
> Requirement: every project mentioned has an official repo link, a brief activity-level note, and an assessment of its relevance to this repo.
> Tables are often better than paragraphs for many-entry comparisons.

### 3.1 {{Core peer projects / direct competitors}}

| Project | Maintainer | Key metric | Relevance to this repo |
|---------|-----------|------------|------------------------|
| {{Project A}} | {{maintainer}} | {{stars / latest release / users}} | {{relevance, points worth borrowing}} |
| ... | | | |

### 3.2 {{Adjacent projects / upstream-downstream stack}}

> Not direct competitors, but in the same ecosystem and may affect this repo's decisions.

{{...}}

### 3.3 {{Stable patterns emerging this period}}

> Patterns distilled from the ecosystem panorama — things others are doing that this repo might follow, or deliberately not follow.

- **{{Pattern 1}}**: {{description + examples + trade-off for this repo}}
- **{{Pattern 2}}**: {{...}}

---

## 4. Taxonomy / perspectives (optional)

> If a simple linear list cannot express the ecosystem structure, use 2-4 perspectives that each cut the same domain differently.
> Examples: by abstraction layer / by responsibility / by deployment shape / by user type.
> Perspectives should be orthogonal, not replacements of each other.
> If this repo's ecosystem is not that complex, delete this section.

### 4.1 Perspective I: {{...}}

{{...}}

### 4.2 Perspective II: {{...}}

{{...}}

### 4.3 When to use which perspective

{{Give the reader a selection guide.}}

---

## 5. Existing academic and industry taxonomies (optional)

> If there are recognized academic surveys or industry stack maps to reference, list them here.
> Not required — many emerging fields lack established taxonomies.

### 5.1 Academic surveys

- {{arXiv / survey 1}}: {{brief commentary}}

### 5.2 Industry stack maps

- {{...}}

---

## 6. Specific recommendations for `{{REPO_NAME}}`

> Evidence in §3-§5 → recommendations in §6. The argumentative chain between them must be clear.
> Order by "value / implementation cost." Mark each recommendation with current state (TODO / in progress / done).

### 6.1 Trade-offs by phase (if phases apply)

{{...}}

### 6.2 Projects worth deep-reading first

> Which projects deserve an hour or two of careful reading of README / main source / comparison of design trade-offs.

1. {{Project X}} — reason: {{...}}
2. {{Project Y}} — reason: {{...}}

### 6.3 Concrete engineering actions

Not bounded by time. Ordered by "value / implementation cost."

| # | Action | Status | Value |
|---|--------|--------|-------|
| 1 | {{action}} | TODO / in progress / done | {{description of value}} |
| 2 | ... | | |

---

## 7. Open questions and what next checkpoint should answer

Next checkpoint should answer these first. Items already resolved by this period's deep research are marked `[resolved YYYY-MM]` with a synthesized answer; newly raised items are marked `[new in YYYY-MM]`.

### Experimental questions (require running code in this repo to answer)

- ☐ **Q1**: {{...}}
- ☐ **Q2**: {{...}}

### Technical selection questions

- ☐ **Q3**: {{...}}
- ✅ **Q4** [resolved YYYY-MM]: {{...}}

### Ecosystem-tracking questions

- ☐ **Q5**: {{...}}

### Long-horizon tracking questions

- ☐ **Q6**: {{...}}

### Source-quality improvement questions

- ☐ **Q7**: {{e.g., this period some claim depended on a C/D-tier source; can we find primary data next time?}}

### New this period

- ☐ **Q8** [new in YYYY-MM]: {{...}}

---

## 8. Changelog

### {{YYYY-MM-DD}} — {{version note}}

> First checkpoint: write "baseline established."
> Subsequent checkpoints: write "main changes vs. last period."

**Architecture narrative**:

- {{...}}

**New projects**:

- {{...}}

**Status changes**:

- {{...}}

**Judgment revisions**:

- {{...}}

---

## Appendix A: full reference links

> All links cited in the body, grouped.
> Prefer A-tier sources (official repos, official blogs, arXiv). C/D-tier sources should not appear in the appendix at all.

### A.1 {{group 1, e.g., "core peer projects"}}

- {{Project A}}: {{URL}}
- ...

### A.2 {{group 2}}

- {{...}}

---

## Appendix B: glossary

> Terms, abbreviations, and self-coined labels specific to this repo.
> Extend each period.

| Term | Meaning |
|------|---------|
| {{Term 1}} | {{meaning}} |
| {{Term 2}} | {{meaning}} |

---

**End of document. Next checkpoint scheduled for {{Month YYYY}}.**

Run the incremental-research loop per §0.2, paying particular attention to the open questions listed in §7.
