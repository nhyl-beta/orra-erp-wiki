---
tags: [orra-erp, documents, vault]
---
# Documents and Confidentiality
Up: [[00 Start Here]]

## Form codes used across the flows
> [!note] Code meanings are inferred from the flow step each code sits on (see the sample-documents deliverable for the authoritative register).

| Code | Document |
|---|---|
| PRP | Proposal |
| NOA | Notice of Award |
| CTR | Contract |
| BLP | Blueprint / plan set |
| TOD | Turnover document |
| CAF | Client acceptance form |
| TRN | Transmittal |
| RFI / RFA | Request for Information / Approval |
| CO | Change order |
| PR / PO | Purchase request / purchase order |
| DR | Delivery receipt |
| BCR | Budget change request |
| DSR | Daily site report |
| WPR | PM weekly progress report |
| PBR | Progress billing |
| FIR | Final inspection report |
| COC | Certificate of completion |
| DTR | Daily time record (attendance) |
| PAY | Payroll |
| DAR | Document access request |

The sample-documents deliverable holds a **24-type register**, a numbering and confidentiality standard, and 15 filled sample forms (RFI, RFA, TRN, PR, PO, DR, DSR, DTR, PAY, BCR, CO, WPR, PBR, FIR, DAR). See [[10 Deliverables]].

## Confidentiality levels (assumption, awaiting confirmation)
Three levels: **Internal**, **Confidential**, **Restricted**. Contracts and payroll are Restricted. Access to Confidential and Restricted is by grant (G in the matrix); when Drive is the store ([[13 Google Drive Integration]]), Restricted files are encrypted by the API before upload; Restricted needs two-step sign-in; purge, legal hold and retention need a second approver. See [[03 Roles and Permissions]].

## Vault behaviour
- Editable document types; file integrity check on upload; versioned uploads.
- Download and project-edit actions are written to the audit trail.
- Open questions: who may delete or download legal and CAD files, which documents are Restricted, retention periods ([[08 Open Questions]], questions 7–8).
