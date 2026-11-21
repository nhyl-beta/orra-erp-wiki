---
tags: [orra-erp, google-drive, storage]
---
# Google Drive Integration
Up: [[00 Start Here]]

> [!summary] Requirement and assumption (21 Nov 2026)
> ORRA wants Google Drive to be the repository where files and documents are stored, organised by the system. **Assumption: ORRA has a dedicated 1 TB plan on a single Google account** (no Workspace shared drives). To be confirmed in question 15 ([[08 Open Questions]]).

## Decision: Drive is the main store, Orra-ERP is the gatekeeper
Files live in ORRA's Drive. Orra-ERP creates the folder tree, records every file in its database and is the only normal way in. Three parts:

1. **A (main): Drive adapter with OAuth.** One ORRA-owned Google account; the API holds its refresh token (env secret) and uploads as that account, so every file counts against the 1 TB. A new `gdrive:<fileId>` storage type sits next to `s3:`.
2. **D: encrypt Restricted files** in the API before upload (AES-GCM, key in env, backed up). Drive holds ciphertext, so anyone opening Drive directly cannot read contracts or payroll.
3. **E: Picker import** for the existing archive: staff pick folders or files in the Google Picker, the app indexes them (file id + SHA-256) and optionally copies them into the managed tree.

Fallbacks: **B** (Neon bucket main, Drive as automatic copy) if the client rejects the single-account login or Drive reliability worries them; **C** (move a project's files to Drive when an Admin sets it to Archived) if Neon/Render storage has to stay small.

## Why not a service account
A Google **service account has no storage quota and cannot own files in a normal My Drive**, so uploads fail. A service account plus **shared drive** works only on Google Workspace. Revisit it if question 15 shows ORRA has Workspace.

## Account setup (verify before building)
- Dedicated mailbox, not a person's; two Admins hold the sign-in and recovery details; 2-step sign-in on.
- OAuth consent screen set to **In production**. Apps left in **Testing** get refresh tokens that expire after 7 days.
- Scope `drive.file` (app sees only files it created) limits the damage if the token leaks. Existing files come in through the Picker, which grants per-file access.
- Store the refresh token as a secret on the API host (Render env), never in the web build.
- Limits that matter little at ORRA's size: 750 GB/day upload per user, 5 TB per file, 325,000 API quota units/min per user (a file create costs 50).

## Folder tree (built by the system)
```
Orra-ERP (root folder in the 1 TB account)
├── Projects/
│   └── EC-2026-0147 Metro Bulacan Trading Corp/
│       ├── 01 Proposal and Award        (PRP, NOA, CTR)
│       ├── 02 Design                    (BLP, TRN, TOD, CAF)
│       ├── 03 Construction              (RFI, RFA, DSR, DR, CO)
│       ├── 04 Procurement and Finance   (PR, PO, BCR)
│       └── 05 Closeout                  (FIR, COC)
├── HR and Payroll/                      (Restricted, encrypted)
├── Legal and Contracts/                 (Restricted, encrypted)
└── Company Admin/                       (Internal)
```
Files are named by the numbering standard in [[05 Documents and Confidentiality]]. Folder ids are cached in the database.

## What changes in the code
- The storage router (`core/storage/index.ts`) already picks the backend from the file URL prefix, and the S3 adapter already has `putFile` (stream from disk). Add `gdrive.adapter.ts` with the same shape: `put`, `putFile` (resumable upload), `open`, `delete`; add `isGDriveUrl` and one branch in the router.
- `stored_files` already holds SHA-256 and size, so integrity checks and the "Check file" action carry over. For encrypted files, hash the plaintext and store a flag.
- `put` has no folder context: add an optional project/category hint so the adapter picks the folder. `exists()` is synchronous; return true for `gdrive:` (as Vercel Blob does) and let `open` report a missing file.
- New env vars: `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REFRESH_TOKEN`, `GDRIVE_ROOT_FOLDER_ID`, `RESTRICTED_FILE_KEY`.
- A one-time script to obtain the refresh token, and a retry queue for failed uploads (Drive calls can fail or be rate-limited).
- Extend the existing legacy import page with the Picker.

## Risks and handling
| Risk | Handling |
|---|---|
| One account is a single point of failure (password change, security lock, owner leaves) | Dedicated mailbox, two Admins hold recovery, document the owner; alert when token refresh fails |
| Token expires after 7 days | Consent screen In production; test by waiting past 7 days before the client demo |
| Staff open Drive directly | Share the root folder with no one except Admins; Restricted is encrypted anyway; ask question 17 |
| Purge and legal hold | Drive trash keeps files about 30 days; purge flow calls permanent delete after the second approval; legal hold blocks delete in the app |
| Lost encryption key | Back up the key separately from the API host; losing it makes Restricted files unreadable |
| Integrity | SHA-256 in the database, verified on upload and download |
| Versions | One Drive file per app version; the database is the version history |
| Drive outage or rate limits | Retry queue, clear error message, copy of the database backup |
| API host streams every file | Free Render instance (512 MB RAM, sleeps after 15 min, disk wiped on restart) is weak for large CAD files; use a paid instance for ORRA |

## Neon and stack notes
- Postgres on the Neon free plan: 1 GB per project, compute scales to zero after 5 minutes idle. With Drive holding the files, the database holds only metadata, audit and payroll rows: fine for the demo, move to a paid plan for production.
- Neon Object Storage is in beta; with Drive as the main store it is only a fallback.
- Cloudflare Pages (web) is unaffected.
- Replaces the Neon Object Storage choice in [[07 Hosting and Infrastructure]].

## Alternatives considered
| Option | Pros | Cons |
|---|---|---|
| A Drive main (OAuth) | Simplest; uses the 1 TB | Drive outage = no files; single account |
| B Neon main + Drive copy | Fast, audited, survives Drive outage | Pays Neon storage; beta object storage |
| C Hot / cold (archive to Drive) | Keeps Neon small; uses Archived step | Not in Drive while active |
| D Encrypt Restricted | Direct Drive access reads nothing | No preview/search; key management |
| E Picker / link attach | Cheap way to bring in old files | Weak control unless copied |
| F Drop folder ingest | Matches how staff work today | Extra moving parts; skip unless asked |
| Shared drive + service account | Clean ownership | Needs Workspace |
| Link-only | Fastest | No integrity, central permissions or audit; not for legal documents |

## Effect on the plan
For the 4 Dec demo: the adapter writes and reads a test folder in the real account, the tree is created automatically, and one Restricted file is encrypted end to end. Picker import and the retry queue can follow. Open questions 15–17 are in [[08 Open Questions]].
