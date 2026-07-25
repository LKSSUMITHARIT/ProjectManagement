# Project Team

> **Purpose**
>
> The Project Team defines all users who are authorized to participate in a Project. It establishes the organizational structure, responsibilities, access boundaries, and operational ownership required to successfully deliver the Project.
>
> Unlike Resource Allocation, which is **Batch-specific and time-bound**, the Project Team defines **who belongs to the Project** throughout its lifecycle.

---

# Overview

Every Project consists of one or more users assigned to various business roles.

The Project Team enables:

- Role-based access
- Organizational ownership
- Team collaboration
- Communication
- Reporting
- Resource planning

A Project Team acts as the parent team for all Batches created under the Project.

---

# Position in Business Hierarchy

```text
Client
    │
    ▼
Project
│
├── Project Team
│      ├── Project Manager
│      ├── Batch Manager
│      ├── Team Lead
│      ├── Reviewer
│      ├── QC
│      ├── Resource Manager
│      ├── Finance
│      └── Artists
│
└── Batches
```

---

# Objectives

The Project Team module enables organizations to:

- Build the project organization
- Define business ownership
- Assign operational responsibilities
- Control project access
- Support collaboration
- Provide reporting hierarchy

---

# Team Structure

```text
Project Manager
│
├── Batch Manager(s)
│      │
│      ├── Team Lead(s)
│      │      │
│      │      └── Artists
│      │
│      ├── Reviewer(s)
│      └── QC
│
├── Resource Manager
└── Finance
```

---

# Team Membership

Each member belongs to the Project in one or more business roles.

A user may belong to:

- Multiple Projects
- Multiple Teams
- Multiple Roles (if permitted)

Example:

| User | Roles |
|-------|------|
| John | Project Manager |
| Sarah | Batch Manager |
| David | Team Lead |
| Alex | Reviewer |
| Emma | QC |
| Kevin | Artist |

---

# Team Roles

## Project Manager

Responsible for:

- Overall project ownership
- Planning
- Client communication
- Project execution
- Financial coordination
- Project closure

---

## Batch Manager

Responsible for:

- Batch planning
- Batch execution
- Resource requests
- Delivery coordination

---

## Team Lead

Responsible for:

- Task creation
- Subtask planning
- Artist assignment
- Production review
- Feedback implementation

---

## Artist

Responsible for:

- Executing assigned Subtasks
- Uploading work
- Updating progress

Artists become actively involved in production only after being allocated to a Batch through the Resource Allocation process.

---

## Reviewer

Responsible for:

- Final Review
- Quality feedback
- Approval
- Minor Fix
- Major Fix

Reviewers do not create Subtasks.

---

## QC Engineer

Responsible for:

- Quality validation
- QC approval
- QC feedback

---

## Resource Manager

Responsible for:

- Allocation approvals
- Capacity planning
- Resource balancing

---

## Finance

Responsible for:

- Billing
- Payment tracking
- Financial reporting

---

# Team Membership Lifecycle

```text
Invited
    │
Active
    │
Inactive
    │
Removed
```

---

# Membership Status

| Status | Description |
|----------|-------------|
| Invited | User added but not yet active |
| Active | Current project member |
| Inactive | Temporarily unavailable |
| Removed | No longer part of the project |

Historical memberships are retained for audit purposes.

---

# Project Team vs Resource Allocation

These concepts are intentionally separate.

## Project Team

Defines **who belongs to the Project**.

Examples:

- Project Manager
- Batch Manager
- Team Lead
- Reviewer
- QC
- Artists

Project membership does **not** indicate active production work.

---

## Resource Allocation

Defines **who is working on which Batch and for how long**.

Resource Allocation determines:

- Allocation Percentage
- Allocation Period
- Capacity
- Utilization
- Approval Status

Example:

```text
Project
│
├── Artist A
├── Artist B
└── Artist C

↓

Batch Allocation

Artist A → Batch A → 50%

Artist A → Batch B → 50%

Artist B → Batch A → 100%
```

---

# Project Team Permissions

Membership alone does not grant permissions.

Permissions are determined by:

- Role
- Security Profile
- Organization Policy

Example:

```text
User

↓

Project Team

↓

Role

↓

Permission Set

↓

Allowed Operations
```

---

# Communication

All Project Team members can participate in Project-level discussions according to their permissions.

Supported features include:

- Rich Text
- Mentions
- Attachments
- Notifications
- Activity Timeline

---

# Notifications

Typical notifications include:

- Added to Project
- Removed from Project
- Role Changed
- Project Announcement
- Batch Created
- Resource Request
- Project Closure

---

# Business Rules

## BR-001

Every Project must have exactly one active Project Manager.

---

## BR-002

A user may belong to multiple Projects.

---

## BR-003

A user may hold multiple Project roles if permitted by organizational policy.

---

## BR-004

Removing a user from the Project does not delete historical audit records.

---

## BR-005

Removing an Artist from the Project does not modify historical Task or Subtask ownership.

---

## BR-006

Project Team membership is independent of Batch Resource Allocation.

---

## BR-007

Only Project Team members can be assigned operational roles within the Project.

---

## BR-008

Only allocated Artists may perform production work within a Batch.

---

## BR-009

Role changes affect future permissions but must not alter historical records.

---

## BR-010

Inactive members remain visible in historical reports.

---

# Suggested Data Model

## Project Team

| Field | Description |
|------|-------------|
| Project Team Id | Primary Key |
| Project Id | Parent Project |
| User Id | Team Member |
| Role Id | Business Role |
| Start Date | Membership Start |
| End Date | Membership End |
| Status | Active / Inactive |
| Remarks | Optional Notes |

---

# Reporting

The Project Team module supports reports such as:

- Project Organization Chart
- Team Directory
- Team Composition
- Team Role Distribution
- Active Members
- Inactive Members
- Cross-Project Membership
- Resource Availability
- Team Performance

---

# Future Enhancements

Future releases may introduce:

- Team Templates
- Skill Matrix
- Competency Mapping
- Department Hierarchy
- Cost Center Assignment
- Role Delegation
- Organizational Chart Visualization
- AI Team Recommendations
- Succession Planning
- Automatic Team Provisioning

---

# Related Documents

- Project.md
- Batch.md
- ResourceAllocation.md
- RolesAndResponsibilities.md
- UserPersonas.md
- RolesAndPermissions.md *(planned)*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Project Team domain specification |
