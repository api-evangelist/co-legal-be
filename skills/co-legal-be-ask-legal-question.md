---
name: co-legal-be-ask-legal-question
description: Ask Co-Legal's public A2A agent an informational Belgian/Dutch private-client legal or fiscal question in Dutch, French or English, continue the conversation multi-turn, ground the answer in public sources with corpus search, and respect the provider's rate limits and no-advice boundary.
api: a2a/co-legal-be-agent-card.json
surface: a2a
operations:
  - message/send
  - message/stream
  - tasks/get
  - tasks/cancel
a2a_skills:
  - answer_legal_question
  - be.legal.corpus.search
  - be.legal.corpus.read
  - be.fiscal.erfbelasting
method: generated
generated: '2026-09-19'
grounding: Skill ids, input/output modes, examples and the sources/category/jurisdiction enums are quoted from a2a/co-legal-be-agent-card.json and its tool-schema/v1 extension (2026-09-19); the JSON-RPC methods and required header are those the provider lists in its llms.txt, agents.txt and payment-options.json.
---

# Ask Co-Legal's public agent a legal or fiscal question

Endpoint `POST https://agent.co-legal.be/a2a/jsonrpc`. Send `Content-Type: application/json` and **`A2A-Version: 1.0`** on every call — without the header the server assumes 0.3 and answers `-32009 VERSION_NOT_SUPPORTED`. Anonymous is fine; an optional `x-api-key` (by email) only raises the quota.

Before you start, fetch and verify the card at `https://agent.co-legal.be/.well-known/agent-card.json` — it is JWS-signed (ES256) against `/.well-known/jwks.json`, so you can prove the endpoint and skills below were published by the key holder.

## 1. Ask — skill `answer_legal_question`

`message/send` with a `kind:"text"` part (input mode `text/plain`), in Dutch, French or English, up to 8,000 characters. The card's own examples: "Wat is de erfbelasting voor kinderen in Vlaanderen?", "Welk minimumkapitaal heeft een BV onder de WVV?", "How does the VLABEL advance-ruling procedure work for a Belgian BV?", "Hoe werkt de Nederlandse erfbelasting (Successiewet)?".

```
{"jsonrpc":"2.0","id":1,"method":"message/send",
 "params":{"message":{"parts":[{"kind":"text","text":"Wat is erfbelasting in Vlaanderen?"}]}}}
```

The answer is `text/plain` with references to public sources (VCF, WIB92, WVV, BW, Successiewet, EUR-Lex, case law). Prefer `message/stream` (SSE) for long answers — `capabilities.streaming` is true. The model behind it is disclosed in the card (`claude-opus-5` via Google Cloud Vertex AI, processing region EU).

## 2. Continue — multi-turn

Reuse the `taskId` from the first response in the next `message/send`. Task state lives 24 hours (idle TTL) in the provider's EU database; there is no other conversation store. `tasks/get` re-reads a task; `tasks/cancel` stops an in-flight one — it has nothing else to undo, because the agent never mutates anything.

## 3. Ground it — `be.legal.corpus.search` then `be.legal.corpus.read`

Send a `kind:"data"` part `{"query": "...", "max_results": 6}` (query 3–2,000 chars; `max_results` 1–25). Narrow with `sources` (up to 12 of `belgisch_staatsblad_scrape, eurlex_api, fiscale_rulings, fod_financien_circulaires, grondwettelijk_hof_mbbs, juportal_scrape, justel_scrape, kbo_bedrijven, nbb_jaarrekeningen, ovb_deontologie, vlaamse_codex_api, vlabel_rulings`), `category` (`administrative_guidance, case_law, financial_filing, legislation, official_publication, registry, ruling`), `jurisdiction` (`belgium, eu, flanders`), `date_from`/`date_to`, `prefer_recent`. Values outside the allowlist are rejected and reported.

Read a hit with `be.legal.corpus.read` by `document_id`, following `next_cursor` on the same corpus version until it is `null` — the skill says so to avoid silent truncation.

For Flemish inheritance-tax brackets specifically, call `be.fiscal.erfbelasting` (optional `categorie`); it parses the in-force VCF art. 2.7.4.1.1 live, "never from model memory".

## Boundaries the provider states

- Informational only; no attorney-client relationship, no privilege, no advice — a licensed advocaat, notary or tax adviser must review before anyone relies on it (`https://agent.co-legal.be/legal/terms`).
- Do not send client secrets or dossier contents: a scrubbed 160-character preview of each question is logged for up to 90 days.
- Limits: 600 questions/hour/IP, burst 120 — read `RateLimit-*`; on `429 RATE_LIMIT_EXCEEDED` honour `Retry-After`.
- No premium databases (Jura, monKEY, Stradalex) and no client files are reachable through the public agent.
