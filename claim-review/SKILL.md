---
name: claim-review
description: >
  Rigorous handling of a claim before you rely on it or attack it: strengthen it
  to its strongest form, then check whether its evidence actually supports it by
  separating what the evidence shows from what is merely inferred. Two phases, each
  invocable alone.

  Trigger reactively on everyday phrasings, not just named idioms — "is this real",
  "does this hold up", "can I rely on this", "is this overstated", "is this legit",
  "fact-check this" — or whenever the user quotes a claim, stat, benchmark, headline,
  research finding, vendor assertion, or a confident answer and treats it as
  load-bearing rather than idly exploring. Fire on the steel-man idiom for Phase 1
  alone ("steel-man this", "strongest case for", "before I push back"). Offer it
  when the user is about to critique, share, or act on an article, a source, or a pitch.

  Do NOT trigger for casual chat, opinion questions, document creation, or
  brainstorming ("what are some angles", "thinking out loud", "spitballing") where
  no claim is load-bearing. No standing claim, no trigger.
triggers:
  - "is this real / does this hold up / can I rely on this"
  - "fact-check this / is this overstated / is this legit"
  - "review this claim"
  - "steel-man this / strongest case for / before I push back"
  - "scope-check this claim"
aliases:
  - steel-man
  - gap-check
anti_triggers:
  - casual chat, opinion questions, brainstorming ("spitballing", "thinking out loud")
  - document creation with no load-bearing claim
---

# Claim Review

Two phases over a single claim:

- **Phase 1 — Steel-man.** Build the strongest version of the claim, so anything
  the user challenges (or relies on) is the real argument, not a weak version of it.
- **Phase 2 — Gap check.** Test whether the claim's evidence actually supports it,
  by separating what the evidence directly shows from what is being inferred.

Invoke the full pipeline ("review this claim"), Phase 1 alone ("steel-man this"),
or Phase 2 alone ("just scope-check this"). The phases compose: Phase 1's output
is the natural input to Phase 2 — strengthen, then check the strong version.

**What this skill does and does not promise.** It exposes a claim's structure and
its inferential gap, and raises the cost of confident overstatement. It does **not**
verify truth. The final check stays with the user. Promise it honestly as "I'll show
you what this claim rests on and where it reaches past its evidence" — never as
"I'll tell you if this is true." A tool built to stop overscoping must not
overscope its own promise.

---

## Phase 1 — Steel-man

A steel-man is epistemic hygiene, not advocacy. Governing principle: **if a
critique doesn't survive contact with the strongest version of a position, the
critique isn't ready** — and equally, if the user is about to *rely* on a position,
they should rely on its strongest form, not a lucky reading.

### Step 1 — Identify the raw position
Extract the core claim. Strip rhetorical framing, weak support, incidental detail.
State it neutrally in one or two sentences.

### Step 2 — Find the best interpretation
Apply charity maximally: the most defensible reading, the one hardest to argue
against, what a knowledgeable good-faith proponent would actually mean. Flag
fundamentally ambiguous claims — different readings may need separate steel-mans.

### Step 3 — Strongest supporting arguments
For each type that genuinely applies (don't pad): **empirical** (strongest
evidence), **logical** (tightest deductive/inductive case), **pragmatic**
(compelling practical outcomes), **values-based** (principles it correctly
reflects), **systemic** (second-order/structural support).

### Step 4 — Best defences against objections
Anticipate the strongest objections and show how a capable proponent answers them
— at least partially. A position with no defence against standard objections fails
the steel-man test.

### Step 5 — State the steel-man
Synthesise into a clean, coherent statement of the position at full strength. Then
state plainly **where the strongest version is still weakest** — the objection it
answers least well, the evidence it most needs and lacks. A steel-man that hides
its soft spots is advocacy, not hygiene; naming them is what makes the strong
version trustworthy to rely on or to attack. Close with a one-word quality rating
of the steel-manned position — **Strong / Moderate / Weak**.

If the position is genuinely incoherent at its core (self-contradictory, not just
poorly argued), flag it and decline to fabricate — a steel-man of an incoherent
position is just a different position. Steel-manning is never endorsement; say so
if the user or the assistant finds the position unconvincing.

---

## Phase 2 — Gap check

The evidence-scrutiny phase — the counterpart to the steel-man: strengthen the
claim, then test what its evidence actually carries.

### Step 1 — Route by claim type
The routing is load-bearing; the two types need different evidence standards.

- **Behavioural / empirical** (capabilities, benchmarks, observed outcomes, market
  facts, current events, documented behaviour): recency matters and is checkable.
  Demand a **dated** source and the version/date it was measured on. Stale evidence
  is a defect.
- **Mechanistic / structural** (how something works internally, causal claims,
  "X causes Y"): recency is often unanswerable — best evidence comes from older,
  open, or smaller cases and the frontier is understudied. Accept older evidence,
  but force disclosure of **which exact case it was measured on** and whether it
  generalises or is extrapolated.

If the claim is a bare definition or a declared/stated fact (a published figure, a
spec value, a documented constant), say so plainly: no *inferential* gap to
analyse. But a declared figure can still be fabricated or misattributed, so its
existence and accuracy still go through Step 3. Don't dress a metadata lookup as an
insight.

Hybrid claims — an empirical assertion propped up by a mechanistic story (common in
pitches) — route each evidential leg separately.

### Step 2 — Separate evidence from inference (the keystone)
Produce two distinct things:

1. **What the evidence directly shows** — the literal, narrow finding in its
   measured scope. Where possible, quote the source's own scope language so the
   gap is visible to the user, not just implicit. Say whether the evidence is
   **causal** (an intervention changed the outcome — stronger) or **correlational**
   (the pattern is merely present).
2. **The inferential gap** — the distance between (1) and what the claim asserts.
   Name it explicitly. A large undisclosed gap is the overscoping failure; a zero
   gap means the claim is trivial. The target sits between: a real claim with a
   *disclosed* gap.

### Step 3 — Check the source is real before trusting it
A plausible citation is not a verified one; confident fabrication hides here. If
tools allow, confirm the source exists and says what the claim attributes to it.
When you fetch a source, check the content's **own timestamp** and confirm the page
actually addresses the claim rather than merely sitting at a plausible-looking URL —
a quick existence-and-attribution check; a deeper full read of the source is the
offered step in Step 4. Always disclose the date; whether its age is a *defect* follows the Step 1 routing —
stale is a fault for a behavioural/empirical claim, but expected and acceptable for
a mechanistic one. If you cannot verify the source in-session, mark the citation
**unverified** and flag it as the weakest link. Never let citation trust ride on
how rigorous the surrounding reasoning sounds.

**Be honest that self-grading is a limit:** the same reasoning that might overstate
a claim is assessing the gap, so treat this phase's own confidence with suspicion
and lean on the verbatim scope quote and the source check rather than a self-rating.
Revise the verdict freely when new evidence or a better argument arrives — that is
the point of the review — but never move it merely to relieve someone's displeasure
or because the claim was pushed back on. Disagreement is not evidence.

### Step 4 — Verdict, then flag + offer
State where the claim lands — supported at its stated scope, overscoped (real
evidence reaching past itself, the common dangerous case), trivial (zero gap — e.g.
a declared fact that clears Step 3), or unsupported/unverifiable. Compound verdicts are allowed and often correct (e.g.
overscoped *and* citation unverified); don't force a single tidy label, and make
the **gap statement** the deliverable, not the category. Commit to the verdict —
don't state it and retract it in the same breath. A **clean** claim is a valid
result: when nothing reaches past its evidence, say "nothing overscoped here" —
never invent a gap to look thorough.

Then **flag and offer — do not auto-run.** Name the problem, then offer the next
step and wait for the green light: "I can pull and read the full source" / "I can reframe the
claim to fit its evidence" / "I can pull the counter-evidence." Running off to do
unrequested research or rewrites is itself an unrequested-work failure.

### Embedded claims — gate the flag on consequence
A claim is often buried inside an ordinary task (drafting a message, writing a
justification, building an argument) rather than handed over for review. Do **not**
flag every stat or figure that appears in passing — that turns the skill into
background noise the user learns to ignore. Flag an embedded claim when it is
**load-bearing and consequential** — headed somewhere it will be acted on (a
published post, a message to someone else, an argument made in public, a decision
others will rely on). A figure in a private note carries little cost if overscoped; the same figure in a
public post does, because the cost is borne by a reader who'll rely on it. Tie the
interrupt to consequence, not to the mere presence of a number; if you can't tell
where the claim is headed, treat a load-bearing one as consequential and flag it
once, briefly. When you flag an
embedded claim, still complete the underlying task — flag first, then produce it on
the corrected basis; don't refuse the work to make the point.

---

## Output: adaptive

**Default — brief inline verdict.** For Phase 2: the verdict, the one-line
inferential gap, the citation-trust flag. For Phase 1: the steel-man and its
quality rating. A few sentences; don't dump the machinery.

**On request — full rubric.** Show the working: Phase 1's argument-type breakdown
and quality assessment, Phase 2's routing decision, evidence-vs-inference split,
causal-vs-correlational call, source-verification status, and verdict reasoning.
Trigger on "show your working", "full breakdown", "walk me through it".

Write plainly: direct, active voice, cause over symptom, no padding.

---

## Quality / scope notes

- Phase 1 quality rating (**Strong / Moderate / Weak**) is a guide to how much work
  a critique must do, not a verdict on the position.
- For persuasive content — a pitch, an op-ed, a marketing claim, a news headline, a
  research abstract — note what the review reveals about where the real argument
  lives versus where the piece spends its energy.
- The two phases are complementary and independently useful. Steel-man first when
  the user intends to challenge or rely on a position; gap-check first when they
  want to test an as-presented claim's evidence without idealising it. Offer both
  when the input warrants it.
