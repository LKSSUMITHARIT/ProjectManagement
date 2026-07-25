# User Personas

> **Purpose**
>
> This document defines the primary users of the Project Management Platform, their responsibilities, goals, permissions, pain points, and how they interact with the system.
>
> These personas guide product design, workflow decisions, UI/UX, authorization, reporting, and future AI capabilities.

---

# Overview

The platform is designed for organizations that manage production-oriented projects involving multiple departments, specialized roles, and structured review processes.

Users interact with the platform according to their responsibilities within the production lifecycle.

The personas defined here represent the primary users expected during **Phase 1**, along with users planned for future releases.

---

# User Hierarchy

```text
Organization
│
├── System Administrator
├── Management
│   ├── Delivery Head
│   ├── Production Head
│   ├── Resource Manager
│   └── Finance Manager
│
├── Project Team
│   ├── Project Manager
│   ├── Batch Manager
│   ├── Team Lead
│   ├── Reviewer
│   ├── QC
│   └── Artist
│
├── Finance Team
│
└── Client (Future)
```

---

# Persona Overview

| Persona | Primary Responsibility | Phase |
|----------|------------------------|-------|
| System Administrator | Platform Configuration | Phase 1 |
| Delivery Head | Business Oversight | Phase 1 |
| Production Head | Production Oversight | Phase 1 |
| Resource Manager | Resource Planning | Phase 1 |
| Project Manager | Project Delivery | Phase 1 |
| Batch Manager | Batch Execution | Phase 1 |
| Team Lead | Task Planning & Reviews | Phase 1 |
| Artist | Production Work | Phase 1 |
| Reviewer | Internal Reviews | Phase 1 |
| QC Engineer | Quality Validation | Phase 1 |
| Finance Executive | Billing & Payments | Phase 1 |
| Client | External Reviews | Future |
| Vendor | Outsourced Production | Future |

---

# 1. System Administrator

## Purpose

Manages the platform configuration and system administration.

## Responsibilities

- User Management
- Roles & Permissions
- Workflow Configuration
- Process Configuration
- State Configuration
- Master Data
- Business Rules
- System Settings

## Goals

- Maintain platform integrity
- Configure workflows
- Manage security
- Support business users

## Primary Modules

- Administration
- User Management
- Workflow
- Security
- Audit

---

# 2. Delivery Head

## Purpose

Monitors overall business delivery across all projects.

## Responsibilities

- Project Portfolio
- Revenue Tracking
- Delivery Performance
- Risk Monitoring
- Executive Reporting

## Goals

- Deliver projects on time
- Improve profitability
- Reduce delivery risks

## Primary Modules

- Dashboard
- Reports
- Finance
- Projects

---

# 3. Production Head

## Purpose

Oversees production execution across all departments.

## Responsibilities

- Production Monitoring
- Team Performance
- Review Efficiency
- Workflow Compliance
- Production KPIs

## Goals

- Maximize throughput
- Improve quality
- Optimize production

## Primary Modules

- Batch
- Assets
- Tasks
- Reports

---

# 4. Resource Manager

## Purpose

Plans and approves resource allocation across batches.

## Responsibilities

- Allocation Requests
- Capacity Planning
- Utilization
- Team Balancing
- Workload Monitoring

## Goals

- Prevent overallocation
- Improve utilization
- Balance workload

## Primary Modules

- Resource Allocation
- Batch
- Reports

---

# 5. Project Manager

## Purpose

Owns the successful delivery of a project.

## Responsibilities

- Project Planning
- Batch Creation
- Team Assignment
- Project Communication
- Delivery Schedule
- Client Coordination
- Project Billing

## Goals

- Deliver projects successfully
- Maintain client satisfaction
- Monitor project health

## Primary Modules

- Client
- Project
- Batch
- Communication
- Dashboard

---

# 6. Batch Manager

## Purpose

Manages day-to-day execution of a production batch.

## Responsibilities

- Batch Planning
- Resource Requests
- Asset Planning
- Progress Monitoring
- Delivery Coordination

## Goals

- Deliver batches on schedule
- Coordinate production teams
- Resolve production bottlenecks

## Primary Modules

- Batch
- Resource Allocation
- Assets
- Dashboard

---

# 7. Team Lead

## Purpose

Plans production work and manages execution at the task level.

## Responsibilities

- Create Tasks
- Create Subtasks
- Assign Artists
- Review Work
- Convert Review Feedback into Subtasks
- Monitor Progress
- Approve Production Work

## Goals

- Ensure production quality
- Distribute work effectively
- Complete tasks efficiently

## Primary Modules

- Assets
- Tasks
- Reviews
- Workflow
- Kanban Board

---

# 8. Artist

## Purpose

Executes production work assigned through subtasks.

## Responsibilities

- Work on Assigned Subtasks
- Update Progress
- Upload Deliverables
- Respond to Feedback
- Participate in Reviews

## Goals

- Complete assigned work
- Meet quality standards
- Deliver on schedule

## Primary Modules

- My Work
- Tasks
- Subtasks
- Deliverables
- Communication

---

# 9. Reviewer

## Purpose

Performs production reviews before work progresses.

## Responsibilities

- Review Deliverables
- Provide Feedback
- Approve Work
- Request Minor Fix
- Request Major Fix

## Important Note

Reviewers provide **feedback only**.

They do **not** create subtasks.

Subtasks are created by the Team Lead or Project Manager.

## Primary Modules

- Review
- Task
- Deliverables

---

# 10. QC Engineer

## Purpose

Validates production quality before client delivery.

## Responsibilities

- Verify Deliverables
- Identify Issues
- Approve QC
- Return Work to Production

## Goals

- Improve quality
- Reduce client defects

## Primary Modules

- QC Review
- Deliverables
- Tasks

---

# 11. Finance Executive

## Purpose

Manages project billing and payment tracking.

## Responsibilities

- Generate Invoices
- Record Payments
- Apply Discounts
- Apply Waivers
- Track Outstanding Balances

## Goals

- Maintain accurate financial records
- Track receivables
- Support financial reporting

## Primary Modules

- Finance
- Clients
- Projects
- Reports

---

# Future Personas

## Client

The Client Portal will allow external customers to:

- View Project Progress
- Review Deliverables
- Approve Work
- Request Changes
- Download Deliverables
- Participate in Discussions

---

## Vendor

Future vendor support will include:

- Assigned Production Work
- Deliverables
- Reviews
- Communication

---

# Common User Capabilities

Most authenticated users can:

- View dashboards (role-dependent)
- Search entities
- Upload attachments
- Participate in discussions
- View activity history
- Receive notifications

Permissions determine which actions are available.

---

# AI Personas (Future)

The platform is designed to introduce AI assistants that collaborate with human users.

Planned AI personas include:

| AI Persona | Purpose |
|------------|---------|
| AI Project Manager | Project planning and monitoring |
| AI Resource Planner | Capacity and allocation optimization |
| AI Review Assistant | Automated quality checks |
| AI Reporting Assistant | Report generation and insights |
| AI Knowledge Assistant | Context-aware help and documentation |
| AI Production Analyst | Production analytics and forecasting |

These AI assistants will augment user workflows rather than replace business ownership or approvals.

---

# Persona-to-Module Matrix

| Module | Admin | Delivery | Production | Resource | PM | Batch | Lead | Artist | Reviewer | QC | Finance |
|---------|:----:|:--------:|:----------:|:--------:|:--:|:-----:|:----:|:------:|:--------:|:--:|:-------:|
| Client | ✓ | ✓ | | | ✓ | | | | | | ✓ |
| Project | ✓ | ✓ | ✓ | | ✓ | | | | | | ✓ |
| Batch | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | | | | |
| Resource | | | | ✓ | ✓ | ✓ | | | | | |
| Asset | | | ✓ | | | ✓ | ✓ | ✓ | | | |
| Task | | | ✓ | | | ✓ | ✓ | ✓ | ✓ | ✓ | |
| Workflow | ✓ | | | | | | | | | | |
| Reviews | | | ✓ | | | | ✓ | | ✓ | ✓ | |
| Deliverables | | | | | | | ✓ | ✓ | ✓ | ✓ | |
| Finance | | ✓ | | | ✓ | | | | | | ✓ |
| Reports | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | | | | ✓ |

---

# Design Considerations

The platform should be designed so that:

- Every user sees information relevant to their role.
- Navigation is role-oriented rather than module-oriented where appropriate.
- Dashboards are personalized.
- Permissions are enforced consistently.
- Users interact only with entities within their scope of responsibility.
- AI assistants provide recommendations without bypassing business approvals.

---

# Related Documents

- ProductOverview.md
- ProductHierarchy.md
- ProductModules.md
- TargetAudience.md
- 08-Security/RolesAndPermissions.md *(planned)*
- 03-Modules/*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial User Personas documentation |
