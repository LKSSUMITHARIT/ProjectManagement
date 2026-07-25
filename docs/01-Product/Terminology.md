# Terminology

> **Purpose**
>
> This document defines the common business and technical terminology used throughout the Project Management Platform. A shared vocabulary ensures that stakeholders, developers, testers, business analysts, project managers, and end users interpret business concepts consistently.
>
> Unless explicitly stated otherwise, the definitions in this document are considered authoritative across all project documentation.

---

# Overview

The Project Management Platform is designed around a structured production workflow. Many terms used throughout the system have specific business meanings that differ from their general usage.

This glossary serves as the single source of truth for those terms.

---

# Terminology Categories

- Organization
- Project Management
- Production
- Workflow
- Reviews
- Resource Management
- Finance
- Deliverables
- Communication
- System
- Reporting

---

# Organization

## Client

An organization or customer for whom projects are executed.

A Client can own multiple Projects.

---

## Parent Client

A higher-level organization that groups one or more Clients.

Example:

```text
Microsoft
    ├── Xbox Studios
    ├── Mojang
    └── Bethesda
```

---

## Contact

A person representing a Client.

Contacts may receive invoices, notifications, or review requests.

---

## Region

A geographical business region assigned to a Client.

Examples:

- North America
- Europe
- APAC

---

# Project Management

## Project

A contractual engagement executed for a Client.

A Project contains one or more Batches.

---

## Project Team

The collection of users responsible for delivering the Project.

Typical members include:

- Project Manager
- Batch Manager
- Team Leads
- Artists

---

## Required Software

The list of software applications authorized for use within a Project.

This list is used to determine software access for allocated artists.

---

# Production

## Batch

A production unit within a Project.

A Batch groups related Assets and defines the production workflow used during execution.

---

## Batch Stage

A logical phase within a Batch.

Each stage is associated with a Workflow that governs the Tasks created under that stage.

Examples:

- Modeling
- Texturing
- Rigging
- Animation

---

## Asset

An individual production deliverable.

Examples:

- Character
- Vehicle
- Environment
- Weapon
- Animation
- UI Screen

Each Asset belongs to one Batch.

---

## Task

A production activity performed on an Asset.

A Task follows a configured Workflow and progresses through multiple review stages.

A Task may contain multiple Subtasks.

---

## Subtask

The smallest assignable work item.

Each Subtask:

- Is assigned to one Artist
- Belongs to one Task
- Cannot be reassigned
- Has its own status

---

## Artist

A production resource responsible for executing assigned Subtasks.

---

# Subtask Types

## General Subtask

The initial production work created by the Team Lead before execution begins.

---

## FR Fix Subtask

A Subtask created after Final Review feedback.

---

## Client Fix Subtask

A Subtask created after Client Review feedback.

---

## Review Round

A complete review iteration.

Each review cycle generates a new round so the platform can maintain historical production data.

Example:

```text
Round 1

↓

Round 2

↓

Round 3
```

---

# Workflow

## Workflow

A configurable business process defining how a Task progresses from creation to completion.

A Workflow consists of one or more Processes and States.

---

## Process

A major stage in the business workflow.

Examples:

- Production
- WIP Review
- Final Review
- QC
- Client Review

Kanban swimlanes are based on Processes.

---

## State

The current status of a Task within a Process.

States define the exact position of work inside a workflow.

Example:

```text
Process

↓

In Review

↓

Waiting Approval
```

---

## Transition

A valid movement from one State to another according to Workflow rules.

---

## Workflow Transition

A business event that moves a Task between workflow states.

Every transition is recorded in the audit history.

---

# Reviews

## WIP Review

Work-In-Progress Review.

An early quality check performed before production is complete.

---

## Lead Review

Review performed by the Team Lead.

The Lead may:

- Approve
- Reopen work
- Close completed Subtasks

---

## Final Review (FR)

Internal review performed after Lead approval.

Possible outcomes include:

- Approve
- Minor Fix
- Major Fix

---

## Quality Control (QC)

Validation stage ensuring production quality before client delivery.

---

## Client Review

External review performed by the Client.

Possible outcomes include:

- Approve
- Minor Fix
- Major Fix

---

## Feedback

Comments provided during a review describing required changes.

Feedback itself does not assign work.

The Team Lead or Project Manager converts feedback into new Subtasks.

---

## Minor Fix

A review outcome indicating that small corrections are required.

Typically, the work returns to production without repeating every review stage, depending on the configured Workflow.

---

## Major Fix

A review outcome indicating significant corrections are required.

The Task re-enters the full review cycle according to the configured Workflow.

---

# Resource Management

## Resource

A user available for project work.

Examples:

- Artist
- Team Lead
- Reviewer

---

## Allocation

The assignment of a Resource to a Batch.

---

## Allocation Request

A request submitted by a Batch Manager to reserve Resources for a Batch.

Requires approval by a Resource Manager.

---

## Allocation Percentage

The percentage of a Resource's available capacity assigned to a Batch.

Example:

```text
Batch A : 60%

Batch B : 40%
```

---

## Capacity

The total amount of work a Resource can perform during a defined period.

---

## Utilization

The percentage of available capacity currently allocated to production work.

---

# Deliverables

## Deliverable

The output produced by completing a Task.

---

## Version

A specific revision of a Deliverable.

---

## Changeset

The source control revision associated with a Deliverable.

Examples:

- Git Commit
- Perforce Changelist
- SVN Revision

---

## Repository

The external source control system where production files are stored.

Examples:

- Git
- Perforce
- SVN

---

## File Path

The location of the Deliverable within the source control repository.

---

# Finance

## Invoice

A financial document generated **against a Project** and issued to the associated Client.

---

## Outstanding Amount

The unpaid balance remaining on an Invoice.

---

## Discount

A reduction in the Invoice amount granted before settlement.

---

## Waiver

A business-approved write-off that closes part or all of an outstanding balance without payment.

---

## Payment

A financial transaction recorded against an Invoice.

---

# Communication

## Discussion

A contextual communication thread attached to a business entity.

Supported at:

- Project
- Batch
- Asset
- Task

---

## Mention

A reference to another user within a discussion that triggers a notification.

---

## Attachment

A file uploaded as part of a discussion or business record.

This is separate from production deliverables.

---

# Reporting

## Dashboard

A visual summary of business metrics and operational status.

---

## KPI

Key Performance Indicator.

A measurable value used to evaluate operational or business performance.

Examples:

- Asset Completion
- Resource Utilization
- On-Time Delivery
- Review Turnaround Time

---

## Kanban Board

A visual representation of Tasks organized by Workflow Processes and States.

The platform uses:

- **Swimlanes** based on **Process**
- **Columns** based on **State**

---

# System

## Activity Timeline

A chronological history of actions performed on a business entity.

---

## Audit Log

A permanent record of significant business or system events.

---

## Notification

A system-generated message informing users about business events.

---

## Role

A collection of permissions assigned to users.

---

## Permission

Authorization allowing a user to perform a specific action.

---

## Custom Field

A configurable field added by an organization without modifying the application.

---

## Tag

A configurable label used to categorize and search business entities.

---

# General Terms

## Production

The execution phase where Artists perform work assigned through Subtasks.

---

## Work Item

A generic term referring to any executable unit of work.

Examples:

- Task
- Subtask

---

## Lifecycle

The complete journey of an entity from creation through completion and closure.

---

## Traceability

The ability to track every business action, decision, workflow transition, review, assignment, and financial event throughout the lifecycle of a Project.

---

# Naming Conventions

Throughout the documentation, the following capitalization rules apply:

| Term | Usage |
|------|-------|
| Client | Business Entity |
| Project | Business Entity |
| Batch | Business Entity |
| Asset | Business Entity |
| Task | Business Entity |
| Subtask | Business Entity |
| Workflow | Configurable Workflow Definition |
| Process | Workflow Stage |
| State | Position within a Process |
| Review Round | Review Iteration |
| Deliverable | Production Output |

---

# Related Documents

- ProductOverview.md
- ProductHierarchy.md
- ProductModules.md
- BusinessLifecycle.md
- 02-Domain/*
- 03-Modules/*
- 04-Workflow/*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial terminology reference |
