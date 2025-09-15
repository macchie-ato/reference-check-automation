# 📄 Reference Check Automation

This project automates a multi-step reference check process using Google Forms, Sheets, Docs, Drive, and Slack. Designed to minimize manual tracking and reduce turnaround time, while giving recruiters visibility and control at every step.

---

## ✨ Features

- ✅ **Prefill Form Links** using candidate metadata from Sheets
- ✅ **Auto-Writeback** of Form Responses to the master tracker
- ✅ **Generate PDFs** using conditional templates (Peer vs Manager)
- ✅ **Slack Notifications** to assigned recruiters (with email fallback)
- ✅ Modular, idempotent, and scoped to prevent duplicates

---

## 📁 Folder Structure

| Folder | Description |
|--------|-------------|
| `scripts/` | Google Apps Script modules (`prefill`, `writeback`, `pdf`, `slack`) |
| `assets/` | Sample form, PDF output, Slack previews, diagrams |
| `README.md` | You're reading it ✨ |

---

## ⚙️ Modules Overview

### 🧩 `prefill.onEdit.gs`
- Trigger: `onEdit`
- Checks if key fields are filled → Generates Record ID + Prefill Link
- Writes status as `Invited`

### 🧩 `writeBack.onFormSubmit.gs`
- Trigger: `onFormSubmit`
- Locates candidate row via Record ID
- Stamps submission metadata (timestamp, responder, raw JSON)
- Verifies responses and gates next steps

### 🧩 `generatePDF.gs`
- Trigger: manual or timed
- Selects template based on reference type (Peer vs Manager)
- Builds PDF → saves to Drive folder → writes back URL

### 🧩 `notifySlack.gs`
- Trigger: time-based or chained
- DMs recruiter with PDF link and summary
- Falls back to email if Slack ID is not mapped

---

## 🧪 Example Files (Add to `assets/`)

| Preview | Type |
|---------|------|
| `sample-form.png` | Google Form Screenshot |
| `sample-pdf.png` | Final Reference PDF |
| `slack-message.png` | Slack DM Example |
| `flowchart.png` | System Flow Diagram (optional) |

---

## 💡 Notes & Best Practices

- Use `PropertiesService` for tokens (Slack, Drive)
- Avoid inline secrets (no hardcoded tokens!)
- Maintain a central `config.gs` for shared constants
- Store PDF files in structured Drive folders: `/RefChecks/{Job}_{Candidate}`
- Add validation sections in Google Forms for internal logic

---

## 🖤 Built with care for busy recruiters, TA leads, and HR teams that deserve better tools.
