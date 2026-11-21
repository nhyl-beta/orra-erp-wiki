---
tags: [orra-erp, thesis]
---
# Thesis vs Client Version
Up: [[00 Start Here]]

Two versions of one product. The **thesis version** (EasyConstruct) stays as-is for academic submission; **Orra-ERP** is the separate client version so thesis and client work never mix.

| | Thesis: EasyConstruct | Client: Orra-ERP |
|---|---|---|
| Repo | `nhyl-beta/EasyConstruct` (`thesis-final`, plus `thesis-final-staging` and `thesis-final-test`) | `nhyl-beta/orra-erp`, local copy `C:\Users\nhylc\Dev\OrraERP` |
| Purpose | Capstone, 10 role modules | Real use at ORRA, secure legal-document management |
| Roles | Fixed thesis list | Not fixed; driven by interviews ([[03 Roles and Permissions]]) |
| Updates | `thesis-final-staging` → PR → `thesis-final` | Weekly from client input |
| Hosting | Cloudflare Pages + Render + Neon + Filebase | Cloudflare Pages + Render; Neon Object Storage; option to run on client server ([[07 Hosting and Infrastructure]]) |

For now the `thesis-final` branch is the source for the client repo copy.

## Thesis-only: do not carry over without a decision
- Manuscript objectives and the `objectives-*` docs.
- ScopeLimitation.pdf / Final Scope (10 role modules): a starting point only.
- Thesis presentation prep, Obsidian thesis design notes, scope-vs-interview gap reports.
- Rule-based "AI" reference validation (external price references): deferred even in the thesis; revisit only if the client asks.
- Planned payroll items (spreadsheet upload for site personnel; dynamic statutory contributions): confirm with the client first.
- The thesis role list: Owner, Admin, IT Designer, Project Manager, HR, Finance Manager, Architect, Engineer, Site Personnel, Consultant.

## Thesis docs worth copying across
client-version-change-plan, client-demo-interview-updates, client-demo-changes-staging-prompt, admin-overview-and-fresh-db-staging-prompt, deployment-readme.
