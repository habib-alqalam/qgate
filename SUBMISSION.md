# Qalam Gate

**A trust layer that makes AI document checks safe enough for government use: bilingual rule checks, a human approval gate, and a tamper-evident audit trail.**

## Description (for judges)

Government service desks in the UAE verify passports and Emirates IDs by hand, in English and Arabic. AI can read those documents in seconds, but a regulator cannot accept a decision it cannot inspect, and no official will sign off on a black box.

Qalam Gate is the layer between the model and the decision. Every case runs explicit rules — expiry, name match across EN/AR, date-of-birth match — and each result is shown with its severity, in Arabic or English with full RTL. Approval is never automatic: a named reviewer must give a reason, and approval is refused outright while any critical rule fails. Every step is written to a SHA-256 hash-chained audit log that anyone can re-verify, and the built-in Tamper test proves a single altered entry breaks the chain.

For government entities, regulated banks, and any team that must defend an automated decision.

*Synthetic data, illustrative rules.*

## Live demo

https://public-viuntisf.devinapps.com

## 60-second judge walkthrough

1. Open https://public-viuntisf.devinapps.com — the **valid** case is loaded, all rules pass.
2. Click **ع** in the header — the whole interface flips to Arabic RTL: labels, rule messages, audit actions.
3. Click **EN** to switch back.
4. Click the **expired-passport** sample — the passport expiry rule turns red and is marked *critical*.
5. Type a reviewer name and a reason, then click **Approve** — approval is refused: critical failures block sign-off.
6. Click **Reject** — the decision is recorded with the reviewer's name and reason.
7. Click the **valid** sample, enter a reviewer name and reason, and click **Approve** — this time it goes through.
8. Scroll to the **Audit trail** — CaseCreated, RulesEvaluated, ApprovalRequested, Approved, each with its own hash linked to the previous one.
9. Click **Verify chain** — every hash recomputes, the chain is intact.
10. Click **Tamper test**, then **Verify chain** again — verification reports the chain broken at entry #2.

## How Devin built this

Only capabilities actually used on this repo:

- **Built in a Devin session** — the whole demo (rules engine, EN/AR localisation, hash chain, UI) written by Devin from a prompt, shipped as one dependency-free static file.
- **E2E UI testing with recordings** — Devin drove the running app in a browser and recorded it; the runs caught and fixed 2 UI bugs (a stale decision message persisting across sample switches, and an untranslated audit label in Arabic).
- **Devin Review** — Devin reviewed its own PR #1 and flagged real correctness bugs (expiry off by a day, rules cached at sign-off, double-click corrupting the audit chain, a sample-switch race); all were fixed in PR #2.
- **Repo setup and knowledge** — Devin configured the repo environment (static server on port 8080, Web Crypto needs localhost/HTTPS) so every later session starts ready to run.
- **devinapps deploy** — the live link above is a Devin-deployed static build.
- **Parallel Devin sessions** — one session built and fixed the app while a second wrote these submission docs, both landing as separate PRs.

## Judging criteria

- **Innovation** — the missing piece in gov AI is not extraction, it is provable accountability: hash-chained audit plus an enforced human gate.
- **Practicality** — runs anywhere with one command, no backend, no data leaves the browser; rules and samples map to real passport/Emirates ID fields.
- **Demo quality** — 60 seconds, three visible proofs: Arabic RTL, blocked approval, broken chain.
- **Devin use case** — build, review, browser test, deploy and document, across parallel sessions.
