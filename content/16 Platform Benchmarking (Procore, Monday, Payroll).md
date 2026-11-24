---
tags: [orra-erp, benchmarking, procore, monday, payroll, ui-ux]
aliases: [Platform Benchmarking, Procore Monday Payroll, Reference Systems]
Up: [[00 Start Here]]
---

# Platform Benchmarking (Procore, Monday.com, Payroll Providers)

> [!summary]
> Three outside systems used as reference points, each for a specific gap in Orra-ERP: **Procore** for a vendor-neutral construction *business-process* skeleton (not just what one client interview captured), **Monday.com** for closing the computer-literate/non-technical UI gap and for consolidated reporting, and **ADP/Gusto/QuickBooks Payroll** combined into one improved payroll design for Orra. See also [[14 Interview Integration Plan (11-11-26)]] (client-stated requirements) and [[11 System Flowchart]] (current Orra flow).

## 1. Procore — construction business-flow alignment

### Why this matters more than the interview transcript alone
The 11 Nov interview ([[14 Interview Integration Plan (11-11-26)]]) captures what *this one client* asked for, filtered through one conversation. Procore's phase model is an industry-standard construction business flow, independent of any single client's memory or phrasing — useful as a neutral checklist to sanity-check Orra's own stage list in [[11 System Flowchart]], rather than building only off what got mentioned in the room.

### The reference process (phase by phase)
Procore's own construction project lifecycle breaks into five phases — initiation, planning, execution, monitoring and closure — and Procore's published Project Manager Process Guide lays out what sits inside each one:

| Phase | What happens | Orra equivalent today |
|---|---|---|
| Pre-Con & Estimating | Bid review, prequalification, pre-bid RFIs, addenda | Proposal/BOQ/estimation module |
| Contract Award | Role overview, external communications, contract issuance | Contract + NOA (basis-of-truth doc) |
| Project Planning & Scheduling | Purchase order workflow, project documents, site meetings | Project registry, document vault |
| Execution | RFIs, submittals, change process, payment process, safety, notifications | RFA workflow, PR/PO settlement, notifications |
| Closeout | Final inspections, as-builts, O&M manual, Certificate of Substantial Performance, final billing, subcontractor closeout | Final Inspection Approved, COC, Closed Milestone |

A standardized workflow makes recurring processes (like getting contractors paid) easier to fill and track and eliminates delays from formatting mistakes or missing information, and a workflow takes a phase of a project, defines the required tasks, puts them in order, and establishes who's responsible for each one — which is exactly the "basis of truth" chain already documented for Orra (Approved Proposal → Contract+NOA → NTP → Approved Budget → RFA decision → Final Inspection → COC).

**Action item:** walk the stage list in [[11 System Flowchart]] against this table and flag any gap (e.g. nothing in Orra currently maps to a formal "pre-bid RFI" or "subcontractor closeout" step) — not necessarily to build it, but to consciously decide it's out of scope rather than it being an accidental omission.

### Procore's UI/UX — what to copy and what to avoid
Reviews are split in a way that's directly useful:

- **On the "copy this" side:** many users describe Procore as having a clean and intuitive interface that makes it easy to use, even for those with limited technical knowledge, and reviewers specifically credit a mobile-first design that lets field crews upload photos and daily logs effortlessly.
- **On the "avoid this" side:** just as many reviewers say the opposite — Procore's interface centralizes project data but often overwhelms new users with layered menus and terminology that can slow down navigation, and independent summaries note users find the learning curve steep for new users despite the interface being generally intuitive. One reviewer put it bluntly: being a catch-all platform for construction management, its interface may not be as user-friendly as software that focuses on just one aspect.
- Even Procore's own recent work is an admission of this: they've been running a redesign specifically to modernize an outdated tool with a cleaner interface, and a separate "Redesigned Procore Analytics Interface" project whose stated goal is less time fighting the interface, more time getting your data into the tools your business runs on.

**Why this matters for Orra:** Procore is the proof case that a platform can be "intuitive" and still fail the exact competency-gap problem the client is trying to solve (see §2) — depth of features and menu layering is the direct cause reviewers cite for the steep learning curve. Procore's phase/workflow *structure* is worth validating against; its UI *density* is the thing to deliberately avoid, since it's optimized for large GC teams with dedicated coordinators, not a small team with mixed technical literacy.

## 2. Monday.com — ease-of-use UI and consolidated reporting

### Ease of use (the UI mechanism, not just "it's simple")
roughly 70% of monday.com's users are classified as non-tech users, and reviewers consistently point to the same three mechanisms rather than vague "simplicity":

1. **Color as the primary status signal** — status lives in colored cells directly on the board, not behind a menu.
2. **Non-imposing data entry** — monday.com's own design rule is that they will never ask a user to add metadata the system needs for its own internal operations; only what the task itself needs.
3. **Drag-and-drop over forms** — reduces the learning curve for new users compared to filling in structured fields.

One G2/TrustRadius reviewer's description is close to a one-line spec for what the client is asking for: very simple to setup and understand the UI across multiple teams, especially for users not tech savvy such as users of Jira or Azure DevOps. The honest trade-off: building effective, well-structured boards requires time and design discipline — which is why, in Orra, that complexity should sit in the *admin/IT configuration layer* (roles, workflow templates), never in the *daily-use screens* for Owner/HR/site staff.

### Consolidated reporting — the specific pattern to borrow
This is the part most directly reusable for Orra's planned Owner and IT dashboards:

- A dashboard pulls data from multiple connected boards and displays it through widgets — teams use monday.com dashboards for an instant summary overview of their projects, making it easy to monitor progress, track performance, and make informed decisions at a glance, with 50+ widget types to view data any way you want (numbers, charts, etc.) pulling from several boards in one place.
- Dashboards are **live and self-maintaining**: dashboards automatically update based on the data living in the boards they're connected to, so there's no need to keep maintaining them manually — a direct answer to the client's "I want it simple" ask, since nobody has to re-build a report each week.
- Widgets are **interconnected**: when one data point is updated, it reflects on other dashboard elements that depend on it — i.e., a single source of truth feeding every view, rather than separate static exports per module.
- Reports are shareable by link or email directly from the dashboard, without needing the recipient to dig through boards themselves.

**Action item for Orra's Owner/IT dashboards** (referenced as "planned, not yet built" in [[14 Interview Integration Plan (11-11-26)]]): design them as live widgets pulling from existing module tables (e.g. "Open RFAs across all projects," "Approved Budget vs Settled PRs," "Pending HR flags," "Document version conflicts") instead of per-module static reports — same underlying data, zero duplicate maintenance, and it directly serves the non-technical Owner persona from the interview who wants a glance-level view, not a drill-down tool.

## 3. Payroll — combined improvement plan for Orra

The CPA-review video itself wasn't retrievable (YouTube blocked content access; only metadata came through, and the video carries referral/affiliate links for all three providers, which is a bias flag worth keeping in mind). Independent comparisons of the same three providers converge on three distinct strengths — combined below into one feature set rather than picking a single "winner" to copy.

| Source of inspiration | Their strength | Orra feature to build |
|---|---|---|
| **Gusto** | Payroll pulls from the same place as HR data — org chart, coworker directory, employee profiles already on file | Payroll reads directly from the 201/HR-file employee record (already planned in [[14 Interview Integration Plan (11-11-26)]]) instead of a separate payroll-only employee list; the existing org-chart Roles & Permissions view becomes the same view payroll runs against |
| **QuickBooks Payroll** | Payroll is tightly wired into the accounting ledger — no re-entry between payroll and accounting | A payroll run posts directly against the same budget/PR-settlement ledger that "Settled PRs/Orders" already tracks as a basis-of-truth document, instead of being a separate, siloed calculation |
| **ADP** | Flexible plans that adapt as a business changes stage/size, rather than one rigid structure | Payroll structure configurable per role type — office staff (fixed/salaried) vs. site personnel (daily-wage, spreadsheet-based) — directly answering the still-unconfirmed "spreadsheet upload for site personnel" item noted in the client-version plan |

**Two additional improvements, not from any one provider alone but implied by all three together:**

- **Error-prevention gate before finalizing a run.** The independently-sourced point behind the comparison video is that payroll errors are expensive — mistakes or poor processes can cause penalties in the thousands of dollars. Orra already has a PM-only-approval pattern for materials and RFIs; extend that same approval gate to payroll runs (a second person reviews and approves before disbursement is marked final), rather than relying on a single preparer.
- **No full setup required before the first run.** Gusto's ease-of-start model (no fees, usable immediately) maps to the client's own "as not technical like IT like you guys, but still I want it in a simple, simple, simple way" ask — Orra's payroll module should let a small roster be run with minimal setup, with the fuller statutory-contribution configuration (still flagged "confirm with client" in the client-version plan) layered on later rather than gating the first use.

> [!warning] Still needs client confirmation
> The dynamic statutory contributions and spreadsheet-upload items above remain unconfirmed requirements per the existing plan — this note sharpens *what to ask about*, it doesn't replace that confirmation step. Fold into the next round of open questions alongside those already logged in [[07 Open Questions]].

## Open items this raises
1. Should Orra's "basis of truth" document chain explicitly add a pre-bid/pre-award stage, matching Procore's Pre-Con & Estimating phase, or is that confirmed out of scope?
2. Confirm the statutory-contribution and site-personnel-spreadsheet payroll items with the client now that there's a clearer target shape (Gusto/QuickBooks/ADP-inspired), rather than leaving them as an open-ended "payroll TBD."
3. Decide whether the Owner/IT dashboards (not yet built) should be scoped for this version's Dec deadline, given how directly the monday.com live-widget model would answer the client's stated ease-of-use concern.
