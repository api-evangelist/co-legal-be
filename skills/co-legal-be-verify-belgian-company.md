---
name: co-legal-be-verify-belgian-company
description: Verify a Belgian counterparty before a transaction — resolve its KBO/BCE enterprise number to the registered entity, confirm its EU VAT number against VIES, and check the structure of the IBAN it gave you — using Co-Legal's free, anonymous, read-only MCP tools (or the identical A2A skills).
api: mcp/co-legal-be-mcp-tools.json
surface: mcp (a2a equivalents noted)
operations:
  - kbo_lookup
  - vies_validate
  - iban_validate
a2a_skills:
  - be.kbo.lookup
  - be.vies.validate
  - iban.validate
method: generated
generated: '2026-09-19'
grounding: Every tool name above exists verbatim in the live tools/list saved at mcp/co-legal-be-mcp-tools.json (2026-09-19); every A2A skill id exists in a2a/co-legal-be-agent-card.json. Parameter names and constraints are quoted from those documents.
---

# Verify a Belgian company with Co-Legal

No key, no signup, no cost. Endpoint `POST https://agent.co-legal.be/mcp` (Streamable HTTP, POST only, `Accept: application/json, text/event-stream`). Every tool here is declared `readOnlyHint: true`, `idempotentHint: true` — retry freely after a timeout. Answers are informational and cite the official source; they are not legal advice.

## 1. Resolve the enterprise number — `kbo_lookup`

Input: `enterprise_number` (string, required, 10–16 characters — "Belgian KBO/BCE number, 10 digits (dots/spaces ok)", e.g. `0403.170.701`).

Returns the official name, status, legal form and start date from the public KBO register, with the source URL. Check `status` is active before going further; a struck-off entity will still resolve.

A2A equivalent: skill `be.kbo.lookup`, sent as a `kind:"data"` part `{"enterprise_number": "..."}` to `POST https://agent.co-legal.be/a2a/jsonrpc` with the mandatory `A2A-Version: 1.0` header.

## 2. Confirm the VAT number — `vies_validate`

Input: `vat` (string, required; example `BE0403170701` — a Belgian VAT number is `BE` + the same ten digits with the dots removed).

Returns validity against the official EU VIES service plus, where the Member State exposes it, the registered trade name and address. Compare the name with step 1; a mismatch is a finding, not an error. VIES is a live upstream (`openWorldHint: true`): a transient failure there is not a "no".

A2A equivalent: skill `be.vies.validate`.

## 3. Check the account number — `iban_validate`

Input: `iban` (string, required).

Pure compute — ISO 13616 check digits via MOD-97 plus the country length. The tool "confirms well-formedness, not that the account exists or is active", so treat a pass as "not obviously mistyped", never as "belongs to this company".

A2A equivalent: skill `iban.validate` (tagged `source:deterministic`).

## Limits and errors

- Anonymous per-IP fair-use bucket: read `RateLimit-Limit` / `RateLimit-Remaining` / `RateLimit-Reset` (and `X-RateLimit-*`) on every response; the landing page states 600 questions per hour per IP with a burst of 120. On `429 RATE_LIMIT_EXCEEDED` honour `Retry-After`.
- Errors are JSON-RPC 2.0 objects whose `data[0].reason` is the machine discriminator (see `errors/co-legal-be-problem-types.yml`).
- Do not put client secrets or file contents into any request; the provider logs a scrubbed 160-character preview of questions for 90 days.
