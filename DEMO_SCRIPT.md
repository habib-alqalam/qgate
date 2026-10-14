# Qalam Gate — 2-minute live demo script

**Before you start:** open https://public-viuntisf.devinapps.com in a full-screen browser window, valid sample loaded, Arabic toggle showing **ع**.

---

**0:00–0:15 — The problem**

> *(demo on screen, don't click yet)*
> "Every UAE service desk checks passports and Emirates IDs by hand, in Arabic and English. AI can read them in seconds — but no regulator accepts a decision it can't inspect, and no official signs a black box. Qalam Gate is the layer that makes the AI decision defensible."

**0:15–0:30 — Bilingual by default**

> *Click **ع**.*
> "One toggle: full Arabic, right-to-left — labels, rule messages, and the audit log itself, not just the buttons."
> *Click **EN**.*

**0:30–0:55 — The rules are explicit**

> *Click the **expired-passport** sample.*
> "Four rules run on every case: passport expiry, Emirates ID expiry, name match across Arabic and English, and date of birth. Here the passport has expired — flagged red, and marked critical."

**0:55–1:20 — The human gate**

> *Type a reviewer name and a reason, click **Approve**.*
> "Now I try to approve it as a reviewer. Refused. There is no auto-approve path in this system, and a critical failure can't be signed away."
> *Click **Reject**.*
> "The rejection is recorded — with who, and why."

**1:20–1:40 — A clean approval**

> *Click the **valid** sample, enter reviewer name and reason, click **Approve**.*
> "A clean case goes through — still with a named human and a written reason."

**1:40–2:00 — Tamper-evident audit**

> *Scroll to the audit trail, click **Verify chain**.*
> "Every step is hash-chained with SHA-256, each entry sealing the one before it. Verify: intact."
> *Click **Tamper test**, then **Verify chain**.*
> "Now I silently edit one entry. Verification points straight at entry #2. You can't quietly rewrite what happened."

**Close (if time allows)**

> "Built end to end with Devin in one afternoon: Devin wrote it, reviewed its own PR and fixed four correctness bugs, tested it in a real browser, deployed it, and documented it — in parallel sessions."

---

**Fallback if the live link is down:** run locally with
`python3 -m http.server 8080 --directory qalam-gate/public` and open http://localhost:8080.
(Web Crypto needs localhost or HTTPS — don't open the file directly with `file://`.)
