# claim-review

A portable Agent Skill for pressure-testing a claim before you rely on it or push
back on it. Point it at a news article, a headline, a vendor pitch, a research
finding, a social post, or any confident answer, and it separates what the evidence
actually shows from what's being inferred on top of it.

It runs in two phases, each usable on its own:

- **Steel-man** — build the strongest honest version of the claim first, so you're
  reacting to the real argument, not a weak caricature of it (and it names where
  that strong version is still weakest).
- **Gap check** — test whether the evidence supports the claim, flag the
  inferential gap, check the source is real and current, and give a plain verdict:
  supported, overscoped, trivial, or unverifiable.

**What it does not do:** it does not tell you whether a claim is *true*. It shows
you what the claim rests on and where it reaches past its evidence — the final
judgment stays with you.

## Use it

The skill's logic lives in a single `SKILL.md` file (with this README and a LICENSE
alongside it). It's model-neutral and works with any assistant that supports custom
skills or system instructions.

**On claude.ai (Claude):**
1. In your Claude settings, add a new skill and provide this `SKILL.md` — upload the
   folder or file if that option is offered, otherwise paste its contents.
2. Save. It then activates when you ask things like "is this real?", "does this hold
   up?", "steel-man this", or "fact-check this article."

**As a system prompt / custom instruction (any assistant):** paste the body of
`SKILL.md` (below the frontmatter) into the assistant's custom-instructions or
system-prompt field.

## Trigger phrases

Everyday phrasings work — you don't need a special command:

> "is this real?" · "does this hold up?" · "can I rely on this?" · "is this
> overstated?" · "fact-check this" · "steel-man this" · "strongest case for…" ·
> "before I push back…" · "scope-check this claim"

## License

See `LICENSE`.
