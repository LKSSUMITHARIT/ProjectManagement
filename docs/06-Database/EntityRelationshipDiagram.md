# Entity Relationship Diagram (ERD)

**Document ID:** DB-003

**Version:** 1.0

**Status:** Draft

**Owner:** Solution Architecture Team

---

# Purpose

This document defines the logical Entity Relationship Model (ERM) for the **AI Project & Asset Management Platform**.

It identifies:

- Core business entities
- Relationships
- Cardinality
- Ownership
- Parent-child hierarchy
- Junction entities
- Future extensibility

This document is technology independent. Physical table definitions are documented in **Tables.md**.

---

# High-Level Domain Model

```text
Organization
    │
    ├──────────── Users
    │                │
    │                ├──── UserRole ──── Role
    │                │
    │                └──── ProjectTeam
    │
    ├──────────── Clients
    │                │
    │                └──── Projects
    │                       │
    │                       ├──── Batches
    │                       │      │
    │                       │      ├──── Assets
    │                       │      │       │
    │                       │      │       ├── AssetVersions
    │                       │      │       └── Reviews
    │                       │      │
    │                       │      └──── Deliverables
    │                       │
    │                       ├──── Tasks
    │                       │      │
    │                       │      ├── SubTasks
    │                       │      ├── Comments
    │                       │      ├── Attachments
    │                       │      └── Reviews
    │                       │
    │                       ├──── WorkflowInstances
    │                       │
    │                       ├──── ResourceAllocations
    │                       │
    │                       ├──── Invoices
    │                       │      └── Payments
    │                       │
    │                       └──── Notifications
    │
    └──────────── Audit Logs
```

---

# Core Entity Groups

The platform consists of the following major domains.

| Domain | Purpose |
|---------|----------|
| Organization | Multi-company support |
| Security | Users, Roles, Permissions |
| Client | Customer information |
| Project | Project lifecycle |
| Production | Batches & Deliverables |
| Asset | Digital assets |
| Task | Work management |
| Workflow | State engine |
| Review | Review cycles |
| Finance | Billing & Payments |
| Communication | Notifications & Messages |
| AI | AI Knowledge & Conversations |
| Audit | Change history |

---

# Organization Domain

```text
Organization
    │
    ├── Departments
    │
    ├── Teams
    │
    ├── Users
    │
    └── BusinessSettings
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Organization | Department | 1:N |
| Organization | Team | 1:N |
| Organization | User | 1:N |
| Organization | Client | 1:N |

---

# Security Domain

```text
User
 │
 ├──── UserRole ──── Role
 │                     │
 │                     └──── Permission
 │
 └──── LoginHistory
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| User | UserRole | 1:N |
| Role | UserRole | 1:N |
| Role | Permission | M:N |
| User | LoginHistory | 1:N |

---

# Client Domain

```text
Client
   │
   ├── Contacts
   ├── Addresses
   ├── Attachments
   └── Projects
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Client | Contact | 1:N |
| Client | Address | 1:N |
| Client | Project | 1:N |

---

# Project Domain

```text
Project
 │
 ├── Milestones
 ├── Teams
 ├── Batches
 ├── Tasks
 ├── ResourceAllocation
 ├── Deliverables
 ├── WorkflowInstances
 └── Invoices
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Project | Batch | 1:N |
| Project | Task | 1:N |
| Project | Milestone | 1:N |
| Project | ResourceAllocation | 1:N |
| Project | Deliverable | 1:N |
| Project | Invoice | 1:N |

---

# Batch Domain

```text
Batch
 │
 ├── Assets
 ├── BatchStages
 ├── Deliverables
 └── Reviews
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Batch | Asset | 1:N |
| Batch | BatchStage | 1:N |
| Batch | Deliverable | 1:N |

---

# Asset Domain

```text
Asset
 │
 ├── AssetVersions
 ├── AssetMetadata
 ├── AssetTags
 ├── Reviews
 └── Comments
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Asset | AssetVersion | 1:N |
| Asset | Review | 1:N |
| Asset | Comment | 1:N |

---

# Task Domain

```text
Task
 │
 ├── SubTasks
 ├── TaskComments
 ├── Attachments
 ├── TaskChecklist
 ├── Reviews
 └── WorkflowInstance
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Task | SubTask | 1:N |
| Task | Comment | 1:N |
| Task | Attachment | 1:N |
| Task | Review | 1:N |

---

# Workflow Domain

```text
Workflow
 │
 ├── WorkflowState
 │
 ├── WorkflowTransition
 │
 └── WorkflowInstance
          │
          └── WorkflowHistory
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Workflow | WorkflowState | 1:N |
| Workflow | WorkflowTransition | 1:N |
| Workflow | WorkflowInstance | 1:N |
| WorkflowInstance | WorkflowHistory | 1:N |

---

# Review Domain

```text
Review
 │
 ├── ReviewRounds
 │
 ├── Feedback
 │
 └── ReviewAttachments
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Review | ReviewRound | 1:N |
| ReviewRound | Feedback | 1:N |

---

# Finance Domain

```text
Invoice
 │
 ├── Payments
 │
 └── InvoiceItems
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| Invoice | Payment | 1:N |
| Invoice | InvoiceItem | 1:N |

---

# Communication Domain

```text
Notification
 │
 ├── NotificationRecipients
 │
 └── NotificationHistory
```

---

# AI Domain

```text
KnowledgeDocument
 │
 ├── KnowledgeChunk
 │
 └── Embedding
```

```text
Conversation
 │
 └── ConversationMessage
```

```text
Prompt
 │
 └── PromptVersion
```

### Relationships

| Parent | Child | Cardinality |
|----------|--------|-------------|
| KnowledgeDocument | KnowledgeChunk | 1:N |
| KnowledgeChunk | Embedding | 1:1 |
| Conversation | ConversationMessage | 1:N |
| Prompt | PromptVersion | 1:N |

---

# Audit Domain

Every business entity may have history.

```text
Project
    │
    └── ProjectHistory

Task
    │
    └── TaskHistory

Workflow
    │
    └── WorkflowHistory

Asset
    │
    └── AssetHistory
```

---

# Cross-Domain Relationships

```text
Organization
    │
    ├── Client
    │      │
    │      └── Project
    │              │
    │              ├── Batch
    │              │      │
    │              │      └── Asset
    │              │             │
    │              │             └── Review
    │              │
    │              ├── Task
    │              │     │
    │              │     └── Review
    │              │
    │              ├── Workflow
    │              │
    │              └── Invoice
    │
    └── Users
```

---

# Many-to-Many Relationships

| Entity A | Junction | Entity B |
|------------|------------|------------|
| User | UserRole | Role |
| Role | RolePermission | Permission |
| User | ProjectTeam | Project |
| Task | TaskTag | Tag |
| Asset | AssetCategory | Category |
| User | NotificationRecipient | Notification |

---

# Common Audit Columns

Every transactional table should contain:

- CreatedDate
- CreatedBy
- ModifiedDate
- ModifiedBy
- IsDeleted
- DeletedDate
- DeletedBy
- RowVersion

---

# Tenant Ownership

Every business entity belongs to an Organization (Tenant).

```text
Organization

    │

    ├── Client

    ├── Project

    ├── User

    ├── Batch

    ├── Asset

    ├── Task

    ├── Invoice

    └── Review
```

All major tables contain:

```
OrganizationId
```

---

# Relationship Rules

- Every Project belongs to one Client.
- Every Batch belongs to one Project.
- Every Asset belongs to one Batch.
- Every Task belongs to one Project.
- Reviews may be attached to Tasks or Assets.
- Workflow Instances may control Projects, Tasks, Assets, Reviews, or Batches.
- Invoices belong to Projects.
- Payments belong to Invoices.
- Users belong to Organizations.
- Permissions are inherited through Roles.

---

# Database Growth Strategy

Future domains can be added without affecting existing relationships.

Examples:

- CRM
- Procurement
- HR
- AI Marketplace
- Plugin Store
- ERP
- Manufacturing
- Digital Twin

---

# Related Documents

- DatabaseArchitecture.md
- Tables.md
- DataDictionary.md
- WorkflowRequirements.md
- APIRequirements.md
- MultiTenancy.md
- Auditing.md
