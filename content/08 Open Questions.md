---
tags: [orra-erp, interview, open-questions]
---
# Open Questions (next interview)
Up: [[00 Start Here]]

Twenty-seven questions (14 carried over, 3 on Google Drive added 21 Nov, 7 more added 11 Nov–28 Nov), most carried over unanswered from the 20 and 24 October interviews. **Questions 1–6 block the final flowchart and role matrix, so ask those first.** Questions 15–17 are about the Google Drive requirement ([[13 Google Drive Integration]]). Questions 23–25 come from benchmarking Orra against Procore, Monday.com, and payroll providers ([[16 Platform Benchmarking (Procore, Monday, Payroll)]]); questions 26–27 come from the UI-UX design brief ([[17 UI-UX Design Plan]]). Plan: send to the ORRA contacts Tue 24 Nov, interview Wed 25 Nov ([[09 Plan to December Demo]]). Fill the Answer column during the interview.

| # | Topic | Question | Why it matters | Answer |
|---|---|---|---|---|
| 1 | Services | Does one project ever move from Design to Construction or to Project Management, or is each service a separate engagement? | Decides whether the flowchart branches once or allows hand-offs |  |
| 2 | Government vs private | For a government job, what are the first and last steps, and who signs on the owner's side? | Shapes flow 1 and the PBR and WPR forms |  |
| 3 | RFI / RFA | After the Architect or Engineer answers, does the Consultant always review? When must the owner sign? | Fixes the lanes in flow 2 |  |
| 4 | Roles | What exactly did "ID Manager → Admin Manager" and "Design Manager → PM Manager" mean? Which screens does each see? | Final role list and matrix |  |
| 5 | DCO | Is the Document Control Officer a separate person, or a duty of Admin or Site Personnel? | Adds or removes a role |  |
| 6 | Admin screen | Which tabs or buttons on the Admin dashboard should be removed or hidden? | Final Admin UI |  |
| 7 | Files | Who may delete or download legal and CAD files? Only Admin? | Vault permissions, Restricted level |  |
| 8 | Files | Which documents are Restricted? How long must each type be kept? | Retention and legal hold rules |  |
| 9 | First rollout | For the first real project, which files and milestones go in first? | Seed data for the December demo |  |
| 10 | Attendance | Office staff: one button or geolocation? Site: phone + photo, or a photo of the paper logbook? | Flow 4 and the site phone screen |  |
| 11 | Payroll | Are SSS, PhilHealth, Pag-IBIG, tax and overtime rules standard, or are there company-specific deductions? Cut-off and pay dates? | Payroll computation |  |
| 12 | Forms | Can ORRA give one blank copy of each paper form they use (RFI, transmittal, PR, PO, DTR, payslip)? | Printed layouts match theirs |  |
| 13 | Hosting | Will it run on ORRA's own server, and who looks after it after December? | Deployment and support plan |  |
| 14 | Sign-in | Is Google sign-in with company accounts acceptable for all staff, including site crews? | Login design |  |
| 15 | Google Drive | Is the ~~1 TB~~ **2 TB** (per 11 Nov interview) a Google Workspace plan (shared drives) or a single Google account? Who owns it, who administers it, and who holds its sign-in and recovery? | Single account = OAuth route; Workspace = shared drive route |  |
| 16 | Google Drive | Should the existing Drive archive be imported as-is, or reorganised into the new folder structure? Roughly how many files and GB? | Import scope and storage size |  |
| 17 | Google Drive | After go-live, may staff still open files directly in Drive, or only through Orra-ERP? | Direct access bypasses Restricted-file rules and the audit trail |  |
| 18 | Roles | Owner recovery button: blind one-click reset emailing IT, or does Owner see which credentials are being reset? | Scopes the fail-safe UI ([[14 Interview Integration Plan (11-11-26)]]) |  |
| 19 | Roles | Does Consultant access drop to zero at project completion, or keep read-only access to their own past TOR/plans? | Scopes offboarding logic |  |
| 20 | Google Drive | Upload model: ORRA uploads to Drive via API (OAuth-connected), or PM/Architect manually drops files into Drive and pastes the link? | Decides integration effort and pitch-deadline feasibility |  |
| 21 | Google Drive | Is there a cutoff date for migrating the legacy 5TB server into Drive, or is it an ongoing background task? | Migration scheduling |  |
| 22 | Timeline | Confirm: is Dec 12–14 a hard deadline for a pitch-ready build (separate from thesis defense), and must Drive integration be live by then or can it be a manual stub? | Drives the whole build order |  |
| 23 | Lifecycle | Does Orra ever need to model a pre-award bidding/tender stage (multiple bidders, addenda, pre-bid RFIs) before the Proposal phase, or does ORRA always arrive as the already-selected contractor? | Procore-benchmark gap; scopes whether flow 1 needs a new stage before Proposal ([[16 Platform Benchmarking (Procore, Monday, Payroll)]]) |  |
| 24 | Payroll | Should an approved payroll batch post as a labor-cost line against the project's budget, the way POs and budget changes already do — or stay a standalone report? | QuickBooks-benchmark gap; ties payroll into the existing budget ledger ([[16 Platform Benchmarking (Procore, Monday, Payroll)]]) |  |
| 25 | Dashboards | For the December demo, do the 8 advisory signals need the full color-coded consolidated dashboard treatment, or is a plain table acceptable given the timeline? | Monday.com-benchmark presentation question; scopes dashboard UI work before Dec ([[16 Platform Benchmarking (Procore, Monday, Payroll)]]) |  |
| 26 | Lifecycle | Should the currently-built mandatory lifecycle gates (consultant required, site coordinates required, procurement initiated, etc.) be loosened to conditional/optional, or do they stay as hard gates for the December build? | UI-UX brief's PART 7 proposes loosening built gates — a scope decision, not a clarification ([[17 UI-UX Design Plan]]) |  |
| 27 | Roles | Admin/HR are confirmed merged — is Finance's own scope ("too broad" per interview) still open, and what does Finance actually need to do day to day beyond PR/PO/payroll approval? | Finance workflow still undefined per the UI-UX brief PART 6.3 ([[17 UI-UX Design Plan]]) |  |
