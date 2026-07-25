# Business Lifecycle

> **Purpose**
>
> This document describes the end-to-end business lifecycle supported by the Project Management Platform. It explains how work enters the organization, progresses through production, undergoes quality validation, is delivered to the client, billed, and finally archived.
>
> This lifecycle represents the business journey rather than the technical implementation.

---

# Overview

The Project Management Platform manages the complete production lifecycle from the moment a client project is initiated until the project is financially and operationally closed.

The lifecycle ensures:

- Standardized execution
- Controlled approvals
- Complete traceability
- Financial visibility
- Resource accountability
- Production transparency

---

# Business Lifecycle Overview

```text
Client Onboarding
        │
        ▼
Project Planning
        │
        ▼
Batch Planning
        │
        ▼
Resource Planning
        │
        ▼
Production Planning
        │
        ▼
Production Execution
        │
        ▼
Review Cycle
        │
        ▼
Quality Validation
        │
        ▼
Client Approval
        │
        ▼
Delivery
        │
        ▼
Billing
        │
        ▼
Payment
        │
        ▼
Project Closure
```

---

# Lifecycle Phases

The platform divides the production journey into the following business phases.

| Phase | Description |
|---------|-------------|
| 1 | Client Management |
| 2 | Project Planning |
| 3 | Batch Planning |
| 4 | Resource Allocation |
| 5 | Production Planning |
| 6 | Production Execution |
| 7 | Internal Reviews |
| 8 | Client Acceptance |
| 9 | Delivery Management |
| 10 | Finance |
| 11 | Project Closure |

---

# Phase 1 — Client Management

Every engagement begins with a Client.

## Activities

- Create Client
- Configure Client Information
- Configure Billing Details
- Configure Contacts
- Configure Parent Client
- Configure Region/Country

## Output

An active Client ready to receive Projects.

---

# Phase 2 — Project Planning

A Project represents a contractual engagement with a Client.

## Activities

- Create Project
- Define Project Team
- Configure Required Software
- Configure Financial Information
- Configure Communication
- Create Initial Documentation

## Output

A production-ready Project.

---

# Phase 3 — Batch Planning

Projects are divided into one or more Batches.

Each Batch represents a production package.

## Activities

- Create Batch
- Configure Workflow
- Configure Production Stages
- Assign Batch Team
- Configure Timeline

## Output

Production-ready Batch.

---

# Phase 4 — Resource Allocation

Resources are allocated before production begins.

## Business Flow

```text
Batch Manager
        │
Raises Request
        │
        ▼
Resource Manager
        │
Approve / Reject
        │
        ▼
Artist Allocation
```

## Activities

- Raise Allocation Request
- Review Capacity
- Approve Allocation
- Allocate Artists

## Output

Production team assigned.

---

# Phase 5 — Production Planning

Once resources are available, production planning begins.

## Activities

- Create Assets
- Create Tasks
- Create Initial Subtasks
- Assign Artists
- Configure Workflow

## Output

Production-ready work.

---

# Phase 6 — Production Execution

Artists execute assigned Subtasks.

## Business Flow

```text
Task
    │
    ▼
General Subtasks
    │
    ▼
Artist
    │
    ▼
Done
```

During execution:

- Artists update progress.
- Deliverables are uploaded.
- Communication occurs.
- Activities are logged.

---

# Phase 7 — Review Lifecycle

After production work reaches review milestones, the Task enters the review process.

The review lifecycle is controlled by the configured Workflow.

---

## Stage 1 — WIP Review

Purpose:

Early validation before completion.

Possible Outcomes:

- Approve
- Feedback

Feedback returns the Task to Production.

---

## Stage 2 — Lead Review

The Team Lead reviews the completed Task.

The Lead may:

- Approve
- Reopen production

Unlike other reviewers, the Lead has authority to reopen existing Subtasks or close them before advancing the Task.

---

## Stage 3 — Final Review (Optional)

Performed by an internal reviewer.

Possible Outcomes:

- Approve
- Minor Fix
- Major Fix

Reviewers provide feedback only.

The Team Lead converts feedback into one or more **FR Fix Subtasks**.

---

## Stage 4 — Quality Control (Optional)

QC validates quality before client submission.

Possible Outcomes:

- Approve
- Reject

QC communicates directly with the production team through the configured workflow.

---

## Stage 5 — Client Review (Optional)

The client evaluates the completed work.

Possible Outcomes:

- Approve
- Minor Fix
- Major Fix

The client provides feedback only.

The Team Lead or Project Manager creates **Client Fix Subtasks** based on that feedback.

---

# Review Round Lifecycle

Every review iteration creates a new Review Round.

```text
Round 1
      │
      ▼
Feedback
      │
      ▼
New Subtasks
      │
      ▼
Round 2
      │
      ▼
Feedback
      │
      ▼
Round 3
```

The platform maintains complete history for every review round.

---

# Phase 8 — Delivery Management

Once production is approved, deliverables are prepared.

## Activities

- Validate Deliverables
- Capture Repository Information
- Capture Version
- Capture File Path
- Capture Changeset
- Record Delivery

Actual production files remain in external source control systems.

---

# Phase 9 — Billing

After work is delivered (or according to contractual milestones), invoices are generated.

> **Important**
>
> Invoices are created **against Projects** and issued to the associated Client.

## Activities

- Generate Invoice
- Review Invoice
- Issue Invoice
- Track Outstanding Amount

---

# Phase 10 — Payment

Finance records client payments.

Supported scenarios:

- Full Payment
- Partial Payment
- Discount
- Waiver

Outstanding balances are updated accordingly.

---

# Phase 11 — Project Closure

When production and financial obligations are complete, the Project may be closed.

## Closure Checklist

- All Batches Closed
- All Assets Completed
- All Tasks Closed
- All Deliverables Delivered
- All Reviews Completed
- Outstanding Payments Resolved *(or approved for write-off/waiver according to business policy)*
- Final Reports Generated

---

# Entity Lifecycle

## Client

```text
Created
    │
Active
    │
Inactive
```

---

## Project

```text
Created
    │
Planning
    │
Active
    │
Completed
    │
Closed
```

---

## Batch

```text
Planning
    │
Active
    │
Completed
    │
Closed
```

---

## Asset

```text
Created
    │
In Production
    │
Completed
    │
Closed
```

---

## Task

The detailed Task lifecycle is controlled by the assigned Workflow.

At a high level:

```text
Open
    │
Production
    │
Reviews
    │
Completed
    │
Closed
```

Workflow documentation defines the exact Processes and States.

---

## Subtask

```text
Open
    │
In Progress
    │
Done
    │
Closed
```

Additional outcomes:

- Reopen
- Discarded

---

## Invoice

```text
Draft
    │
Issued
    │
Partially Paid
    │
Paid
    │
Closed
```

---

# Cross-Cutting Activities

The following occur throughout the lifecycle:

## Communication

Available at:

- Project
- Batch
- Asset
- Task

---

## Activity Timeline

Every significant business event is recorded.

Examples:

- Status Changes
- Workflow Transitions
- Assignments
- Reviews
- Comments
- Attachments
- Deliverables
- Financial Transactions

---

## Notifications

Notifications are generated for important events, including:

- Assignment
- Review Requests
- Allocation Approval
- Workflow Changes
- Payment Events

---

## Reporting

Dashboards and reports update continuously throughout the lifecycle.

Examples:

- Executive Dashboard
- Project Dashboard
- Batch Dashboard
- Resource Dashboard
- Financial Dashboard

---

# Future Lifecycle Extensions

Future releases will introduce additional lifecycle capabilities, including:

- Client Portal Workflow
- Vendor Workflow
- Procurement Workflow
- Change Request Management
- Production Forecasting
- AI-Assisted Planning
- Predictive Risk Detection
- Automated Workflow Recommendations

---

# Lifecycle Principles

The business lifecycle follows these principles:

- Every stage has a defined owner.
- Planning and execution are separate responsibilities.
- Workflows govern Task progression.
- Reviews provide feedback, while Leads convert feedback into actionable Subtasks.
- Every significant business event is auditable.
- Deliverables reference external source control systems rather than storing production files.
- Financial tracking is performed at the Project level and aggregated to the Client level.
- The lifecycle is configurable to support different production pipelines.

---

# Related Documents

- ProductOverview.md
- ProductHierarchy.md
- ProductArchitecture.md
- BusinessLifecycle.md
- 02-Domain/*
- 03-Modules/*
- 04-Workflow/*
- 06-Database/*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Business Lifecycle documentation |
