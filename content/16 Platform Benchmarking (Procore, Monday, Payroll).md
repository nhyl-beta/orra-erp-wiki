---
tags: [orra-erp, benchmarking, procore, monday, payroll, ui-ux]
aliases: [Platform Benchmarking, Procore Monday Payroll, Reference Systems]
Up: [[00 Start Here]]
---

# Platform Benchmarking (Procore, Monday.com, Payroll Providers)

> [!summary]
> Three outside systems, each checked against what Orra **already has built**, not treated as a blank-slate wishlist: **Procore** validates the gated phase model in [[14 System Flowchart]] against an industry-standard construction lifecycle; **Monday.com** informs how the *existing* per-role dashboards and the 8-signal advisory engine (already in [[14 System Flowchart]] §9) should look and consolidate, not whether to build dashboards; **ADP/Gusto/QuickBooks Payroll** sharpen the *existing* HR→Finance payroll flow (§5) rather than proposing a new approval step it already has. See also [[14 Interview Integration Plan (11-11-26)]] and [[03 Roles and Permissions]].

## 1. Procore — construction business-flow alignment

### Why a vendor model, not just the interview
[[14 Interview Integration Plan (11-11-26)]] captures what *this one client* said in one room. Procore's phase model is an industry-standard construction business flow, independent of any single client's phrasing — a neutral checklist to walk Orra's own gated stages against.

### Orra's phases vs. Procore's phases
Procore's own construction project lifecycle breaks into five phases — initiation, planning, execution, monitoring and closure — and its published Project Manager Process Guide lays out what sits inside each one. Lined up against the gates already defined in [[14 System Flowchart]]:

| Procore phase | What Procore does there | Orra's equivalent (already built) |
|---|---|---|
| Initiation / Pre-Con & Estimating | Bid review, prequalification, pre-bid RFIs, addenda | **Not modeled** — Orra's Proposal phase (§2a) starts from "PM: Create new project" straight to an Architect-authored proposal; there's no competitive bid/tender step, no addenda log, no multi-bidder comparison |
| Contract Award | Contract issuance, external communications | **Gate P5** — PM/Admin upload Notice of Award + Contract, PM sets contract value |
| Planning & Scheduling | Purchase order workflow, project documents, site meetings | **Gates C1–C6** (Pre-Construction) — requirements, budget lines, milestones, site-crew staffing linked to employee records, NTP + site coordinates, purchase requests |
| Execution | RFIs, submittals, change process, payment process, safety | RFI/RFA flow (§3), Purchasing flow (§4), Construction phase (§2d) |
| Closeout | Final inspections, as-builts, O&M, Certificate of Substantial Performance, final billing | Closeout Phase (§2e) — final inspection and COC gates |

Orra already covers four of Procore's five phases with named gates — the one genuine, structural gap is the first one: **nothing in Orra represents a pre-award bidding/tender stage.** That's worth a deliberate yes/no, not an assumption (see Open Questions below), since Procore's own workflow principle is that a standardized workflow makes a recurring process like this easier to track and removes delays from missing information — exactly the kind of thing worth deciding on purpose rather than by omission.

### Procore's UI/UX — what to copy and what to avoid
Reviews split in a directly useful way:

- **Copy this:** many users describe Procore's interface as clean and intuitive, easy to use even for those with limited technical knowledge, with a mobile-first design that lets field crews upload photos and daily logs effortlessly.
- **Avoid this:** just as many reviewers say the opposite — the interface centralizes project data but often overwhelms new users with layered menus and terminology that can slow down navigation, and users report a steep learning curve despite the interface being generally intuitive. One reviewer summed it up: being a catch-all platform for construction management, its interface may not be as user-friendly as software that focuses on just one aspect. Procore's own team is still actively redesigning parts of it (Drawings tool, Analytics interface) specifically to cut down the time users spend fighting the interface.

**Why this matters for Orra:** Procore is proof that a platform can be "intuitive" in reviews and still fail the exact competency-gap problem the client stated — menu depth and feature layering is what reviewers blame for the learning curve. Procore's *gate/phase structure* is worth validating against (see table above); its UI *density* is the thing to deliberately not inherit, since it's built for large GC teams with dedicated coordinators, not ORRA's small, mixed-literacy team.

## 2. Monday.com — ease-of-use UI and consolidated reporting

### What Orra already has that this maps onto
[[14 System Flowchart]] §1 already routes every role to its own dashboard (Owner, Admin, IT Designer, PM, HR, Finance, Architect, Engineer, Consultant, Site Personnel), and §9 already runs **8 advisory signal rules** as background jobs surfaced on those dashboards — cost variance, cumulative change impact, burn vs progress, issue recurrence, stalled stage, projected finish, overdue tasks, and milestone slip. Structurally, this is close to what a monday.com dashboard does: pull from multiple sources and surface it in one place. **The gap isn't the engine — it's the presentation.**

### The specific UI mechanism to borrow
roughly 70% of monday.com's users are classified as non-tech users, and reviewers consistently point to a few concrete mechanisms, not vague "simplicity":

1. **Color as the primary status signal**, directly on the item, not behind a menu — map this onto the 8 signal rules: a cost-variance tile should be a red/amber/green chip at a glance, not a row in a table the Owner has to read.
2. **Non-imposing data entry** — monday.com's own rule is to never ask a user to add metadata the system needs for its own operations, only what the task itself needs. Worth auditing Orra's gate checklists (P1–P5, D1–D3, C1–C6) against this: are all required fields genuinely needed by the next gate, or is some of it bookkeeping for Orra's own sake?
3. **Drag-and-drop over forms** where the gate allows it.

### Consolidated reporting — the specific pattern to apply
- A dashboard pulls data from multiple sources and displays it through widgets, giving an instant summary — this is precisely what §9's signal table should become visually, rather than a static list: Owner's "All dashboards (read-only), portfolio" view (§10) is the natural home for a consolidated, color-coded read of all 8 signals across every project at once.
- Dashboards should be **live and self-maintaining** — no one re-builds a report; the signal jobs already run as background jobs, so the remaining work is purely presentational.
- Widgets are **interconnected** — one update reflects everywhere it's relevant, reinforcing a single source of truth instead of per-module static exports.
- Reports are shareable by link, which matters directly for Owner's **read-only** dashboard access already defined in §10 — a shareable consolidated view fits that role better than making the Owner log in and click through per-project screens.

**Action item:** when building out the 8-signal dashboard UI (not yet detailed beyond "surfaced on dashboards" in §9), design it as a monday.com-style consolidated widget board — color-severity tiles per signal, one combined cross-project view for Owner, per-project drill-down for PM/Finance — rather than a plain table. This is a presentation decision on top of an engine that already exists.

## 3. Payroll — sharpening the existing flow, not replacing it

The CPA-review video itself wasn't retrievable (YouTube blocked content access; only metadata came through, and the video carries referral/affiliate links for all three providers — a bias flag worth keeping in mind). Independent comparisons of ADP, Gusto, and QuickBooks Payroll converge on three distinct strengths, checked here against Orra's **already-built** payroll flow ([[14 System Flowchart]] §5: clock-in → HR verify → HR generate batch → HR add lines → HR submit → Finance review → approve/fix loop → contribution + payroll reports).

| Source | Their strength | Already in Orra? | What to actually change |
|---|---|---|---|
| **QuickBooks Payroll** | Payroll and accounting are the same ledger, no re-entry | **No** — §5 ends at a standalone "Payroll summary report"; nothing shows it posting against the project's budget lines from §2c (gate C2) | Post each approved payroll run as a labor-cost line against the project's budget, the same way [[03 Roles and Permissions]] already has Finance managing budgets, BCR, and payroll in one role |
| **Gusto** | Payroll reads from the same employee record as HR, not a separate list | **Partly** — §2c gate C4 already links staffed site personnel to employee records, but §5's "HR: Generate payroll batch" doesn't show it pulling from that same linked record | Make the Pre-Construction employee-record link (C4) the one and only source payroll reads from — no separate payroll-only roster |
| **ADP** | Payroll structure flexes by employee type/stage rather than one rigid path | **No** — §5 shows one uniform path from DTR to payroll lines regardless of employee type | Fork the "HR: Add payroll lines" step by employee type (office/salaried vs. site/daily-wage), which is exactly what [[08 Open Questions]] Question 11 is already asking about — use this comparison to shape that discussion, not to raise a new question |

**What NOT to add:** an approval gate before finalizing a payroll run. Orra already has one — Finance reviews the batch, and either approves or kicks it back to HR to fix and resubmit. All three providers' emphasis on catching errors before disbursement (since payroll mistakes can cost real penalties) confirms this existing gate is the right call; it isn't a gap.

**One genuinely new idea, from Gusto specifically:** a quick-run mode. Gusto's model is usable immediately with no setup fee before the first run. Nothing in §5 suggests Orra can process a first payroll before the full statutory-contribution configuration (SSS/PhilHealth/Pag-IBIG rules, per Question 11) is finalized — worth keeping separate on purpose, so a demo payroll run isn't blocked on that still-open configuration question.

## Open items this raises (added to [[08 Open Questions]] as Q23–Q25)
23. Does Orra ever need to model a pre-award bidding/tender stage (multiple bidders, addenda, pre-bid RFIs) before the Proposal phase, or does ORRA always arrive as the already-selected contractor? (Procore gap — see §1)
24. Should an approved payroll batch post as a labor-cost line against the project's budget (gate C2), the way POs and budget changes already do — or stay a standalone report? (QuickBooks-style gap — see §3)
25. For the December demo, do the 8 advisory signals (§9) need the full color-coded consolidated dashboard treatment, or is a plain table acceptable for now given the timeline? (Monday.com-style presentation question — see §2)
