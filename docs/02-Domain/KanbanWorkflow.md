# Kanban Workflow

> **Purpose**
>
> The Kanban Workflow provides a visual representation of production work by displaying Tasks based on their current Workflow Process and Workflow State.
>
> Unlike traditional Kanban boards that organize work only by status, this platform organizes work using the Workflow Engine, allowing Processes, States, and Workflow Actions to drive the board dynamically.
>
> The Kanban board is a visualization layer over the Workflow Engine and does not contain business logic.

---

# Overview

The Kanban Board displays Tasks according to their current Workflow.

Example

```text
Workflow

↓

Process

↓

State

↓

Task Card
```

Every movement on the Kanban Board executes a Workflow Transition.

---

# Objectives

The Kanban Board provides:

- Real-time production visibility
- Workflow visualization
- Task prioritization
- Workload balancing
- Bottleneck identification
- Production monitoring
- Review tracking

---

# Architecture

```text
Workflow

↓

Process (Swimlane)

↓

State (Column)

↓

Task Card
```

---

# Board Structure

The board consists of:

- Workflow
- Swimlanes
- Columns
- Task Cards
- Filters
- Quick Actions

---

# Swimlanes

Swimlanes represent Workflow Processes.

Example

```text
Production

Lead Review

Final Review

QC

Client Review

Completed
```

Each Swimlane groups related Workflow States.

---

# Columns

Columns represent Workflow States.

Example

```
Production

-----------------------------------

Open

In Progress

Waiting

Completed
```

Lead Review

```
Waiting

Reviewing

Approved
```

Final Review

```
Waiting

Reviewing

Approved

Minor Fix

Major Fix
```

---

# Example Board

```text
┌───────────────────────────────────────────────────────────────────────┐
│                        PRODUCTION                                     │
├────────────┬──────────────┬──────────────┬──────────────┐
│ Open       │ In Progress  │ Waiting      │ Completed    │
├────────────┼──────────────┼──────────────┼──────────────┤
│ Task-101   │ Task-108     │ Task-122     │ Task-130     │
│ Task-102   │ Task-109     │              │              │
└────────────┴──────────────┴──────────────┴──────────────┘

┌───────────────────────────────────────────────────────────────────────┐
│                        FINAL REVIEW                                   │
├────────────┬──────────────┬──────────────┬──────────────┐
│ Waiting    │ Reviewing    │ Minor Fix    │ Approved     │
├────────────┼──────────────┼──────────────┼──────────────┤
│ Task-140   │ Task-150      │ Task-162     │ Task-170     │
└────────────┴──────────────┴──────────────┴──────────────┘
```

---

# Task Card

Each card displays:

- Task Number
- Title
- Priority
- Asset
- Assigned Lead
- Assigned Artists
- Due Date
- Current Process
- Current State
- Progress
- Review Round
- Tags
- Blockers

Optional

- Thumbnail
- Version
- Story Points
- Time Logged

---

# Card Color Indicators

Suggested colors

| Indicator | Meaning |
|------------|----------|
| Blue | Normal |
| Green | Approved |
| Orange | Waiting Review |
| Yellow | Minor Fix |
| Red | Major Fix |
| Gray | Closed |

---

# Card Badges

Badges may include:

- Review Round
- Number of Feedback Items
- Number of Open SubTasks
- Attachments
- Deliverables
- Comments
- Mentions
- Blocked
- Overdue

---

# Drag and Drop

Dragging a card does not directly change State.

Instead

```text
User Drops Card

↓

Workflow Engine

↓

Validate Transition

↓

Permission Check

↓

Execute Workflow Action

↓

Refresh Board
```

If validation fails

↓

Card returns to original position.

---

# Quick Actions

Task Cards support:

- Open Task
- View Asset
- Add Comment
- Upload Deliverable
- View Feedback
- Start Timer
- Stop Timer
- Assign User
- Watch Task

---

# Filters

Supported filters

- Project
- Batch
- Asset
- Lead
- Artist
- Client
- Workflow
- Process
- State
- Priority
- Due Date
- Review Round
- Tags

---

# Search

Search by

- Task Number
- Asset Name
- Batch
- Project
- Client
- Artist
- Lead
- Deliverable Version

---

# WIP Limits

Each Workflow State may define:

- Maximum Tasks
- Maximum Story Points
- Maximum Review Capacity

Example

```
Final Review

Maximum

10 Tasks
```

---

# Swimlane Metrics

Each Swimlane displays

- Total Tasks
- Waiting Tasks
- Active Tasks
- Average Time
- Blocked Tasks

---

# Board Metrics

Dashboard examples

- Total Open Tasks
- Average Cycle Time
- Bottleneck Analysis
- Tasks per Artist
- Review Queue
- SLA Violations

---

# Business Rules

## BR-001

Every Task appears only once on a Kanban Board.

---

## BR-002

Task location is determined by Process and State.

---

## BR-003

Manual movement executes a Workflow Transition.

---

## BR-004

Permission and Validation rules apply before movement.

---

## BR-005

Cards cannot bypass Workflow Processes.

---

## BR-006

Board updates occur in real time.

---

## BR-007

Swimlanes are generated from Workflow Processes.

---

## BR-008

Columns are generated from Workflow States.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| BoardId | Primary Key |
| WorkflowId | Workflow |
| ProcessId | Swimlane |
| StateId | Column |
| DisplayOrder | Position |
| WIPLimit | Maximum Tasks |
| IsCollapsed | UI State |

---

# Reporting

Typical reports include:

- Cycle Time
- Lead Time
- Workflow Bottlenecks
- WIP Analysis
- Task Aging
- Review Queue
- Blocked Tasks
- Team Capacity

---

# Future Enhancements

Future releases may include:

- AI Board Optimization
- Predictive Bottleneck Detection
- Smart WIP Recommendations
- Capacity Forecasting
- Heat Maps
- Multi-board Views
- Cross-project Boards
- Timeline View
- Gantt View
- Portfolio Kanban

---

# Design Principles

The Kanban Workflow follows these principles:

- The board is a visualization of the Workflow Engine.
- Workflow rules always take precedence over UI interactions.
- Swimlanes represent Workflow Processes.
- Columns represent Workflow States.
- Every movement is validated by the Workflow Engine.
- Real-time synchronization ensures production visibility.
- The board must scale to thousands of Tasks without sacrificing responsiveness.

---

# Related Documents

- Workflow.md
- WorkflowProcess.md
- WorkflowState.md
- WorkflowTransition.md
- Task.md
- ReviewWorkflow.md
- Dashboard.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Kanban Workflow specification |
