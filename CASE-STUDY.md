# Case Study: Reference Check Automation

## The problem

Reference checks were the part of the hiring process everyone 
dreaded. A recruiter would manually email a candidate asking for 
referee details, wait for a reply, then email each referee 
individually with a list of questions, wait again, chase anyone 
who didn't respond, manually copy responses into a tracker, 
format a summary, and finally send it back to the hiring manager.

Every step was manual. Every step introduced delays. A process 
that should take 24–48 hours regularly stretched to a week or 
more — not because anyone was slacking, but because it was 
entirely dependent on people remembering to follow up.

The data was also inconsistent. Different recruiters asked 
different questions, formatted responses differently, and stored 
them in different places. There was no single source of truth.

---

## What I built

An end-to-end automated reference check workflow that handles the 
entire process from candidate submission to recruiter notification 
— without anyone needing to chase, copy-paste, or manually format 
a document.

The workflow runs on Google Apps Script and connects Google Sheets, 
Forms, Docs, Drive, and Slack. It's modular by design — each step 
is a separate script that only fires when the previous one is 
verified complete.

**Stack:** Google Apps Script · Google Workspace (Sheets, Forms, 
Docs, Drive) · SmartRecruiters · Slack

---

## How it works

1. **Recruiter triggers the process** — A candidate row in the 
masterlist sheet is updated, which auto-generates a prefilled 
Google Form link for that specific candidate

2. **Candidate submits referee details** — They fill out the form 
with referee names, roles, and contact info. No back-and-forth 
emails needed

3. **Referee forms go out automatically** — On form submission, 
the system generates prefilled referee forms (one per referee) 
and sends them out. The masterlist updates in real time

4. **Responses write back to the tracker** — When a referee 
submits, their responses are automatically verified and written 
back into the correct row and columns in the masterlist

5. **PDF report is generated** — Once responses are verified, 
a formatted PDF is created from a Google Docs template and saved 
to a structured Drive folder (organised by job ID and candidate 
name)

6. **Recruiter gets a Slack notification** — A direct message is 
sent to the requesting recruiter with a link to the completed 
report. Falls back to email if the Slack DM fails

Each step is gated — no Slack notification unless the PDF exists, 
no PDF unless the form submission is verified. Nothing runs twice.

---

## The result

What used to take 3–5 days of back-and-forth now completes in 
hours, with zero manual chasing required from the recruiter. 
The output is consistent every time — same format, same questions, 
same filing structure — regardless of which recruiter runs the 
process.

The recruiter's only job is to trigger the process and wait for 
the Slack notification.

---

## What I'd build next

The current version handles the core flow well, but there's no 
automated chasing yet. If a referee doesn't respond within 48 
hours, someone still has to follow up manually. The next version 
would add time-based triggers that send reminder emails to 
non-responding referees at set intervals — and escalate to the 
recruiter if they still don't respond after a second nudge.

---

## Links

- [GitHub repo + full code](https://github.com/macchie-ato/reference-check-automation)
- [Back to portfolio](https://macchie-ato.github.io)
