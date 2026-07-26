# Workflow Process

> **Purpose**
>
> A **Workflow Process** represents a major business phase within a Workflow.
>
> It groups together multiple Workflow States that share a common business objective.
>
> In the Project Management Platform, **Kanban Swimlanes are based on Workflow Processes**, while **Kanban Columns are based on Workflow States**.

---

# Overview

A Workflow is divided into one or more Processes.

Each Process represents a significant phase of production.

Unlike States, which describe the exact position of work, a Process answers:

> **"Which department or business phase currently owns this Task?"**

Examples include:

- Production
- WIP Review
- Lead Review
- Final Review
- Quality Control
- Client Review
- Completed

---

# Workflow Hierarchy

```text
Workflow
    │
    ├── Process
    │       │
    │       ├── States
    │       └── Transitions
    │
    └── Rules
```

---

# Objectives

Workflow Processes enable organizations to:

- Divide production into logical business phases
- Group related workflow states
- Simplify Kanban visualization
- Support production reporting
- Measure cycle time by department
- Enable configurable review pipelines

---

# Process vs State

| Process | State |
|----------|-------|
| Business Phase | Current Position |
| Stable | Changes Frequently |
| Used for Swimlanes | Used for Columns |
| Represents ownership | Represents execution |

Example

```text
Process

Production

States

Open
↓

Assigned
↓

In Progress
↓

Waiting for WIP Review
```

---

# Standard Processes

The platform recommends the following default Processes.

---

## Production

The Task is actively being worked on by Artists.

Typical States

- Open
- Assigned
- In Progress
- Waiting for Review

Owner

- Artist
- Team Lead

---

## WIP Review

Intermediate review before work is complete.

Purpose

- Verify direction
- Reduce major rework
- Provide early feedback

Possible Outcomes

- Approved
- Feedback

---

## Lead Review

Internal review performed by the Team Lead.

Purpose

- Validate production quality
- Ensure completeness
- Decide readiness for Final Review

Possible Outcomes

- Approve
- Rework

---

## Final Review

Internal review by the designated Reviewer.

Purpose

- Validate artistic quality
- Ensure production standards

Possible Outcomes

- Approve
- Minor Fix
- Major Fix

---

## Quality Control

Validation of technical quality.

Purpose

- Verify specifications
- Check technical compliance
- Validate deliverables

Possible Outcomes

- Pass
- Fail

QC communicates directly with Artists and does not generate Review Rounds.

---

## Client Review

External review performed by the Client.

Purpose

- Business acceptance
- Creative approval

Possible Outcomes

- Approve
- Minor Fix
- Major Fix

---

## Completed

The Task has successfully completed every configured review stage.

No further production work is expected.

---

# Process Ownership

Each Process is owned by a business role.

| Process | Primary Owner |
|----------|---------------|
| Production | Artist |
| WIP Review | Team Lead |
| Lead Review | Team Lead |
| Final Review | Reviewer |
| QC | QC Engineer |
| Client Review | Client |
| Completed | System |

---

# Process Configuration

Each Process contains

- Process Name
- Display Name
- Sequence
- Icon
- Colour
- Default Owner Role
- Enabled Flag

---

# Kanban Representation

Processes become Kanban Swimlanes.

Example

```text
----------------------------------------------------

Production

----------------------------------------------------

Open | Assigned | In Progress

----------------------------------------------------

Final Review

----------------------------------------------------

Waiting | Reviewing | Approved

----------------------------------------------------

Client Review

----------------------------------------------------

Waiting | Reviewing | Approved
```

---

# Process Transition

Tasks move between Processes through Workflow Transitions.

Example

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

A Task may revisit the same Process multiple times.

---

# Review Rounds

Processes support unlimited review iterations.

Example

```text
Round 1

Production

↓

Final Review

↓

Minor Fix

↓

Production

↓

Final Review

Round 2

↓

Client Review

↓

Major Fix

↓

Production

↓

Final Review

Round 3
```

---

# Reporting

Since Processes represent business departments, reporting is primarily Process-based.

Examples

- Tasks by Process
- Average Time in Process
- Bottleneck Analysis
- Department Throughput
- Review Queue
- Pending Client Reviews
- Pending QC
- Production Velocity

---

# Business Rules

## BR-001

Every Workflow must contain at least one Process.

---

## BR-002

Every Process belongs to one Workflow.

---

## BR-003

A Process contains one or more Workflow States.

---

## BR-004

Processes define logical business ownership.

---

## BR-005

Tasks may return to a previous Process during rework.

---

## BR-006

Processes may be optional depending on Workflow configuration.

Examples

- No WIP Review
- No QC
- No Client Review

---

## BR-007

Process Sequence is used for visualization and reporting only.

Workflow Transitions determine actual execution.

---

## BR-008

Deleting a Process is not permitted if it is referenced by an active Workflow Version.

---

## BR-009

Process names should be unique within a Workflow.

---

## BR-010

Every Process must contain at least one State.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| Process Id | Primary Key |
| Workflow Id | Parent Workflow |
| Name | Process Name |
| Display Name | Display Name |
| Sequence | Display Order |
| Default Role | Responsible Role |
| Icon | UI Icon |
| Colour | Kanban Colour |
| Is Enabled | Active Flag |

---

# Future Enhancements

Future releases may include:

- Parallel Processes
- Conditional Processes
- Automatic Process Assignment
- SLA Monitoring
- Department Capacity Analysis
- AI Bottleneck Detection
- Swimlane Configuration
- Process-Level Permissions
- Process Templates
- Cross-Workflow Process Library

---

# Design Principles

The Workflow Process module follows these principles:

- Processes represent business phases, not statuses.
- Processes group related Workflow States.
- Swimlanes are generated from Processes.
- Processes define business ownership.
- Processes remain reusable across Workflows.
- Tasks may revisit Processes multiple times during rework.
- Processes provide the primary dimension for production reporting.

---

# Related Documents

- Workflow.md
- WorkflowState.md
- WorkflowTransition.md
- Task.md
- Review.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow Process specification |
