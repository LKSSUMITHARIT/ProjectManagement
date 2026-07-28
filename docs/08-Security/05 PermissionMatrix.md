# Permission Matrix

**Document Version:** 1.0  
**Module:** Permission Matrix  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Solution Architects, Security Architects, Administrators, Backend Developers, AI Agents

---

# Purpose

This document defines the standard permission matrix for the Project & Asset Management Platform.

The matrix maps **Roles → Permissions → Modules → Actions** to ensure consistent authorization across the platform.

This document complements:

- Authentication.md
- Authorization.md
- Roles.md

---

# Authorization Model

The platform follows

```text
User

↓

Role(s)

↓

Permission(s)

↓

Policy

↓

Resource

↓

Action
```

Permissions are always evaluated before executing business logic.

---

# Permission Naming Convention

Permissions follow the convention

```text
Module.Action
```

Examples

```text
Project.Read

Task.Assign

Review.Approve

Asset.Upload

Workflow.Execute

Report.Export
```

---

# Standard Actions

Most modules support one or more of the following actions.

| Action | Description |
|----------|-------------|
| Read | View data |
| Create | Create new record |
| Update | Modify record |
| Delete | Remove record |
| Approve | Approve workflow |
| Reject | Reject workflow |
| Assign | Assign resources/tasks |
| Upload | Upload files |
| Download | Download files |
| Export | Export data |
| Import | Import data |
| Execute | Execute workflow/process |
| Archive | Archive record |
| Restore | Restore archived record |
| Manage | Administrative management |

---

# Module Permission Matrix

## Client Management

| Permission | Description |
|------------|-------------|
| Client.Read | View clients |
| Client.Create | Create client |
| Client.Update | Edit client |
| Client.Delete | Delete client |
| Client.Archive | Archive client |

---

## Project Management

| Permission | Description |
|------------|-------------|
| Project.Read | View projects |
| Project.Create | Create project |
| Project.Update | Update project |
| Project.Delete | Delete project |
| Project.Archive | Archive project |
| Project.Restore | Restore project |

---

## Batch Management

| Permission | Description |
|------------|-------------|
| Batch.Read | View batches |
| Batch.Create | Create batch |
| Batch.Update | Update batch |
| Batch.Delete | Delete batch |
| Batch.Close | Close batch |
| Batch.Reopen | Reopen batch |

---

## Task Management

| Permission | Description |
|------------|-------------|
| Task.Read | View tasks |
| Task.Create | Create task |
| Task.Update | Update task |
| Task.Delete | Delete task |
| Task.Assign | Assign task |
| Task.Complete | Complete task |
| Task.Reopen | Reopen task |

---

## Asset Management

| Permission | Description |
|------------|-------------|
| Asset.Read | View assets |
| Asset.Upload | Upload asset |
| Asset.Update | Update asset |
| Asset.Delete | Delete asset |
| Asset.Download | Download asset |
| Asset.Lock | Lock asset |
| Asset.Unlock | Unlock asset |
| Asset.Version.Create | Create asset version |
| Asset.Version.Read | View versions |

---

## Review Management

| Permission | Description |
|------------|-------------|
| Review.Read | View reviews |
| Review.Create | Create review |
| Review.Update | Update review |
| Review.Delete | Delete review |
| Review.Approve | Approve review |
| Review.Reject | Reject review |
| Review.Comment | Add comments |

---

## Workflow Engine

| Permission | Description |
|------------|-------------|
| Workflow.Read | View workflow |
| Workflow.Execute | Execute workflow |
| Workflow.Update | Update workflow |
| Workflow.Cancel | Cancel workflow |
| Workflow.Restart | Restart workflow |

---

## Resource Management

| Permission | Description |
|------------|-------------|
| Resource.Read | View resources |
| Resource.Create | Create resource |
| Resource.Update | Update resource |
| Resource.Delete | Delete resource |
| Resource.Assign | Allocate resource |

---

## Team Management

| Permission | Description |
|------------|-------------|
| Team.Read | View teams |
| Team.Create | Create team |
| Team.Update | Update team |
| Team.Delete | Delete team |

---

## Communication

| Permission | Description |
|------------|-------------|
| Communication.Read | View conversations |
| Communication.Create | Send messages |
| Communication.Delete | Delete messages |

---

## Notification

| Permission | Description |
|------------|-------------|
| Notification.Read | View notifications |
| Notification.Manage | Configure notifications |

---

## Finance

| Permission | Description |
|------------|-------------|
| Finance.Read | View finance |
| Finance.Create | Create financial records |
| Finance.Update | Update financial records |
| Finance.Delete | Delete financial records |
| Finance.Approve | Approve invoices |
| Finance.Export | Export financial reports |

---

## Reporting

| Permission | Description |
|------------|-------------|
| Report.Read | View reports |
| Report.Export | Export reports |
| Dashboard.Read | View dashboards |

---

## Source Control

| Permission | Description |
|------------|-------------|
| SourceControl.Read | View repositories |
| SourceControl.Manage | Manage repositories |
| SourceControl.Sync | Synchronize repositories |
| SourceControl.Merge | Merge pull requests |

---

## Administration

| Permission | Description |
|------------|-------------|
| User.Manage | Manage users |
| Role.Manage | Manage roles |
| Permission.Manage | Manage permissions |
| Tenant.Manage | Manage tenant |
| System.Configure | Configure system |

---

# Default Role Permission Matrix

Legend

| Symbol | Meaning |
|---------|---------|
| ✔ | Allowed |
| ◐ | Limited / Own Records Only |
| ✖ | Not Allowed |

---

## Core Modules

| Module | Sys Admin | Tenant Admin | PM | Lead | Developer | Reviewer | Client | Auditor |
|---------|:---------:|:------------:|:--:|:----:|:---------:|:--------:|:------:|:-------:|
| Clients | ✔ | ✔ | ✔ | ✔ | ✖ | ✖ | Read | Read |
| Projects | ✔ | ✔ | ✔ | Read | Read | Read | Read | Read |
| Batches | ✔ | ✔ | ✔ | ✔ | Read | Read | Read | Read |
| Tasks | ✔ | ✔ | ✔ | ✔ | ◐ | Read | Read | Read |
| Assets | ✔ | ✔ | ✔ | ✔ | ◐ | ✔ | Download | Read |
| Reviews | ✔ | ✔ | Read | ✔ | Respond | ✔ | Read | Read |
| Workflow | ✔ | ✔ | ✔ | Execute | Read | Read | ✖ | Read |
| Resources | ✔ | ✔ | ✔ | Read | ✖ | ✖ | ✖ | Read |
| Teams | ✔ | ✔ | Read | ✔ | Read | Read | ✖ | Read |

---

## Administration

| Module | Sys Admin | Tenant Admin | PM | Developer | Client |
|---------|:---------:|:------------:|:--:|:---------:|:------:|
| Users | ✔ | ✔ | ✖ | ✖ | ✖ |
| Roles | ✔ | Limited | ✖ | ✖ | ✖ |
| Permissions | ✔ | ✖ | ✖ | ✖ | ✖ |
| Tenant Settings | ✔ | ✔ | ✖ | ✖ | ✖ |
| Security Settings | ✔ | Limited | ✖ | ✖ | ✖ |

---

## Finance

| Module | Finance Manager | PM | Lead | Developer | Client |
|---------|:---------------:|:--:|:----:|:---------:|:------:|
| Budgets | ✔ | Read | ✖ | ✖ | ✖ |
| Revenue | ✔ | Read | ✖ | ✖ | ✖ |
| Invoices | ✔ | Read | ✖ | ✖ | ✖ |
| Export | ✔ | Limited | ✖ | ✖ | ✖ |

---

# AI Agent Permissions

AI Agents use dedicated service identities.

Example permissions

| AI Agent | Permissions |
|----------|-------------|
| Requirement Agent | Requirement.Generate, Project.Read |
| Documentation Agent | Documentation.Generate, Project.Read |
| Review Agent | Review.Generate, Asset.Read |
| Workflow Agent | Workflow.Analyze, Workflow.Read |
| Reporting Agent | Report.Generate, Dashboard.Read |

AI Agents never receive:

```text
User.Manage

Role.Manage

Permission.Manage

System.Configure
```

unless explicitly required and approved.

---

# Permission Evaluation Order

```text
Authenticated User

↓

Tenant Validation

↓

Role Resolution

↓

Permission Resolution

↓

Policy Evaluation

↓

Resource Ownership

↓

Access Granted / Denied
```

---

# Permission Inheritance

Permissions are cumulative.

Example

```text
Developer

+

Reviewer

↓

Developer Permissions

+

Reviewer Permissions
```

---

# Custom Permissions

Tenants may create additional permissions.

Requirements

- Follow naming convention
- Belong to a module
- Document purpose
- Be auditable

Example

```text
Asset.Publish

Task.Estimate

Project.Clone
```

---

# Administrative Rules

Only **System Administrators** may:

- Manage global permissions
- Create system roles
- Modify platform configuration
- Manage security policies

Tenant Administrators are restricted to their own tenant.

---

# Auditing

The following actions are audited:

- Permission Granted
- Permission Revoked
- Role Assignment
- Role Removal
- Permission Changes
- Administrative Overrides

---

# Development Guidelines

Developers should

- Check permissions, not role names
- Use centralized authorization services
- Keep permissions granular
- Deny access by default
- Audit privileged operations

---

# AI Development Guidelines

AI-generated code must

- Validate permissions before business logic
- Support multiple roles
- Respect tenant boundaries
- Avoid hardcoded role checks
- Log authorization failures

AI must never

- Bypass permission checks
- Assume administrators always have unrestricted access to tenant data
- Trust client-side permission information
- Grant implicit permissions

---

# Permission Matrix Checklist

Before deployment verify:

- ✓ All modules define permissions
- ✓ Permission naming follows standards
- ✓ Default roles configured
- ✓ Administrative permissions reviewed
- ✓ AI service permissions restricted
- ✓ Tenant isolation validated
- ✓ Authorization policies tested
- ✓ Permission changes audited

---

# Future Enhancements

Planned capabilities include:

- Attribute-Based Access Control (ABAC)
- Dynamic Permission Policies
- Time-Limited Permissions
- Delegated Permissions
- Risk-Based Authorization
- AI Permission Recommendations
- Fine-Grained Data Masking
- Conditional Access Rules

---

# Summary

The Project & Asset Management Platform uses a standardized permission matrix built on Role-Based Access Control (RBAC). Permissions are organized by module and action, evaluated through centralized authorization services, and enforced after authentication and tenant validation. The matrix provides a consistent, auditable, and extensible foundation for securing users, administrators, APIs, background services, and AI agents across the platform.
