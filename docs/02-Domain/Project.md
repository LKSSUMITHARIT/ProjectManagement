# Project Domain

> **Purpose**
>
> The Project domain is the central business entity of the Project Management Platform. It represents a contractual engagement between the organization and a Client, defining the scope of work, production team, financial information, workflows, deliverables, and operational execution.
>
> Every production activity, invoice, deliverable, resource allocation, and workflow execution ultimately belongs to a Project.

---

# Overview

A Project is created for a specific Client and serves as the root entity for all production activities.

It contains everything required to successfully deliver work, including:

- Project Information
- Project Team
- Production Batches
- Software Requirements
- Financial Information
- Deliverables
- Communication
- Reports
- Activity History

---

# Business Hierarchy

```text
Client
    │
    ▼
Project
│
├── Team
├── Software Requirements
├── Batches
│     ├── Assets
│     ├── Tasks
│     └── Deliverables
│
├── Finance
├── Communication
├── Documents
└── Activity Timeline
```

---

# Objectives

The Project module enables organizations to:

- Manage production work
- Organize batches
- Assign project teams
- Track financial performance
- Monitor production progress
- Manage software licensing
- Track deliverables
- Generate invoices
- Maintain complete audit history

---

# Business Ownership

| Property | Value |
|----------|-------|
| Domain Owner | Project Management Office (PMO) |
| Operational Owner | Project Manager |
| Financial Owner | Finance Department |
| Production Owner | Production Head |

---

# Project Information

## Basic Information

Typical information includes:

- Project Name
- Display Name
- Project Code
- Client
- Parent Project (Future)
- Description
- Business Unit
- Category
- Priority
- Status

---

## Timeline

The Project maintains important planning dates.

Examples:

- Start Date
- Planned End Date
- Actual Start Date
- Actual Completion Date
- Contract End Date

---

## Commercial Information

The Project stores commercial metadata such as:

- Purchase Order Number
- Contract Reference
- Currency
- Billing Model
- Billing Frequency
- Project Value
- Tax Information

> Actual invoices are maintained in the Finance module.

---

# Project Team

Each Project maintains its own team.

Typical roles include:

- Project Manager
- Batch Managers
- Team Leads
- Resource Manager
- Artists
- Reviewers
- QC Engineers
- Finance Representative

A user may participate in multiple Projects.

---

# Project Team Hierarchy

```text
Project Manager
        │
 ┌──────┴────────┐
 │               │
 ▼               ▼
Batch Manager  Resource Manager
       │
       ▼
Team Lead
       │
       ▼
Artists
```

---

# Software Requirements

Each Project maintains a list of software required for production.

Examples:

- Autodesk Maya
- Blender
- Photoshop
- Unreal Engine
- Unity
- Substance Painter
- Houdini

---

## Purpose

This list is used by the Resource Allocation system.

Only Artists allocated to the Project (through Batches) should be granted access to the required software according to organizational licensing and infrastructure policies.

Future integrations may automate software entitlement based on these requirements.

---

# Production Structure

Projects are divided into one or more Batches.

```text
Project

↓

Batch A

Batch B

Batch C
```

Each Batch represents an independent production unit.

---

# Financial Relationship

The financial hierarchy is:

```text
Client
      │
      ▼
Project
      │
      ▼
Invoices
      │
      ▼
Payments
```

Important Business Rule:

> Every Invoice belongs to a Project.

The Client receives the Invoice because the Project belongs to that Client.

---

# Financial Summary

The Project displays aggregated financial information.

Examples:

- Project Value
- Total Invoiced
- Amount Received
- Outstanding Amount
- Discounts
- Waivers
- Revenue
- Profit Margin
- Billing Progress

These values are derived from Finance transactions.

---

# Communication

Each Project contains its own communication space.

Supported features:

- Discussions
- Rich Text Messages
- Mentions
- Attachments
- Announcements
- Activity Timeline

Project communication is independent of Batch, Asset, or Task discussions.

---

# Documents

Typical project-level documents include:

- Scope Documents
- Contracts
- Statement of Work (SOW)
- Project Plans
- Production Guidelines
- Reference Material
- Design Documents

These documents are administrative and are separate from production deliverables.

---

# Deliverables

Project deliverables are generated from completed production Tasks.

The platform stores metadata about each deliverable, including:

- Repository
- File Path
- Version
- Changeset / Commit
- Uploaded By
- Delivery Date

Actual production files remain in the organization's source control system.

---

# Dashboard

The Project Dashboard provides a consolidated view of project health.

Typical widgets include:

- Overall Progress
- Batch Progress
- Resource Utilization
- Open Tasks
- Review Status
- Financial Summary
- Delivery Timeline
- Recent Activity
- Pending Reviews
- Upcoming Milestones

---

# Activity Timeline

Every important action is recorded.

Examples:

- Project Created
- Team Updated
- Batch Created
- Software Added
- Invoice Generated
- Payment Recorded
- Deliverable Submitted
- Workflow Modified
- Project Closed

---

# Business Rules

## BR-001

Every Project must belong to exactly one Client.

---

## BR-002

A Project must have one Project Manager.

---

## BR-003

A Project may contain multiple Batches.

---

## BR-004

A Batch cannot exist without a Project.

---

## BR-005

Invoices are generated against Projects.

---

## BR-006

Financial summaries are calculated from invoice and payment records.

---

## BR-007

Software requirements are maintained at the Project level and inherited by production planning. Batch-level restrictions or overrides may be introduced in future releases if required.

---

## BR-008

Project communication is independent from Batch, Asset, and Task communication.

---

## BR-009

A Project cannot be closed until:

- All Batches are closed
- Financial closure requirements are satisfied according to business policy
- Outstanding approvals are completed

---

## BR-010

Deleting a Project is not permitted after production has begun.

Projects should instead be archived.

---

# Lifecycle

```text
Draft
    │
Planning
    │
Active
    │
On Hold
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
| Draft | Initial project creation |
| Planning | Project setup in progress |
| Active | Production has started |
| On Hold | Work temporarily suspended |
| Completed | Production completed |
| Closed | Financial and operational closure completed |
| Archived | Historical reference only |

---

# Permissions

Typical permissions include:

| Permission | Description |
|------------|-------------|
| View Project | View project details |
| Create Project | Create new projects |
| Edit Project | Modify project information |
| Archive Project | Archive completed projects |
| Manage Team | Add or remove project members |
| Manage Software | Maintain required software |
| View Finance | View project financial summary |
| Generate Invoice | Create project invoices |
| Manage Communication | Project discussions |
| View Reports | Access project dashboards |

---

# Reporting

Typical Project reports include:

- Project Dashboard
- Project Status Report
- Production Progress
- Resource Utilization
- Batch Summary
- Delivery Schedule
- Financial Summary
- Revenue Report
- Outstanding Invoice Report
- Project Profitability
- Software Usage
- Project Timeline

---

# Future Enhancements

Planned capabilities include:

- Project Templates
- Project Cloning
- Multi-Phase Projects
- Portfolio Management
- Budget vs Actual Tracking
- Risk Register
- Issue Register
- Change Request Management
- Project Health Score
- AI Project Assistant
- Predictive Delivery Forecasting
- Automated Project Scheduling

---

# Related Documents

- Client.md
- Batch.md
- Finance.md
- ResourceAllocation.md
- CommunicationModel.md
- DeliverableManagement.md
- BusinessLifecycle.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Project domain specification |
