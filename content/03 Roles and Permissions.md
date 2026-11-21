---
tags: [orra-erp, roles, permissions]
---
# Roles and Permissions
Up: [[00 Start Here]]

Eleven proposed roles across 20 modules (one row each below). The client confirms or corrects each cell; the answers become **permission rows in the database**, so roles are data and changing them needs no redeploy.

**Key:** M manage (create, edit, delete) · A approve or decide · C create or submit · V view all · V\* view only projects they are staffed on · M\* manage only own projects · G only files granted to them · own = own records · — no access

| Module | Owner | Admin Manager | IT Designer | Project Manager | HR | Finance | Architect | Engineer | Consultant | Site Personnel | DCO |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Dashboard | V | V | V | V* | V | V | V* | V* | V* | V* | V* |
| Projects: create, staff, advance phase | V | M | V | M* | — | V | V* | V* | V* | V* | V* |
| Phase override, archive | V | M | — | — | — | — | — | — | — | — | — |
| Proposals [PRP] | V | V | V | A | — | V | C | V* | A | — | — |
| Designs, plan sets, blueprints | V | V | V | A | — | — | C | V* | A | V* | V* |
| RFI / RFA | V | V | — | A (sends, signs) | — | — | A (answers) | C | A (remarks) | — | C (logs) |
| Transmittals [TRN] | V | V | — | C | — | — | V* | V* | V* | — | M |
| Purchase requests [PR] | V | V | — | A (endorse) | — | A | — | C | — | — | — |
| Purchase orders, payments [PO] | V | A (above limit) | — | V* | — | M | — | V* | — | — | — |
| Deliveries [DR] | V | V | — | V* | — | V | — | A (inspect) | — | C | — |
| Budgets, budget changes [BCR] | V | A | — | A | — | M | — | C | — | — | — |
| Change orders [CO] | V | A | — | C | — | A | — | A (quantities) | — | — | — |
| Site reports, PM reports [DSR] [WPR] | V | V | — | C | — | — | V* | C | V* | C | V* |
| Attendance [DTR] | — | V | — | V* | M | — | own | own | — | C | C (logbook) |
| Payroll [PAY] | V | V (totals) | — | — | C | A | — | — | — | — | — |
| Documents: Internal | V | M | V | C | V | V | C | C | C | C | C |
| Documents: Confidential and Restricted | V | M | — | G | G | G | G | G | G | — | G |
| Purge, legal hold, retention | A | M (needs 2nd approver) | — | — | — | — | — | — | — | — | — |
| Users, roles, permissions | V | V (proposes) | M | — | — | — | — | — | — | — | — |
| Audit log, security | V | V | V | — | — | — | — | — | — | — | — |

## Rules that hold whatever the cells say
- Nobody approves their own request.
- The person who receives a delivery cannot be the one who issued its PO.
- A **Restricted** file needs two-step sign-in.
- Every view, download and change is logged.

## What changed from the thesis roles
- **New: DCO** (Document Control Officer): logs RFIs, manages transmittals, files logbook entries. Still open whether it is a separate person or a duty of Admin/Site Personnel (question 5, [[08 Open Questions]]).
- **Admin Manager** replaces the thesis Admin; the meaning of "ID Manager → Admin Manager" and "Design Manager → PM Manager" is still to be clarified (question 4).
- **Project Manager** owns approvals for materials and RFIs; project-staffed visibility (V\*) applies to most field roles.
- **Owner** is read-mostly, with approval of purge and legal hold.
- Thesis role list for comparison: Owner, Admin, IT Designer, PM, HR, Finance Manager, Architect, Engineer, Site Personnel, Consultant.

Related: [[05 Documents and Confidentiality]] · [[11 Assumptions Awaiting Confirmation]]
