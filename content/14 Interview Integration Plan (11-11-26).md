---
tags: [orra-erp, interview, integration-plan, roles, hr, google-drive]
aliases: [Integration Plan, 11-11 Interview, Solidified Requirements]
---
# Integration Plan — from the 11 Nov 2026 Interview
Up: [[00 Start Here]]

> [!summary]
> Source: INTERVIEW TRANSCRIPT ORRA (11/11/26), 61 pages, Admin + HR + IT Designer (Mark) + dev team (nhyl, grace, zheki, mj). This is the solidified build list extracted from that transcript, plus open questions and a suggested build order. Supersedes/corrects a few items in [[05 Client-Driven Changes]] and [[06 Hosting and Infrastructure]] — see callouts there.

## A. HR / 201 Files
| # | Integration | Detail |
|---|---|---|
| A1 | Employee record schema | Employee #, hire date, role, department (add/remove-able field), attendance, payroll (frequency configurable per employee) |
| A2 | 201 file document set | IDs, legal/employment docs, COC from past company, NBI clearance, health cert, training certs — attached per employee, not per project |
| A3 | Missing/expired doc flagging | Auto-notify when a required doc is absent (e.g. no birth certificate) or past its "valid until" date |
| A4 | Consultant record type | Separate from regular employee: visit-based (not monthly), tracks license (PRC/PTR) expiry, auto-reminds for renewal |
| A5 | Resignation/offboarding flow | Status → inactive → archived (not deleted) → auto-delete after a configurable hold period (client said ~2 months) |

## B. Roles & Permissions
| # | Integration | Detail |
|---|---|---|
| B1 | Merge Admin + HR | One role in the system — client confirmed this on 11/11 (corrects [[05 Client-Driven Changes]], which had it as "set aside") |
| B2 | Architect scoping | Architect sees only their own uploaded documents/library |
| B3 | Consultant scoping | Sees only TOR + plans for their assigned project; explicitly blocked from contracts, OTP, other doc types |
| B4 | Owner fail-safe | A dedicated "recover IT access" action, usable only by Owner, to reset IT's credentials |
| B5 | Post-completion visibility | Once a project is marked completed, only PM + Admin keep visibility; assigned Engineers lose access to that project (historical assignment record stays) |

## C. Document / Project Library
| # | Integration | Detail |
|---|---|---|
| C1 | Mother Library | Master template store (door/window/cabinet/wall/ceiling details, DWG/CAD/RVT) that architects copy-and-modify from per project, never duplicate-stored |
| C2 | File size policy | No/very high limit for CAD/DWG/RVT; normal limit for PDFs/Office docs |
| C3 | Project/contract search | Search by project name or contract name returns the match directly |
| C4 | Project record fields | Owner, address, project name, amount, NOA date, NTP date, COC — the "big three" milestone PDFs |
| C5 | NTP → start date | Issuing NTP auto-sets the project's start date to the next day |
| C6 | Master project registry | One table of all projects, split Ongoing vs Completed, clean columns (not crammed into one line), row-select to edit/delete |
| C7 | Project detail export | Print/PDF button on a project's full detail sheet |

## D. External-Party Access (architectural decision, not just a feature)
| # | Integration | Detail |
|---|---|---|
| D1 | No system login for external parties | Client/Designer/Contractor access via **Google Drive share links**, not ORRA accounts |
| D2 | PM-managed share workflow | PM uploads to Drive → copies link → logs it in a tracked table with a descriptive name (e.g. "RFI — approval of current materials") |
| D3 | RFI/RFA exchange location | Lives in Drive/email between Designer and Client, not as an in-app approval flow for those parties |

## E. Storage
| # | Integration | Detail |
|---|---|---|
| E1 | Primary file storage → Google Drive | Client's **2 TB** Drive (only ~20GB used) should replace the planned Neon Object Storage for new uploads, especially the CAD/DWG mother library — **conflicts with the current plan in [[06 Hosting and Infrastructure]]**, needs a decision |
| E2 | Legacy server offload | Old on-prem server (~5TB, nearly full) needs its reusable files migrated into Drive, organized by project folder |

## F. Dashboards
| # | Integration | Detail |
|---|---|---|
| F1 | IT dashboard | Total accounts, active, deactivated, sensitive events (deletions, failed logins/password errors) |
| F2 | Owner dashboard | Graphical/visual only — budget and status charts, no raw tables |

## Open Questions (new, from this interview)
Add to [[07 Open Questions]]:
1. Owner recovery button (B4): blind one-click reset emailing IT, or does Owner see which credentials are being reset?
2. Does Consultant access drop to zero at project completion, or keep read-only access to their own past TOR/plans?
3. Architect library isolation (B2): ever shared between Architects (e.g. senior reviewing junior), or always absolute?
4. Does ORRA need any in-system record of the Drive/email RFI-RFA exchange (D3), or is Drive the entire source of truth?
5. Who creates the per-project Drive folder/share link — PM only, or Admin too?
6. Does the system need its own audit trail of who opened an externally-shared Drive link, or is Drive's own activity log the answer?
7. Upload model: does ORRA upload to Drive via API (OAuth-connected account), or does PM/Architect manually drop files into Drive and paste the link into ORRA?
8. Is there a cutoff date for migrating the legacy 5TB server into Drive, or is it an ongoing background task?
9. Single point of failure: does the 2TB Drive belong to one Google account? What's the plan if that account needs to change?
10. Is NOA a required/tracked field only, or does it trigger automation like NTP does?
11. Does moving a project from Ongoing → Completed require a formal step (e.g. COC attached first), or is it a manual status flag?
12. Confirm: is **Dec 12–14** a hard deadline for a pitch-ready build, separate from the thesis defense date — and must Google Drive integration be live by then, or can it be a manual link-paste stub for the pitch?

## Suggested Build Approach
Given the Dec 12–14 pitch deadline and the client's own ask for one-on-one department follow-ups before finalizing:

1. **Lock the storage architecture decision first.** The Google Drive-as-storage model (D, E) changes the whole file-handling design — get answers to questions 7 and 9 above before writing storage code. Building against Neon Object Storage and retrofitting Drive later costs more time than is available.
2. **Run the department follow-ups tightly scoped**, not open-ended — bring each department (HR, Finance, Architect, Engineering) this list's A/B/C items to confirm or correct, rather than a second freeform interview.
3. **Build order for the pitch:**
   1. Roles/permissions merge (B1, B2, B3, B5) — low risk, high visible impact
   2. Project registry + lifecycle fields (C4–C7) — what the pitch demo will actually show
   3. HR/201 flagging (A3) — directly answers the client's stated #1 pain point ("nawawala yung mga files")
   4. Google Drive integration (D, E) — scope to **manual link-paste first** (PM pastes a Drive link into a field), not full OAuth API upload; automate after the pitch if it lands
4. **Treat Owner/IT dashboards (F) as post-pitch polish** unless specifically requested for the demo.
