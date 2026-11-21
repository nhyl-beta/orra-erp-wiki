---
tags: [orra-erp, flows]
---
# Flows, Forms and Screens
Up: [[00 Start Here]]

Of **21 flowchart steps**, 14 are already built from the thesis version or the client demo changes, 3 need a change, and 4 are new for the client version.

## The five flows
1. **Project lifecycle** — Proposal → Award → Design / Construction / Project Management service → closeout.
2. **RFI / RFA** — swimlanes: PM sends and signs; Architect/Engineer answer; Consultant remarks; DCO logs and transmits.
3. **Purchasing** — Purchase request → PM endorsement → Finance approval → PO → delivery receipt → payment; budget changes and change orders alongside.
4. **Attendance and payroll** — clock-in (office, site phone) → HR verification → payroll batch → Finance review and approval.
5. **Secure document vault** — upload with integrity check, versioning, confidentiality level, access request, purge and legal hold.

| Flow | Step | Form | Screen | Build status |
|---|---|---|---|---|
| 1 Lifecycle | Proposal and approval | PRP | Project detail (Proposal phase) | Built |
| 1 Lifecycle | Award and contract | NOA, CTR | Document vault, project detail | Built; vault rules new |
| 1 Lifecycle | Choose the service | — | New project wizard | Change: add Project Management as a service on the Construction type |
| 1 Lifecycle | Design plan sets and turnover | BLP, TOD, CAF, TRN | Project detail (Turnover) | Built |
| 1 Lifecycle | Construction on site | DSR | Project detail, reports | Built |
| 1 Lifecycle | PM service weekly report | WPR | PM reports | Built; layout to confirm with ORRA |
| 1 Lifecycle | PM service progress billing | PBR | none yet | New |
| 1 Lifecycle | Final inspection and completion | FIR, COC | Project detail (closeout checks) | Built |
| 2 RFI/RFA | Raise, route, answer | RFI, RFA | RFI and RFA register | Built (multi-recipient, no-login reply link) |
| 2 RFI/RFA | DCO log and transmittal | TRN | RFI register: New transmittal | Change: add DCO role |
| 2 RFI/RFA | Change order from a request | CO | Approvals | Built |
| 3 Purchasing | Purchase request and endorsement | PR | PM approvals | Built |
| 3 Purchasing | Purchase order and payment | PO | Finance purchasing | Built |
| 3 Purchasing | Receive delivery | DR | Site phone, purchasing | Built |
| 3 Purchasing | Budget change | BCR | Approvals | Built |
| 4 Payroll | Office clock-in | — | Office one-button clock-in | New, if ORRA confirms |
| 4 Payroll | Site clock-in and logbook | DTR | Site phone | Change: add DCO logbook entry |
| 4 Payroll | Payroll batch and approval | PAY | HR payroll, Finance review | Built; deductions to confirm |
| 5 Vault | Upload, check, version | — | Document vault | Built (integrity check); confidentiality levels new |
| 5 Vault | Access request | DAR | Document vault | New |
| 5 Vault | Delete, purge, legal hold | DAR | Document vault | New |

## Sample data used in the demo
- **EC-2026-0147**: private client, Construction service, Metro Bulacan Trading Corp.
- **PM-2026-0031**: government, Project Management service (fictional).
All names and amounts are invented; payroll deductions are placeholders.

Forms: [[05 Documents and Confidentiality]] · Roles: [[03 Roles and Permissions]]
