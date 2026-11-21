---
tags: [orra-erp, flowchart, system-flow]
aliases: [System Flowchart, Full Flow]
---
# EasyConstruct / Orra-ERP — Complete System Flowchart

Up: [[00 Start Here]]

> [!info] What this page covers
> Every user action across all 10 roles, mapped through the five main flows of the system. Based on the `thesis-final` branch of EasyConstruct. Gate checks (P1–P5, D1–D3, C1–C6, K1–K4, X1–X6, T1–T3) must pass before a project can advance.

---

## 1. Authentication and Entry

```mermaid
flowchart TD
    START([User opens app]) --> LOGIN[Login page]
    LOGIN -->|Enter email + password| AUTH{Authenticate}
    AUTH -->|Invalid| ERR[Show error, rate-limit after 40 attempts/15min]
    ERR --> LOGIN
    AUTH -->|Valid| TOKEN[Issue JWT, record login in audit log]
    TOKEN --> ROLE{Check user role}

    ROLE -->|Owner| OD[Owner Dashboard]
    ROLE -->|Admin| AD[Admin Dashboard]
    ROLE -->|IT Designer| ITD[IT Designer Dashboard]
    ROLE -->|Project Manager| PMD[PM Dashboard]
    ROLE -->|HR| HRD[HR Dashboard]
    ROLE -->|Finance Manager| FD[Finance Dashboard]
    ROLE -->|Architect| ARCHD[Architect Dashboard]
    ROLE -->|Engineer| ENGD[Engineer Dashboard]
    ROLE -->|Consultant| COND[Consultant Dashboard]
    ROLE -->|Site Personnel| SPD[Site Personnel Dashboard]

    LOGIN -->|Forgot password| FORGOT[Forgot Password page]
    FORGOT -->|Enter email| RESET_EMAIL[Send reset link via SMTP]
    RESET_EMAIL --> RESET[Reset Password page]
    RESET -->|New password| LOGIN

    OD -->|Owner Recovery| RECOVER[Recover IT Designer account]
```

> **Shared pages** accessible to multiple roles: Settings, Archive Search, Completed Workflows, Reports, Blueprint Reviews, HR views, Engineer views, Resources, Requests, Transmittals, Print pages, Legacy Import, AI Validation Reference.

---

## 2. Project Lifecycle (Flow 1)

This is the backbone of the system. A project moves through sequential phases, with gate checks at each transition.

### 2a. Project Creation and Proposal Phase (0–10%)

```mermaid
flowchart TD
    PM_CREATE[PM: Create new project] --> WIZARD[New Project Wizard]
    WIZARD -->|Set name, client, type, delivery type| PROJ_CREATED[Project in Proposal phase]
    PROJ_CREATED --> STAFF_ARCH[PM: Staff an Architect — gate P1]
    PROJ_CREATED --> STAFF_CON[PM: Staff a Consultant — gate P2]
    PROJ_CREATED --> ADD_MEMBERS[PM: Add project members]

    STAFF_ARCH --> ARCH_PROPOSAL[Architect: Create proposal with files]
    ARCH_PROPOSAL --> SUBMIT_WF[Architect: Submit proposal via workflow — gate P3]
    SUBMIT_WF --> CON_REVIEW[Consultant: Review proposal]
    CON_REVIEW -->|Approve / Reject / Revise| PM_APPROVE[PM: Approve proposal — gate P4]

    PM_APPROVE --> UPLOAD_AWARD[PM/Admin: Upload Notice of Award + Contract]
    UPLOAD_AWARD --> SET_VALUE[PM: Set contract value — gate P5]
    SET_VALUE --> ALL_P{All P1-P5 gates pass?}
    ALL_P -->|No| FIX_P[Fix missing items]
    FIX_P --> ALL_P
    ALL_P -->|Yes| ADVANCE_D[PM: Advance to Design phase]
```

### 2b. Design Phase (10–25%)

```mermaid
flowchart TD
    DESIGN_START([Project enters Design phase]) --> ARCH_DESIGN[Architect: Create design]
    ARCH_DESIGN -->|Upload files, assign to staffed Engineer| D1_CHECK[Gate D1: Design with files + assigned engineer]

    ARCH_DESIGN --> ARCH_REVISION[Architect: Create design revision]
    ARCH_REVISION --> ATTACH_FILES[Architect: Attach revision files]

    D1_CHECK --> CON_DESIGN_REVIEW[Consultant: Create design review]
    CON_DESIGN_REVIEW -->|Approve / Reject / Request Changes| REVIEW_DECIDE{Review decision}
    REVIEW_DECIDE -->|Changes needed| ARCH_REVISION
    REVIEW_DECIDE -->|Approved| D2_CHECK[Gate D2: All designs approved, no pending reviews]

    ARCH_DESIGN --> BLUEPRINT[Architect: Upload blueprint]
    BLUEPRINT -->|Set status Current + Approved| D3_CHECK[Gate D3: Approved current blueprint]

    D2_CHECK --> ALL_D{All D1-D3 gates pass?}
    D3_CHECK --> ALL_D
    ALL_D -->|Yes| ADVANCE_PC[PM: Advance to Pre-Construction]
    ALL_D -->|No| FIX_D[Fix missing items]
    FIX_D --> ALL_D
```

### 2c. Pre-Construction Phase (25–30%)

```mermaid
flowchart TD
    PC_START([Project enters Pre-Construction]) --> ENG_REQ[Engineer: Create requirements - Materials and Specifications]
    ENG_REQ -->|Submit for review| PM_REQ_APPROVE[PM: Approve requirements — gate C1]

    PC_START --> FM_BUDGET[Finance: Create budget lines]
    FM_BUDGET -->|Set planned amounts| FM_APPROVE_BUDGET[Finance: Approve all budget lines — gate C2]

    PC_START --> PM_MILESTONES[PM: Create milestones with dates]
    PM_MILESTONES -->|Set to Active status| C3_CHECK[Gate C3: Milestones dated and active]

    PC_START --> PM_STAFF_SITE[PM: Staff site personnel]
    PM_STAFF_SITE --> HR_LINK[HR/IT: Link to employee records]
    HR_LINK --> PM_CREATE_TASKS[PM/Engineer: Create tasks]
    PM_CREATE_TASKS -->|Assign tasks to staffed site workers| C4_CHECK[Gate C4: Site crew staffed + linked to tasks]

    PC_START --> PM_NTP[PM: Upload Notice to Proceed]
    PM_NTP --> PM_COORDS[PM: Set site latitude/longitude]
    PM_COORDS --> C5_CHECK[Gate C5: NTP + site location]

    PC_START --> ENG_PR[Engineer: Create purchase requests]
    ENG_PR --> C6_CHECK[Gate C6: Procurement initiated]

    PM_REQ_APPROVE --> ALL_C{All C1-C6 gates pass?}
    FM_APPROVE_BUDGET --> ALL_C
    C3_CHECK --> ALL_C
    C4_CHECK --> ALL_C
    C5_CHECK --> ALL_C
    C6_CHECK --> ALL_C
    ALL_C -->|Yes| ADVANCE_CON[PM: Advance to Construction]
    ALL_C -->|No| FIX_C[Fix missing items]
    FIX_C --> ALL_C
```

### 2d. Construction Phase (30–95%, progress from tasks)

```mermaid
flowchart TD
    CON_START([Project enters Construction]) --> SP_WORK[Site Personnel: Work on tasks]
    SP_WORK -->|Update task status| TASK_PROGRESS[Progress calculated from completed/total tasks]

    SP_WORK --> SP_REPORT[Site Personnel: Submit daily site report - DSR]
    SP_WORK --> ENG_REPORT[Engineer: Submit engineering reports]
    SP_WORK --> SP_ISSUES[Site Personnel: Report issues]

    SP_ISSUES --> ENG_RESOLVE[Engineer: Resolve issues]
    ENG_RESOLVE --> PM_CLOSE_ISSUE[PM: Close issue — gate K3]

    CON_START --> PM_WF[PM: Manage active workflows]
    PM_WF -->|All stages decided| K4_CHECK[Gate K4: No active workflows]

    TASK_PROGRESS -->|All tasks Completed| K1_CHECK[Gate K1: All tasks completed]
    CON_START --> PM_CLOSE_MILESTONES[PM: Mark milestones completed/cancelled]
    PM_CLOSE_MILESTONES --> K2_CHECK[Gate K2: All milestones closed]

    K1_CHECK --> ALL_K{All K1-K4 gates pass?}
    K2_CHECK --> ALL_K
    PM_CLOSE_ISSUE --> ALL_K
    K4_CHECK --> ALL_K
    ALL_K -->|Yes| ADVANCE_CL[PM: Advance to Closeout]
    ALL_K -->|No| FIX_K[Continue work]
    FIX_K --> CON_START
```

### 2e. Closeout Phase (95–99%)

```mermaid
flowchart TD
    CL_START([Project enters Closeout]) --> ENG_FIR[Engineer: Submit Final Inspection report]
    ENG_FIR -->|Set status Approved| X1_CHECK[Gate X1: Final inspection approved]

    CL_START --> PM_COC[PM/Admin: Upload Certificate of Completion]
    PM_COC --> X2_CHECK[Gate X2: COC on file]

    CL_START --> HR_PAYROLL[HR: Generate closeout payroll batch]
    HR_PAYROLL --> FM_PAY_APPROVE[Finance: Approve payroll — gate X3]

    CL_START --> PM_CL_WF[PM: Start Project Closeout workflow]
    PM_CL_WF -->|All stages completed| X4_CHECK[Gate X4: Closeout workflow completed]

    CL_START --> PM_CLOSE_RFI[PM: Close all open RFI/RFA]
    PM_CLOSE_RFI --> X5_CHECK[Gate X5: No open RFI/RFA]

    CL_START --> FM_SETTLE[Finance/PM: Settle all purchase requests and orders]
    FM_SETTLE --> X6_CHECK[Gate X6: No unsettled procurement]

    X1_CHECK --> ALL_X{All X1-X6 gates pass?}
    X2_CHECK --> ALL_X
    FM_PAY_APPROVE --> ALL_X
    X4_CHECK --> ALL_X
    X5_CHECK --> ALL_X
    X6_CHECK --> ALL_X
    ALL_X -->|Yes| COMPLETE[PM: Advance to Completed]
    ALL_X -->|No| FIX_X[Fix remaining items]
    FIX_X --> CL_START
    COMPLETE --> ARCHIVE[Admin only: Archive project]
```

### 2f. Special Transitions

```mermaid
flowchart TD
    ACTIVE([Active project in Design / Pre-Construction / Construction]) -->|PM or Admin| HOLD[Put On Hold]
    HOLD -->|Write reason| ON_HOLD([On Hold — writes locked])
    ON_HOLD -->|PM or Admin| RESUME[Resume]
    RESUME --> ACTIVE

    ACTIVE -->|PM or Admin| CANCEL[Cancel project]
    CANCEL -->|Write reason| CANCELLED([Cancelled — writes locked])
```

### 2g. Design Delivery Track (Plan Sets Only)

```mermaid
flowchart TD
    DD_START([Design-type project]) --> DD_PROPOSAL[Proposal phase: same P1-P5 gates]
    DD_PROPOSAL --> DD_DESIGN[Design phase]

    DD_DESIGN --> DP1[Gate DP1: Every plan set has a lead]
    DD_DESIGN --> DP2[Gate DP2: Every plan set has a design with files]
    DD_DESIGN --> DD_D2[Gate D2: All designs approved]
    DD_DESIGN --> DD_D3[Gate D3: Approved current blueprint]
    DD_DESIGN --> DD_D4[Gate D4: No open RFI/RFA]

    DP1 --> DD_ADVANCE{All gates pass?}
    DP2 --> DD_ADVANCE
    DD_D2 --> DD_ADVANCE
    DD_D3 --> DD_ADVANCE
    DD_D4 --> DD_ADVANCE
    DD_ADVANCE -->|Yes| DD_TURNOVER[Turnover phase]

    DD_TURNOVER --> T1[Gate T1: Turnover document on file]
    DD_TURNOVER --> T2[Gate T2: Client acceptance on file]
    DD_TURNOVER --> T3[Gate T3: Design Turnover workflow completed]
    DD_TURNOVER --> T4[Gate T4: No open RFI/RFA]
    DD_TURNOVER --> T5[Gate T5: No unsettled procurement]

    T1 --> DD_COMPLETE{All T1-T5 pass?}
    T2 --> DD_COMPLETE
    T3 --> DD_COMPLETE
    T4 --> DD_COMPLETE
    T5 --> DD_COMPLETE
    DD_COMPLETE -->|Yes| DD_DONE[Completed → Archived]
```

---

## 3. RFI / RFA Flow (Flow 2)

```mermaid
flowchart TD
    RFI_START([Need information or approval]) --> WHO{Who raises it?}
    WHO -->|Engineer| ENG_RFI[Engineer: Create RFI/RFA]
    WHO -->|DCO| DCO_RFI[DCO: Log RFI]

    ENG_RFI --> PM_ROUTE[PM: Route to recipients]
    DCO_RFI --> PM_ROUTE
    PM_ROUTE -->|Multi-recipient, no-login reply link| RECIPIENTS[Recipients receive email with reply link]

    RECIPIENTS --> REPLY[Recipient: Reply via link - no login needed]
    REPLY --> ARCH_ANSWER[Architect/Engineer: Provide technical answer]
    ARCH_ANSWER --> CON_REMARKS[Consultant: Add remarks]
    CON_REMARKS --> PM_SIGN[PM: Sign off on response]

    PM_SIGN -->|Leads to scope change?| CO_DECIDE{Change order needed?}
    CO_DECIDE -->|Yes| PM_CO[PM: Create change order]
    PM_CO --> FM_CO_APPROVE[Finance: Approve change order]
    FM_CO_APPROVE --> ENG_CO_QTY[Engineer: Confirm quantities]
    ENG_CO_QTY --> ADMIN_CO[Admin: Final approval if above limit]
    CO_DECIDE -->|No| RFI_CLOSE[PM: Close RFI/RFA]

    PM_ROUTE --> DCO_TRANSMIT[DCO: Create transmittal - TRN]
    DCO_TRANSMIT --> TRANSMIT_LOG[Transmittal logged in register]
```

---

## 4. Purchasing Flow (Flow 3)

```mermaid
flowchart TD
    NEED([Material or service needed]) --> ENG_PR[Engineer: Create purchase request - PR]
    ENG_PR --> PM_ENDORSE[PM: Endorse purchase request]
    PM_ENDORSE --> FM_APPROVE_PR[Finance Manager: Approve PR]
    FM_APPROVE_PR --> FM_PO[Finance: Create purchase order - PO]
    FM_PO --> DELIVER[Supplier delivers]
    DELIVER --> SP_RECEIVE[Site Personnel: Log delivery receipt - DR]
    SP_RECEIVE --> ENG_INSPECT[Engineer: Inspect delivery]
    ENG_INSPECT --> FM_PAY[Finance: Process payment]

    ENG_PR --> ENG_BCR[Engineer: Create budget change request - BCR]
    ENG_BCR --> PM_BCR[PM: Approve budget change]
    PM_BCR --> FM_BCR[Finance: Approve budget change]

    FM_PO -->|Above limit| ADMIN_PO[Admin: Approve PO above limit]
    ADMIN_PO --> FM_PAY

    subgraph Closeout Check
        FM_PAY --> SETTLE{All PR and PO settled?}
        SETTLE -->|Unsettled| BLOCK[Blocks project closeout - gate X6]
    end
```

---

## 5. Attendance and Payroll Flow (Flow 4)

```mermaid
flowchart TD
    CLOCK([Staff arrives]) --> WHERE{Location?}
    WHERE -->|Office| OFFICE_BTN[Office: One-button clock-in]
    WHERE -->|Site| SITE_PHONE[Site: Phone clock-in with geolocation]

    OFFICE_BTN --> DTR[Daily time record created]
    SITE_PHONE --> GEO_CHECK{Inside geofence?}
    GEO_CHECK -->|Yes| DTR
    GEO_CHECK -->|No| FLAG[Flagged but not blocked]
    FLAG --> DTR

    SITE_PHONE --> DCO_LOG[DCO: Logbook entry]

    DTR --> HR_VERIFY[HR: Verify attendance records]
    HR_VERIFY --> HR_GENERATE[HR: Generate payroll batch]
    HR_GENERATE --> HR_ADD_LINES[HR: Add payroll lines - deductions, overtime]
    HR_ADD_LINES --> HR_SUBMIT[HR: Submit payroll batch]

    HR_SUBMIT --> FM_REVIEW[Finance: Review payroll batch]
    FM_REVIEW -->|Check validation| FM_APPROVE_PAY[Finance: Approve payroll]
    FM_APPROVE_PAY --> PAID[Payroll processed]

    FM_REVIEW -->|Issues found| HR_FIX[HR: Fix payroll entries]
    HR_FIX --> HR_SUBMIT

    subgraph Reports
        HR_VERIFY --> ATT_REPORT[Attendance report]
        FM_APPROVE_PAY --> CONTRIB_REPORT[Contribution report - SSS, PhilHealth, Pag-IBIG]
        FM_APPROVE_PAY --> PAYROLL_REPORT[Payroll summary report]
    end
```

---

## 6. Secure Document Vault Flow (Flow 5)

```mermaid
flowchart TD
    UPLOAD_START([User uploads a file]) --> CONF_LEVEL{Confidentiality level?}
    CONF_LEVEL -->|Internal| INT_UPLOAD[Upload to Drive - gdrive adapter]
    CONF_LEVEL -->|Confidential| CONF_UPLOAD[Upload to Drive - access by grant only]
    CONF_LEVEL -->|Restricted| ENCRYPT[API encrypts with AES-GCM]
    ENCRYPT --> REST_UPLOAD[Upload ciphertext to Drive]

    INT_UPLOAD --> INTEGRITY[SHA-256 hash computed and stored]
    CONF_UPLOAD --> INTEGRITY
    REST_UPLOAD --> INTEGRITY

    INTEGRITY --> DB_RECORD[Record in stored_files table]
    DB_RECORD --> AUDIT[Log upload in audit trail]

    subgraph Access
        USER_ACCESS([User requests file]) --> CHECK_GRANT{Has access grant?}
        CHECK_GRANT -->|No, Confidential/Restricted| REQUEST_ACCESS[Submit document access request - DAR]
        REQUEST_ACCESS --> ADMIN_GRANT[Admin: Grant or deny access]
        CHECK_GRANT -->|Yes or Internal| DOWNLOAD[Download file]
        DOWNLOAD -->|Restricted| DECRYPT[API decrypts before serving]
        DOWNLOAD --> VERIFY[Verify SHA-256 on download]
        DOWNLOAD --> LOG_DL[Log download in audit trail]
    end

    subgraph Versioning
        NEW_VERSION([User uploads new version]) --> VERSION_CHECK[Link to same document, increment version]
        VERSION_CHECK --> INTEGRITY
    end

    subgraph Purge and Legal Hold
        DELETE_REQ([User requests deletion]) --> FIRST_APPROVE[First approver: Admin]
        FIRST_APPROVE --> SECOND_APPROVE[Second approver: Owner]
        SECOND_APPROVE --> PERM_DELETE[Permanent delete from Drive and database]

        LEGAL_HOLD([Admin sets legal hold]) --> BLOCK_DELETE[All deletion blocked on this document]
    end

    subgraph Import
        PICKER([Staff opens Google Picker]) --> SELECT_FILES[Select existing Drive files]
        SELECT_FILES --> INDEX[App indexes: file id + SHA-256]
        INDEX -->|Optionally| COPY_TO_TREE[Copy into managed folder tree]
    end
```

---

## 7. Workflow Engine (Cross-Cutting)

```mermaid
flowchart TD
    INITIATE([Authorized role starts a workflow]) --> SELECT_TPL[Select from 8 seeded templates]
    SELECT_TPL --> CREATE_WF[Create workflow instance for the project]
    CREATE_WF --> STAGE_1[Stage 1: assigned role acts]

    STAGE_1 -->|Decide: Approve| NEXT_STAGE[Move to next stage]
    STAGE_1 -->|Decide: Reject| REJECT_WF[Workflow rejected - notify initiator]
    STAGE_1 -->|Decide: Revise| RESUBMIT[Initiator: Resubmit with changes]
    RESUBMIT --> STAGE_1

    NEXT_STAGE --> MORE{More stages?}
    MORE -->|Yes| STAGE_N[Stage N: next role acts]
    STAGE_N --> MORE
    MORE -->|No| WF_COMPLETE[Workflow completed]

    INITIATE --> ATTACH[Attach files to workflow]
    INITIATE --> FORECAST[View impact forecast]

    subgraph Templates managed by Admin
        ADMIN_TPL([Admin: Create workflow template]) --> DEFINE_STAGES[Define stages, roles, order]
        ADMIN_TPL --> DELETE_TPL[Admin: Delete template]
    end

    subgraph Budget Change Workflow
        ENG_BCR_WF([Engineer starts budget change]) --> FM_BCR_WF[Finance: Review budget impact]
        FM_BCR_WF --> PM_BCR_WF[PM: Approve or reject]
    end
```

---

## 8. Admin and Platform Actions

```mermaid
flowchart TD
    subgraph IT_Designer[IT Designer]
        IT1[Manage user accounts - create, update, delete]
        IT2[Manage roles and permissions]
        IT3[Handle support requests]
        IT4[View audit logs and security overview]
        IT5[Manage document types]
        IT6[View reconciliation data]
        IT7[Configure AI validation references]
    end

    subgraph Admin_Manager[Admin Manager]
        A1[All project management overrides]
        A2[Archive projects - Admin only]
        A3[Manage workflow templates]
        A4[Override PM approvals - needs 10+ char reason]
        A5[View all dashboards and activity logs]
        A6[Approval hierarchy configuration]
        A7[Security settings]
        A8[Manage document types and categories]
    end

    subgraph Owner_Role[Owner]
        O1[View all dashboards - read only]
        O2[Approve purge and legal hold]
        O3[Owner portfolio view]
        O4[Owner approval of proposals]
        O5[Account recovery for IT Designer]
    end

    subgraph Platform_Jobs[Automated Jobs]
        J1[Advisory signals: 8 decision-support rules]
        J2[Attendance exception detection]
        J3[Overdue task notifications]
        J4[Design request sweep]
    end
```

---

## 9. Advisory Decision-Support Signals

The system runs 8 signal rules as background jobs, surfaced on dashboards:

| Signal | What it detects | Who sees it |
|---|---|---|
| Cost variance | Actual vs planned budget divergence | Finance, PM, Admin |
| Cumulative change impact | Total change orders as % of contract | PM, Admin |
| Burn vs progress | Money spent vs % complete | Finance, PM |
| Issue recurrence | Same issue category repeating | Engineer, PM |
| Stalled stage | Workflow stage stuck past threshold | Current stage owner |
| Projected finish | Estimated completion vs deadline | PM, Admin |
| Overdue tasks | Tasks past their due date | Site Personnel, PM |
| Milestone slip | Milestone behind estimated date | PM, Admin |

---

## 10. Role Action Summary

| Role | Creates | Approves / Decides | Views |
|---|---|---|---|
| **Owner** | — | Purge, legal hold, proposals | All dashboards (read-only), portfolio |
| **Admin** | Workflow templates, document types | Phase override, archive, PO above limit, admin override with reason | All projects, activity logs, security |
| **IT Designer** | User accounts, roles, permissions | Support requests | Audit logs, security, reconciliation |
| **Project Manager** | Projects, milestones, tasks, change orders, reports | Proposals, requirements, RFI routing, budget changes, design reviews, phase advance | Staffed projects, approvals |
| **HR** | Payroll batches, employee records, attendance | Attendance verification | Workforce, attendance |
| **Finance Manager** | Budget lines, POs, payments | PR, budget changes, payroll, expense reports | Budget, expenses, profitability |
| **Architect** | Proposals, designs, blueprints, revisions | RFI answers, plan set leads | Staffed projects, documentation |
| **Engineer** | Requirements, purchase requests, tasks, issues, reports | Delivery inspection, budget change requests | Staffed projects, issues |
| **Consultant** | Design reviews, advisory docs | Proposal review, design review, RFI remarks | Staffed projects, proposals |
| **Site Personnel** | DTR (attendance), daily site reports, deliveries | Task status updates | Own tasks, own attendance |
| **DCO** | RFI logs, transmittals, logbook entries | — | Staffed projects |

---

Related: [[03 Roles and Permissions]] · [[04 Flows, Forms and Screens]] · [[08 Open Questions]]