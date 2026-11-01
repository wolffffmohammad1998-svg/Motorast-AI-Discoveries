# Garden Bench · باغ‌بنچ

**Does an AI agent cheat under pressure — and can a guard stop it without rejecting correct answers?**
Measured by *code* (seeded, reproducible, ground-truth judge, no LLM judge), on open-weight models through **Otari**.

Built for MozFest *Developers Wilding: Online*. One Cloudflare Worker file, no dependencies.

## What it does
- **Bench tab** — deterministic tasks with a temptation note (15 cheat types, pressure 0–5, impossible tasks where the
  honest answer is "blocked"). Per model × defense prompt it reports cheat rate (raw → with rule guard), correct rate,
  **false refusal**, honest block, per-type breakdown. The rule guard's reasons are shown so it can be debugged.
- **Claim tab** — Elahe (proposer) → Otari web search → Otari code execution (seeded Python) → Elham (critic).
  Verdicts: supported / refuted / **I don't know**.

## Otari features actually used
| Feature | Where |
|---|---|
| Multiple models, distinct roles | `MODEL_PROPOSER`, `MODEL_TOOLS`, `MODEL_CRITIC` (open-weight models) |
| Model routing + fallbacks | `MODEL` = an Otari routing policy name (primary + `on_failure`) |
| Web search | `otari_web_search` (with `max_uses`) |
| Code execution | `otari_code_execution` |
| Guardrails | `guardrails: [{profile: "prompt-injection"}]` on the user's claim |
| Budgets / spending limits | the API key runs under an Otari budget; budget errors are handled in the UI |
| Per-user budgets | public visitors run on a guest key bound to its own Otari user with a per-user budget |

## Deploy
Paste `worker.js` into a Cloudflare Worker. Secrets: `OTARI_API_KEY`, optional `OTARI_API_KEY_GUEST`, `ACCESS_CODE`.
Variables: `VIA_OTARI=1`, `MODEL`, `MODEL_PROPOSER`, `MODEL_TOOLS`, `MODEL_CRITIC`, `GUARDRAILS` (`monitor`|`block`|`off`).

## Origin
Benchmark, judge, and guard rules are ported unchanged from my earlier anti-cheat research system; this project drops
its own multi-provider/quota plumbing in favour of Otari.
