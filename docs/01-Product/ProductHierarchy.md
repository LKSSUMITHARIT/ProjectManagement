# Product Hierarchy

> **Purpose**
>
> This document defines the hierarchical structure of the Project Management Platform. It explains how business entities relate to one another, how work flows from high-level planning to execution, and how information is organized throughout the system.
>
> The hierarchy serves as the foundation for permissions, navigation, reporting, workflow execution, resource planning, and data modeling.

---

# Overview

The platform follows a hierarchical production model.

Business planning starts at the **Client** level and progressively breaks down into increasingly granular production units until work reaches an individual artist through a **Subtask**.

```text
Client
    │
    ▼
Project
    │
    ▼
Batch
    │
    ▼
Asset
    │
    ▼
Task
    │
    ▼
Subtask
```

This hierarchy ensures:

- Clear ownership
- Better planning
- Scalable production
- Accurate reporting
- Complete traceability

---

# Hierarchy Levels

| Level | Entity | Purpose |
|---------|---------|---------|
| 1 | Client | Customer organization |
| 2 | Project | Contract / Engagement |
| 3 | Batch | Production Unit |
| 4 | Asset | Production Deliverable |
| 5 | Task | Production Activity |
| 6 | Subtask | Individual Work Assignment |

---

# Complete Product Hierarchy

```text
Organization
│
├── Client
│   │
│   ├── Project
│   │   │
│   │   ├── Project Team
│   │   ├── Required Software
│   │   ├── Communication
│   │   ├── Documents
│   │   ├── Financial Information
│   │   │
│   │   └── Batch
│   │       │
│   │       ├── Batch Team
│   │       ├── Resource Allocation
│   │       ├── Workflow
│   │       ├── Production Stages
│   │       ├── Communication
│   │       │
│   │       └── Asset
│   │           │
│   │           ├── Attachments
│   │           ├── Communication
│   │           ├── Deliverables
│   │           │
│   │           └── Task
│   │               │
│   │               ├── Workflow
│   │               ├── Reviews
│   │               ├── Deliverables
│   │               ├── Activity Timeline
│   │               ├── Communication
│   │               │
│   │               └── Subtask
│   │                   │
│   │                   ├── Assigned Artist
│   │                   ├── Feedback
│   │                   ├── Attachments
│   │                   ├── Status
│   │                   └── Round
│   │
│   └── Invoices
│
└── Reports
```

---

# Level 1 — Client

The Client represents the organization receiving services.

## Contains

- Projects
- Contacts
- Addresses
- Financial Summary
- Active Projects
- Outstanding Payments

## Owned By

Business / Sales

---

# Level 2 — Project

A Project represents a contractual engagement executed for a Client.

## Contains

- Project Team
- Required Software
- Communication
- Documents
- Batches
- Billing Information

## Responsibilities

- Production Planning
- Financial Tracking
- Client Communication
- Delivery Management

---

# Level 3 — Batch

A Batch is a logical production package within a Project.

It is the primary planning and execution unit.

## Contains

- Batch Team
- Workflow
- Stages
- Assets
- Resource Allocation

## Responsibilities

- Production Scheduling
- Resource Planning
- Workflow Selection
- Delivery Tracking

---

# Level 4 — Asset

An Asset represents an actual production deliverable.

Examples include:

- Character
- Vehicle
- Environment
- Weapon
- Animation
- UI Screen
- Prop

Each Asset belongs to exactly one Batch.

## Contains

- Tasks
- Deliverables
- Attachments
- Communication

---

# Level 5 — Task

A Task represents a production activity performed on an Asset.

Each Task follows a configurable Workflow.

## Contains

- Workflow
- Process
- State
- Reviews
- Deliverables
- Timeline
- Subtasks

A Task may have multiple Subtasks.

---

# Level 6 — Subtask

A Subtask is the smallest assignable work item.

Each Subtask:

- Belongs to one Task
- Is assigned to one Artist
- Cannot be reassigned
- Has its own lifecycle
- Belongs to a Review Round

## Supported Types

- General
- Final Review Fix
- Client Fix

---

# Supporting Hierarchies

## Team Hierarchy

```text
Project
    │
    ├── Project Manager
    ├── Leads
    └── Members

Batch
    │
    ├── Batch Manager
    ├── Leads
    └── Artists
```

---

## Resource Hierarchy

Resources are allocated at the **Batch** level.

```text
Resource
      │
      ▼
Allocation Request
      │
      ▼
Approval
      │
      ▼
Batch Allocation
      │
      ▼
Task Assignment
      │
      ▼
Subtask Assignment
```

---

## Workflow Hierarchy

The workflow model is independent of the business hierarchy.

```text
Workflow
      │
      ▼
Process
      │
      ▼
State
```

Every Task references:

- Workflow
- Current Process
- Current State

---

## Review Hierarchy

```text
Task
    │
    ▼
Review Round
    │
    ├── WIP Review
    ├── Final Review
    ├── QC
    └── Client Review
            │
            ▼
Feedback
            │
            ▼
New Subtasks
```

Each review cycle is recorded independently.

---

## Deliverable Hierarchy

```text
Project
    │
    ▼
Batch
    │
    ▼
Asset
    │
    ▼
Task
    │
    ▼
Deliverable
        │
        ├── Repository
        ├── Branch
        ├── File Path
        ├── Version
        └── Changeset
```

---

## Communication Hierarchy

Communication is contextual.

```text
Project
    │
    ├── Discussion
    │
Batch
    │
    ├── Discussion
    │
Asset
    │
    ├── Discussion
    │
Task
    │
    └── Discussion
```

Each discussion is isolated to its business context.

---

# Navigation Hierarchy

Users navigate the application using the production hierarchy.

```text
Client
    ▼
Project
    ▼
Batch
    ▼
Asset
    ▼
Task
    ▼
Subtask
```

Breadcrumb example:

```text
Clients
 > Microsoft
 > Halo Infinite
 > Environment Batch 03
 > Jungle Temple
 > Texturing
 > Texture Polish
```

---

# Reporting Hierarchy

Reports can be generated at every hierarchy level.

| Level | Example Reports |
|---------|----------------|
| Client | Revenue, Outstanding, Active Projects |
| Project | Progress, Profitability, Delivery |
| Batch | Production, Utilization, Timeline |
| Asset | Completion, Review Status |
| Task | Workflow, Reviews, Aging |
| Subtask | Artist Productivity, Workload |

---

# Permission Hierarchy

Permissions cascade through the hierarchy.

Example:

```text
Project Access
      │
      ▼
Batch Access
      │
      ▼
Asset Access
      │
      ▼
Task Access
      │
      ▼
Subtask Access
```

Organizations may override inherited permissions where necessary.

---

# Audit Hierarchy

Every level maintains its own activity timeline.

```text
Project Timeline
Batch Timeline
Asset Timeline
Task Timeline
```

Each timeline records:

- Status Changes
- Workflow Transitions
- Assignments
- Comments
- Reviews
- Deliverables
- Attachments

---

# Financial Hierarchy

Financial ownership follows the production hierarchy.

```text
Client
      │
      ▼
Project
      │
      ▼
Invoice
      │
      ▼
Payment
      │
      ├── Discount
      └── Waiver
```

> **Note:** Invoices are created **against Projects** and issued to the associated Client.

---

# Hierarchy Principles

The product hierarchy follows these principles:

- Parent entities own child entities.
- Work flows from higher-level planning to lower-level execution.
- Reporting aggregates upward through the hierarchy.
- Permissions inherit downward unless explicitly overridden.
- Communication remains contextual.
- Workflow execution occurs at the Task level.
- Resource planning occurs at the Batch level.
- Financial management occurs at the Project level.
- Audit history exists independently at each hierarchy level.

---

# Related Documents

- ProductOverview.md
- ProductArchitecture.md
- ProductModules.md
- 02-Domain/EntityRelationship.md
- 03-Modules/*
- 04-Workflow/*
- 06-Database/*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Product Hierarchy |
