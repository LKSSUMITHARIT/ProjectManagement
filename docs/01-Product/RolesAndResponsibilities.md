# Roles and Responsibilities

> **Purpose**
>
> This document defines the organizational roles within the Project Management Platform, their responsibilities, decision-making authority, ownership boundaries, and interactions throughout the production lifecycle.
>
> While **User Personas** describe *who uses the system*, this document defines *what each role is responsible for* and *what authority they possess*.

---

# Overview

The Project Management Platform follows a responsibility-driven operating model where every production activity has a clearly defined owner.

The objective is to ensure:

- Clear ownership
- Accountability
- Controlled approvals
- Better collaboration
- Complete traceability
- Separation of responsibilities

---

# Organizational Structure

```text
Executive Management
        │
        ▼
Delivery Head
        │
 ┌──────┴────────┐
 │               │
 ▼               ▼
Production    Finance
Head          Manager
 │
 ▼
Project Manager
 │
 ▼
Batch Manager
 │
 ▼
Team Lead
 │
 ▼
Artist

Supporting Roles

• Resource Manager
• Reviewer
• QC Engineer
• System Administrator
```

---

# Responsibility Matrix

| Role | Primary Responsibility | Decision Authority |
|------|------------------------|--------------------|
| System Administrator | Platform Configuration | System Configuration |
| Delivery Head | Portfolio Delivery | Strategic |
| Production Head | Production Operations | Operational |
| Project Manager | Project Delivery | Project |
| Batch Manager | Batch Execution | Batch |
| Team Lead | Task Planning | Task |
| Artist | Production Work | Assigned Work |
| Reviewer | Quality Review | Review Outcome |
| QC Engineer | Quality Validation | QC Approval |
| Resource Manager | Resource Allocation | Allocation Approval |
| Finance Executive | Billing & Payments | Financial Processing |

---

# 1. System Administrator

## Purpose

Responsible for configuring and maintaining the platform.

## Responsibilities

- Manage Users
- Manage Roles
- Configure Permissions
- Configure Workflows
- Configure Processes
- Configure States
- Configure Notifications
- Configure Master Data
- Configure System Settings
- Monitor Audit Logs

## Decision Authority

May configure system behavior but does not participate in production execution.

---

# 2. Delivery Head

## Purpose

Responsible for successful delivery across the organization.

## Responsibilities

- Portfolio Monitoring
- Revenue Monitoring
- Delivery Health
- Strategic Planning
- Executive Reporting
- Escalation Management

## Decision Authority

- Approve strategic decisions
- Resolve project escalations
- Approve delivery changes

---

# 3. Production Head

## Purpose

Responsible for production efficiency and execution.

## Responsibilities

- Production Planning
- Capacity Monitoring
- Review Efficiency
- Team Performance
- Production KPIs
- Delivery Forecasting

## Decision Authority

- Production policy
- Resource prioritization
- Production escalations

---

# 4. Resource Manager

## Purpose

Responsible for resource planning across all projects.

## Responsibilities

- Approve Allocation Requests
- Capacity Planning
- Workload Balancing
- Utilization Monitoring
- Resource Forecasting

## Decision Authority

- Approve or reject allocations
- Adjust resource priorities
- Balance workloads

---

# 5. Project Manager

## Purpose

Owns the complete lifecycle of a project.

## Responsibilities

### Project Planning

- Create Projects
- Define Teams
- Configure Project Settings
- Manage Required Software

### Delivery

- Schedule Deliveries
- Track Progress
- Manage Risks
- Coordinate Clients

### Financial

- Generate Project Invoices
- Monitor Payments
- Track Outstanding Amounts

### Communication

- Client Communication
- Project Discussions
- Status Reporting

## Decision Authority

- Project planning
- Project schedule
- Team assignment
- Project closure

---

# 6. Batch Manager

## Purpose

Responsible for execution of one or more production batches.

## Responsibilities

### Batch Planning

- Create Batch
- Configure Batch Workflow
- Configure Stages
- Manage Batch Team

### Resource Management

- Raise Allocation Requests
- Monitor Allocations
- Track Capacity

### Production

- Monitor Batch Progress
- Resolve Production Issues
- Coordinate Delivery

## Decision Authority

- Batch planning
- Batch schedule
- Resource requests

---

# 7. Team Lead

## Purpose

Owns task planning and production quality.

## Responsibilities

### Planning

- Create Tasks
- Create Subtasks
- Assign Artists

### Production

- Monitor Progress
- Review Work
- Close Tasks

### Reviews

- Perform Lead Review
- Convert Review Feedback into Subtasks
- Manage Review Rounds

### Communication

- Coordinate Artists
- Resolve Technical Questions

## Decision Authority

- Task planning
- Artist assignment
- Task approval
- Subtask creation

---

# 8. Artist

## Purpose

Executes production work.

## Responsibilities

- Work on Assigned Subtasks
- Update Progress
- Upload Deliverables
- Respond to Feedback
- Participate in Reviews

## Restrictions

- Cannot reassign Subtasks
- Cannot approve Reviews
- Cannot close Tasks
- Cannot approve Deliverables

## Decision Authority

Limited to assigned work.

---

# 9. Reviewer

## Purpose

Performs quality reviews during production.

## Responsibilities

- Review Deliverables
- Provide Feedback
- Approve Work
- Request Minor Fix
- Request Major Fix

## Important Responsibilities

The Reviewer **does not create production Subtasks**.

Instead, the Reviewer provides structured feedback.

The Team Lead or Project Manager analyzes the feedback and creates the required production Subtasks.

## Decision Authority

- Review decision
- Feedback quality

---

# 10. QC Engineer

## Purpose

Validates production quality before delivery.

## Responsibilities

- Verify Deliverables
- Validate Standards
- Approve QC
- Reject QC

## Decision Authority

QC Approval

---

# 11. Finance Executive

## Purpose

Responsible for project billing.

## Responsibilities

- Generate Invoices
- Record Payments
- Apply Discounts
- Apply Waivers
- Close Financial Records

## Decision Authority

Financial processing according to organizational policy.

---

# Responsibility Across Business Entities

| Entity | Owner | Supporting Roles |
|---------|-------|------------------|
| Client | Project Manager | Finance |
| Project | Project Manager | Delivery Head |
| Batch | Batch Manager | Team Lead |
| Asset | Team Lead | Artists |
| Task | Team Lead | Reviewer |
| Subtask | Assigned Artist | Team Lead |
| Deliverable | Team Lead | Artist |
| Invoice | Finance | Project Manager |

---

# Approval Responsibilities

## Resource Allocation

```text
Batch Manager
        │
        ▼
Allocation Request
        │
        ▼
Resource Manager
        │
Approve / Reject
```

---

## Task Review

```text
Artist
      │
      ▼
Team Lead
      │
Approve
      │
      ▼
Final Review
```

---

## Final Review

```text
Reviewer
      │
      ├── Approve
      ├── Minor Fix
      └── Major Fix
```

---

## Client Review

```text
Client
      │
      ├── Approve
      ├── Minor Fix
      └── Major Fix
```

---

# Responsibility During Feedback

When feedback is received:

## Reviewer Responsibilities

- Identify issues
- Document feedback
- Classify severity
- Approve or reject work

## Team Lead Responsibilities

- Analyze feedback
- Break work into Subtasks
- Assign Artists
- Track completion

## Artist Responsibilities

- Complete assigned Subtasks
- Upload revised work

This separation ensures that planning remains with the Team Lead while reviewers focus on quality.

---

# RACI Matrix

| Activity | PM | Batch | Lead | Artist | Reviewer | QC | Resource | Finance |
|----------|:--:|:----:|:----:|:------:|:--------:|:--:|:--------:|:-------:|
| Create Project | A/R | | | | | | | |
| Create Batch | A | R | | | | | | |
| Raise Allocation Request | | R | | | | | | |
| Approve Allocation | | | | | | | A/R | |
| Create Asset | | R | A | | | | | |
| Create Task | | | A/R | | | | | |
| Create Subtask | | | A/R | | | | | |
| Execute Subtask | | | | A/R | | | | |
| Lead Review | | | A/R | | | | | |
| Final Review | | | | | A/R | | | |
| QC Review | | | | | | A/R | | |
| Client Review | A | | | | | | | |
| Generate Invoice | A | | | | | | | R |
| Record Payment | | | | | | | | A/R |

**Legend**

- **R** – Responsible (performs the work)
- **A** – Accountable (owns the outcome)
- **C** – Consulted
- **I** – Informed

---

# Guiding Principles

The platform enforces the following principles:

- Every business entity has a clear owner.
- Planning and execution are separate responsibilities.
- Reviewers evaluate quality but do not plan work.
- Subtasks are always created by Leads or Project Managers.
- Resource allocation requires approval.
- Financial activities remain under Finance ownership.
- Workflow approvals are role-based.
- All important actions are audited.

---

# Related Documents

- UserPersonas.md
- ProductHierarchy.md
- ProductModules.md
- 08-Security/RolesAndPermissions.md *(planned)*
- 03-Modules/*
- 04-Workflow/*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Roles and Responsibilities documentation |
