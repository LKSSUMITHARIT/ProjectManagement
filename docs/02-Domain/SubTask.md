# SubTask Domain

> **Purpose**
>
> A **SubTask** is the smallest executable unit of work in the Project Management Platform. It represents an individual assignment given to a single Artist for completing a portion of a Task.
>
> SubTasks are the only work items directly assigned to Artists. All production effort, time tracking, progress updates, file submissions, and execution history are maintained at the SubTask level.

---

# Overview

A Task may consist of one or more SubTasks.

SubTasks are created by the **Team Lead** or **Project Manager** based on:

- Initial planning
- Final Review feedback
- Client Review feedback

Unlike Tasks, SubTasks are execution-oriented and do not contain independent workflows.

Instead, they support and contribute to the completion of their parent Task.

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
SubTask
```

---

# Objectives

The SubTask module enables organizations to:

- Divide Tasks into executable work
- Assign work to individual Artists
- Track production effort
- Track work completion
- Manage review feedback implementation
- Maintain production history
- Measure individual productivity

---

# Business Ownership

| Property | Value |
|----------|-------|
| Domain Owner | Production |
| Operational Owner | Team Lead |
| Execution Owner | Assigned Artist |

---

# SubTask Information

Typical information includes:

- SubTask Number
- Title
- Description
- Parent Task
- Assigned Artist
- SubTask Type
- Review Round
- Priority
- Estimated Hours
- Actual Hours
- Due Date
- Status

---

# SubTask Types

Every SubTask belongs to one of the following categories.

---

## General

Created during initial Task planning.

Example

```text
Create Base Mesh

Create UV Layout

Texture Face

Texture Clothes
```

---

## FR Fix

Created from **Final Review** feedback.

These SubTasks represent work requested by the Final Reviewer.

Example

```text
Improve Skin Texture

Adjust Eye Shader

Fix Hair Normal
```

---

## Client Fix

Created from **Client Review** feedback.

Example

```text
Change Armor Color

Increase Weapon Size

Modify Logo Placement
```

---

# Review Round

Every SubTask belongs to a Review Round.

Example

```text
Round 1

General SubTasks

↓

Round 2

FR Fix SubTasks

↓

Round 3

Client Fix SubTasks
```

This allows complete production traceability.

---

# Assignment

Each SubTask is assigned to exactly **one Artist**.

Example

```text
Task

Character Texturing

│

├── SubTask A

Artist John

├── SubTask B

Artist David

└── SubTask C

Artist Sarah
```

Multiple Artists may work on the same Task through different SubTasks.

---

# Reassignment Policy

SubTasks **cannot** be reassigned.

If ownership changes:

```text
Existing SubTask

↓

Discarded

↓

New SubTask Created

↓

Assigned to New Artist
```

This preserves historical ownership and productivity metrics.

---

# Status

A SubTask progresses independently from the parent Task.

Supported statuses:

| Status | Description |
|----------|-------------|
| Open | Newly created |
| In Progress | Artist has started work |
| Done | Artist completed work and submitted it |
| Reopened | Reopened by Team Lead after review |
| Closed | Accepted and finalized |
| Discarded | Cancelled or replaced |

---

# Status Lifecycle

```text
Open
   │
In Progress
   │
Done
   │
Closed
```

Rework

```text
Done

↓

Reopened

↓

In Progress

↓

Done

↓

Closed
```

Cancellation

```text
Open

↓

Discarded
```

---

# Work Execution

Artists perform all production activities within a SubTask.

Typical activities include:

- Production work
- File creation
- Internal notes
- Time logging
- Progress updates
- Work submission

---

# Deliverables

A SubTask may generate one or more working files.

Examples:

- Maya Scene
- Blender File
- PSD
- FBX
- PNG
- Unreal Asset

Each submission references:

- Repository
- File Path
- Changeset
- Version

Actual files remain in Source Control.

---

# Time Tracking

Each SubTask records production effort.

Typical information:

- Estimated Hours
- Actual Hours
- Start Time
- End Time
- Total Duration

This information supports utilization and productivity reports.

---

# Progress

SubTask progress is updated by the assigned Artist.

Typical progress values:

```text
0%

25%

50%

75%

100%
```

Task progress is calculated from SubTask completion.

---

# Communication

Each SubTask includes a discussion area.

Supported features:

- Rich Text
- Mentions
- Attachments
- Internal Notes

SubTask communication is intended for execution-level collaboration.

---

# Attachments

Examples include:

- Reference Images
- Screenshots
- Working Files
- Design Notes
- Feedback Images

---

# Activity Timeline

Every production event is recorded.

Examples:

- Created
- Assigned
- Started
- Progress Updated
- Work Submitted
- Reopened
- Closed
- Discarded

---

# Relationship with Reviews

SubTasks are created by the Team Lead after review decisions.

Reviewers **never** assign work directly.

Example

```text
Final Review

↓

Feedback

↓

Lead Reviews Feedback

↓

Creates New FR Fix SubTasks

↓

Assigns Artists
```

The same flow applies to Client Review.

---

# Relationship with Feedback

One Feedback Item may result in:

- One SubTask
- Multiple SubTasks

Likewise,

One SubTask may resolve:

- One Feedback Item
- Multiple Feedback Items

Therefore the relationship should be **many-to-many**.

Example

```text
Feedback A

┐

├── SubTask 1

┘

Feedback B

↓

SubTask 1
```

A junction table should be maintained:

```text
FeedbackSubTask
```

---

# Business Rules

## BR-001

Every SubTask belongs to exactly one Task.

---

## BR-002

Every SubTask is assigned to exactly one Artist.

---

## BR-003

SubTasks cannot be reassigned.

---

## BR-004

Reassignment requires creating a new SubTask.

---

## BR-005

SubTasks belong to one Review Round.

---

## BR-006

SubTasks belong to one SubTask Type.

---

## BR-007

Reviewers never create SubTasks.

Only Team Leads or authorized Project Managers may create SubTasks.

---

## BR-008

Completing all SubTasks does **not** automatically complete the Task.

The Team Lead must manually verify and complete the Task.

---

## BR-009

Discarded SubTasks remain in the system for audit purposes.

---

## BR-010

Historical assignments, comments, files, and timelines must never be modified.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| SubTask Id | Primary Key |
| Task Id | Parent Task |
| Artist Id | Assigned Artist |
| Round No | Review Round |
| Type | General / FR Fix / Client Fix |
| Status | Current Status |
| Priority | Priority |
| Estimated Hours | Planned Effort |
| Actual Hours | Actual Effort |
| Progress | Completion Percentage |
| Due Date | Planned Completion |
| Description | Work Details |

---

# Reporting

Typical reports include:

- Artist Workload
- SubTask Aging
- Open SubTasks
- Productivity Report
- Time Tracking Report
- Rework Analysis
- Review Round Analysis
- SubTask Completion Report
- Effort Variance
- Artist Performance

---

# Future Enhancements

Future releases may include:

- AI Task Breakdown
- AI Artist Assignment Suggestions
- Skill-Based Assignment
- Automatic Effort Estimation
- Workload Balancing
- SLA Monitoring
- Smart Notifications
- AI Productivity Analysis
- Intelligent Scheduling
- Personal Work Dashboard

---

# Design Principles

The SubTask module follows these principles:

- SubTasks are the smallest executable work units.
- One SubTask is owned by one Artist.
- SubTasks cannot be reassigned.
- New review rounds create new SubTasks rather than modifying completed work.
- Historical production records are immutable.
- Reviewers provide feedback but never assign implementation work.
- Team Leads are responsible for translating feedback into executable SubTasks.
- Task completion is always a manual management decision after verifying all work has been merged successfully.

---

# Related Documents

- Task.md
- Review.md
- Feedback.md
- Workflow.md
- WorkflowProcess.md
- WorkflowState.md
- DeliverableManagement.md
- ResourceAllocation.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial SubTask domain specification |
