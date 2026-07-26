# Workflow Domain

> **Purpose**
>
> A **Workflow** defines the complete business process that governs how a Task progresses from creation to completion.
>
> It specifies the available Processes, States, Transitions, Review Stages, approval rules, and business validations.
>
> Workflows are reusable templates that can be assigned to Batch Stages and inherited by Tasks.

---

# Overview

A Workflow is the core engine of the Project Management Platform.

Unlike traditional systems where a Task has only a single Status, this platform separates execution into:

- Workflow
- Process
- State

This separation allows the system to model complex production pipelines while keeping the Kanban board clean and intuitive.

---

# Workflow Hierarchy

```text
Workflow
    │
    ├── Processes
    │       │
    │       ├── States
    │       │
    │       └── Transitions
    │
    └── Rules
```

---

# Objectives

The Workflow module enables organizations to:

- Configure production pipelines
- Define review stages
- Control workflow transitions
- Support multiple production methodologies
- Configure approval rules
- Enable reusable workflow templates
- Standardize production execution

---

# Position in Business Hierarchy

```text
Batch Stage

↓

Workflow

↓

Task

↓

Workflow Execution
```

---

# Workflow Architecture

```text
Workflow
│
├── Processes
│      │
│      ├── States
│      └── Transitions
│
├── Business Rules
├── Review Rules
├── Notification Rules
└── Permissions
```

---

# Workflow Components

A Workflow consists of:

- Workflow Information
- Processes
- States
- Transitions
- Review Configuration
- Permission Rules
- Validation Rules

---

# Example Workflow

```text
Production

↓

WIP Review

↓

Production

↓

Lead Review

↓

Production

↓

Final Review

↓

QC

↓

Client Review

↓

Completed
```

Each organization may configure different workflows.

---

# Workflow Properties

Typical information includes:

- Workflow Name
- Workflow Code
- Description
- Version
- Status
- Default Workflow
- Active Flag

---

# Workflow Assignment

A Workflow is assigned to a Batch Stage.

```text
Batch Stage

↓

Workflow

↓

Task
```

Tasks inherit the Workflow during creation.

---

# Workflow Versioning

Workflow definitions should be versioned.

Example

```text
Character Workflow

Version 1

↓

Version 2

↓

Version 3
```

Existing Tasks continue using the Workflow version assigned when they were created.

---

# Workflow Execution

Every Task stores:

```text
WorkflowId

ProcessId

StateId
```

The Workflow itself is never modified during execution.

Only the Process and State change.

---

# Review Configuration

Each Workflow determines whether the following review stages exist:

- WIP Review
- Lead Review
- Final Review
- QC
- Client Review

Example

| Review | Enabled |
|----------|---------|
| WIP | Yes |
| Lead | Yes |
| Final Review | Yes |
| QC | Yes |
| Client Review | No |

This allows different production pipelines.

---

# Workflow Rules

A Workflow may define:

- Allowed transitions
- Required approvals
- Mandatory reviews
- Automatic notifications
- Required attachments
- Mandatory comments
- Required deliverables

---

# Notifications

Workflow events may generate notifications.

Examples:

- Task Started
- Review Requested
- Review Approved
- Review Rejected
- Feedback Added
- Task Closed

---

# Permissions

Workflow actions may be restricted by role.

Examples:

| Action | Allowed Role |
|---------|--------------|
| Start Task | Artist |
| Request WIP Review | Artist |
| Approve WIP | Lead |
| Send to Final Review | Lead |
| Final Approval | Reviewer |
| QC Approval | QC |
| Client Approval | Client |
| Close Task | Lead |

---

# Business Rules

## BR-001

Every Workflow has a unique name.

---

## BR-002

Every Workflow contains at least one Process.

---

## BR-003

Every Process contains one or more States.

---

## BR-004

Every Transition belongs to one Workflow.

---

## BR-005

A Task references exactly one Workflow.

---

## BR-006

Changing a Workflow affects only future Tasks.

---

## BR-007

Workflow definitions are immutable once published.

Changes require a new Workflow Version.

---

## BR-008

A Workflow may optionally disable:

- WIP Review
- Final Review
- QC
- Client Review

according to business requirements.

---

## BR-009

Workflow transitions must follow configured Transition Rules.

---

## BR-010

Every workflow execution event must be recorded in the Audit Log.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| Workflow Id | Primary Key |
| Workflow Code | Business Code |
| Workflow Name | Name |
| Description | Description |
| Version | Workflow Version |
| Is Active | Active Flag |
| Is Default | Default Workflow |

---

# Reporting

Typical reports include:

- Workflow Usage
- Workflow Performance
- Average Cycle Time
- Review Statistics
- Bottleneck Analysis
- Transition Analysis
- Workflow Comparison

---

# Future Enhancements

Future releases may include:

- BPMN Import/Export
- Visual Workflow Designer
- Drag-and-Drop Editor
- Conditional Branching
- Parallel Workflow Execution
- SLA Rules
- AI Workflow Optimization
- Workflow Simulation
- Approval Matrix Builder
- Dynamic Workflow Generation

---

# Design Principles

The Workflow engine is designed around the following principles:

- Workflows are reusable templates.
- Tasks execute Workflow instances.
- Workflows are version-controlled.
- Business rules are configuration-driven.
- Workflow execution is fully auditable.
- Review stages are configurable.
- Workflows should support future BPMN compatibility.

---

# Related Documents

- WorkflowProcess.md
- WorkflowState.md
- WorkflowTransition.md
- Task.md
- Review.md
- Feedback.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow domain specification |
