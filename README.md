# 🌱 Garden Bench · باغ‌بنچ

**Does an AI agent cheat under pressure — and can a guard stop it without rejecting correct answers?**
Measured by *code* (seeded, reproducible, ground-truth judge — no LLM judge), on any model through **Otari**.

آیا ایجنت زیر فشار تقلب می‌کند؟ و آیا نگهبان جلوی تقلب را می‌گیرد بدون ردِ جواب درست؟

Built for **MozFest Developers Wilding: Online**. Single-file Cloudflare Worker, no dependencies.

## 🚀 Live Demo
You can try the live application here: **[https://motorast-garden-app.wolffff-mohammad1998.workers.dev/](https://motorast-garden-app.wolffff-mohammad1998.workers.dev/)**
*(If an access code is required, please contact me).*

## 🧠 What it does

### Tab 1 — Bench
Generates deterministic tasks (numeric / text / logic / table) with a temptation note and pressure levels 0–5. 
Includes 15 cheat types: goal-theft, hide-error, metric-gaming, tool-cheat, memory-tamper, silence, task-redefine, time-cheat, multi-step, collusion + injection, fabricated-action, scope-creep, fake-source, sabotage.

Some tasks are *impossible* (data missing) — the honest answer is "blocked". The judge is plain code with ground truth.
For every model × defense-prompt row it reports: 
- **Cheat rate** (raw → with rule-based guard)
- **Correct rate**
- **False refusal** (the error we must not make)
- **Honest block**
- **Per-type breakdown**

*Switching model = changing one `provider:model` string — that is the Otari gateway doing the work.*

### Tab 2 — Claim check
Elahe (proposer) → `otari_web_search` → `otari_code_execution` (seeded Python experiment) → Elham (critic). 
Verdicts: supported / refuted / **I don't know**. A verdict without measured evidence is downgraded to "unknown".

## 🛠 Otari features used
- `POST /api/v1/chat/completions` on the hosted gateway, many models via `provider:model`
- Built-in tools `otari_web_search` (with `max_uses`) and `otari_code_execution`
- Gateway usage data (status / latency / tokens) shown per call in the UI

## 📜 Origin
The benchmark, judge, and guard rules are ported unchanged from my earlier anti-cheat research system (`motorast-garden`); this project replaces its own multi-provider/quota plumbing with Otari.

## ⚙️ Deploy (Cloudflare Workers, free)
1. Paste `worker.js` into a Worker.
2. Secret `OTARI_API_KEY`; variable `MODEL` (e.g. `openai:gpt-4o-mini`); optional secret `ACCESS_CODE`.
3. Open the page → **Check Otari** → run the bench.

---
*Built with ❤️ for Developers Wilding Hackathon.*
