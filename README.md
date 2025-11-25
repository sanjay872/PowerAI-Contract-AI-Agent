# **PowerAI Contract Agent**

AI-powered contract generation system built using **n8n**, **OpenAI**, **Google Docs API**, and **Python micro-webhooks**.
Given simple user inputs, the agent automatically **creates a Google Doc**, **generates contract content using OpenAI**, **exports it to PDF**, **stores metadata in MongoDB**, and exposes webhooks to **retrieve and update contract status**.

> 🔗 **Live Demo (Frontend):** [https://poweraiagent.netlify.app/](https://poweraiagent.netlify.app/)
> 🧩 **Backend / Workflows:** n8n + Python (this repository)

---

## 🚀 **How It Works (High-Level Flow)**

The PowerAI Contract Agent automates contract creation using this workflow:

1. **User submits contract information**

   * A public **n8n webhook** receives contract inputs (names, terms, dates, pricing, clauses, etc.).

2. **Google Docs document is created**

   * A Python Google API helper creates a fresh Google Doc template.

3. **OpenAI generates contract text**

   * Contract content is produced based on the submitted information.
   * Content is inserted into the Google Doc.

4. **Document is exported to PDF**

   * Google Docs → PDF conversion is triggered.
   * The resulting PDF is uploaded to cloud storage.

5. **PDF URL is returned to the user**

   * A webhook responds with the final contract link.

6. **Metadata saved to MongoDB**

   * Each contract includes fields like:

     * `contractId`
     * `user inputs`
     * `generated PDF URL`
     * `current status` (generated, pending approval, approved, changes required)
     * `timestamp`

7. **Additional webhooks provide extra functionality**

   * **Fetch existing contracts**
   * **Update contract status (HITL workflow)**
   * **AI-based review or summary**

---

## 🧠 **Core Features**

### ✅ **AI-Generated Contracts**

Uses OpenAI to generate legally structured contract text based on user-provided metadata.

### ✅ **Google Docs Integration**

* Automatically creates a new Google Doc
* Inserts generated content
* Converts to PDF
* Provides shareable PDF URL

### ✅ **MongoDB Contract Tracking**

Stores:

* Contract details
* Status updates
* Review notes
* PDF links
* Timestamps

### ✅ **Multiple Webhooks**

All functionality is handled by modular n8n + Python endpoints:

| Purpose                | Webhook                  |
| ---------------------- | ------------------------ |
| Create contract        | `/webhook/create`        |
| Get contract by ID     | `/webhook/status`        |
| Get all contracts      | `/webhook/list`          |
| Update contract status | `/webhook/update-status` |
| AI review              | `/webhook/ai-review`     |
| AI summary             | `/webhook/summary`       |

Each webhook is isolated for clarity and reliability.

### ✅ **Simple Frontend Demo**

A lightweight single-file frontend (Netlify-hosted) that:

* Shows the latest contract PDF preview
* Calls AI summary & AI review webhooks
* Allows HITL approval or change requests

## 🌐 **Frontend Demo Endpoints**

The Netlify frontend uses hard-coded endpoints in `index.html`.

```js
// Latest contract status
const STATUS_URL =
  "https://sanjaysakthivel.app.n8n.cloud/webhook/status?id=1hq_Rq_XNm29osZPSHT5E5HJ67JL2lia9";

// AI Review webhook
const AI_REVIEW_URL =
  "https://sanjaysakthivel.app.n8n.cloud/webhook-test/another-ai?id=1hq_Rq_XNm29osZPSHT5E5HJ67JL2lia9";

// Summary webhook
const SUMMARY_URL =
  "https://sanjaysakthivel.app.n8n.cloud/webhook/another-ai?id=1hq_Rq_XNm29osZPSHT5E5HJ67JL2lia9";

// HITL approval:
// GET /webhook/hitl?approved=true|false&comments=...&id=<contractId>
```

---

## 🏗️ **Architecture Overview**

```
User Input → n8n Webhook
       → Python (Google Docs + OpenAI)
       → Google Doc Created
       → AI-generated text inserted
       → Export to PDF + store URL
       → Save metadata in MongoDB
       → Return PDF URL to frontend
```

Additional workflows handle:

* Status retrieval
* AI review
* Summarization
* Human-in-the-loop approvals

---

## 📘 **Tech Stack**

| Component                  | Technology                             |
| -------------------------- | -------------------------------------- |
| Workflow Orchestration     | **n8n**                                |
| AI Text Generation         | **OpenAI GPT-4o / GPT-4o-mini**        |
| Contract Document Creation | **Google Docs API**                    |
| PDF Generation             | Google Drive Export API                |
| Backend Handlers           | Python (Flask/FastAPI style functions) |
| Database                   | MongoDB Atlas                          |
| Frontend Demo              | Plain HTML/CSS/JS + Netlify            |

---

## 🧪 **Future Enhancements**

* Template-based clause insertion
* Multilingual contract generation
* Version history tracking in MongoDB
* Multi-tenant support
* Role-based access for teams
* Email notifications when PDFs are ready

---

## 📜 **License**

MIT License.
