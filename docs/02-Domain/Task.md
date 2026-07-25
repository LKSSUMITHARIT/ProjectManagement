# Task Domain

> **Purpose**
>
> A **Task** is the primary workflow execution unit within the Project Management Platform. It represents a specific production activity that must be performed on an Asset. Every Task follows a configurable Workflow, progresses through multiple review cycles, and is completed through one or more Subtasks executed by Artists.
>
> The Task is the central entity used for production tracking, workflow execution, reviews, approvals, deliverables, and reporting.

---

# Overview

Tasks are automatically generated from the **Batch Stages** defined for a Batch.

Examples:

```text
Asset : Hero Character

Tasks

• Modeling
• UV Mapping
• Texturing
• Rigging
• Animation
```

Each Task has its own:

- Workflow
- Process
- State
- Reviews
- Feedback
- Subtasks
- Deliverables
- Discussion
- Activity Timeline

A Task remains active until it successfully completes all configured workflow stages.

---

# Position in Business Hierarchy

```text
Client
    │
Project
    │
Batch
    │
Asset
    │
Task
│
├── Workflow
├── Reviews
├── Feedback
├── Subtasks
├── Deliverables
├── Attachments
├── Discussion
└── Activity Timeline
```

---

# Objectives

The Task module enables organizations to:

- Execute production work
- Track workflow progress
- Manage reviews
- Manage feedback cycles
- Track deliverables
- Monitor productivity
- Maintain production history
- Provide complete traceability

---

# Business Ownership

| Property | Value |
|----------|-------|
| Domain Owner | Production |
| Operational Owner | Team Lead |
| Execution Owner | Artists |
| Review Owner | Reviewer / QC / Client |

---

# Task Information

Typical information includes:

- Task Name
- Task Code
- Asset
- Batch Stage
- Workflow
- Current Process
- Current State
- Priority
- Due Date
- Estimated Hours
- Actual Hours
- Progress
- Review Round

---

# Task Generation

Tasks are initially generated from Batch Stages.

Example:

```text
Batch

Stages

↓

Modeling
↓

Texturing
↓

Rigging
```

Creating a new Asset produces

```text
Hero Character

↓

Modeling Task

↓

Texturing Task

↓

Rigging Task
```

---

# Workflow

Every Task is attached to exactly one Workflow.

The Workflow determines

- Processes
- States
- Transitions
- Approval Rules
- Review Sequence

Tasks inherit the Workflow from the originating Batch Stage.

An authorized Lead may override the Workflow if required.

---

# Workflow Structure

Each Task stores

```text
WorkflowId

ProcessId

StateId
```

Example

```text
Workflow

Game Character Workflow

↓

Process

Final Review

↓

State

Waiting Approval
```

This design enables multiple States inside the same Process.

---

# Processes

Typical workflow processes include

```text
Production

↓

WIP Review

↓

Lead Review

↓

Final Review

↓

QC

↓

Client Review

↓

Completed
```

Processes are configurable.

Organizations may create additional Processes.

---

# States

Each Process contains one or more States.

Example

```text
Production

•

Open

•

In Progress

•

Blocked

•

Ready for Review
```

Kanban columns are generated from States.

---

# Workflow Execution

A Task progresses through the Workflow using valid transitions.

Example

```text
Open

↓

In Progress

↓

WIP Review

↓

Production

↓

Lead Review

↓

Final Review

↓

QC

↓

Client Review

↓

Completed

↓

Closed
```

Every transition is audited.

---

# Review Cycle

A Task may pass through multiple review rounds.

Example

```text
Round 1

↓

Round 2

↓

Round 3
```

Each round maintains

- Reviews
- Feedback
- Subtasks
- Deliverables

This provides complete production history.

---

# Reviews

Tasks support multiple review types.

Examples

- WIP Review
- Lead Review
- Final Review
- QC Review
- Client Review

Each Review stores

- Reviewer
- Decision
- Comments
- Attachments
- Date
- Round

---

# Feedback

Feedback is created during

- Final Review
- Client Review

Feedback contains

- Rich Text
- Attachments
- Priority
- Category

Feedback itself does **not** assign work.

The Team Lead converts Feedback into new Subtasks.

---

# Subtasks

Subtasks represent actual production work.

Subtask Types

- General
- FR Fix
- Client Fix

Each Subtask belongs to

- One Task
- One Review Round

Subtasks are assigned to one Artist only.

Subtasks cannot be reassigned.

---

# Review Outcomes

## WIP Review

Options

- Approved
- Feedback

---

## Lead Review

Options

- Approved
- Rework

The Lead may reopen existing Subtasks before sending work back to Production.

---

## Final Review

Options

- Approve
- Minor Fix
- Major Fix

Minor Fix

↓

New FR Fix Subtasks

↓

Production

↓

QC

↓

Client

Major Fix

↓

New FR Fix Subtasks

↓

Production

↓

FR

↓

QC

↓

Client

---

## QC

Options

- Pass
- Fail

QC communicates directly with Artists.

No additional FR cycle is required.

---

## Client Review

Options

- Approve
- Minor Fix
- Major Fix

Minor Fix

↓

Client Fix Subtasks

↓

Production

↓

QC

↓

Client

Major Fix

↓

Client Fix Subtasks

↓

Production

↓

FR

↓

QC

↓

Client

---

# Deliverables

Tasks produce Deliverables.

Each Deliverable stores

- Repository
- File Path
- Version
- Changeset
- Uploaded By
- Upload Date

Actual production files remain in Source Control.

---

# Communication

Each Task has its own discussion.

Supported features

- Rich Text
- Mentions
- Attachments
- Emoji
- Activity Feed

---

# Activity Timeline

Every Task action is recorded.

Examples

- Created
- Workflow Changed
- State Changed
- Review Started
- Review Completed
- Feedback Added
- Subtask Created
- Deliverable Uploaded
- Closed

---

# Kanban Representation

The Batch Kanban displays Tasks.

Card example

```text
Asset

Hero Character

--------------------

Task

Texturing

--------------------

Process

Final Review

--------------------

State

Waiting Approval

--------------------

Round

2

--------------------

Priority

High
```

---

# Business Rules

## BR-001

Every Task belongs to exactly one Asset.

---

## BR-002

Every Task belongs to one Batch Stage.

---

## BR-003

Every Task references one Workflow.

---

## BR-004

Every Task stores

- WorkflowId
- ProcessId
- StateId

---

## BR-005

Tasks may contain multiple Subtasks.

---

## BR-006

Multiple Artists may work on a Task through independent Subtasks.

---

## BR-007

A Task cannot be automatically completed when all Subtasks are closed.

The Team Lead must manually complete the Task after verifying merged work.

---

## BR-008

Feedback never modifies existing approved Subtasks.

Instead, new Subtasks are created.

---

## BR-009

Every Review creates a new Review Round.

---

## BR-010

Minor Fix and Major Fix create new Subtasks instead of reopening completed production.

---

## BR-011

Subtasks cannot be reassigned.

If reassignment is required

- Existing Subtask is Discarded
- New Subtask is created

---

## BR-012

Workflow transitions are validated against the configured Workflow definition.

---

## BR-013

All Task history is permanent and cannot be deleted.

---

# Lifecycle

```text
Created
    │
Production
    │
Review
    │
Approved
    │
Completed
    │
Closed
```

---

# Suggested Data Model

| Field | Description |
|---------|-------------|
| Task Id | Primary Key |
| Asset Id | Parent Asset |
| Batch Stage Id | Originating Stage |
| Workflow Id | Workflow |
| Process Id | Current Process |
| State Id | Current State |
| Review Round | Current Round |
| Priority | Priority |
| Progress | Calculated Progress |
| Due Date | Planned Completion |
| Status | Current Status |

---

# Reporting

Typical reports include

- Task Dashboard
- Task Aging
- Task Progress
- Task Cycle Time
- Review Performance
- Review Rounds
- Workflow Analytics
- Process Bottlenecks
- Lead Performance
- Artist Productivity
- Pending Reviews

---

# Future Enhancements

Future versions may include

- AI Priority Recommendation
- AI Workflow Optimization
- Automatic Bottleneck Detection
- SLA Monitoring
- Smart Task Routing
- AI Review Assistance
- Task Dependency Visualization
- Production Forecasting
- Task Health Score
- Intelligent Risk Prediction

---

# Related Documents

- Workflow.md
- WorkflowProcess.md
- WorkflowState.md
- WorkflowTransition.md
- Review.md
- Feedback.md
- SubTask.md
- Asset.md
- BatchStage.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Task domain specification |
