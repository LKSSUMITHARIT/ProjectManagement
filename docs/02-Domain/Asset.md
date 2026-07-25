# Asset Domain

> **Purpose**
>
> An **Asset** represents the primary production item within a Batch. It is the business entity on which actual production work is performed. Every Asset consists of one or more Tasks, and each Task contains one or more Subtasks that are executed by Artists.
>
> Assets are the bridge between production planning (Batch) and production execution (Tasks).

---

# Overview

An Asset is an individual production deliverable that passes through one or more production stages before completion.

Examples include:

- Character
- Environment
- Vehicle
- Weapon
- Animation
- Prop
- UI Screen
- VFX Shot
- Cinematic
- Audio Asset

Each Asset belongs to exactly one Batch and inherits its production pipeline from that Batch.

---

# Business Hierarchy

```text
Client
    │
Project
    │
Batch
    │
Asset
│
├── Tasks
│      ├── Subtasks
│      ├── Reviews
│      └── Deliverables
│
├── Attachments
├── Communication
└── Activity Timeline
```

---

# Objectives

The Asset module enables organizations to:

- Organize production work
- Track individual deliverables
- Generate production Tasks
- Monitor progress
- Manage versions
- Track review history
- Measure production performance
- Maintain complete traceability

---

# Business Ownership

| Property | Value |
|----------|-------|
| Domain Owner | Production Department |
| Operational Owner | Team Lead |
| Execution Owner | Assigned Artists |

---

# Asset Information

## Basic Information

Typical information includes:

- Asset Name
- Display Name
- Asset Code
- Batch
- Asset Type
- Category
- Priority
- Description
- Status

---

## Production Information

Additional production details include:

- Workflow Template
- Planned Delivery Date
- Actual Delivery Date
- Complexity
- Estimated Effort
- Current Progress

---

# Asset Types

The platform supports configurable Asset Types.

Examples:

```text
Character

Environment

Weapon

Vehicle

Animation

Prop

UI

VFX

Lighting

Audio
```

Organizations may define their own Asset Types.

---

# Task Generation

Tasks are created from the Batch Stages.

Example:

```text
Batch Stages

↓

Modeling

↓

Texturing

↓

Rigging

↓

Animation
```

Creating a new Character Asset automatically creates:

```text
Character

├── Modeling
├── Texturing
├── Rigging
└── Animation
```

Each Task inherits the Workflow configured for its Stage.

---

# Asset Structure

```text
Asset
│
├── Task
│      │
│      ├── General Subtasks
│      ├── FR Fix Subtasks
│      └── Client Fix Subtasks
│
├── Deliverables
├── Attachments
├── Communication
└── Timeline
```

---

# Task Relationship

An Asset may contain one or more Tasks.

Each Task:

- Represents one production discipline
- Has its own Workflow
- Has its own Reviews
- Has its own Deliverables
- Has independent progress

Example:

```text
Asset

├── Modeling
├── UV
├── Texturing
├── Rigging
└── QA
```

---

# Progress Calculation

Asset progress is calculated from its Tasks.

Typical metrics include:

- Total Tasks
- Open Tasks
- In Progress Tasks
- Review Tasks
- Closed Tasks

Overall Asset completion is derived from Task completion.

---

# Deliverables

Each completed Task may generate one or more Deliverables.

The Asset provides a consolidated view of all Deliverables.

The system stores metadata including:

- Repository
- File Path
- Version
- Changeset
- Upload Date
- Submitted By

Actual production files remain in external source control.

---

# Version Management

Assets maintain a history of production versions.

Example:

```text
Character A

Version 1

↓

Version 2

↓

Version 3

↓

Final
```

Each version references the corresponding repository path and source control changeset.

---

# Communication

Every Asset has its own discussion thread.

Supported features:

- Rich Text Comments
- Attachments
- Mentions
- Activity Feed
- Internal Notes

Asset communication is independent of Project, Batch, and Task discussions.

---

# Attachments

Asset-level attachments may include:

- Reference Images
- Concept Art
- Specifications
- Client References
- Design Documents
- Technical Notes

These are separate from production Deliverables.

---

# Activity Timeline

Every Asset event is recorded.

Examples:

- Asset Created
- Task Generated
- Task Completed
- Review Completed
- Deliverable Uploaded
- Version Created
- Asset Closed

---

# Asset Dashboard

The Asset page provides a complete production overview.

Typical sections include:

- Asset Information
- Progress Summary
- Task List
- Review Status
- Deliverables
- Version History
- Communication
- Attachments
- Activity Timeline

---

# Asset List View

The primary Asset list should display:

| Column | Description |
|----------|-------------|
| Asset Code | Business Identifier |
| Asset Name | Display Name |
| Asset Type | Character, Environment, etc. |
| Priority | Production Priority |
| Overall Progress | Calculated Progress |
| Open Tasks | Remaining Tasks |
| Pending Reviews | Active Reviews |
| Assigned Lead | Team Lead |
| Due Date | Planned Delivery |
| Status | Current Status |

The list should support:

- Search
- Filtering
- Sorting
- Bulk Operations
- Grouping
- Saved Views

---

# Business Rules

## BR-001

Every Asset belongs to exactly one Batch.

---

## BR-002

An Asset may contain multiple Tasks.

---

## BR-003

Tasks are initially generated from the configured Batch Stages.

---

## BR-004

Each generated Task references the originating Batch Stage.

---

## BR-005

Additional Tasks may be created manually if authorized.

---

## BR-006

Asset progress is calculated from Task progress.

---

## BR-007

An Asset cannot be marked as Completed until all mandatory Tasks are completed.

---

## BR-008

An Asset cannot be Closed until all Tasks are Closed.

---

## BR-009

Deleting an Asset is not permitted once production has started.

Assets should instead be archived.

---

## BR-010

Communication, Deliverables, Versions, and Activity History must be retained permanently for audit purposes.

---

# Lifecycle

```text
Draft
    │
Planned
    │
In Production
    │
In Review
    │
Completed
    │
Closed
    │
Archived
```

---

# Status Definitions

| Status | Description |
|----------|-------------|
| Draft | Asset created but not yet planned |
| Planned | Tasks generated and ready |
| In Production | Active work in progress |
| In Review | One or more Tasks under review |
| Completed | Production complete |
| Closed | Operationally closed |
| Archived | Historical reference |

---

# Suggested Data Model

## Asset

| Field | Description |
|------|-------------|
| Asset Id | Primary Key |
| Batch Id | Parent Batch |
| Asset Code | Business Identifier |
| Name | Asset Name |
| Display Name | Display Name |
| Asset Type Id | Asset Type |
| Priority | Priority |
| Status | Current Status |
| Complexity | Complexity Level |
| Estimated Effort | Estimated Production Hours |
| Planned Delivery Date | Planned Completion |
| Actual Delivery Date | Actual Completion |
| Description | Notes |

---

# Reporting

Typical reports include:

- Asset Progress Report
- Asset Completion Report
- Asset Aging Report
- Asset Delivery Report
- Production Velocity
- Task Distribution
- Review Summary
- Version History Report
- Artist Productivity
- Asset Cycle Time

---

# Future Enhancements

Future releases may include:

- Asset Templates
- Asset Cloning
- Asset Dependencies
- Parent-Child Assets
- Linked Assets
- Asset Cost Tracking
- AI Asset Planning
- AI Complexity Estimation
- Asset Health Score
- Automated Task Generation Rules
- Production Forecasting

---

# Design Principles

The Asset module follows these principles:

- An Asset represents a single production deliverable.
- Assets are the primary planning unit within a Batch.
- Tasks define the production disciplines required to complete an Asset.
- Subtasks define the actual work assigned to Artists.
- Asset progress is derived from Task progress.
- Deliverables and Versions provide complete production traceability.
- Every production activity is fully auditable.

---

# Related Documents

- Batch.md
- BatchStage.md
- Task.md
- Subtask.md
- Workflow.md
- DeliverableManagement.md
- CommunicationModel.md
- AuditModel.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Asset domain specification |
