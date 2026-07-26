# Workflow State

> **Purpose**
>
> A **Workflow State** represents the exact position of a Task within a Workflow Process.
>
> While a **Process** identifies *who currently owns the Task*, the **State** identifies *what is currently happening to the Task*.
>
> Workflow States are the smallest units of workflow execution and determine the actions that users can perform at any point in time.

---

# Overview

Every Workflow Process contains one or more Workflow States.

Example:

```text
Process

Production

│

├── Open
├── Assigned
├── In Progress
├── Waiting for WIP Review
└── Rework
```

Only one State can be active for a Task at any given time.

---

# Workflow Hierarchy

```text
Workflow

↓

Process

↓

State

↓

Transition
```

---

# Objectives

Workflow States enable the platform to:

- Track the exact execution position of a Task
- Control user actions
- Validate workflow transitions
- Drive Kanban columns
- Generate notifications
- Trigger automation
- Maintain audit history

---

# Process vs State

| Process | State |
|----------|-------|
| Business Phase | Execution Status |
| Swimlane | Kanban Column |
| Changes Less Frequently | Changes Frequently |
| Department Ownership | Current Action |

Example

```text
Process

Final Review

States

Waiting

↓

Under Review

↓

Approved

↓

Rejected
```

---

# State Properties

Each Workflow State defines:

- State Name
- Display Name
- Process
- Sequence
- Colour
- Icon
- Description
- Is Initial State
- Is Final State
- Allow Time Entry
- Allow File Upload
- Allow SubTask Creation
- Allow Review
- Allow Rework
- Is Active

---

# Standard States

The following are recommended default States.

---

## Production Process

### Open

Task has been created.

No production work has started.

---

### Assigned

Task is assigned to the Team Lead.

SubTasks may be created.

---

### In Progress

Artists are actively working.

SubTasks may move independently.

---

### Waiting for WIP Review

Artist requests WIP Review.

Task ownership moves to Reviewer/Lead.

---

### Rework

Task returned for corrections.

Production resumes.

---

## WIP Review Process

### Waiting

Awaiting reviewer.

---

### Reviewing

Reviewer is examining the work.

---

### Feedback

Reviewer requests changes.

---

### Approved

Review successful.

---

## Lead Review Process

States

- Waiting
- Reviewing
- Reopened
- Approved

---

## Final Review Process

States

- Waiting
- Reviewing
- Minor Fix
- Major Fix
- Approved

---

## QC Process

States

- Waiting
- Testing
- Failed
- Passed

---

## Client Review Process

States

- Waiting
- Reviewing
- Minor Fix
- Major Fix
- Approved

---

## Completed Process

States

- Completed
- Closed

---

# State Ownership

Every State has an owner.

| State | Owner |
|---------|-------|
| Open | System |
| Assigned | Team Lead |
| In Progress | Artist |
| Reviewing | Reviewer |
| Approved | Reviewer |
| Passed | QC |
| Closed | Team Lead |

---

# Allowed Operations

Each State controls available actions.

Example

## Open

Allowed

- Edit Task
- Assign Lead

Not Allowed

- Upload Files
- Close Task

---

## In Progress

Allowed

- Upload Files
- Log Time
- Update Progress
- Create Deliverables

Not Allowed

- Close Task

---

## Reviewing

Allowed

- Add Feedback
- Approve
- Reject

Not Allowed

- Edit Production Data

---

## Closed

Allowed

- View

Not Allowed

- Edit
- Review
- Upload
- Delete

---

# Kanban Representation

States become Kanban Columns.

Example

```text
Production

------------------------------------------------

Open

Assigned

In Progress

Waiting WIP Review

Rework
```

---

# State Behaviour

Each State may trigger automatic system behaviour.

Examples

Open

↓

Create Timeline Entry

↓

Notify Team Lead

---

Waiting Review

↓

Notify Reviewer

↓

Start SLA Timer

---

Approved

↓

Move to Next Process

↓

Create Audit Entry

---

# Automation Rules

A State may automatically perform:

- Notifications
- Email
- Activity Log
- SLA Calculation
- Time Tracking
- Workflow Transition
- Deliverable Validation

---

# Entry Rules

Each State may define entry conditions.

Example

Final Review

Requirements

- All mandatory SubTasks completed
- Deliverables uploaded
- Lead Approval completed

---

# Exit Rules

A State may define exit validations.

Example

Client Approved

Requirements

- Client decision recorded
- Deliverable submitted
- Review comments saved

---

# Permissions

State permissions override general permissions.

Example

```text
State

Reviewing

↓

Allowed

Approve

Reject

Feedback

↓

Not Allowed

Modify Task

Delete Task
```

---

# Business Rules

## BR-001

Every State belongs to exactly one Workflow Process.

---

## BR-002

Every Process must contain at least one State.

---

## BR-003

Only one State may be active at a time.

---

## BR-004

Every Workflow must define one Initial State.

---

## BR-005

A Workflow may contain multiple Final States.

Example

Completed

Closed

Cancelled

---

## BR-006

Transitions between States are validated using Workflow Transitions.

---

## BR-007

Changing State records an Activity Log entry.

---

## BR-008

State changes are fully auditable.

---

## BR-009

Permissions may vary by State.

---

## BR-010

Automation Rules execute after successful State transitions.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| State Id | Primary Key |
| Process Id | Parent Process |
| Name | Internal Name |
| Display Name | UI Name |
| Sequence | Display Order |
| Colour | UI Colour |
| Icon | UI Icon |
| Is Initial | Initial State |
| Is Final | Final State |
| Allow Time Entry | Boolean |
| Allow Upload | Boolean |
| Allow Review | Boolean |
| Allow SubTask | Boolean |
| Allow Rework | Boolean |
| Is Active | Boolean |

---

# Reporting

Typical reports include:

- Tasks by State
- Average Time in State
- State Bottlenecks
- State Transition Analysis
- Work-in-Progress Report
- Review Queue
- SLA Compliance
- Aging by State

---

# Future Enhancements

Future releases may include:

- State-Level SLA
- Automatic Escalation
- State Expiry
- AI State Prediction
- Conditional State Visibility
- Dynamic Permissions
- State-Level Webhooks
- State Templates

---

# Design Principles

The Workflow State module follows these principles:

- States represent the exact execution point of a Task.
- States belong to one Process.
- States drive Kanban columns.
- States control available user actions.
- States may trigger automation and notifications.
- State transitions are validated through Workflow Transitions.
- Every State change is fully auditable.

---

# Related Documents

- Workflow.md
- WorkflowProcess.md
- WorkflowTransition.md
- Task.md
- Review.md
- Feedback.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow State specification |
