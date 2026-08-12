---
name: skill-architect
description: >
  Standardizes how agent skills are created, audited, and updated so a SKILL.md
  reliably gets discovered and does its job. Use it when scaffolding a new skill,
  when auditing or updating an existing skill's frontmatter or structure, or when
  checking a skill's quality before you rely on it.

  Trigger reactively on everyday phrasings, not just named commands — "create a
  skill", "write a new skill", "scaffold a SKILL.md", "help me with the skill
  frontmatter / description / triggers", "audit this skill", "review this skill",
  "why doesn't my skill activate", "score this skill", "is this skill any good".
  It runs a three-part Quality Gate — a binary checklist, a trigger-recall probe,
  and an independent adversarial review — and it is grounded in how skill
  discovery actually works (only name + description are loaded for selection).

  Do NOT trigger for general file editing outside skill definitions, for executing
  the task a skill is about (this authors the skill, it doesn't run it), or for
  casual questions that don't involve a SKILL.md.
triggers:
  - "create a skill / write a new skill / scaffold a SKILL.md"
  - "audit this skill / review this skill / score this skill"
  - "update the skill definition / fix the frontmatter"
  - "why doesn't my skill activate / is this skill good"
aliases:
  - skill-sensei
  - skill-quality-gate
anti_triggers:
  - general file editing outside of skill definitions
  - executing the task a skill describes (this authors skills, it does not run them)
  - casual questions unrelated to a SKILL.md
---

# skill-architect

Author, audit, and update agent skills so they reliably activate and do their job.
The heart of this skill is a **three-part Quality Gate** that a skill must clear
before you trust it: a binary checklist, a trigger-recall probe, and an independent
adversarial review. Everything else supports getting a skill through that gate.

Select the path that matches what you're doing:

- **PATH A — CREATE** a new skill from scratch.
- **PATH B — UPDATE** an existing skill's frontmatter or structure.
- **PATH C — AUDIT** a skill against the Quality Gate without necessarily changing it.

---

## How skill discovery actually works (read this before authoring or scoring anything)

These facts drive every decision below. Getting them wrong is the most common reason
a skill silently never fires.

- **Only `name` and `description` are loaded for selection.** When the assistant
  decides whether to activate a skill, it sees the name and the description — not the
  body, not any custom frontmatter. So *all* trigger vocabulary must live in the
  `description` string itself. A separate `triggers:` list is fine as human-readable
  documentation, but it has **no mechanical effect** on whether the skill fires.
- **The description must be third person** ("Use it when…", "It runs…"), never first
  or second person. Mixed point of view causes discovery misses.
- **The description must state both WHAT the skill does and WHEN to recall it**, and
  it should carry realistic paraphrases of how a user would actually ask — not just
  one canonical command word.
- **`anti_triggers` do not affect selection either.** They exist to bound the skill's
  scope once it is already active (guarding against a skill overreaching into work it
  shouldn't touch) and to document intent for anyone reading the file. Keep them, but
  don't rely on them to *prevent* activation — that's the description's job.
- **Keep the body focused.** Aim for well under ~500 lines. Push anything past the
  core protocol — long rationale, worked examples, lookup tables — into companion
  files (`references/`, `examples/`) and leave a one-line pointer in the body.

**Quality is proven by real use, not by self-scoring at authoring time.** The most
reliable signal that a skill works is watching it succeed or fail on real requests.
Build a few evaluation scenarios *before* polishing the prose, and every new skill
should ship with **≥3 gap-based eval scenarios** — concrete situations where the
assistant would fail or underperform *without* the skill. If the skill doesn't
change behavior on those scenarios, it isn't earning its place.

---

## The Quality Gate

A skill is trustworthy only when it clears all three parts below, in order.

### (a) Binary pass/fail checklist — every item must be true, no partial credit

- Frontmatter has `name` and `description`. The description is third person, states
  both WHAT and WHEN, and carries the trigger vocabulary inline (not hidden in a
  separate list).
- The skill's name is kebab-case and semantically accurate to the skill's **full**
  scope — no inherited legacy name, and no verb that under-describes what it does
  (don't call something `-creator` if it also audits and updates; prefer `manager`
  or `architect`).
- `anti_triggers` are present and meaningfully bound the skill's capability — they
  name real out-of-scope actions, not filler.
- Any file-write or file-edit step in the skill's protocol respects safe-edit
  discipline (read before overwrite; prefer surgical, anchored edits over blind
  full-file rewrites; verify the result). See **Safe-edit discipline** below.
- If the skill hard-depends on another skill or tool by name (a handoff, a shared
  definition, a citation), that dependency is declared explicitly near the top so
  someone installing this skill alone doesn't hit a dead reference.
- The body is focused (well under ~500 lines); anything beyond the core protocol is
  pushed to companion files with a one-line pointer left behind.
- The body contains operative protocol only. Narrative rationale — background
  justification, dated retellings, incident history — is extracted to a companion
  `references/rationale.md` with a pointer in its place.
- Any tooling the skill *ships and runs itself* (scripts in `scripts/`) is written
  against a broadly available runtime with no install step — the environment a
  hosted assistant runs skills in typically has no package manager and no arbitrary
  installs. A script the skill *emits as its deliverable* is product, not tooling,
  and can be in any language the user wants.
- **≥3 gap-based eval scenarios** ship with the skill (for a new skill) or already
  exist (for an audited one).

### (b) Trigger-recall probe

Assemble **5–8 realistic phrasings that SHOULD activate** the skill and **3 that
should NOT**. Then have an **independent reviewer that sees only the frontmatter** —
not the skill's body, not the surrounding conversation — predict activation for each.

If prediction only succeeds when the reviewer can see the body, the description has
failed at its one mechanical job: rewrite the description until the frontmatter alone
carries the recall. If you have no way to spawn a separate reviewer, run the probe in
a genuinely fresh context (a new chat) rather than in the session that authored the
skill, and note that substitution in your report.

### (c) Independent adversarial review

Have a **separate reviewer** (never the agent that authored the skill) read the
finished SKILL.md looking for dead citations, internal contradictions, and scope
drift. Author-and-reviewer being the same context is the failure mode this guards
against — a fresh set of eyes catches what the author's own assumptions hide. Same
fresh-context substitution rule as (b) if no separate reviewer is available.

Only after (a) + (b) + (c) all pass is the skill ready to ship.

---

## Safe-edit discipline

When any path below writes or edits a file, follow these interlocks:

1. **Read before you overwrite.** Never replace an existing file you haven't read
   this session.
2. **Surgical over wholesale.** For a targeted change in a large file, use a precise,
   unique anchor and edit in place. Reserve full-file rewrites for genuine structural
   overhauls, and only after reading the original in full.
3. **Baseline, then verify.** Where version control is available, check the file's
   state before and after (`git status` / `git diff`); investigate any unexpected
   deletions immediately and restore from the last good version if content was lost.
4. **Cold read before you're done.** After finishing edits, read the completed file
   top to bottom once more to confirm frontmatter is well-formed, arrays are flat,
   and nothing was silently dropped.

---

## PATH A: CREATE

**Step 1 — Intent analysis.** Pin down the skill's domain, the expert persona it
adopts, and its single core capability. Write down its Intent Map: WHAT it does,
its INPUT (the phrasings and data that reach it), its OUTPUT (what it produces), and
WHY it's needed. Pick a kebab-case name that covers the skill's full scope, and check
the proposed name and any aliases don't collide with skills the assistant already has.

**Step 2 — Scaffold.** Create `skill-name/SKILL.md` with the frontmatter
(`name`, `description`, `anti_triggers`; optional `aliases`, `version`). Write the
description in third person, stating WHAT + WHEN, with trigger vocabulary inline.
Make `anti_triggers` name real out-of-scope actions. Don't create empty
`references/`/`examples/` directories — add them only when you have real content for
them. If drafting surfaces narrative rationale, put it in `references/rationale.md`
and leave a pointer. Draft the ≥3 gap-based eval scenarios now.

**Step 3 — Run the Quality Gate** (a)+(b)+(c) and record a short report:

```
Skill                      : <skill-name>
Gate (a) Binary checklist  : [PASS / FAIL — list failing items]
Gate (b) Trigger probe     : [PASS / FAIL — list mispredicted phrasings]
Gate (c) Adversarial review: [PASS / FAIL — list findings]
Status                     : [Ready / Refinement required]
```

**Step 4 — Refine.** For each failing item, apply the smallest fix that addresses it,
then re-run Step 3. Repeat until all three parts pass.

**Step 5 — Cold read** the finished file (see Safe-edit discipline) and confirm the
skill is ready to ship.

---

## PATH B: UPDATE

**Step 1 — Read first.** Read the target SKILL.md this session and establish a
baseline (`git status` / `git diff` if available). Identify exactly which Quality
Gate item(s) are failing.

**Step 2 — Surgical remediation.** Note the Intent Map for the change (WHAT is
changing, INPUT/OUTPUT contract, WHY). Apply the smallest edit that fixes each
failing item — no full-file rewrite unless the structure is fundamentally broken. If
narrative rationale has accreted in the body, extract it to `references/rationale.md`
— that's a valid update even with no other failure.

**Step 3 — Verify.** Re-check the diff for unexpected deletions and restore if
needed. Re-run the Quality Gate; all three parts must pass before finalizing.

**Step 4 — Cold read** the edited file. If the `description` changed, remember that
anywhere the old description was registered or copied needs to be re-synced.

---

## PATH C: AUDIT

**Step 1 — Read** the named skill. If none is named, ask which one.

**Step 2 — Run the Quality Gate** (a)+(b)+(c) against it.

**Step 3 — Structural check.** Confirm safe-edit discipline appears on the skill's
write/edit steps; the frontmatter carries no stale model/runtime pins; `anti_triggers`
genuinely bound scope; the body is operative protocol only (flag in-body narrative
rationale as an update target); and any named dependency is declared.

**Step 4 — Findings report:**

```
Skill                      : <skill-name>
Gate (a) Binary checklist  : [PASS / FAIL — list failing items]
Gate (b) Trigger probe     : [PASS / FAIL — list mispredicted phrasings]
Gate (c) Adversarial review: [PASS / FAIL — list findings]
Scope guard (anti_triggers): [Effective / Weak]
Dependencies declared      : [Yes / No / N/A]
Recommendation             : [Update via PATH B / None]
```
