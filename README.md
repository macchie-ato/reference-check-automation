# Reference Check Automation

End-to-end reference check workflow using Google Apps Script, 
Google Workspace, SmartRecruiters, and Slack.

---

## The problem

Reference checks are nobody's favourite part of the hiring process. 
In most teams they look like this: recruiter emails candidate asking 
for referee details, candidate replies eventually, recruiter emails 
each referee separately, chases the ones who don't respond, manually 
copies answers into a spreadsheet, formats a summary doc, sends it 
to the hiring manager. Repeat for every hire.

It's not complicated work. It's just a lot of steps that all depend 
on someone remembering to do the next thing. Which means it's slow, 
inconsistent, and the first thing that gets dropped when a recruiter 
is juggling five open roles.

This project automates the whole thing. The recruiter triggers it 
once. Everything else runs itself.

---

## How it works

The workflow is split into five sequential steps. Each one only runs 
if the previous one completed successfully — nothing fires twice, 
nothing skips ahead.

**Step 1 — Prefill link generation**
When a recruiter marks a candidate row in the masterlist, the script 
auto-generates a prefilled Google Form link scoped to that candidate. 
No manual copy-pasting of URLs.

**Step 2 — Candidate submits referee details**
The candidate fills out the form with referee names, job titles, and 
contact details. This replaces the email thread that would normally 
take two to three days.

**Step 3 — Referee forms go out**
On submission, the system generates a separate prefilled form for 
each referee and sends it automatically. Responses write back to 
the correct row in the masterlist in real time.

**Step 4 — PDF generation**
Once all referee responses are verified, a formatted PDF is built 
from a Google Docs template and saved to a structured Drive folder 
organised by job ID and candidate name.

**Step 5 — Recruiter notification**
A Slack DM goes to the requesting recruiter with a direct link to 
the completed report. Falls back to email if the Slack DM fails.

---

## Stack

- Google Apps Script (all automation logic)
- Google Sheets (masterlist and tracker)
- Google Forms (candidate and referee inputs)
- Google Docs + Drive (PDF generation and storage)
- SmartRecruiters (source of candidate data)
- Slack (recruiter notifications)

---

## Structure

reference-check-automation/
├── scripts/
│   ├── config.gs              # Central config — IDs, tab names
│   ├── module1_prefill.gs     # Prefill logic on edit/open
│   ├── module2_emailDraft.gs  # Draft email with prefilled link
│   ├── module3-1_verify.gs    # Write-back from form to masterlist
│   ├── module3-2_pdfGen.gs    # PDF builder from template
│   ├── module3-3_notify.gs    # Slack DM with email fallback
│   └── utils.gs               # Shared helpers
├── assets/                    # Redacted screenshots and flowchart
└── README.md

---

## Setup

1. Copy the Sheet, Form, and Docs templates into your own Drive
2. Open config.gs and add your Sheet ID, Form ID, and Folder ID
3. Add your Slack bot token via Script Properties — not hardcoded
4. Edit the referee form templates if needed (peer vs. manager 
   versions included)
5. Set up triggers: onEdit, onFormSubmit, and time-based as needed
6. Run a test with dummy data before going live

Real credentials have been stripped from all scripts. Use Script 
Properties for anything sensitive.

---

## What it doesn't do yet

There's no automated chasing built in. If a referee doesn't respond, 
someone still has to follow up manually. The next version will add 
time-based reminder emails to non-responding referees, with an 
escalation to the recruiter if they still haven't replied after a 
second nudge.

---

## Links

- Portfolio: https://macchie-ato.github.io
