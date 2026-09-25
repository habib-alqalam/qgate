# Qalam Gate

Trust layer demo for UAE government documents. One static file — `public/index.html` — with inline CSS and JS. No build step, no framework, no database, no server: samples, rules, the SHA-256 audit chain (Web Crypto), verify and tamper all run in the browser.

> Synthetic data · illustrative rules. Nothing here is a real document or a real government rule.

## Run

Open `public/index.html` in a browser, or serve the folder:

```bash
cd qalam-gate/public && python3 -m http.server 3000
```

Deploy target is the `qalam-gate/public` directory as a static site.

## Samples

`valid`, `expired-passport`, `name-mismatch` — each a passport and an Emirates ID record with English and Arabic names.

## Rules

| id | severity |
| --- | --- |
| `passport-expiry` | critical |
| `eid-expiry` | critical |
| `name-match` (case/space-insensitive) | critical |
| `dob-match` | critical |

Approve is disabled and refused while any critical rule has failed. There is no auto-approve path: reviewer name and reason are always required.

## Audit chain

Every case carries an append-only log — `CaseCreated`, `RulesEvaluated`, `ApprovalRequested`, then `Approved` or `Rejected`. Each entry is chained:

```
hash = sha256([prevHash, seq, ts, actor, action, details].join('|'))
```

"Verify chain" recomputes every hash. "Tamper test" silently edits entry #2, after which verification reports the chain broken at that entry.

## Localisation

The header toggle switches EN ⇄ ع; Arabic sets `dir="rtl"` and translates every label, rule message and audit action.
