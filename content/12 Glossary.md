---
tags: [orra-erp, glossary, reference]
aliases: [Glossary, Terms, Acronyms, Technical Words]
---
# Glossary — Technical Words and Acronyms

Up: [[00 Start Here]]

> [!info] What this page covers
> Every acronym, status code and technical term used across this vault and the [[11 System Flowchart]] / `System Flowchart.canvas`, explained in plain language. Organized by category — use Ctrl/Cmd+F to jump to a term.

---

## 1. Construction & Project Documents

| Term | Meaning |
|---|---|
| **RFI** | Request for Information — a question raised (usually by the PM or an Engineer) asking the Architect or Consultant to clarify something about the design. Answered with free text; no approve/reject outcome. |
| **RFA** | Request for Approval — a request that needs a formal decision, not just an answer. The responder must choose one of three outcomes: **approved**, **approved as noted**, or **rejected**. |
| **Returned document** | For a decided RFA only: a record of when the physical/hard-copy document came back from the contractor's staff (who returned it, their position, and the date). This is a paper-trail step that happens *after* a decision — not a rejection or a block. |
| **NOA** | Notice of Award — the document confirming the project/contract was awarded; uploaded by the PM or Admin during the Proposal phase. |
| **NTP** | Notice to Proceed — the document authorizing construction to begin; uploaded by the PM during Pre-Construction, along with the site's coordinates. |
| **COC** | Certificate of Completion — the document certifying the project is finished; uploaded during Closeout. |
| **DSR** | Daily Site Report — a report Site Personnel submit each day describing work done on site. |
| **DTR** | Daily Time Record — the attendance record created each time staff clock in (whether at the office or on site). |
| **DAR** | Document Access Request — submitted when a user wants to open a file (Confidential or Restricted) they don't already have access to; an Admin grants or denies it. |
| **Transmittal** | A formal cover record for sending a set of documents to named recipients, tracked separately from RFI/RFA — it has its own create → issue → acknowledge cycle. |
| **BCR** | Budget Change Request — raised by an Engineer when a change affects the project budget; reviewed by Finance and approved or rejected by the PM through the Workflow Engine. |
| **Milestone** | A dated checkpoint in a project's schedule (e.g. "Foundation complete"); the PM creates, activates and closes these during Pre-Construction and Construction. |

## 2. Lifecycle Phases & Gate Codes

The project lifecycle moves through six phases: **Proposal → Design → Pre-Construction → Construction → Closeout → Completed → Archived** (with **On Hold** and **Cancelled** as side branches). Each phase has "gates" — conditions that must all be true before the project can advance to the next phase.

| Code range | Phase | What the gates check |
|---|---|---|
| **P1–P5** | Proposal | Architect staffed, Consultant staffed, proposal submitted, proposal approved, contract value set |
| **D1–D3** | Design | Design files uploaded with an assigned engineer, all designs approved with no pending review, blueprint uploaded and marked Current + Approved |
| **DP1–DP2** | Design Delivery track (Design-only projects) | Lead assigned, design files uploaded |
| **C1–C6** | Pre-Construction | Requirements approved, budget approved, milestones active, site staffed, tasks assigned, purchase requests created |
| **K1–K4** | Construction (exit) | All tasks completed, milestones closed, issues resolved, active workflows managed |
| **X1–X6** | Closeout | Final inspection approved, COC uploaded, closeout payroll approved, closeout workflow started, no open design requests, all purchase requests/orders settled |
| **T1–T5** | Turnover (Design Delivery track's closeout) | Document on file, client accepted, workflow done, no open requests, settled |

## 3. Roles

| Term | Meaning |
|---|---|
| **PM** | Project Manager |
| **HR** | Human Resources |
| **Finance / Finance Manager** | Manages budgets, purchase requests, orders, payroll approval |
| **IT Designer** | Manages user accounts, roles, audit logs, support requests — **not** the same as a design "Architect" |
| **Admin** | Company-wide overrides, archiving, workflow templates, break-glass access |
| **Owner** | Read-only oversight of everything, plus purge/legal-hold approval |
| **DCO** (Document Control Officer) | A role **proposed for Orra-ERP only** — it does **not** exist in the actual EasyConstruct thesis code's 10 role IDs. Don't confuse it with a real, implemented role. |

## 4. Purchasing & Procurement

| Term | Meaning |
|---|---|
| **PR** | Purchase Request — raised by an Engineer or PM when material/service is needed; goes through PM endorsement then Finance approval (or rejection, which is final — a rejected PR cannot be revised, only re-created). |
| **Order / Procurement Order** | A *separate* record created by Finance only after a PR is approved. Goes through ship → deliver → pay, and can be cancelled, resumed, or voided. The person who delivers an order can never be the same person who created the PR. |
| **Settled** | A PR or order is "settled" once it's been paid/completed — all PRs and orders must be settled before a project can close out (gate X6). |

## 5. Technical / Software Terms

| Term | Meaning |
|---|---|
| **JWT** (JSON Web Token) | The security token issued when a user logs in; proves who they are on every request afterward without re-entering a password. |
| **SSE** (Server-Sent Events) | A one-way live connection from server to browser used for the notification feed — the server pushes new notifications to you instantly instead of your browser having to keep asking. |
| **SHA-256** | A one-way mathematical fingerprint computed for every uploaded file, used to verify the file hasn't been altered (the fingerprint is checked again on every download). |
| **AES-GCM** | The encryption method used to scramble "Restricted" files before they're stored, so only authorized users can unscramble (decrypt) them. |
| **API** | Application Programming Interface — the set of web addresses (endpoints) the frontend calls to read or change data on the server. |
| **CRUD** | Create, Read, Update, Delete — the four basic operations most records in the system support. |
| **Webhook / SMTP** | SMTP is the protocol used to send emails (password resets, request notifications, client replies). |
| **Workflow template** | A reusable, multi-stage approval sequence (8 are seeded by default) that Admins can create; each stage names a role that must act before the workflow can move on. |
| **Break-glass role** | A role (usually Admin) given access to an action as a backup/emergency path, even though it isn't the role's normal job — used so nothing gets permanently stuck if the usual actor is unavailable. |
| **Quartz** | The static-site generator used to publish this Obsidian vault as the public wiki (`nhyl-beta.github.io/orra-erp-wiki`). |
| **JSON Canvas** | The open file format behind Obsidian's `.canvas` files (like `System Flowchart.canvas`) — a spatial board of boxes and arrows, stored as plain JSON. |
| **Gate** | A named, automatically-checked condition (see section 2) that must pass before a project phase can advance — distinct from a manual approval. |
| **Advisory signal** | One of 8 automated background checks (cost variance, burn vs progress, overdue tasks, etc.) that flag risk without blocking anything — purely informational. |

---
Back to: [[00 Start Here]] · Full flow: [[11 System Flowchart]]
