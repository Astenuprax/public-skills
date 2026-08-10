# Claim Review — Gemini Gem

A Gemini Gem port of the `claim-review` skill: strengthen a claim to its strongest
form, then test whether its evidence actually supports it. Aimed at checking news
articles, sources, vendor and marketing claims, statistics, and research findings —
separating what the evidence shows from what's inferred on top.

## Create the Gem

1. Open [gemini.google.com](https://gemini.google.com) and select **Gem manager**
   in the sidebar → **New Gem**.
2. Name it **Claim Review**.
3. Open `claim-review.gem.md`, copy everything **below the first horizontal line
   (`---`)**, and paste it into the Gem's **Instructions** box. (Skip the file's own
   title and that rule — they're just a wrapper.)
4. Save. Start a chat with the Gem and give it a claim: "is this real?", "steel-man
   this", "does this headline hold up?"

Gemini's own web access powers the freshness check in Phase 2 — the Gem will look at
a cited source's date when it can reach it.

## Notes

- Google publishes no character limit for Gem instructions, so this port keeps the
  skill's full logic. Google's suggested shape (Persona / Task / Context / Format)
  is already built into the instructions.
- You can optionally attach reference files to the Gem via **Knowledge**, but the
  skill needs none to work.

## License

MIT — see the `LICENSE` in the parent package.
