# Workflow Permission

> **Purpose**
>
> Workflow Permissions determine **who can perform what action at each stage of the workflow**.
>
> They provide fine-grained authorization beyond standard Role-Based Access Control (RBAC) by considering the current Workflow, Process, State, Transition, User Role, and ownership of the Task.
>
> Workflow Permissions ensure that only authorized users can execute business actions while maintaining complete auditability.

---

# Overview

Every Workflow Action is protected by a Permission Policy.

The Workflow Engine validates permissions before executing any Transition.

```text
User

↓

Workflow Action

↓

Permission Validation

↓

Allowed ?

↓

YES → Execute

NO → Reject
```

---

# Objectives

Workflow Permissions provide:

- Secure workflow execution
- Role-based authorization
- Ownership validation
- Department segregation
- Review integrity
- Audit compliance

---

# Permission Hierarchy

Permissions are evaluated using multiple levels.

```text
System

↓

Role

↓

Workflow

↓

Process

↓

State

↓

Transition

↓

Business Rules
```

The most restrictive permission always wins.

---

# Permission Sources

Permissions may be granted by:

- System Role
- Project Role
- Team Membership
- Workflow Configuration
- Assignment
- Ownership
- Special Privileges

---

# Permission Evaluation

The engine validates permissions in the following order.

```text
User

↓

Account Active

↓

Role Validation

↓

Project Access

↓

Workflow Access

↓

Process Permission

↓

State Permission

↓

Transition Permission

↓

Business Rule

↓

Execute
```

---

# Standard Roles

The platform supports the following default roles.

| Role | Description |
|------|-------------|
| System Administrator | Full access |
| Delivery Manager | Portfolio management |
| Project Manager | Project ownership |
| Team Lead | Production management |
| Artist | Production execution |
| Reviewer | Final Review |
| QC Engineer | Quality Control |
| Client | Client Review |
| Viewer | Read-only |

---

# Permission Scope

Permissions may apply at different scopes.

| Scope | Description |
|------|-------------|
| Global | Entire System |
| Project | Single Project |
| Batch | Single Batch |
| Asset | Single Asset |
| Task | Single Task |
| Workflow | Workflow Instance |
| Review | Review Session |

---

# Ownership Rules

Certain actions require ownership.

Example

```text
Artist

↓

Assigned SubTask

↓

Allowed

Update Progress

Upload Deliverables

Log Time
```

Another Artist cannot perform these actions.

---

# Lead Permissions

Team Leads may:

- Create Tasks
- Create SubTasks
- Assign Artists
- Request Reviews
- Reopen SubTasks
- Close Tasks
- Merge Deliverables
- View Team Workload

---

# Project Manager Permissions

Project Managers may:

- Configure Workflow
- Create Batch
- Assign Leads
- View Reports
- Reassign Tasks
- Override Workflow
- Close Batch
- Close Asset

---

# Reviewer Permissions

Reviewers may:

- Review Deliverables
- Add Feedback
- Approve
- Reject
- Minor Fix
- Major Fix

Reviewers cannot:

- Create SubTasks
- Assign Artists
- Edit Production Data

---

# QC Permissions

QC Engineers may:

- Review Deliverables
- Record QC Result
- Request Fix
- Approve QC

QC does not create Review Rounds.

---

# Client Permissions

Clients may:

- Review Deliverables
- Add Feedback
- Approve
- Minor Fix
- Major Fix

Clients cannot:

- Edit Tasks
- Create SubTasks
- View Internal Notes
- View Internal Discussions

---

# Transition Permissions

Example

| Transition | Allowed Roles |
|------------|---------------|
| Start Work | Artist |
| Submit WIP Review | Artist |
| Approve WIP | Team Lead |
| Submit Lead Review | Team Lead |
| Final Review | Reviewer |
| QC Approval | QC |
| Client Review | Client |
| Close Task | Team Lead |

---

# State Permissions

Permissions may change depending on State.

Example

State

```text
Production/In Progress
```

Allowed

- Upload Files
- Log Time
- Update Progress

Not Allowed

- Final Approval

---

State

```text
Final Review/Reviewing
```

Allowed

- Review
- Feedback
- Approve

Not Allowed

- Edit Deliverables

---

# Administrative Override

Administrators may override permissions.

Every override must:

- Require Reason
- Be Logged
- Be Audited

---

# Delegation

Future versions may allow temporary delegation.

Example

```text
Lead

↓

Vacation

↓

Delegate Review

↓

Another Lead
```

---

# Permission Matrix

Example

| Action | Artist | Lead | PM | Reviewer | QC | Client |
|---------|:------:|:----:|:--:|:--------:|:--:|:------:|
| Create Task | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ |
| Create SubTask | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ |
| Upload Deliverable | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Submit Review | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Approve FR | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| Approve QC | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ |
| Client Approval | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Close Task | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ |

---

# Permission Caching

To improve performance:

- Role Permissions cached
- Workflow Permissions cached
- State Permissions cached
- User Effective Permissions cached

Cache invalidates on:

- Role changes
- Workflow changes
- Assignment changes

---

# Audit Requirements

Every permission check should record:

- User
- Action
- Workflow
- Process
- State
- Result
- Timestamp
- IP Address
- Device

Permission failures should also be logged.

---

# Business Rules

## BR-001

Permissions must be validated before every Workflow Transition.

---

## BR-002

Permission validation occurs before Business Rule validation.

---

## BR-003

Only assigned Artists may update their SubTasks.

---

## BR-004

Only Team Leads or Project Managers may create SubTasks.

---

## BR-005

Reviewers cannot modify production data.

---

## BR-006

Clients cannot view internal communication.

---

## BR-007

Administrative overrides require justification and audit.

---

## BR-008

Permission rules are versioned with the Workflow.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| PermissionId | Primary Key |
| WorkflowId | Workflow |
| ProcessId | Process |
| StateId | State |
| TransitionId | Transition |
| RoleId | Role |
| Action | Permission |
| Allow | Boolean |
| RequiresOwnership | Boolean |
| RequiresAssignment | Boolean |

---

# Reporting

Typical reports include:

- Permission Audit
- Unauthorized Access Attempts
- Override History
- Reviewer Activity
- Workflow Security Report

---

# Future Enhancements

Future releases may include:

- Attribute-Based Access Control (ABAC)
- Dynamic Permissions
- Temporary Delegation
- Approval Matrix Builder
- AI Permission Suggestions
- Multi-Tenant Permission Templates

---

# Design Principles

The Workflow Permission module follows these principles:

- Permissions are evaluated before business logic.
- Permissions are configuration-driven.
- Ownership is enforced where applicable.
- Every decision is auditable.
- Workflow permissions extend, but do not replace, RBAC.
- Security should never be hard-coded into workflow transitions.

---

# Related Documents

- Workflow.md
- WorkflowTransition.md
- WorkflowRule.md
- WorkflowValidation.md
- Security/RBAC.md
- RolesAndResponsibilities.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow Permission specification |
