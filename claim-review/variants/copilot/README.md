# Claim Review — Microsoft 365 Copilot agent

A Copilot declarative-agent port of the `claim-review` skill: strengthen a claim to
its strongest form, then test whether its evidence supports it. For checking news
articles, sources, vendor and marketing claims, statistics, and research findings.

Two files, two deployment routes — pick one:

- **`declarativeAgent.json`** — the portable declarative-agent manifest (schema
  v1.6). Use it with the **Microsoft 365 Agents Toolkit** (VS Code) or by importing
  into the Copilot **Agent Builder** to create a publishable/shareable agent.
- **`instructions.md`** — the same instructions as plain markdown. Paste it into the
  **Instructions** box of the no-code **Agent Builder** in Microsoft 365 Copilot if
  you just want a personal agent without touching JSON.

## Deploy with Agent Builder (no-code)

1. In Microsoft 365 Copilot, open **Create agent** / **Agent Builder**.
2. Set the name to **Claim Review** and paste the `description` (from the manifest)
   and the contents of `instructions.md` into their respective fields.
3. Optionally add the conversation starters listed in the manifest.
4. Save and test against a claim: "does this article hold up?", "steel-man this".

## Deploy with Agents Toolkit (publishable)

1. Drop `declarativeAgent.json` into an Agents Toolkit declarative-agent project.
2. Provision / publish per the Toolkit flow (it wraps the manifest in the app
   package and runs RAI validation).

## Requirements & notes

- **No Copilot add-on licence required for this agent.** It grounds only in its own
  instructions (and, if web search is on, public sites), so Microsoft 365 Copilot
  Chat users — any Microsoft 365 subscription with a Microsoft Entra account — can
  run it at no additional cost. A paid Copilot licence is needed only for agents that
  ground in tenant data (SharePoint, Graph connectors, email).
- **Hard limits honoured:** `instructions` is 6,868 / 8,000 chars, `description`
  659 / 1,000, `name` 12 / 30 (UI), 4 / 12 conversation starters. It uses only
  long-stable fields plus the `WebSearch` capability, so you can retarget
  `version`/`$schema` to the schema version your Toolkit or tenant expects.
- **Web/freshness:** the manifest enables the `WebSearch` capability so Phase 2's
  source-freshness check can reach live public sources. Web search is the one
  capability that stays free-tier (no metered billing). To restrict it to specific
  domains, add a `sites` array (max 4) to the `WebSearch` object.
- **Copilot Studio** uses a different instruction/orchestration format; if you build
  there instead, use `instructions.md` as the source text and adapt to that guidance.
- Don't move these instructions into a knowledge file to dodge the char limit —
  knowledge sources aren't trusted as instructions and can be sanitised at runtime.

## License

MIT — see the `LICENSE` in the parent package.
