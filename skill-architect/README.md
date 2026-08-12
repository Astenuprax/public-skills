# skill-architect

A portable Agent Skill for authoring, auditing, and updating other agent skills so
they reliably get discovered and do their job. It's the meta-skill: point it at a
skill you're writing (or one that mysteriously never activates) and it puts the skill
through a three-part **Quality Gate** before you trust it.

The gate is:

- **Binary checklist** — the non-negotiables of a well-formed `SKILL.md`: a
  third-person description that carries its own trigger vocabulary, an accurate
  kebab-case name, real scope-bounding `anti_triggers`, a focused body, and at least
  three gap-based eval scenarios.
- **Trigger-recall probe** — an independent reviewer that sees *only* the frontmatter
  predicts whether the skill fires on realistic phrasings. If it can't, the
  description has failed its one mechanical job.
- **Independent adversarial review** — a fresh set of eyes hunts for dead citations,
  contradictions, and scope drift before the skill ships.

It's grounded in how skill discovery actually works: **only `name` and `description`
are loaded for selection**, so every trigger word has to live in the description
itself. Most "my skill never activates" problems trace straight back to that fact.

Three modes: **CREATE** a new skill, **UPDATE** an existing one, or **AUDIT** a skill
against the gate without changing it.

## Use it

The skill's logic lives in a single `SKILL.md` (with this README and a LICENSE
alongside). It's model-neutral and works with any assistant that supports custom
skills or system instructions.

**On claude.ai (Claude):**
1. In your Claude settings, add a new skill and provide this `SKILL.md` — upload the
   folder or file if that option is offered, otherwise paste its contents.
2. Save. It then activates when you ask things like "create a skill", "audit this
   skill", or "why doesn't my skill activate?"

**As a system prompt / custom instruction (any assistant):** paste the body of
`SKILL.md` (below the frontmatter) into the assistant's custom-instructions or
system-prompt field.

## Trigger phrases

Everyday phrasings work — no special command needed:

> "create a skill" · "write a new skill" · "scaffold a SKILL.md" · "help me with the
> skill description / frontmatter / triggers" · "audit this skill" · "review this
> skill" · "score this skill" · "why doesn't my skill activate?"

## License

See `LICENSE`.
