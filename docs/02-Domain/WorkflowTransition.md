# Workflow Transition

> **Purpose**
>
> A **Workflow Transition** represents a controlled business transaction that moves a Task from one Workflow State to another. Unlike traditional workflow engines where a transition is simply a connection between two states, this platform treats every transition as a **business action** with its own permissions, validations, automation, notifications, audit logging, and workflow rules.
>
> Every button a user clicks (Approve, Reject, Submit for Review, Start Work, etc.) is implemented as a Workflow Transition.

---

# Overview

Workflow Transitions define **how work progresses** through the production pipeline.

A Transition is responsible for:

- Validating business rules
- Validating permissions
- Executing automation
- Recording audit history
- Updating workflow state
- Triggering notifications
- Creating review rounds
- Generating feedback containers
- Recording deliverable versions

Without a valid Transition, a Task cannot move between States.

---

# Workflow Hierarchy

```text
Workflow
│
├── Process
│
├── State
│
└── Transition
        │
        ├── Validation
        ├── Permission
        ├── Automation
        ├── Notification
        └── Audit
```

---

# Objectives

Workflow Transitions enable the platform to:

- Control Task movement
- Enforce production rules
- Prevent invalid workflow changes
- Support configurable business logic
- Trigger automated system actions
- Record complete workflow history
- Support future BPMN implementation

---

# Transition Architecture

```text
Source Process

↓

Source State

↓

Transition

↓

Validation

↓

Permission Check

↓

Business Rules

↓

Automation

↓

Audit

↓

Target Process

↓

Target State
```

---

# Transition Components

Each Transition contains:

- Transition Information
- Source Process
- Source State
- Target Process
- Target State
- Business Rules
- Validation Rules
- Permission Rules
- Automation
- Notifications
- Audit Rules

---

# Transition Information

Typical properties include:

- Transition Name
- Display Name
- Description
- Icon
- Colour
- Display Order
- Active Flag

---

# Example Transition

```text
Transition

Submit For Final Review

Source

Production

↓

Waiting For Lead Approval

Target

Final Review

↓

Waiting
```

---

# Transition Types

The platform supports several categories of Transitions.

---

## Manual Transition

Initiated by a user.

Example

```text
Approve

Reject

Start Work

Close Task
```

---

## Automatic Transition

Executed automatically after business validation.

Example

```text
Lead Approved

↓

Move To Final Review
```

---

## Conditional Transition

Executed only when configured conditions are satisfied.

Example

```text
Workflow

Has QC

YES

↓

QC Process

NO

↓

Client Review
```

---

## System Transition

Performed internally by the Workflow Engine.

Example

```text
Task Created

↓

Move To Open
```

---

# Source Definition

Every Transition begins from one State.

Example

```text
Process

Production

State

In Progress
```

---

# Target Definition

Every Transition moves to one destination State.

Example

```text
Process

Lead Review

State

Waiting
```

---

# Transition Flow

```text
Source

↓

Permission Check

↓

Validation

↓

Business Rules

↓

Automation

↓

Notifications

↓

Audit

↓

State Change

↓

Target
```

---

# Permission Rules

Transitions define who may execute them.

Examples

| Transition | Allowed Role |
|------------|--------------|
| Start Work | Artist |
| Request WIP Review | Artist |
| Approve WIP | Team Lead |
| Send To FR | Team Lead |
| FR Approval | Reviewer |
| QC Approval | QC |
| Client Approval | Client |
| Close Task | Team Lead |

---

# Validation Rules

Transitions may require:

- Assigned Artist
- Assigned Lead
- All Mandatory SubTasks Completed
- Deliverables Uploaded
- Source Control Changeset
- Mandatory Comments
- Mandatory Attachments
- Mandatory Review
- Minimum Reviewers

Example

```text
Submit To Final Review

Requires

✓ All SubTasks Done

✓ Deliverables Uploaded

✓ Changeset Number

✓ Repository Path
```

---

# Business Rules

Transitions execute business rules.

Examples

- Increment Review Round
- Generate Feedback Container
- Lock Deliverables
- Freeze Time Entry
- Close Previous Review
- Create Activity Log
- Start SLA Timer
- Stop SLA Timer

---

# Automation

Transitions may perform automatic actions.

Examples

- Send Email
- Send Notification
- Create Timeline Entry
- Update Progress
- Generate Deliverable Version
- Validate Repository
- Create Review Record
- Create Feedback Container
- Generate Audit Record

---

# Notification Rules

Each Transition may notify different users.

Example

```text
Submit For Review

↓

Reviewer

↓

Team Lead

↓

Project Manager
```

Notifications may include:

- Email
- In-App Notification
- Teams
- Slack
- Webhook

---

# Source Control Integration

A Transition may require production files.

Example

```text
Repository

Required

✓

↓

Repository Path

Required

✓

↓

Changeset

Required

✓

↓

Version Number

Generated
```

This ensures every review is associated with an exact file version.

---

# Review Integration

Transitions drive the review process.

Example

```text
FR

↓

Minor Fix

↓

Create Feedback

↓

Create FR Fix SubTasks

↓

Return To Production
```

Major Fix

```text
FR

↓

Major Fix

↓

Feedback

↓

Production

↓

FR Again
```

---

# Client Review Example

```text
Client Review

↓

Approve

↓

Completed
```

Minor Fix

```text
Client Review

↓

Minor Fix

↓

Client Fix SubTasks

↓

Production

↓

QC

↓

Client
```

Major Fix

```text
Client Review

↓

Major Fix

↓

Client Fix SubTasks

↓

Production

↓

FR

↓

QC

↓

Client
```

---

# Review Round Management

Transitions may automatically:

- Increment Round Number
- Create Review
- Create Feedback
- Link Feedback
- Generate New SubTasks

---

# Audit

Every Transition records:

- Previous Process
- Previous State
- Target Process
- Target State
- User
- Date
- Time
- Comments
- Attachments
- IP Address
- Device
- Review Round

Audit records are immutable.

---

# Error Handling

If validation fails:

```text
Transition

↓

Validation Failed

↓

Rollback

↓

Display Validation Errors

↓

Remain In Current State
```

---

# Transition Sequence

```text
User Action

↓

Permission Check

↓

Business Validation

↓

Workflow Validation

↓

Automation

↓

Audit

↓

Notification

↓

State Updated
```

---

# Business Rules

## BR-001

Every Transition belongs to one Workflow.

---

## BR-002

Every Transition has one Source State.

---

## BR-003

Every Transition has one Target State.

---

## BR-004

Transitions may execute only if the user has permission.

---

## BR-005

Validation must complete successfully before State changes.

---

## BR-006

Automation executes only after successful validation.

---

## BR-007

Every successful Transition generates an Audit record.

---

## BR-008

Transitions may generate Reviews.

---

## BR-009

Transitions may generate Feedback.

---

## BR-010

Transitions may generate SubTasks.

---

## BR-011

Transitions may require Source Control metadata.

---

## BR-012

Transition Rules are versioned with the Workflow.

---

## BR-013

Deleting a Transition from a published Workflow Version is prohibited.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| Transition Id | Primary Key |
| Workflow Id | Parent Workflow |
| Name | Transition Name |
| Display Name | UI Display Name |
| Source Process Id | Current Process |
| Source State Id | Current State |
| Target Process Id | Destination Process |
| Target State Id | Destination State |
| Display Order | UI Order |
| Is Automatic | Auto Transition |
| Is Active | Active |

---

# Reporting

Typical reports include:

- Transition History
- Transition Frequency
- Failed Transition Report
- Average Transition Time
- Workflow Bottlenecks
- Review Transition Analysis
- Rework Analysis
- SLA Compliance

---

# Future Enhancements

Future releases may include:

- Conditional Expressions
- Scripted Validation
- Dynamic Routing
- AI Decision Support
- Event-Based Transitions
- Webhook Actions
- Parallel Workflow Branches
- BPMN Gateway Support
- Plugin-Based Automation

---

# Design Principles

The Workflow Transition module follows these principles:

- Transitions represent **business actions**, not just state changes.
- Every Transition is fully configurable.
- Permissions and validations are configuration-driven.
- Automation is executed only after successful validation.
- Workflow history is fully auditable.
- Transitions are version-controlled with their parent Workflow.
- Source Control integration is a first-class part of production workflows.
- The engine is designed to evolve into a full BPMN-compatible workflow system.

---

# Related Documents

- Workflow.md
- WorkflowProcess.md
- WorkflowState.md
- WorkflowRule.md
- WorkflowPermission.md
- WorkflowValidation.md
- WorkflowAutomation.md
- WorkflowNotification.md
- ReviewWorkflow.md
- FeedbackWorkflow.md
- Task.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow Transition specification |
