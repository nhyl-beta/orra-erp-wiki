---
tags: [orra-erp, hosting]
---
# Hosting and Infrastructure
Up: [[00 Start Here]]

- Moving **off Vercel** (pricing limits). Goal: free, card-free setup.
- **Web client:** Cloudflare Pages. **API:** Render. **Database:** Neon Postgres.
- **File storage:** Neon Object Storage (private bucket `orra-bucket`, production branch, aws-ap-southeast-1), replacing Filebase/Vercel Blob. Existing Vercel Blob files are not migrated; the new bucket starts empty.
- Not deployed yet as of 31 Oct 2026.
- **Client server:** the same API image should run on ORRA's own server, with a safe way to build a fresh empty database. The server is assumed to be maintained by a fairly beginner IT person, so setup must be click-by-click simple ([[07 Open Questions]], question 13).
- Under evaluation: Neon Managed Better Auth (Google sign-in) and Neon Realtime (live notifications).
- Domain easyconstruct.online (GoDaddy) was bought for EasyConstruct; undecided whether the client version uses it or its own.

## File storage: Google Drive requirement
The client wants Google Drive to be the repository for files and documents, organised by the system. Assumption: ORRA has a dedicated **1 TB plan on a single Google account**. Drive becomes the main store through an OAuth-based adapter, with Restricted files encrypted; the Neon Object Storage plan above becomes a fallback. See [[10 Google Drive Integration]].

> [!warning] Conflict to resolve (11 Nov interview)
> The client stated the real plan is **2 TB** (not 1 TB), only ~20GB used, and explicitly called the Neon Object Storage spend wasteful while Drive sits idle — they want Drive to be the **primary** store, not a fallback, at least for the architect's large CAD/DWG mother-library files. Open question: manual link-paste workflow vs full OAuth API upload (see [[14 Interview Integration Plan (11-11-26)]], question 7). Needs a decision before more storage code is written.

## Docs
free-reliable-hosting-migration-plan, hosting-migration-end-to-end-runbook, hosting-migration-code-prep-prompt, deployment-click-by-click-guide.

Thesis hosting for comparison: Cloudflare Pages + Render + Neon + Filebase, scheduled jobs from GitHub Actions (see the thesis wiki *Deployment and Hosting*).
