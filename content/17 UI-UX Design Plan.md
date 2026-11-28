---
tags: [orra-erp, ui-ux, refactoring-brief, procore, monday, roles]
aliases: [UI-UX Design Plan, Refactoring Brief, UX Strategy, Complete Project Understanding]
Up: [[00 Start Here]]
---

# Orra-ERP — UI/UX Design Plan and Refactoring Brief

> [!summary]
> A consolidated working brief (originally drafted externally, cleaned up and cross-linked here) covering the UX problem, a hybrid Procore × monday.com design philosophy, the full business-process understanding from the 11 Nov interview, and a development roadmap. It supersedes an earlier, shorter draft of the same ideas — that draft's unique concrete detail (interaction strategies, phased UX plan, success metrics) has been folded into §9 below rather than kept as a separate section. See [[16 Platform Benchmarking (Procore, Monday, Payroll)]] for the Procore/monday.com/payroll research this draws on, and [[14 Interview Integration Plan (11-11-26)]] for the interview analysis it's built from. **A "Correlation with the existing wiki" section at the end flags where this brief agrees, extends, or conflicts with decisions already recorded elsewhere in the wiki — read that before treating anything here as settled.**

## PART 1 — UNDERSTANDING THE PROJECT

### 1.1 What is Orra-ERP?

Orra-ERP is a client-oriented company and construction operations management platform intended to centralize ORRA Construction's information, project records, company documents, and operational activities.

The system originated from EasyConstruct, which was developed as an academic thesis project. Although EasyConstruct already provides several construction-management modules, the system was initially designed using generalized business processes and predefined workflows.

The client implementation is different.

Orra-ERP must reflect how ORRA actually manages its projects, communicates with clients and other external parties, handles company records, maintains employee documents, and organizes construction-related information.

The purpose is not simply to add more features or reproduce an existing commercial construction-management platform.

The purpose is to establish a practical digital environment that supports ORRA's real operations.

### 1.2 The relationship between EasyConstruct and Orra-ERP

These two systems should be treated as separate products.

**EasyConstruct**

- Academic thesis implementation.
    
- Developed around generalized construction-management processes.
    
- Includes multiple predefined roles and workflows.
    
- Contains broader functionality intended to demonstrate a comprehensive construction-management system.
    
- Serves as the technical starting point and source of reusable components.
    

**Orra-ERP**

- Client-oriented implementation.
    
- Based on ORRA's organizational structure and actual business requirements.
    
- Removes unnecessary thesis-oriented functionality.
    
- Revises roles, permissions, and workflows.
    
- Prioritizes company records, project records, document management, and operational usability.
    
- Can introduce additional functionality based on ORRA's confirmed needs.
    

The existing code should therefore be treated as a reusable technical foundation, not as the definitive specification of the client product.

### 1.3 What ORRA actually wants

The November 11 interview reveals that ORRA has a relatively straightforward immediate objective.

The company wants to stop losing time searching for files and managing information scattered across different folders and storage locations.

The Admin repeatedly emphasizes that:

- Employee documents must be complete and updated.
    
- Project contracts and important documents must be easy to find.
    
- Projects must have centralized records.
    
- Ongoing and completed projects must be organized separately.
    
- Important project dates and documents must be accessible in one place.
    
- External project participants must be able to access the appropriate shared documents.
    
- Company information must remain confidential.
    
- The interface must be simple enough for non-technical personnel to use.
    

The IT Designer also emphasizes that the system must retain enough functionality to be useful, without making the interface unnecessarily complicated.

These statements establish the main product direction:

**Orra-ERP should prioritize information organization, document retrieval, project visibility, and operational simplicity.**

---

## PART 2 — THE CORE PROBLEM

### 2.1 The central business problem

ORRA currently experiences difficulties maintaining and retrieving company and project information.

Documents may be stored across different folders, individual computers, shared storage, and other locations. Employees may need to ask colleagues to retrieve contracts or other files because they do not immediately know where the documents are stored.

This increases the time required to retrieve information and creates the possibility of inconsistent copies, outdated documents, or missing records.

The problem is not simply that the company lacks software.

The problem is the absence of a unified and dependable method of organizing, locating, maintaining, and controlling access to operational information.

### 2.2 Supporting problems

**A. Fragmented document storage**

Project documents and company records are difficult to locate because they are distributed across different storage locations.

**B. Incomplete employee records**

Employee 201 files need to be maintained in one identifiable and organized location, with monitoring for missing and expiring documents.

**C. Lack of a consolidated project registry**

Management needs to see all ORRA projects and retrieve their essential information without manually searching through separate folders.

**D. Unclear separation of responsibilities**

Company administration, HR, finance, and project management have overlapping or incorrectly grouped functions in the thesis implementation.

**E. Excessive interface complexity**

The current style of presenting too much information in the same screen makes it difficult to identify important information quickly.

**F. Document access and confidentiality**

Company employees, consultants, clients, designers, contractors, and administrators require different access levels.

**G. Unnecessary system-enforced processes**

Some thesis workflows require users to complete actions that may not exist in ORRA's actual procedures.

### 2.3 Refined problem statement

Orra-ERP addresses the difficulty of organizing and retrieving company and project information within ORRA Construction.

The existing information-handling practices create unnecessary dependence on individual employees to locate documents, maintain project records, and coordinate information across different storage locations.

The existing thesis-derived application also contains predefined workflows and role requirements that do not fully correspond to ORRA's actual organizational structure and operational procedures.

These limitations create a need for a centralized and user-oriented platform that simplifies document management, establishes organized project records, separates company administration from project operations, and provides controlled access to relevant information.

The system must support the company's existing working practices while reducing unnecessary administrative effort and technical barriers to system usage.

### 2.4 Product objective

Develop a centralized company and project information management platform that enables ORRA personnel to organize, search, retrieve, monitor, and preserve company and construction-project records through a unified and accessible interface.

---

## PART 3 — THE ACTUAL ORRA BUSINESS ENVIRONMENT

### 3.1 ORRA's position in a construction project

The November 11 interview provides the San Pablo project as an example of ORRA's role in a Construction Management engagement.

The example identifies the following parties:

|Organization|Responsibility|
|---|---|
|ORRA|Construction Manager|
|HOJ|Client / Owner|
|WTA|Designer|
|CMEC|Contractor|

ORRA is positioned between the client, designer, and contractor, coordinating project-related activities and information.

The Project Manager is responsible for overseeing the project and coordinating relevant communications, records, and activities.

### 3.2 Why this matters to system design

Orra-ERP must distinguish between:

- Internal ORRA personnel.
    
- Project-specific internal personnel.
    
- External consultants.
    
- Clients and project owners.
    
- Designers.
    
- Contractors.
    
- Other authorized external participants.
    

These parties do not automatically share the same responsibilities or information-access requirements.

For example, an external consultant may need access to assigned plans and a Terms of Reference, but not the full project contract or other confidential legal documents.

Similarly, an employee's HR documents should not become visible simply because that employee has been assigned to a construction project.

The system must organize information according to its actual business context.

---

## PART 4 — THE THREE MAIN SYSTEM AREAS

The entire application should be organized around three major operational areas.

### 4.1 Company Administration

Handles information about the company and its personnel.

Includes:

- Employee records.
    
- Employee 201 files.
    
- Employment documents.
    
- Employee status.
    
- Consultant records.
    
- Professional-license monitoring.
    
- Administrative forms and records.
    
- Account creation coordination.
    
- Employee offboarding.
    

### 4.2 Project Operations

Handles information related to individual projects.

Includes:

- Project registration.
    
- Project registry and project details.
    
- Client and stakeholder information.
    
- Project contracts and milestones.
    
- NOA, NTP, and COC records.
    
- Project schedules and progress.
    
- Project-specific documents.
    
- RFI/RFA correspondence.
    
- Project-related approvals and reporting.
    
- Project completion and archiving.
    

### 4.3 Financial and Workforce Operations

Handles company financial and workforce information that may be related to projects but must maintain its own business records.

Includes:

- Attendance information.
    
- Payroll preparation and review.
    
- Financial records.
    
- Project budget information.
    
- Procurement, if applicable.
    
- Purchase requests and orders, subject to process confirmation.
    

These three areas should share appropriate information without forcing one department to manage another department's responsibilities.

---

## PART 5 — DETAILED BUSINESS PROCESSES

### 5.1 Project Registry

**Priority: Critical**

The Project Registry is one of the most important features requested during the interview.

ORRA wants to see all company projects in a centralized list.

The requested organization includes separate views for:

- Ongoing projects.
    
- Completed projects.
    
- Overall project history.
    
- Projects awaiting or undergoing bidding, where relevant.
    

The system should have a searchable table.

#### Required project information

|Field|Purpose|
|---|---|
|Project ID|Unique project identifier|
|Project Name|Official name|
|Client / Owner|Responsible client organization|
|Project Type|Type or classification of project|
|Project Location|Physical address|
|Contract Amount|Recorded project value|
|Notice of Award Date|Award information|
|Contract Date|Contract execution or validation date|
|NTP Date|Notice to Proceed date|
|Start Date|Project commencement|
|Completion Date|Actual or recorded completion|
|Project Manager|Assigned responsible person|
|Status|Current project condition|

#### Expected user interaction

1. Authorized user opens the Project Registry.
    
2. The system displays projects in a structured table.
    
3. The user searches using the project name, ID, owner, or other supported fields.
    
4. The user filters the project list by status.
    
5. The user selects a project.
    
6. A readable project details view opens.
    
7. The project information and associated documents are displayed together.
    
8. Authorized users can open or print the required documents.
    

The user should not need to navigate through several unrelated screens to retrieve a project's basic information.

### 5.2 Project Document Milestones

ORRA specifically identifies three important documents that should be maintained in the project record.

**Notice of Award (NOA)**

Issued by the client to communicate the award of the project.

**Notice to Proceed (NTP)**

Issued by the client to authorize commencement of the project.

The Admin explains that the day following the NTP date becomes the project's start date under ORRA's stated procedure.

**Certificate of Completion (COC)**

A completion document that should be stored in the project record when the project has been completed.

#### Expected process

Project registration → NOA received → Contract recorded → NTP received → Start date recorded → Project monitored → COC uploaded → Project declared completed → Historical record retained.

NOA, NTP, and COC should be accessible through the project details view.

The system records documents supplied by the appropriate parties. It must not generate or falsely authorize documents that are issued by the client.

### 5.3 Employee 201 File Management

**Priority: Critical**

ORRA wants employee records to contain the complete employment-related documents of each individual.

The employee's information should be searchable through an employee name or ID.

#### Employee information

- Employee ID.
    
- Full name.
    
- Employment classification.
    
- Hiring date.
    
- Employment status.
    
- Position.
    
- Department or discipline.
    
- Relevant personal information.
    

#### Employee documents

- Identification documents.
    
- Employment-related legal documents.
    
- Previous-employer employment certificates, subject to confirmation of the exact required document.
    
- NBI clearance.
    
- Health certificates or clearances.
    
- Training certificates.
    
- Other required employment documents.
    

#### Expected process

1. Admin/HR creates an employee record.
    
2. The system provides a corresponding 201 file.
    
3. Required documents are uploaded and categorized.
    
4. The system monitors the completeness of the employee's file.
    
5. Missing documents are identified.
    
6. Expiration dates are monitored where applicable.
    
7. Notifications inform authorized personnel of missing or expiring documents.
    
8. Updated documents are uploaded and retained in the employee's record.
    

Employee records should not require a project association to exist.

An employee may work on multiple projects, while their employment records remain under company administration.

### 5.4 Consultant Management

**Priority: High**

ORRA distinguishes between regularly employed personnel and consultants.

Consultants may be engaged through intermittent visits or on-call arrangements.

Therefore, the system should distinguish employee classification rather than treating every professional as an ordinary monthly employee.

Consultant information may include:

- Consultant ID.
    
- Name.
    
- Professional discipline.
    
- Engagement type.
    
- Assigned project.
    
- PRC license details.
    
- PTR details.
    
- License expiration dates.
    
- Terms of Reference.
    
- Assigned plans and related documents.
    

#### Expected process

Consultant registration → Project assignment → Required document registration → License expiration monitoring → Renewal notification → Updated documents retained.

Consultant access must remain restricted.

The interview identifies the Terms of Reference and relevant plans as documents available to consultants assigned to the project.

They should not automatically receive access to project contracts, NOA, NTP, employee files, or unrelated legal documents.

### 5.5 Project-Based Document Management

**Priority: Critical**

The document-management system must prevent files from becoming scattered across individual folders and storage locations.

The client specifically prefers a setup that avoids duplicate documents.

#### Required behavior

- Each project has a corresponding document directory or Drive location.
    
- Documents are organized according to recognizable categories.
    
- Each document can be searched by relevant information.
    
- Shared documents can be referenced by multiple authorized users.
    
- The same original file should not be uploaded repeatedly merely to make it visible to different people.
    
- The system maintains document references and project associations.
    
- Authorized users can open the original document directly.
    

Example:

An Administrator searches for the Contract of San Pablo.

The system identifies the appropriate project contract and allows the user to open the corresponding file.

The user should not have to ask which employee uploaded it or which personal folder contains it.

### 5.6 Google Drive Integration

The interview identifies Google Drive as ORRA's preferred existing cloud-storage resource.

The client reports having an approximately 2 TB subscription and also mentions an existing on-premises storage server that is already full.

The objective is to maximize the value of existing storage rather than unnecessarily creating another expensive file-storage environment.

#### Project-based Drive structure

Each project should have an associated Drive location.

Authorized participants may include:

- ORRA personnel assigned to the project.
    
- Client / Owner.
    
- Designer.
    
- Contractor.
    

The Project Manager coordinates the sharing of relevant files.

External participants should be able to open the required document and provide the necessary responses or supporting files through the agreed shared-document process.

Orra-ERP should serve as the organized record and navigation point.

#### Technical decisions still required

- Whether Orra-ERP stores files directly in Drive or primarily indexes Drive links.
    
- Whether Google Workspace APIs will be used.
    
- How shared folders and file permissions are administered.
    
- How the existing company server will be accessed or migrated.
    
- What storage and file-size limitations apply to the selected architecture.
    

The interview establishes the preference for using Google Drive, but does not finalize the technical integration architecture.

### 5.7 Mother Library

**Priority: Secondary**

The Mother Library is a separate company-wide architectural and engineering resource library.

It stores reusable technical design details that can be retrieved, modified, and applied to new projects.

Examples include:

- Door details.
    
- Window details.
    
- Stair details.
    
- Cabinet details.
    
- Gutter details.
    
- Wall details.
    
- Ceiling details.
    
- Other standardized architectural and engineering details.
    

Files may include DWG, CAD, Revit, and other professional design formats.

#### Expected process

1. Authorized technical personnel upload standardized design resources.
    
2. Resources are categorized according to discipline and design type.
    
3. Architects search for and retrieve reusable resources.
    
4. The resource is copied for a specific project.
    
5. The copied resource is modified according to the project's requirements.
    
6. The modified file is stored in the corresponding project folder.
    
7. The original master file remains unchanged.
    

This prevents the company from losing standardized technical references through uncontrolled modification.

### 5.8 Project Coordination and External Correspondence

**Priority: High**

ORRA's Project Manager coordinates with the client, designer, contractor, and other involved parties.

The project Drive serves as the shared document environment.

Examples of information that may be managed through this environment include:

- RFI.
    
- RFA.
    
- Material approval requests.
    
- Drawing revisions.
    
- Technical clarification.
    
- External correspondence.
    
- Supporting documents.
    

Orra-ERP should provide an internal register for tracking relevant documents and communication records.

The exact RFI/RFA process and the question of external Orra-ERP accounts require further validation.

The interview does not establish that every external request must be processed through an internal multi-stage approval engine.

### 5.9 Account Management and Employee Offboarding

**Priority: Critical**

System accounts should be associated with actual employee records.

#### Account creation

Employee registration → Account creation by IT → Role assignment → Account activation.

The employee record is established first, allowing account information to be linked to the correct person.

#### Employee resignation or deactivation

When an employee leaves the company:

1. Their employment status is updated.
    
2. Their system account is deactivated by authorized personnel.
    
3. Their historical 201 file is retained.
    
4. Their previous project assignments are preserved.
    
5. Their account access is revoked.
    
6. The historical project information remains accessible to authorized personnel.
    

Deactivating an account must not erase historical information.

The interview explicitly emphasizes that the company must retain the history of which personnel worked on specific projects.

### 5.10 Owner Dashboard

**Priority: High**

The Owner's interface should prioritize company-wide visibility.

The interview specifically describes a preference for graphical and visual summaries instead of highly detailed operational screens.

The Owner should be able to see:

- Total projects.
    
- Ongoing projects.
    
- Completed projects.
    
- Project completion percentages.
    
- Project schedules.
    
- Budget summaries.
    
- Project reports.
    
- Relevant project details.
    
- Supporting plans and authorized documents.
    

The interface should answer:

- How many projects are ongoing?
    
- Which projects are completed?
    
- What is the progress of each project?
    
- What is the relevant project budget?
    
- What projects require attention?
    

The Owner's view should not reproduce the detailed daily tasks of Engineers, Project Managers, HR, or Finance.

### 5.11 Administrative Forms and Records

During the interview, the Admin clarified that certain approval-related forms and documents should be categorized under administration instead of HR.

The discussion mentions forms involving approval and company seals, including a reference to a five-day with-pay matter.

The precise document and approval procedure were not fully explained.

These items should be documented separately and validated with the Admin rather than automatically placed under employee HR records.

---

## PART 6 — CURRENT ROLE AND RESPONSIBILITY STRUCTURE

### 6.1 Owner

Primary responsibility:

- Company-wide oversight.
    
- Project summaries.
    
- Graphical dashboards.
    
- Relevant document visibility.
    
- Emergency recovery authority, subject to secure procedures.
    

### 6.2 Admin / HR

The interview indicates that HR should primarily maintain employee records and 201 files.

Admin functions include company-level administrative records and approval-related documentation.

The precise combination of Admin, HR, and Finance permissions remains to be finalized.

### 6.3 Finance

The client raised Finance as an area where the original system's features were too broad.

However, the November 11 transcript does not fully define the actual Finance workflow.

Finance should not be assigned additional accounting or procurement processes until the relevant personnel validate them.

### 6.4 IT Designer

Primary responsibilities:

- System administration.
    
- Account creation.
    
- Account activation and deactivation.
    
- Technical configuration.
    
- Account recovery coordination.
    
- Security and sensitive-event monitoring.
    

IT should not become the ordinary operator of HR and project documents.

### 6.5 Project Manager

The interview identifies the Project Manager as a project-side administrator.

The PM is responsible for project coordination and operational information.

The San Pablo example identifies its Project Manager as a Civil Engineer.

The PM should primarily handle:

- Project records.
    
- Project dates.
    
- Project schedules.
    
- Technical coordination.
    
- RFI/RFA tracking.
    
- Project correspondence.
    
- Site/project monitoring.
    
- Project progress records.
    

The PM should not be responsible for employee 201 files or general payroll administration.

### 6.6 Architects

Primary responsibilities:

- Architectural design.
    
- Drawings and plans.
    
- Revisions.
    
- Technical deliverables.
    
- Retrieval and modification of Mother Library resources.
    

The Mother Library is intended to be accessible to authorized architectural users.

### 6.7 Engineers

Engineering personnel can have different disciplines, including:

- Civil.
    
- Structural.
    
- Sanitary.
    
- Electrical.
    
- Mechanical.
    

Their system access should correspond to their actual project assignments and technical responsibilities.

The interview does not establish that all Engineers must have identical permissions.

### 6.8 Consultants

Consultants are external or intermittent professionals.

They may be assigned to specific projects and receive limited document access.

The interview identifies TOR and plans as the relevant materials.

### 6.9 Site Personnel

The separation between Site Personnel and PM/Engineering personnel is not fully resolved.

The interview notes that an actual Project Manager may also perform site-related activities.

The system should not create unnecessary separate accounts for responsibilities that may belong to the same person.

However, technical and operational permissions must still be clearly distinguished.

### 6.10 Document Control Officer

The November 11 interview does not conclusively establish DCO as a separate organizational role.

Document-control functions should be retained as responsibilities, but a dedicated role should only be created if ORRA confirms the position.

---

## PART 7 — WHAT SHOULD CHANGE FROM EASYCONSTRUCT

The public thesis implementation contains a fixed project lifecycle:

Proposal → Design → Pre-Construction → Construction → Closeout → Completed → Archived.

It also has On Hold and Cancelled states.

The problem is not necessarily the existence of these statuses. The problem is the mandatory conditions that the original implementation requires before a project can advance.

### 7.1 Proposal requirements

The thesis requires:

- Architect assignment.
    
- Consultant assignment.
    
- Proposal submission.
    
- Proposal approval.
    
- NOA and contract documentation.
    
- Contract value.
    

Refactoring:

- Do not require a consultant for every project.
    
- Make team assignments dependent on actual engagement requirements.
    
- Keep proposal and award records.
    
- Preserve NOA and contract documentation.
    

### 7.2 Design requirements

The thesis requires:

- Design files assigned to an Engineer.
    
- Approval of all designs.
    
- Approved current blueprints.
    

Refactoring:

- Keep design records, files, and revision history.
    
- Make discipline and engineering assignment conditional.
    
- Distinguish draft, review, revision, approved, and issued documents.
    
- Validate the actual design approval sequence.
    

### 7.3 Pre-Construction requirements

The thesis currently includes:

- Materials and Specifications approval.
    
- Budget approval.
    
- Dated and active milestones.
    
- Site workers assigned to tasks.
    
- NTP and site coordinates.
    
- At least one purchase request.
    

Refactoring:

- Do not require site coordinates for every project.
    
- Do not require site workers for engagements that have no site workforce.
    
- Do not require procurement when no purchases are needed.
    
- Make budget and material approvals applicable according to the contract and service scope.
    
- Retain actual NTP records and project date monitoring.
    

### 7.4 Construction requirements

The thesis requires:

- All tasks completed.
    
- All milestones completed or cancelled.
    
- No open issues.
    
- No active workflows.
    

Refactoring:

- Avoid universal blocking rules.
    
- Keep task and milestone monitoring.
    
- Allow non-critical outstanding issues to be tracked and carried into approved closeout arrangements.
    
- Separate project completion from the state of every unrelated workflow.
    

### 7.5 Closeout requirements

The thesis currently checks:

- Final inspection.
    
- Certificate of Completion.
    
- Payroll approved after entering Closeout.
    
- Completed closeout workflow.
    
- No open RFI/RFA.
    
- No unsettled procurement.
    

Refactoring:

- Payroll must be independent from project completion.
    
- Separate operational completion from financial settlement.
    
- Retain historical project records.
    
- Track unresolved requests and deficiencies through explicit disposition or carry-forward procedures.
    
- Use a configurable completion and handover checklist.
    

**The main principle is that project advancement should depend on actual business requirements, not artificial system-generated conditions.**

---

## PART 8 — WHAT SHOULD BE REMOVED, SIMPLIFIED, RETAINED, OR DEFERRED

### Remove from the initial client scope unless a business need is confirmed

- Unnecessary employee-to-project dependencies.
    
- Duplicated document uploads.
    
- Unnecessary role-specific duplicate records.
    
- Mandatory consultant assignment for all projects.
    
- Mandatory procurement initiation.
    
- Mandatory site workforce assignment for all engagements.
    
- Payroll as a project-closeout condition.
    
- Automatic deletion of historical employee or project records.
    
- Artificial approval stages not used by ORRA.
    

### Simplify

- Project lifecycle checks.
    
- Project dashboards.
    
- Document upload and retrieval.
    
- Employee management.
    
- Consultant management.
    
- RFI/RFA tracking.
    
- Role-based access.
    
- Project history and archive.
    

### Retain

- Project registry.
    
- Project details.
    
- NOA, NTP, and COC.
    
- Employee 201 records.
    
- Document categories.
    
- Search functionality.
    
- Project-specific file access.
    
- Account management.
    
- Audit records.
    
- Project status and history.
    
- Owner overview dashboard.
    

### Defer pending confirmation

- Full procurement workflow.
    
- Detailed accounting.
    
- Advanced payroll computation.
    
- External client portal.
    
- Full external approval engine.
    
- Advanced change-order automation.
    
- Advanced BIM integrations.
    
- Automated Google Drive upload and OAuth integration.
    
- Advanced safety-management features.
    
- Advanced AI-driven price validation.
    

---

## PART 9 — PROPOSED UI/UX DESIGN DIRECTION

### 9.1 The central usability problem

Orra-ERP serves individuals with different levels of computer familiarity.

Some users can quickly navigate tables, forms, dashboards, and complex menus.

Others need more straightforward interaction patterns and recognizable actions.

The system must support both.

The solution is not to create one stripped-down application and another complicated application.

The solution is to design one comprehensive application that presents the right information and actions at the right time.

### 9.2 Hybrid Procore × monday.com design philosophy

**Procore — Business Process and Construction Management Reference**

Borrow:

- Project-centered information organization.
    
- Document registers.
    
- Project tracking.
    
- RFI and technical document records.
    
- Construction-related activities.
    
- Project history.
    

**monday.com — User Interaction and Visual Management Reference**

Borrow:

- Clean dashboards.
    
- Visual status indicators.
    
- Table and board views.
    
- Clear action buttons.
    
- Searchable and organized lists.
    
- Simplified interaction.
    
- Progress visualization.
    

**Orra-ERP — Final design direction**

Construction-oriented functionality presented through accessible, role-centered, and visually understandable interactions.

### 9.3 Interface principles

**A. Role-centered dashboards**

Every user should see the records and actions relevant to their position.

**B. Table-first information organization**

Use structured columns for project registries, employee records, documents, and administrative registers.

**C. Search-first retrieval**

Users should be able to search for a project contract or employee record without understanding the underlying storage structure.

**D. Progressive disclosure**

Show essential information first and reveal advanced options when necessary.

**E. Consistent actions**

Use recognizable buttons for Create, Edit, View, Upload, Print, Archive, and other common operations.

**F. Clear statuses**

Combine labels, icons, and consistent colors to communicate progress and outstanding actions.

**G. Reusable interface components**

Use consistent interaction and visual patterns across all modules.

**H. Mobile-friendly site operations**

Consider the actual device and environment used by site personnel.

### 9.4 Recommended application navigation

Home / My Workspace

- Project Registry.
    
- My Work.
    
- Company Administration.
    
- Finance and Workforce.
    
- Project Documents.
    
- Mother Library.
    
- Reports.
    
- Administration and Security.
    

The final menu must be filtered by role and permission.


### 9.5 Detailed interaction strategies

#### 9.5.1 Role-centered dashboards

**Replace the concept of showing users the entire system with showing them what they need to accomplish.**

For example, an Owner, Site Personnel, Project Manager, and HR employee should not have the same dashboard.

![[Pasted image 20261128215354.png]]

The dashboard should answer three questions immediately:

1. What is happening?
    
2. What needs my attention?
    
3. What should I do next?


Different roles receive different versions of the dashboard, based on their actual responsibilities and permissions.

For example:

|User|Dashboard priority|
|---|---|
|Owner|Overall project health, financial summaries, critical issues|
|Project Manager|Pending approvals, milestones, RFIs, project progress|
|Admin/HR|Employee records, attendance, payroll preparation|
|Finance|Purchase requests, purchase orders, payment approvals|
|Architect/Engineer|Assigned projects, drawings, RFIs, technical submissions|
|Site Personnel|Clock-in, daily reports, delivery records|
|DCO|Document registrations, transmittals, RFI records|

These are proposed dashboard priorities and should be validated against the final client-approved role definitions.

#### 9.5.2 Task-first interaction

Users should not need to understand which module contains a particular function before performing an action.

Consider two different approaches.
![[Pasted image 20261128215511.png]]


The module still exists. However, the user can reach their work through a more natural interaction.

This approach is particularly important for people who only use the system occasionally.

#### 9.5.3 Progressive disclosure

This is probably the most important design principle for your particular problem.

Instead of displaying every possible option immediately, expose the essential actions first and reveal advanced controls only when necessary.

This is known as **progressive disclosure**. It is a recognized UX technique for balancing learnability and efficiency for both beginner and experienced users.

For example, consider creating a purchase request.
![[Pasted image 20261128215555.png]]

The beginner sees what is necessary. The experienced user can access additional controls.

The key is that both users are using the same system, the same records, and the same approval process.

#### 9.5.4 Visual status communication

Reduce the amount of interpretation required from users.

For instance, instead of requiring users to understand a complicated workflow or inspect an entire record, present the status directly.

![[Pasted image 20261128215613.png]]


Use a consistent status system throughout the application.

For example:

- Green: Approved or completed.
    
- Yellow: Needs attention or awaiting action.
    
- Blue: In progress.
    
- Red: Rejected, blocked, or overdue.
    
- Gray: Not started or inactive.


Always accompany colors with text and, where useful, icons. Users should never have to rely on color alone.

#### 9.5.5 Guided workflows and simplified forms

A user should understand what they are doing, what information is required, and what happens after they submit it.

Rather than giving users a complicated form with many unrelated fields, organize the process into understandable sections.

For example, an RFI workflow could be:

**Example — RFI submission flow:**

1. **Select project**
    
    Choose the project associated with the inquiry.
    
2. **Describe the concern**
    
    Enter the technical question and attach relevant drawings or images.
    
3. **Select recipient**
    
    Choose the responsible Architect or Engineer.
    
4. **Review submission**
    
    Display the information before final submission.
    
5. **Track progress**
    
    Show who needs to respond and the current RFI status.
    

This is especially relevant because your documented RFI/RFA process involves multiple participants, including the Project Manager, Architect/Engineer, Consultant, and DCO.

The interface should explain the process without making users memorize the entire organizational workflow.

#### 9.5.6 One data source, different user views

This is a critical architectural principle.

You should not create completely separate systems or duplicate records just to accommodate different users.

Instead:

![[Pasted image 20261128220241.png]]

For example, a Project Manager might review purchase requests in a visual approval queue, while Finance accesses the same records through a detailed procurement register.

No duplicated records. No inconsistent status updates. No separate business logic.

This also aligns with monday.com's use of multiple views and consolidated dashboards over shared work data.

### 9.6 Information architecture: My Work vs. Projects

Organize the interface around the following hierarchy.
![[Pasted image 20261128220439.png]]

I particularly recommend separating **My Work** from **Projects**.

These serve different mental models:

- Projects answers: "What is happening with the construction projects?"
    
- My Work answers: "What do I need to accomplish?"

This distinction makes the system easier to understand because users can focus on their responsibilities without having to navigate the full project structure.

### 9.7 Phased UX implementation plan

Do not redesign every screen simultaneously. That introduces unnecessary development work and makes it difficult to determine whether the new design actually solves the problem.

I recommend the following implementation sequence.

1. **Phase 1 — User and workflow analysis**
    
    Before designing, identify the different types of users and their actual responsibilities.
    
    Gather information about:
    
    - Most frequently used functions.
        
    - Tasks that users find confusing.
        
    - Forms that require the most assistance.
        
    - Common mistakes and incorrect submissions.
        
    - Tasks performed on mobile versus desktop.
    
    
    Create user profiles based on actual working behavior and digital proficiency, not age alone.
    
2. **Phase 2 — Information architecture redesign**
    
    Reorganize the application around user responsibilities.
    
    Determine which modules belong in the main navigation, which actions deserve quick access, and which settings should remain administrative.
    
    Finalize the role-to-module mapping before building role-specific dashboards.
    
3. **Phase 3 — UX/UI prototyping**
    
    Develop high-priority screens first:
    
    - Home / My Workspace
        
    - Project overview
        
    - My Work
        
    - Requests and approvals
        
    - Document vault
        
    - Attendance
        
    - Purchasing
        
    
    Create working prototypes in Figma and test them with actual ORRA personnel before committing to implementation.
    
4. **Phase 4 — Component and interaction redesign**
    
    Establish a unified design system covering typography, colors, spacing, buttons, forms, cards, tables, status labels, navigation and responsive behavior.
    
    Implement reusable components rather than independently styling every module.
    
5. **Phase 5 — Progressive implementation**
    
    Refactor the existing front end incrementally.
    
    Prioritize common and high-impact workflows. Preserve existing API contracts, data structures, approval logic, document security, and permission enforcement wherever possible.
    
6. **Phase 6 — Usability testing and refinement**
    
    Test with actual users of different technical proficiency levels.
    
    Observe how they complete tasks without giving them instructions first. Identify where they hesitate, make mistakes, or require help.
    
    Refine the interface based on the observed problems rather than personal design preferences.
    

### 9.8 Usability success metrics

I would introduce a usability evaluation framework.

|Measurement|What you should evaluate|
|---|---|
|Task completion rate|Can users finish their assigned tasks?|
|Task completion time|How long does it take to complete common operations?|
|Error frequency|How often do users make incorrect submissions or selections?|
|Navigation efficiency|How many unnecessary steps do users take?|
|Assistance dependency|How often do users need help from IT or administrators?|
|User confidence|Do users understand what they are doing and what happens next?|
|Consistency|Can users understand similar interactions across different modules?|

Test actual scenarios such as:

- A Site Personnel user clocking in and submitting a daily report.
    
- An Engineer creating an RFI.
    
- A Project Manager reviewing a purchase request.
    
- An HR employee verifying attendance.
    
- A Finance employee reviewing a payroll batch.
    
- An Owner checking the overall status of projects.
    

Set measurable performance targets after establishing the current baseline.

A successful redesign should allow less technically experienced users to complete their responsibilities with less assistance, while experienced users should not lose their efficiency.

### 9.9 Implementation cautions

There are some considerations specific to your current wiki and client requirements.

**First: Finalize the role definitions.**

Your Roles and Permissions document currently lists Admin Manager and HR as separate roles, but the Client-Driven Changes document states that Admin and HR were merged on November 11. This was in fact reconciled on 11 Nov — [[06 Client-Driven Changes]] confirms Admin and HR were merged into one role, with Finance kept separate — so PART 6.2–6.3 below (which still calls this "to be finalized") is the stale half of this document; treat the merge as decided.


**Second: Do not expose every function to everyone.**

The system already has a defined permission model. Simplification should mean presenting fewer irrelevant actions, not weakening authorization. For example, removing an approval button from an unauthorized user's interface must not replace server-side authorization checks.

**Third: Consider site personnel separately.**

The office environment and construction site environment have different interaction requirements. Your site personnel need quick, touch-friendly operations, potentially under poor connectivity or less favorable working conditions. A desktop interface compressed onto a mobile screen is not enough.

**Fourth: Keep advanced configuration away from regular users.**

The complexity of configuring roles, workflow templates, permissions and system settings should primarily belong to authorized administrators and IT personnel. Your benchmarking documentation already identifies this as an important design separation.

---

## PART 10 — RECOMMENDED ADDITIONAL CONSTRUCTION-MANAGEMENT PROCESSES

These are benchmark-derived opportunities, not all confirmed ORRA requirements.

Procore and Autodesk Construction Cloud provide useful examples of how construction companies organize technical and operational records.

### 10.1 Submittal Management

Separate formal technical submissions from RFIs.

Examples:

- Shop drawings.
    
- Material specifications.
    
- Product data.
    
- Samples.
    
- Technical documents.
    

### 10.2 Change Event Management

Record potential changes before preparing a formal Change Order.

Examples:

- Client-requested revisions.
    
- Design changes.
    
- Additional work.
    
- Unexpected site conditions.
    

### 10.3 Daily Site Logs

Record:

- Work performed.
    
- Manpower.
    
- Material deliveries.
    
- Equipment.
    
- Site conditions.
    
- Problems encountered.
    
- Supporting photos.
    

### 10.4 Deficiency and Punch-List Management

Track incomplete work, defects, responsible persons, corrective actions, and verification.

### 10.5 Meeting and Coordination Records

Maintain:

- Meeting dates.
    
- Participants.
    
- Agendas.
    
- Minutes.
    
- Decisions.
    
- Action items.
    
- Responsible personnel.
    

### 10.6 Project Handover

Provide configurable checklists for:

- Final drawings.
    
- COC.
    
- Required certificates.
    
- Warranty documentation.
    
- Final inspection.
    
- Outstanding deficiencies.
    
- Client handover.
    

These features should be added only after validating whether ORRA actually needs and performs those processes.

---

## PART 11 — STORAGE AND INFORMATION SECURITY

### 11.1 Document ownership

ORRA documents are confidential company property.

The system should preserve the confidentiality and integrity of the information supplied to it.

### 11.2 Access principles

- HR documents are accessible only to authorized company personnel.
    
- Consultants only access assigned project information.
    
- Project team members access relevant project records.
    
- External parties receive specifically authorized project-document access.
    
- IT manages system accounts and permissions.
    
- Completed project records remain preserved.
    

### 11.3 Account deactivation

Deactivation removes the former employee's ability to access the system.

It must not delete the employee's historical information, documents, or project involvement.

### 11.4 Historical information

Completed projects should remain searchable and retrievable.

Former employees should remain identifiable in project history even after their accounts are deactivated.

### 11.5 Storage architecture

Investigate Google Drive integration using ORRA's existing subscription.

Avoid unnecessary duplication between application storage and external storage.

The system should maintain clear document references, permissions, and retrieval paths.

Do not use shared credentials as a substitute for individual user authentication. The emergency Owner recovery function should remain separate from routine account management.

---

## PART 12 — DEVELOPMENT ROADMAP

### Phase 1: Establish the correct information structure

- Project Registry.
    
- Project details.
    
- Project statuses.
    
- NOA, NTP, and COC tracking.
    
- Company-wide project search.
    
- Document categories.
    

### Phase 2: Implement company administration

- Employee registration.
    
- Employee 201 files.
    
- Missing-document tracking.
    
- Expiration notifications.
    
- Consultant registry.
    
- Account creation and deactivation.
    

### Phase 3: Implement document management

- Project document indexes.
    
- Google Drive integration or linking.
    
- Shared project document references.
    
- Mother Library.
    
- Document access permissions.
    
- Historical file migration.
    

### Phase 4: Improve project operations

- PM dashboard.
    
- Project schedules.
    
- Technical document records.
    
- RFI/RFA register.
    
- Project reporting.
    
- Project completion and archiving.
    

### Phase 5: Implement validated financial and workforce operations

- Attendance administration.
    
- Payroll preparation and approval.
    
- Project financial information.
    
- Procurement, if confirmed.
    
- Financial reports.
    

### Phase 6: Additional capabilities

- Submittals.
    
- Change management.
    
- Meeting records.
    
- Deficiency tracking.
    
- Advanced dashboard features.
    
- Automated integrations.
    

---

## PART 13 — HOW TO VALIDATE THE NEW SYSTEM

The system must be validated against actual work, not only by examining whether buttons and pages exist.

Test complete scenarios.

### Scenario 1: Registering a project

An authorized person creates a project, records the owner, address, amount, and project details, and uploads or links the NOA.

Expected result: The project is searchable and its record is complete.

### Scenario 2: Recording an NTP

A Project Manager opens the project, records the NTP date, uploads the document, and verifies the resulting start date.

Expected result: The project record contains the actual NTP and the start date follows the client's stated procedure.

### Scenario 3: Retrieving a contract

An Admin searches for a specific contract using the project name.

Expected result: The appropriate document appears without manually navigating several folders.

### Scenario 4: Managing an employee's 201 file

Admin/HR opens an employee record, checks the required documents, identifies missing items, and uploads an updated document.

Expected result: The employee's record is complete and updated.

### Scenario 5: Using the Mother Library

An Architect retrieves a standard design detail, modifies the file, and saves it under a project.

Expected result: The project-specific copy is available without altering the master resource.

### Scenario 6: Project document sharing

The Project Manager opens the project Drive and shares the authorized document with the designated project participants.

Expected result: The intended external party can access the appropriate file without receiving unrelated confidential information.

### Scenario 7: Employee resignation

Admin/HR marks the employee as inactive and IT deactivates the account.

Expected result: The employee cannot access the system, but historical records remain intact.

### Scenario 8: Completed project retrieval

An authorized person searches the completed-project registry and opens an old project.

Expected result: The project details and historical documents remain available according to the access policy.

---

## PART 14 — SUCCESS CRITERIA

The redesign should be considered successful when:

1. Important project documents can be retrieved through project and document searches.
    
2. Employee 201 files are organized and complete.
    
3. Missing and expiring documents can be identified.
    
4. Project records contain the important milestone dates and supporting documents.
    
5. External document sharing follows ORRA's approved process.
    
6. Consultants cannot access unrelated confidential records.
    
7. Former employees lose system access without losing historical records.
    
8. Ongoing and completed projects can be distinguished.
    
9. Non-technical personnel can complete routine tasks without excessive assistance.
    
10. Experienced personnel retain access to the full functionality they need.
    
11. The system does not require unnecessary business actions just to satisfy arbitrary workflow conditions.
    
12. The company can use the system as a dependable source of organized project and administrative information.
    

---

## PART 15 — FINAL PRODUCT DIRECTION

Orra-ERP should not become an unnecessarily large enterprise resource planning system that attempts to automate every possible construction-management activity.

It should become a practical, centralized, and secure company and project information management system designed around ORRA's actual operations.

The first priority is to solve the company's existing problems:

- Missing and scattered documents.
    
- Difficult information retrieval.
    
- Unorganized project history.
    
- Incomplete employee records.
    
- Unclear user responsibilities.
    
- Excessive system complexity.
    
- Uncontrolled information access.
    

Construction-management functionality should support those priorities rather than compete with them.

### Final Design Principle

**Build the system around how ORRA works, not around what the original thesis implementation assumes a construction company should do.**

The system should make information easy to find, business activities easy to understand, records easy to maintain, and access easy to control.

It should provide sufficient functionality for the company without introducing unnecessary complexity.

That is the foundation of the Orra-ERP refactoring initiative.

## How to use this briefing

There are three particularly important things to take away from the consolidated information.

1. **The actual product** — Orra-ERP is primarily a centralized company and project information management platform. It is not necessary to reproduce every function of a full commercial construction ERP.
2. **The immediate development priority** — Project Registry, Document Management, Employee 201 Files, and Account Security should establish the foundation before complex workflow automation is introduced.
3. **The redesign philosophy** — Use Procore to understand construction operations, monday.com to understand visual interaction, and ORRA's interview to determine what should actually exist.

**Where to start concretely:** redesign the Home Dashboard, Project Overview, and My Work screens first — those three screens establish the visual and interaction language the rest of the application can follow (see §9.7 above).

## Reference materials

These are the principal sources for the work consolidated above.

|Source|Purpose|
|---|---|
|[Orra-ERP Wiki](https://nhyl-beta.github.io/orra-erp-wiki/)|Client requirements and target documentation — see also [[16 Platform Benchmarking (Procore, Monday, Payroll)]] and [[14 Interview Integration Plan (11-11-26)]]|
|[EasyConstruct thesis repository](https://github.com/nhyl-beta/EasyConstruct/tree/thesis-final)|Existing technical implementation|
|[Lifecycle gate implementation](https://github.com/nhyl-beta/EasyConstruct/blob/thesis-final/apps/api/src/modules/projects/lifecycle/gates.ts)|Existing mandatory project conditions|
|[Procore](https://www.procore.com/)|Construction operations reference|
|[Autodesk Construction Cloud](https://construction.autodesk.com/)|Document and project coordination reference|
|[monday.com](https://monday.com/)|Visual work-management reference|

The primary interview source is the 61-page INTERVIEW-TRANSCRIPT-ORRA_11-11.pdf (already analyzed in [[14 Interview Integration Plan (11-11-26)]]).

**One important limitation:** The finance workflow, final role consolidation, external Orra-ERP account policy, and Google Drive integration architecture remain open decisions. They should not be treated as approved merely because they appear in this proposed design.

---

## Correlation with the existing wiki

This brief was written as a separate exercise and, in a few places, disagrees with or predates decisions already recorded elsewhere in this wiki. Read this before acting on anything above.

### Confirms / extends what's already decided
- **PART 1–5** (business understanding, three system areas, detailed processes) is a much more detailed restatement of what [[14 Interview Integration Plan (11-11-26)]] already covers at a summary level — treat this brief as the expanded version, not a competing source.
- **9.5 Detailed interaction strategies** and the Procore/monday.com split are the concrete, UI-level follow-through on [[16 Platform Benchmarking (Procore, Monday, Payroll)]] — that note did the vendor research and flagged the competency-gap problem; this one turns it into interface principles.
- **9.9 Implementation caution on advanced configuration** independently reaches the same conclusion [[16 Platform Benchmarking (Procore, Monday, Payroll)]] §2 did: configuration complexity belongs to Admin/IT, not daily-use screens.

### Already resolved — this document is stale here
- **PART 6.2–6.3** (Admin/HR/Finance split "remains to be finalized") — it doesn't. [[06 Client-Driven Changes]] confirms Admin and HR were merged into one role on 11 Nov, with Finance kept separate. Corrected inline in §9.9 above; PART 6 below is left as written (for a record of what was uncertain at the time) but should not be treated as current.
- **PART 6.10** (DCO "not conclusively established") — [[03 Roles and Permissions]] already lists DCO as a proposed role with its own permission column, and [[06 Client-Driven Changes]] lists it as new for the December demo. The genuine open point isn't *whether* DCO exists in the current design — it's whether the client confirms it, which is already tracked as [[08 Open Questions]] Question 5.

### Genuinely new — not yet in the wiki, worth adding
- **PART 7** proposes loosening several of the *mandatory* gates already built into the system (no required consultant, no required site coordinates, no required procurement initiation, payroll independent of closeout, etc. — see [[14 System Flowchart]] gates P1–P5, C1–C6). This is a real, scoped-sized decision: the current flowchart and its gates are *built*, so "make these optional" is a change request, not a clarification. Added as Open Question 26 below.
- **PART 10** (Submittal Management, Change Event Management, Daily Site Logs, Deficiency/Punch-List, Meeting Records, Project Handover) are **not** in [[04 Flows, Forms and Screens]]'s five flows. The document itself is careful to call these "benchmark-derived opportunities, not confirmed ORRA requirements" — treat them as a backlog to validate with the client, not a build list.
- **5.7 Mother Library**, **5.3/5.4 Employee 201 Files and Consultant Management**, and **5.10 Owner Dashboard** go into more process detail than [[14 Interview Integration Plan (11-11-26)]] did — worth folding the specifics (document checklists, expiration monitoring, the three-party San Pablo example) back into that note or [[02 Roles and Permissions]] the next time either is revised, rather than leaving them only here.

### New open questions (added to [[08 Open Questions]] as Q26–Q27)
26. Should the currently-built mandatory lifecycle gates (consultant required, site coordinates required, procurement initiated, etc. — [[14 System Flowchart]] §2) be loosened to conditional/optional per PART 7 of this brief, or do they stay as hard gates for the December build?
27. This brief and [[06 Client-Driven Changes]] now agree Admin/HR are merged — is Finance's own scope (PART 6.3: "too broad," workflow not fully defined) still open, and if so, what does Finance actually need to do day-to-day beyond PR/PO/payroll approval?
