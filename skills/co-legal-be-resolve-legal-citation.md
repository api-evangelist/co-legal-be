---
name: co-legal-be-resolve-legal-citation
description: Turn a Belgian, Dutch or EU legal citation (ECLI, CELEX, statute article) into its canonical official-source URL, read the document text, and — over A2A — verify that a citation is real before you rely on it.
api: mcp/co-legal-be-mcp-tools.json
surface: mcp (a2a equivalents noted; one step is a2a-only)
operations:
  - ecli_lookup
  - nl_rechtspraak_lookup
  - eurlex_lookup
  - legal_lookup
  - nl_legal_lookup
  - legal_search
  - legal_read
a2a_skills:
  - be.ecli.lookup
  - nl.rechtspraak.lookup
  - eu.eurlex.lookup
  - be.legal.lookup
  - nl.legal.lookup
  - be.legal.search
  - be.legal.read
  - legal.citation.verify
method: generated
generated: '2026-09-19'
grounding: Every tool name exists verbatim in mcp/co-legal-be-mcp-tools.json and every skill id in a2a/co-legal-be-agent-card.json (2026-09-19). Identifier shapes and examples are quoted from the tool-schema/v1 extension.
---

# Resolve and verify a legal citation with Co-Legal

Free, anonymous, read-only. MCP: `POST https://agent.co-legal.be/mcp`. A2A: `POST https://agent.co-legal.be/a2a/jsonrpc` with `A2A-Version: 1.0`. Pick the resolver by identifier type.

## Case law

- Belgian ECLI → `ecli_lookup` (`ecli`, required). Shape `ECLI:BE:<court>:<year>:<serial>`, e.g. `ECLI:BE:CASS:2020:ARR.20200305.1F.4`; case-insensitive. Returns EU e-Justice and Juportal URLs plus decoded court / year / serial. A2A: `be.ecli.lookup` (15–80 chars).
- Dutch ECLI → `nl_rechtspraak_lookup` (`ecli`, required), e.g. `ECLI:NL:HR:2021:1102`. Returns the Rechtspraak.nl page, the free Open Data content API URL and EU e-Justice. A2A: `nl.rechtspraak.lookup`.

## Legislation

- EU (CELEX) → `eurlex_lookup` (`celex` required, `language` optional two-letter EUR-Lex code, default `NL`). Examples `32016R0679` (GDPR), `32024R1689` (AI Act), `62019CJ0311` (CJEU C-311/19); a `CELEX:` prefix is accepted. A2A: `eu.eurlex.lookup`.
- Belgian statute → `legal_lookup` (`code` required — one of `BW, WVV, WIB92, VCF, WBTW, WBE, Sw, Ger.W`; `article` optional, e.g. `code=BW, article=4.71`). Returns the canonical Justel URL on ejustice.just.fgov.be with an article anchor where supported. A2A: `be.legal.lookup`.
- Dutch statute → `nl_legal_lookup` (`code` required — `BW4, Successiewet, Wet IB 2001, Wet OB 1968, BW6, Awb, Sr, Rv`; `article` optional, e.g. `code=BW4, article=4:63`). Returns the wetten.overheid.nl URL. A2A: `nl.legal.lookup`.
- Unknown reference → `legal_search` (`keyword` required, `limit` optional). Returns a Justel search URL plus code hints; it does **not** return result rows (Justel results are JS-rendered), so follow up with `legal_lookup`. A2A: `be.legal.search`.

## Read the text — `legal_read`

Input: `url` (required; must be on the allowlist of official sources such as ejustice.just.fgov.be or eur-lex.europa.eu), `max_chars` optional. Returns cleaned full text, HTML or PDF, capped at 30,000 characters — page long documents yourself or quote the relevant article only. A2A: `be.legal.read`.

## Verify before you cite — A2A only: `legal.citation.verify`

Accepts a Belgian/EU ECLI, a CELEX number, a Belgian statute article (e.g. `art. 4.71 BW`) or a Flemish tax ruling number (`VB 25117`) and returns a verdict — `verified / resolvable / malformed / unsupported` — with the canonical URL. There is no MCP tool for this; call it over A2A as a `kind:"data"` part. Use it on every citation an LLM produced before it reaches a file; the skill is tagged `anti-hallucination` for that reason.

## Rules

- All tools are idempotent and read-only; retry on timeout.
- Watch `RateLimit-Remaining`; on `429 RATE_LIMIT_EXCEEDED` wait `Retry-After`.
- A resolver returning a URL proves the identifier is well-formed and routable, not that the cited passage says what you think — read it with `legal_read`.
