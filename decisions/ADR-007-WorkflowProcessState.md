# ADR-007: Workflow Process, State & State Machine Architecture

**ADR ID:** ADR-007

**Title:** Hierarchical Workflow Process & State Machine Model

**Status:** Accepted

**Date:** 2026-07-26

**Decision Makers:**

- Solution Architect
- Product Owner
- Technical Architect
- Business Process Team

---

# Context

The platform manages multiple business entities, each with its own lifecycle, including:

- Client
- Project
- Batch
- Asset
- Task
- Review
- Invoice
- Deliverable
- Resource Allocation
- Change Request

Although every entity has a lifecycle, not every lifecycle is identical.

For example:

- A Project has phases.
- A Task has execution states.
- A Review has approval states.
- An Invoice has payment states.

Many enterprise systems model these using a single **Status** column, which quickly becomes insufficient for complex business processes.

The platform requires a flexible, hierarchical workflow model capable of supporting:

- Multiple workflow definitions
- Multiple business processes
- Multiple states
- Configurable transitions
- Versioning
- Parallel workflows
- Nested workflows

---

# Problem Statement

Using a simple status field creates several limitations:

- Status values become inconsistent.
- No transition validation.
- No audit history.
- No process grouping.
- Difficult reporting.
- Impossible workflow customization.
- Hardcoded business logic.

A structured Workflow → Process → State hierarchy is required.

---

# Decision

The platform will adopt a **three-level workflow hierarchy** consisting of:

```text
Workflow

    ↓

Process

    ↓

State
```

The Workflow Engine will execute transitions through a configurable **State Machine**, ensuring that every state transition is validated, auditable, and extensible.

No business module may directly update entity status.

All state changes must occur through the Workflow Engine.

---

# Architectural Principles

The architecture follows:

- State Machine Pattern
- Domain-Driven Design
- Metadata-Driven Configuration
- Immutable State History
- Versioned Workflows
- Event-Driven Processing
- Separation of Process and State

---

# Workflow Hierarchy

## Level 1 — Workflow

Represents the complete lifecycle for a business entity.

Examples:

- Project Workflow
- Task Workflow
- Review Workflow
- Asset Workflow
- Invoice Workflow

A workflow defines:

- Name
- Version
- Entity Type
- Active Status
- Description

---

## Level 2 — Process

A workflow is divided into one or more business processes.

Example

```text
Project Workflow

│

├── Planning

├── Execution

├── Testing

├── Delivery

└── Closure
```

Each process groups related states.

Benefits include:

- Better reporting
- Easier visualization
- Business-friendly organization
- Modular workflow design

---

## Level 3 — State

A process consists of multiple states.

Example

```text
Execution

↓

Assigned

↓

In Progress

↓

Blocked

↓

Completed
```

Each state defines:

- Display Name
- System Name
- Order
- Entry Actions
- Exit Actions
- SLA
- Permissions
- Allowed Roles
- Notifications
- Automation Rules

---

# Example Workflow Structure

```text
Task Workflow

│

├── Planning

│     ├── Draft

│     ├── Open

│     └── Assigned

│

├── Execution

│     ├── In Progress

│     ├── Blocked

│     └── Pending Review

│

├── Review

│     ├── Under Review

│     ├── Changes Requested

│     └── Approved

│

└── Completion

      ├── Completed

      └── Archived
```

---

# State Machine

Every workflow is executed through a finite state machine.

```text
Draft

↓

Open

↓

Assigned

↓

In Progress

↓

Review

↓

Approved

↓

Completed
```

Invalid transitions are rejected.

Example:

```text
Draft

↓

Completed

❌ Invalid
```

---

# Transition Rules

Transitions define how entities move between states.

Each transition specifies:

- Source State
- Destination State
- Trigger
- Conditions
- Required Permissions
- Required Approvals
- Validation Rules
- Automation Actions

---

# Transition Example

```text
Assigned

↓

Start Work

↓

In Progress
```

Configuration

| Property | Value |
|----------|-------|
| Source | Assigned |
| Target | In Progress |
| Trigger | Start |
| Role | Developer |
| Approval | Not Required |

---

# Process Independence

Processes are logical containers.

States may transition:

- Within the same process
- Across different processes

Example

```text
Execution

↓

Pending Review

↓

Review Process

↓

Approved
```

---

# State Categories

States may be categorized as:

- Initial
- Intermediate
- Waiting
- Review
- Approval
- Completed
- Cancelled
- Terminal

---

# Terminal States

Terminal states cannot transition further unless explicitly reopened.

Examples

- Completed
- Cancelled
- Archived

---

# Reopen Support

Workflows may optionally support reopening.

Example

```text
Completed

↓

Reopen

↓

Assigned
```

Only authorized users may perform reopen operations.

---

# Parallel Processes

A workflow may execute parallel processes.

Example

```text
Project

│

├── Development

└── Documentation
```

Both processes execute independently while sharing the same workflow.

---

# Nested Workflows

Entities may trigger child workflows.

Example

```text
Project

↓

Batch Workflow

↓

Task Workflow

↓

Review Workflow
```

Each workflow maintains its own state history.

---

# Workflow Versioning

Every workflow is version controlled.

Rules:

- Existing instances remain on their original version.
- New instances use the latest published version.
- Historical versions remain immutable.

---

# State History

Every transition creates a history record.

Captured information:

- Previous State
- Current State
- Transition
- User
- Timestamp
- Comments
- Trigger
- Workflow Version

History is immutable.

---

# Workflow Events

Transitions publish domain events.

Examples

- Workflow Started
- State Entered
- State Exited
- Transition Completed
- Process Completed
- Workflow Completed

Modules subscribe to these events.

---

# Automation

States may execute automatic actions.

Examples

- Assign User
- Send Notification
- Create Task
- Trigger AI Analysis
- Generate Document
- Update Metadata
- Invoke External API

---

# SLA Integration

Every state may define:

- Target Duration
- Warning Threshold
- Escalation Threshold

Example

```text
Review

↓

48 Hours

↓

Reminder

↓

72 Hours

↓

Escalation
```

---

# AI Integration

The state machine integrates with AI services.

---

## AI State Recommendation

Suggests:

- Next Best State
- Missing Steps
- Invalid Routing
- Alternative Flow

---

## AI Bottleneck Detection

Identifies:

- Long-running states
- Frequent rework
- Approval delays
- Transition failures

---

## AI Process Optimization

Recommends:

- Workflow simplification
- Additional automation
- SLA improvements
- Resource balancing

---

# Functional Requirements

Administrators shall be able to:

- Create workflows.
- Create processes.
- Create states.
- Configure transitions.
- Publish workflow versions.
- Configure permissions.
- Configure automation.

Users shall be able to:

- View current state.
- Execute valid transitions.
- View workflow history.
- Track process progress.

---

# Database Entities

Primary entities include:

- WorkflowDefinition
- WorkflowVersion
- WorkflowProcess
- WorkflowState
- WorkflowTransition
- WorkflowTransitionRule
- WorkflowInstance
- WorkflowStateHistory
- WorkflowEvent
- WorkflowAutomationRule

---

# APIs

Representative endpoints

```http
GET    /api/workflows

GET    /api/workflows/{id}

GET    /api/workflows/{id}/processes

GET    /api/processes/{id}/states

POST   /api/workflows

POST   /api/workflows/{id}/publish

POST   /api/workflowinstances/{id}/transition

GET    /api/workflowinstances/{id}/history
```

---

# Reporting

Available reports

- Workflow Progress
- Process Duration
- State Duration
- Transition Frequency
- Workflow Completion Rate
- SLA Compliance
- Rework Statistics
- Bottleneck Analysis
- Workflow Version Usage

---

# Security

Supports:

- Role-Based Access Control
- Transition-Level Permissions
- Process Visibility Rules
- State-Level Authorization
- Immutable Audit History
- Tenant Isolation

---

# Performance Requirements

- State transition validation < 100 ms
- Transition execution < 500 ms
- Workflow lookup < 200 ms
- History retrieval < 2 seconds
- Support millions of workflow instances
- Horizontal scalability

---

# Alternatives Considered

## Single Status Field

Rejected because:

- No hierarchy
- No validation
- No versioning
- Poor reporting
- Hardcoded logic

---

## Process Without States

Rejected because:

- Insufficient lifecycle detail
- Difficult automation
- Limited traceability

---

## Third-Party BPM Engine

Rejected because:

- Increased operational complexity
- Licensing costs
- Limited customization
- External dependency

---

# Consequences

## Positive

- Clear separation of workflow, process, and state.
- Highly configurable workflows.
- Strong auditability.
- Simplified reporting.
- AI-ready process optimization.
- Easy future expansion.

## Negative

- More metadata to manage.
- Higher initial implementation effort.
- Requires governance for workflow design.

---

# Future Evolution

The Workflow Process & State architecture is designed to support:

- BPMN 2.0 compatibility
- Visual Process Designer
- Dynamic Rule Engine
- Event Sourcing
- Parallel State Machines
- Long-Running Processes (Saga Pattern)
- Human-in-the-Loop AI Workflows
- Cross-Tenant Workflow Templates
- Process Mining
- Digital Twin Simulation

---

# Decision Summary

The platform adopts a **hierarchical Workflow → Process → State architecture** executed through a centralized **State Machine Engine**. Every lifecycle change is managed through configurable transitions, ensuring consistency, auditability, extensibility, and support for complex enterprise workflows while remaining fully compatible with AI-driven optimization and future distributed architectures.
