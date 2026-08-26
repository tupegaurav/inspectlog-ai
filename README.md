InspectLog
AI-Powered Digital Logbook for Real-Time Manufacturing Quality Control
A lightweight inspection terminal that replaces paper/Excel logbooks on the
shop floor. An inspector logs Check/OK/Rej/Rework counts for a part; an AI
validation agent checks the math and flags anomalies in real time before the
entry is written to the record — no more end-of-shift reconciliation.
How it works
Frontend (this repo) — a single-screen form, styled like a factory
andon/gauge panel, deployed as a static site on GitHub Pages.
Validation + automation — the form POSTs each entry to an
n8n webhook. An AI agent (Groq/LLaMA) checks the entry
against quality-control rules (quantity math, valid part names, typo
detection) and returns a pass/fail verdict with a severity level.
Record — valid entries are appended to a Google Sheet automatically;
invalid entries are rejected with a clear reason, before they ever reach
the log.
```
Inspector fills form → Webhook → AI Agent validates → 
  ├─ valid   → append to sheet   → respond "logged"
  └─ invalid → skip the sheet    → respond with reason
```
Tech stack
Vanilla HTML / CSS / JS (no build step — edit and deploy straight from GitHub)
n8n Cloud for orchestration
Groq (LLaMA / gpt-oss) for validation
Google Sheets as the record store
Files
`index.html` — the inspection form
`style.css` — industrial panel design (andon-light status indicator, gauge-style quantity readouts)
`script.js` — form logic + webhook call. Set your n8n webhook URL at the top of this file.
Status
Proof of concept — actively being wired up and debugged against a real n8n workflow.
