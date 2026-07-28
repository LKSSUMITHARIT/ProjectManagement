# Roles & Permission Model

**Document Version:** 1.0  
**Module:** Roles & Access Management  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Solution Architects, Security Architects, Administrators, Backend Developers, AI Agents

---

# Purpose

This document defines the standard roles used throughout the Project & Asset Management Platform and the permissions assigned to each role.

The platform implements a **Role-Based Access Control (RBAC)** model where users are assigned one or more roles. Each role grants a predefined set of permissions.

Roles are designed to simplify administration while maintaining the principle of **Least Privilege**.

---

# Objectives

The role model should:

- Simplify permission management
- Support enterprise organizations
- Support multiple tenants
- Minimize excessive permissions
- Separate administrative responsibilities
- Enable project-level access
- Support AI service accounts
- Allow future custom roles

---

# RBAC Hierarchy

```text
Tenant

↓

Users

↓

Roles

↓

Permissions

↓

Resources

↓

Actions
```

---

# Role Assignment

A user may have:

- One Role
- Multiple Roles
- Temporary Roles (Future)

Effective permissions are the **union** of all assigned roles.

Example

```text
Developer

+

Reviewer

=

Developer + Reviewer Permissions
```

---

# Standard Roles

The platform provides the following built-in roles.

| Role | Description |
|------|-------------|
| System Administrator | Platform-wide administration |
| Tenant Administrator | Tenant management |
| Security Administrator | Security & identity |
| Project Director | Portfolio management |
| Project Manager | Project execution |
| Delivery Manager | Delivery oversight |
| Team Lead | Team supervision |
| Developer | Task execution |
| Artist / Designer | Creative work |
| QA Engineer | Testing & validation |
| Reviewer | Asset & task reviews |
| Resource Manager | Resource allocation |
| Finance Manager | Financial management |
| Client | Customer access |
| Auditor | Read-only auditing |
| AI Agent | Service identity |
| Guest | Limited access |

---

# System Administrator

Highest privilege role.

Responsibilities

- Platform configuration
- Tenant management
- Security settings
- Global configuration
- Infrastructure settings

Typical permissions

```text
*

(All Permissions)
```

Should be assigned sparingly.

---

# Tenant Administrator

Manages a single tenant.

Responsibilities

- Users
- Roles
- Teams
- Projects
- Configuration

Cannot modify platform-wide settings.

---

# Security Administrator

Responsibilities

- Identity Providers
- MFA
- Password Policies
- Roles
- Permissions
- Authentication

Cannot modify business data unless separately authorized.

---

# Project Director

Responsibilities

- Portfolio oversight
- Client engagement
- Budget approval
- Executive reporting

Permissions include

```text
Project.Read

Project.Update

Report.Read

Finance.Read
```

---

# Project Manager

Responsibilities

- Manage projects
- Assign resources
- Plan schedules
- Track progress

Permissions include

```text
Project.*

Task.*

Batch.*

Workflow.*

Review.Read
```

---

# Delivery Manager

Responsibilities

- Delivery planning
- Resource monitoring
- Milestone tracking
- Release management

---

# Team Lead

Responsibilities

- Team supervision
- Task assignment
- Code reviews
- Asset reviews

Typical permissions

```text
Task.Assign

Task.Update

Review.Approve

Asset.Read
```

---

# Developer

Responsibilities

- Complete assigned work
- Upload deliverables
- Update task status

Permissions include

```text
Task.Read

Task.Update

Asset.Upload

Review.Respond
```

Developers cannot approve their own work unless explicitly allowed by workflow rules.

---

# Artist / Designer

Responsibilities

- Create assets
- Upload versions
- Respond to reviews

Typical permissions

```text
Asset.Read

Asset.Upload

Asset.Update

Review.Read
```

---

# QA Engineer

Responsibilities

- Test features
- Validate deliverables
- Report defects

Typical permissions

```text
Task.Read

Review.Create

Review.Update

Report.Read
```

---

# Reviewer

Responsibilities

- Review submissions
- Approve assets
- Reject assets
- Add comments

Typical permissions

```text
Review.*

Asset.Read

Task.Read
```

---

# Resource Manager

Responsibilities

- Resource planning
- Capacity management
- Team allocation

Permissions

```text
Resource.*

Team.Read

Project.Read
```

---

# Finance Manager

Responsibilities

- Budgets
- Cost tracking
- Revenue
- Invoices
- Financial reporting

Permissions

```text
Finance.*

Report.Export

Project.Read
```

---

# Client

Clients receive limited access.

Typical permissions

```text
Project.Read

Asset.Download

Review.Read
```

Clients cannot:

- View internal users
- Modify workflows
- Access financial data
- Access administration

---

# Auditor

Read-only role.

Can access

- Audit Logs
- Reports
- History
- Configuration

Cannot modify any business data.

---

# AI Agent

AI Agents authenticate using dedicated service identities.

Permissions depend on assigned capabilities.

Examples

```text
Requirement.Generate

Review.Generate

Documentation.Generate

Workflow.Analyze
```

AI Agents never receive unrestricted administrative permissions.

---

# Guest

Minimal access.

Used for

- Demonstrations
- Limited Collaboration
- Temporary Access

---

# Permission Categories

Permissions are grouped by module.

---

## Client

```text
Client.Read

Client.Create

Client.Update

Client.Delete
```

---

## Project

```text
Project.Read

Project.Create

Project.Update

Project.Delete

Project.Archive
```

---

## Batch

```text
Batch.Read

Batch.Create

Batch.Update

Batch.Delete
```

---

## Task

```text
Task.Read

Task.Create

Task.Assign

Task.Update

Task.Delete

Task.Complete
```

---

## Asset

```text
Asset.Read

Asset.Upload

Asset.Update

Asset.Delete

Asset.Download

Asset.Version.Create
```

---

## Review

```text
Review.Read

Review.Create

Review.Update

Review.Approve

Review.Reject
```

---

## Workflow

```text
Workflow.Read

Workflow.Execute

Workflow.Update
```

---

## Team

```text
Team.Read

Team.Create

Team.Update

Team.Delete
```

---

## Resource

```text
Resource.Read

Resource.Assign

Resource.Update
```

---

## Finance

```text
Finance.Read

Finance.Update

Finance.Approve

Finance.Export
```

---

## Reports

```text
Report.Read

Report.Export

Dashboard.Read
```

---

## Administration

```text
User.Manage

Role.Manage

Permission.Manage

System.Configure
```

---

# Role Matrix

| Module | Admin | PM | Lead | Dev | Reviewer | Client |
|---------|------:|---:|-----:|----:|---------:|-------:|
| Projects | CRUD | CRUD | Read | Read | Read | Read |
| Tasks | CRUD | CRUD | CRUD | Update Own | Read | Read |
| Assets | CRUD | CRUD | CRUD | Upload | Review | Download |
| Reviews | CRUD | Read | Approve | Respond | CRUD | Read |
| Reports | CRUD | Read | Read | Limited | Limited | Limited |
| Finance | CRUD | Read | No | No | No | No |
| Users | CRUD | No | No | No | No | No |

---

# Multiple Role Evaluation

Permissions are cumulative.

Example

```text
Developer

+

Reviewer

↓

Can Develop

+

Can Review
```

---

# Temporary Permissions

Future versions may support

- Time-limited access
- Emergency access
- Delegated permissions

---

# Custom Roles

Tenants may create custom roles.

Custom roles consist of:

- Name
- Description
- Permission Set
- Active Status

System roles cannot be deleted.

---

# Role Assignment Rules

- Every user must belong to at least one role.
- Administrative roles should be assigned only to authorized personnel.
- AI Agents use dedicated service roles.
- Clients cannot receive administrative roles.
- Guests receive only minimal permissions.

---

# Auditing

The following actions are audited:

- Role Assignment
- Role Removal
- Permission Changes
- Custom Role Creation
- Role Deletion
- Privileged Access

---

# Development Guidelines

Developers should

- Authorize by permission, not role name
- Avoid hardcoded roles in business logic
- Use policies for complex authorization
- Keep permissions granular
- Apply least privilege

---

# AI Development Guidelines

AI-generated code must

- Check permissions instead of role names
- Support multiple roles
- Respect tenant isolation
- Audit administrative actions
- Deny access by default

AI must never

- Hardcode "Admin" checks
- Assume one role per user
- Grant implicit permissions
- Bypass authorization

---

# Roles Checklist

Before deployment verify:

- ✓ Standard roles created
- ✓ Permission matrix configured
- ✓ Administrative roles restricted
- ✓ AI service roles configured
- ✓ Client permissions limited
- ✓ Role assignment audited
- ✓ Custom roles supported
- ✓ Permission inheritance tested
- ✓ Least privilege validated

---

# Future Enhancements

Planned capabilities include:

- Attribute-Based Access Control (ABAC)
- Dynamic Roles
- Delegated Administration
- Temporary Privilege Elevation
- Just-in-Time Access
- AI Permission Recommendations
- Risk-Based Role Assignment

---

# Summary

The Project & Asset Management Platform uses a flexible Role-Based Access Control (RBAC) model with predefined enterprise roles, fine-grained permissions, and support for multiple role assignments. Permissions are granted through roles rather than directly to users, ensuring centralized management, strong tenant isolation, and adherence to the principle of least privilege. The architecture is designed to support future enhancements such as custom roles, delegated administration, and Attribute-Based Access Control while maintaining compatibility with enterprise identity and governance requirements.
