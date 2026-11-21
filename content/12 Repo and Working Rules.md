---
tags: [orra-erp, repo]
---
# Repo and Working Rules
Up: [[00 Start Here]]

- Client repo: `https://github.com/nhyl-beta/orra-erp.git` (separate from the thesis repo, decided).
- Local copy: `C:\Users\nhylc\Dev\OrraERP`.
- Thesis work continues on `thesis-final` (+ `thesis-final-staging`, `thesis-final-test`), updated by PR from staging.
- **Repo hygiene:** personal notes (docs, .claude, changelog, scratch) stay local and uncommitted; only real project docs (architecture, adr, setup, test accounts) are tracked.
- Architecture is inherited from the thesis monorepo: npm workspaces, `apps/web` (React + Refine), `apps/api` (Express + Drizzle), API modules with repository → service → controller → routes, cross-module imports only through each module's `index.ts`. See the thesis wiki *Monorepo Structure* and *Backend Layering*.
- Work in half-day pieces; small, finishable changes.
