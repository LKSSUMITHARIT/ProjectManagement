# Batch Stage

> **Purpose**
>
> A **Batch Stage** represents a logical production phase within a Batch. It is used to organize production activities, standardize task creation, and associate Tasks with a predefined Workflow.
>
> Batch Stages act as templates from which Tasks are generated for each Asset.

---

# Overview

A Batch is divided into one or more Stages.

Each Stage represents a department, discipline, or production phase.

Examples include:

- Concept Art
- Modeling
- Sculpting
- UV Mapping
- Texturing
- Rigging
- Animation
- Lighting
- Rendering
- Quality Assurance

Stages provide a structured production pipeline while allowing Tasks to follow configurable workflows.

---

# Position in Business Hierarchy

```text
Project
    │
Batch
    │
Batch Stage
    │
Assets
    │
Tasks
    │
Subtasks
```

---

# Objectives

The Batch Stage module enables organizations to:

- Define the production pipeline
- Standardize task creation
- Associate Workflows with production phases
- Track progress by department
- Enable production reporting
- Support reusable production templates

---

# Batch Stage Architecture

```text
Batch
│
├── Stage 1
│      │
│      ├── Workflow
│      ├── Tasks
│      └── Deliverables
│
├── Stage 2
│      │
│      ├── Workflow
│      ├── Tasks
│      └── Deliverables
│
└── Stage N
```

---

# Core Information

Each Batch Stage typically contains:

- Stage Name
- Display Name
- Stage Code
- Description
- Sequence
- Workflow
- Default Lead (Optional)
- Estimated Duration
- Status

---

# Stage Sequence

Stages define the **logical production order**.

Example:

| Sequence | Stage |
|-----------|--------|
| 1 | Modeling |
| 2 | UV Mapping |
| 3 | Texturing |
| 4 | Rigging |
| 5 | Animation |
| 6 | Lighting |
| 7 | Rendering |

> **Important**
>
> The sequence is primarily used for planning and reporting.
>
> It does **not** prevent parallel execution unless future dependency management is enabled.

---

# Workflow Association

Every Stage is associated with **one Workflow**.

```text
Batch Stage

↓

Workflow

↓

Processes

↓

States

↓

Transitions
```

Whenever a Task is created from a Stage, it automatically inherits that Workflow.

---

# Task Generation

Stages are used when creating Tasks for Assets.

Example:

```text
Batch
│
├── Modeling
├── UV
├── Texturing
└── Rigging
```

Creating a new Asset results in:

```text
Asset
│
├── Modeling Task
├── UV Task
├── Texturing Task
└── Rigging Task
```

Each generated Task references the originating Stage.

---

# Workflow Override

By default:

```text
Stage Workflow

↓

Task Workflow
```

However, a Team Lead or authorized user may change the Workflow at the Task level if required by business rules.

This allows exceptional production cases without modifying the Batch configuration.

---

# Stage Progress

Progress is automatically calculated using Task information.

Typical metrics include:

- Total Tasks
- Open Tasks
- In Progress Tasks
- Review Tasks
- Completed Tasks
- Closed Tasks
- Average Cycle Time

---

# Stage Dashboard

The Stage Dashboard may display:

- Completion Percentage
- Active Tasks
- Review Queue
- Pending Approvals
- Resource Utilization
- Average Turnaround Time
- Bottlenecks

---

# Business Rules

## BR-001

Every Batch Stage belongs to exactly one Batch.

---

## BR-002

Every Stage must reference one Workflow.

---

## BR-003

A Stage may generate Tasks for multiple Assets.

---

## BR-004

Each generated Task stores the originating Stage.

---

## BR-005

Changing the Stage Workflow affects only newly created Tasks.

Existing Tasks continue using their assigned Workflow unless manually changed.

---

## BR-006

Tasks may override the inherited Workflow if the user has appropriate permissions.

---

## BR-007

A Stage cannot be deleted if Tasks have already been created from it.

The Stage should instead be marked as Inactive.

---

## BR-008

Stage Sequence is used for planning and reporting only.

It does not enforce execution order.

---

## BR-009

Multiple Stages may execute simultaneously.

---

## BR-010

Every Batch should contain at least one active Stage.

---

# Lifecycle

```text
Draft
    │
Active
    │
Inactive
    │
Archived
```

---

# Suggested Data Model

## Batch Stage

| Field | Description |
|------|-------------|
| Batch Stage Id | Primary Key |
| Batch Id | Parent Batch |
| Stage Code | Business Code |
| Stage Name | Stage Name |
| Display Name | Display Name |
| Workflow Id | Default Workflow |
| Sequence | Display Order |
| Default Lead Id | Optional |
| Estimated Duration | Planned Duration |
| Status | Active / Inactive |
| Description | Notes |

---

# Reporting

Typical reports include:

- Stage Progress Report
- Stage Completion Summary
- Department Performance
- Average Stage Duration
- Stage Bottleneck Analysis
- Workflow Distribution
- Review Queue by Stage
- Task Count by Stage

---

# Future Enhancements

Planned capabilities include:

- Stage Templates
- Stage Dependencies
- Conditional Stage Activation
- Parallel Stage Configuration
- AI-Based Stage Duration Estimation
- Automatic Stage Completion Rules
- Stage-Level SLA Monitoring
- Department Capacity Planning

---

# Design Principles

The Batch Stage module follows these principles:

- Stages define **what work categories exist**, not individual work items.
- Stages act as **Task templates**.
- Every Stage owns one default Workflow.
- Tasks inherit Stage configuration during creation.
- Existing Tasks remain independent after creation.
- Stages provide consistency across Assets within the same Batch.
- Execution remains flexible, allowing parallel production and workflow overrides where authorized.

---

# Related Documents

- Batch.md
- Asset.md
- Task.md
- Workflow.md
- Process.md
- State.md
- KanbanBoard.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Batch Stage domain specification |
