# Glossary

> **Purpose**
>
> This glossary defines the common business, production, workflow, technical, and financial terms used throughout the Project Management Platform documentation.
>
> Unless explicitly stated otherwise, the definitions in this document shall be considered the authoritative meaning of these terms across the entire project.

---

# How to Use This Document

This glossary serves as the standard vocabulary for:

- Product Documentation
- Business Requirements
- Functional Specifications
- Database Design
- API Documentation
- User Manuals
- Architecture Documents

Every document should use these definitions consistently.

---

# A

## Activity Log

A chronological record of user actions and system events related to a business entity.

Example:

- Task Updated
- Status Changed
- User Assigned
- Invoice Generated

---

## Allocation

The assignment of a resource to one or more batches for a defined duration and allocation percentage.

---

## Allocation Request

A request submitted by a Batch Manager or authorized user to reserve a resource for a batch. The request must be approved by the Resource Manager before becoming active.

---

## Asset

A production item within a batch that represents a deliverable or unit of work.

Examples:

- Character
- Vehicle
- Environment
- Animation
- Weapon
- UI Screen
- 3D Model

Each Asset may contain one or more Tasks.

---

## Audit Trail

A permanent record of important business events for compliance, traceability, and reporting.

---

# B

## Batch

A logical grouping of Assets within a Project.

A Batch is used to organize production work, allocate resources, monitor progress, and manage deliveries.

---

## Batch Manager

A user responsible for managing production activities within a Batch, including resource requests, task planning, and delivery coordination.

---

## Business Rule

A configurable rule that controls workflow behavior, permissions, validations, or transitions.

---

# C

## Client

An organization or customer for whom one or more Projects are executed.

---

## Client Fix Task

A Subtask created in response to feedback received during Client Review.

Client Fix Tasks belong to a specific review round.

---

## Client Review

The review stage where the client evaluates completed work and decides whether to approve it or request changes.

Possible outcomes:

- Approve
- Minor Fix
- Major Fix

---

## Closed

The final status indicating that a Task, Subtask, or business process has been successfully completed.

---

## Communication Thread

A contextual discussion attached to a Project, Batch, Asset, or Task.

---

## Custom Field

A configurable field that allows organizations to capture additional business information without modifying the application.

---

# D

## Deliverable

The final output delivered to the client or downstream production stage.

A Deliverable references files stored in an external source control system.

---

## Deliverable Version

A specific revision of a Deliverable associated with a workflow transition, repository revision, or changeset.

---

## Dependency *(Future)*

A relationship indicating that one Task depends on another before work can proceed.

This feature is planned for a future release.

---

## Discarded

A Subtask status indicating that the work is no longer required and has been intentionally abandoned.

---

# F

## Feedback

Comments, observations, or requested changes generated during any review stage.

Feedback is transformed into one or more new Subtasks by the Lead or Project Manager.

---

## Final Review (FR)

The internal production review performed after Lead approval.

Possible outcomes:

- Approve
- Minor Fix
- Major Fix

---

## FR Fix Task

A Subtask created from Final Review feedback.

These tasks belong to a specific Final Review round.

---

# I

## Invoice

A financial document generated against a **Project** for completed work.

Although invoices are issued to the Client, they are always associated with a Project.

---

# K

## Kanban Board

A visual representation of Tasks organized by Workflow Process.

Each card represents a Task, while swimlanes or columns represent configurable Processes.

---

## KPI

Key Performance Indicator used to measure business, production, financial, or operational performance.

---

# L

## Lead

A production supervisor responsible for planning Tasks, creating Subtasks, reviewing work, and coordinating production activities.

---

# M

## Major Fix

Review outcome indicating that substantial rework is required.

Major Fixs continue through the complete review cycle, including Final Review, QC (if configured), and Client Review (if applicable).

---

## Minor Fix

Review outcome indicating that limited corrections are required.

Minor Fix Subtasks bypass the originating review stage on resubmission but continue through the remaining downstream workflow.

---

# O

## Open

The initial status of a newly created Task or Subtask.

No production work has started.

---

## Outstanding Payment

An amount invoiced but not yet received from the Client.

Outstanding balances may be reduced through payments, approved discounts, or waivers.

---

# P

## Parent Client

A Client that owns or manages one or more subsidiary Clients.

---

## Payment

A financial transaction recorded against one or more Project Invoices.

---

## Process

A high-level stage within a Workflow representing a business activity.

Examples:

- Production
- WIP Review
- Final Review
- QC
- Client Review
- Closed

A Process may contain multiple States.

---

## Project

A contractual engagement executed for a Client.

A Project contains one or more Batches.

---

## Project Manager (PM)

A user responsible for project planning, scheduling, client communication, delivery, and overall project execution.

---

# Q

## Quality Control (QC)

The validation stage performed after Final Review.

QC verifies technical quality before work is submitted to the Client.

---

# R

## Resource

A person assigned to perform production work.

Examples:

- Artist
- Animator
- Modeler
- Designer
- Technical Artist

---

## Resource Allocation

Assignment of a Resource to one or more Batches for a specified percentage and duration.

---

## Resource Manager

A user responsible for approving allocation requests and balancing organizational capacity.

---

## Review

A quality validation activity performed during production.

Supported review types include:

- WIP Review
- Final Review
- QC
- Client Review

---

## Review Round

A complete iteration of a review process.

Every new set of review feedback creates a new Round Number.

---

## Rich Text

Formatted text supporting:

- Tables
- Lists
- Images
- Hyperlinks
- Attachments
- Formatting

Used for comments and communication.

---

# S

## Stage

A production stage defined at the Batch level.

Each Stage is associated with a Workflow and serves as the template for Task creation.

---

## State

A specific status within a Process.

Example:

Process: Final Review

States:

- Waiting
- Under Review
- Approved
- Rejected

States represent the current operational condition of a Task.

---

## Status

The current operational condition of a business entity.

Examples:

- Open
- In Progress
- Completed
- Closed

For workflow-enabled entities, Status is represented by the combination of Workflow, Process, and State.

---

## Subtask

The smallest assignable unit of production work.

Each Subtask:

- Is assigned to a single Resource.
- Cannot be reassigned.
- May be closed, reopened, or discarded.
- Belongs to a Task.
- Has a Subtask Type.
- Has a Review Round Number.

---

## Subtask Type

Defines why a Subtask was created.

Supported types include:

- General
- Final Review Fix
- Client Fix

Additional types may be introduced in future releases.

---

# T

## Tag

A configurable label used for classification, filtering, grouping, and reporting.

---

## Task

A production activity within an Asset.

A Task is composed of one or more Subtasks and progresses through a configurable Workflow.

---

## Timeline

A chronological view of Activities, Comments, Reviews, Workflow Changes, and Assignments related to an entity.

---

# U

## User

Any authenticated individual interacting with the platform.

Examples:

- Administrator
- Project Manager
- Lead
- Artist
- Reviewer
- Client (Future)

---

# V

## Version

A unique revision of a Deliverable or production output linked to a repository changeset or source control revision.

---

# W

## Waiver

An approved financial adjustment that reduces or clears an outstanding invoice balance without receiving payment.

---

## WIP Review

Work-In-Progress Review performed before formal completion of a Task.

WIP Review may occur even when not all Subtasks are complete.

---

## Workflow

A configurable business process defining how a Task progresses from creation to completion.

A Workflow consists of:

- Processes
- States
- Transitions
- Rules
- Permissions

---

## Workflow Transition

Movement of a Task from one State or Process to another according to defined workflow rules.

---

# Standard Status Values

## Task Status

- Open
- In Progress
- Closed

> The detailed lifecycle of a Task is controlled by **Workflow + Process + State**, not by the Task Status alone.

---

## Subtask Status

- Open
- In Progress
- Done
- Reopen
- Closed
- Discarded

---

# Standard Review Outcomes

## WIP Review

- Approve
- Feedback

---

## Final Review

- Approve
- Minor Fix
- Major Fix

---

## Quality Control

- Approve
- Reject

---

## Client Review

- Approve
- Minor Fix
- Major Fix

---

# Naming Conventions

To maintain consistency across the platform:

| Entity | Singular | Plural |
|----------|----------|---------|
| Client | Client | Clients |
| Project | Project | Projects |
| Batch | Batch | Batches |
| Asset | Asset | Assets |
| Task | Task | Tasks |
| Subtask | Subtask | Subtasks |
| Workflow | Workflow | Workflows |
| Process | Process | Processes |
| State | State | States |
| Review | Review | Reviews |
| Deliverable | Deliverable | Deliverables |
| Invoice | Invoice | Invoices |

---

# Related Documents

- Vision.md
- ProductGoals.md
- ProductScope.md
- Domain Model Documentation
- Workflow Documentation
- Database Documentation

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Glossary |
