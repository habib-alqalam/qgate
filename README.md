# Qalam Gate

Trust layer for UAE government document workflows: bilingual AR/EN rule checks on passports and Emirates IDs, a human approval gate that refuses to sign off on critical failures, and a SHA-256 hash-chained, tamper-evident audit trail.

Built with Devin for Fish Tank × Hub71.

> Synthetic data · illustrative rules. Nothing here is a real document or a real government rule.

## Live demo

https://public-viuntisf.devinapps.com

## Run locally

```bash
python3 -m http.server 8080 --directory qalam-gate/public
```

Then open http://localhost:8080. Serve it rather than opening the file directly — the audit chain uses Web Crypto, which needs localhost or HTTPS.

## What it does

- **Rule checks** — passport expiry, Emirates ID expiry, EN/AR name match, date-of-birth match, each with a severity.
- **Human gate** — a named reviewer and a written reason are always required; approval is refused while any critical rule fails.
- **Audit trail** — every event is hash-chained to the previous one. *Verify chain* recomputes the chain; *Tamper test* alters one entry and verification reports exactly where it broke.
- **Bilingual** — EN ⇄ ع toggle, full RTL, including rule messages and audit actions.

One static file, no build step, no backend: [`qalam-gate/public/index.html`](qalam-gate/public/index.html). See [`qalam-gate/README.md`](qalam-gate/README.md) for the rules and chain details.

## Docs

- [SUBMISSION.md](SUBMISSION.md) — hackathon submission: pitch, description, judge walkthrough, how Devin built it.
- [DEMO_SCRIPT.md](DEMO_SCRIPT.md) — 2-minute live demo script.
