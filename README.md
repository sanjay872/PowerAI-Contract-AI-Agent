# PowerAI Contract Agent — Demo

**Live demo:** https://poweraiagent.netlify.app/

A tiny, pretty single-file frontend that previews your latest contract PDF and talks to n8n webhooks for summary, AI review, and HITL (approve/changes).

---

## What it does

- **Loads latest contract** from a hard-coded n8n **status** URL and shows a Google Drive **PDF preview**.
- **Generate Summary** calls a hard-coded **summary** webhook and prints the result in the UI.
- **AI Review Again** calls a hard-coded **AI review** webhook and prints the result.
- **HITL Approve / Request Changes** (optional) calls your HITL webhook.

---

## Hard-coded endpoints (in `index.html`)

```js
// Latest contract status (single object expected)
const STATUS_URL   = "https://sanjaysakthivel.app.n8n.cloud/webhook/status?id=1hq_Rq_XNm29osZPSHT5E5HJ67JL2lia9";

// AI review (used by “AI Review Again”)
const AI_REVIEW_URL = "https://sanjaysakthivel.app.n8n.cloud/webhook-test/another-ai?id=1hq_Rq_XNm29osZPSHT5E5HJ67JL2lia9";

// Summary (used by “Generate Summary”)
const SUMMARY_URL   = "https://sanjaysakthivel.app.n8n.cloud/webhook/another-ai?id=1hq_Rq_XNm29osZPSHT5E5HJ67JL2lia9";

// Optional HITL endpoint used by Approve / Request Changes buttons:
// GET <base>/webhook/hitl?approved=true|false&comments=...&id=<filter_id?>
