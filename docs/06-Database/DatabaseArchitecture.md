# Database Architecture

**Document ID:** DB-001

**Version:** 1.0

**Status:** Draft

**Owner:** Solution Architecture Team

---

# Purpose

This document defines the logical and physical database architecture for the **AI Project & Asset Management Platform**. It serves as the foundation for application development, API design, reporting, integrations, AI capabilities, and future scalability.

The architecture is designed to support:

- Enterprise-scale deployments
- Multi-tenant SaaS
- On-premises installations
- High availability
- AI-powered features
- Large binary asset storage
- Workflow-driven business processes
- Horizontal scalability

---

# Design Principles

The database architecture follows these principles:

- Normalize transactional data (3NF or higher)
- Denormalize only where reporting performance requires it
- Maintain strict referential integrity
- Support auditability for all critical entities
- Prefer immutable historical records over destructive updates
- Separate transactional and analytical workloads
- Design for cloud-native scalability
- Keep AI data logically isolated from transactional data

---

# Database Technology Stack

## Primary Database

| Component | Technology |
|------------|------------|
| Relational Database | PostgreSQL |
| Version | Latest LTS |
| ORM | Entity Framework Core |
| Connection Pool | Npgsql |
| Migration Framework | EF Core Migrations |

---

## Supporting Storage

| Component | Technology |
|------------|------------|
| Object Storage | MinIO / Azure Blob / AWS S3 |
| Cache | Redis |
| Message Queue | RabbitMQ |
| Search Engine | Elasticsearch / OpenSearch *(Future)* |
| Vector Database | PostgreSQL + pgvector |
| File Metadata | PostgreSQL |

---

# High-Level Architecture

```text
                    Application Layer
                           │
            ┌──────────────┼──────────────┐
            │              │              │
        REST APIs      SignalR        AI Services
            │              │              │
            └──────────────┼──────────────┘
                           │
                  Repository Layer
                           │
                    Entity Framework
                           │
                    PostgreSQL Cluster
                           │
    ┌──────────────┬──────────────┬──────────────┐
    │              │              │              │
Operational   Reporting DB   AI Vector DB   Audit DB
    │
    └──────────────► Object Storage (Assets)
```

---

# Database Layers

The solution is logically divided into multiple layers.

## 1. Master Data

Stores relatively static business entities.

Examples:

- Organization
- Client
- Department
- Team
- User
- Role
- Permission
- Lookup Values

Characteristics:

- Low update frequency
- High read frequency
- Referential data

---

## 2. Transactional Data

Stores operational business information.

Examples:

- Projects
- Tasks
- Assets
- Batches
- Reviews
- Invoices
- Payments
- Notifications

Characteristics:

- High insert/update rate
- ACID compliance
- Fully normalized

---

## 3. Workflow Data

Stores workflow engine state.

Examples:

- Workflow
- Workflow State
- Workflow Transition
- Workflow Instance
- Approval History

Characteristics:

- Highly relational
- Event driven
- Historical tracking

---

## 4. Audit Data

Stores immutable history.

Examples:

- Audit Logs
- Entity History
- Login History
- Permission Changes

Characteristics:

- Append only
- Immutable
- Long retention

---

## 5. AI Data

Stores AI-specific information.

Examples:

- Prompt Templates
- Embeddings
- Conversations
- AI Usage
- Knowledge Chunks
- Vector Index

Characteristics:

- Large text
- Vector similarity search
- AI optimized

---

## 6. Reporting Data

Optimized for analytics.

Examples:

- Materialized Views
- Summary Tables
- KPI Tables
- Dashboard Aggregates

Characteristics:

- Read optimized
- Refreshable
- Denormalized

---

# Core Business Domains

The database is organized into the following domains.

## Organization Domain

Tables include:

- Organization
- OrganizationSettings
- BusinessCalendar
- Holiday
- TimeZone

---

## Security Domain

Tables include:

- User
- Role
- Permission
- RolePermission
- UserRole
- LoginHistory
- RefreshToken

---

## Client Domain

Tables include:

- Client
- ClientContact
- ClientAddress
- ClientAttachment

---

## Project Domain

Tables include:

- Project
- Milestone
- ProjectTeam
- ResourceAllocation

---

## Production Domain

Tables include:

- Batch
- BatchStage
- Deliverable
- Asset
- AssetVersion

---

## Task Domain

Tables include:

- Task
- SubTask
- TaskComment
- TaskDependency
- Checklist

---

## Workflow Domain

Tables include:

- Workflow
- WorkflowState
- WorkflowTransition
- WorkflowInstance
- WorkflowHistory

---

## Review Domain

Tables include:

- Review
- ReviewRound
- Feedback
- Annotation

---

## Finance Domain

Tables include:

- Invoice
- Payment
- Budget
- Expense

---

## Notification Domain

Tables include:

- Notification
- NotificationTemplate
- NotificationQueue

---

## AI Domain

Tables include:

- Prompt
- PromptVersion
- Conversation
- ConversationMessage
- Embedding
- KnowledgeDocument
- KnowledgeChunk

---

# Relationship Strategy

Relationships follow these rules:

- Use integer or UUID primary keys consistently.
- All foreign keys must be enforced.
- Cascade deletes only where safe.
- Soft delete preferred for business entities.
- Many-to-many relationships implemented using junction tables.

---

# Storage Strategy

## Relational Data

Stored in PostgreSQL.

Examples:

- Users
- Projects
- Tasks
- Workflows

---

## Binary Data

Stored externally.

Examples:

- Images
- Videos
- Documents
- Source Files
- ZIP Archives

Database stores only:

- File metadata
- Hash
- Storage path
- Version

---

## Vector Data

Stored using pgvector.

Examples:

- Document embeddings
- Prompt embeddings
- Knowledge embeddings

Used for:

- Semantic Search
- AI Assistant
- RAG

---

# Scalability Strategy

The architecture supports horizontal growth.

Techniques:

- Read Replicas
- Connection Pooling
- Partitioning
- Materialized Views
- Background Processing
- Distributed Cache
- Object Storage

---

# Multi-Tenancy Strategy

Supported deployment models:

### Shared Database

TenantId in every table.

Suitable for:

- SaaS

---

### Dedicated Database

One database per tenant.

Suitable for:

- Enterprise

---

### Hybrid

Combination of shared and dedicated databases.

---

# High Availability

Supports:

- Streaming Replication
- Automatic Failover
- Point-in-Time Recovery
- Hot Standby
- Backup Replicas

---

# Security Architecture

Security features include:

- TLS encryption
- Row-level security (optional)
- Database roles
- Principle of least privilege
- Encrypted secrets
- Secure connection strings
- Data masking
- Audit trails

---

# Performance Strategy

Performance is achieved using:

- Proper indexing
- Query optimization
- Materialized views
- Redis caching
- Background jobs
- Partitioning
- Bulk operations
- Read replicas

---

# Backup Strategy

Supports:

- Full backups
- Incremental backups
- WAL archiving
- Point-in-Time Recovery
- Automated validation

---

# Disaster Recovery

Recovery objectives:

| Metric | Target |
|---------|--------|
| RPO | < 15 Minutes |
| RTO | < 1 Hour |

---

# AI Readiness

The architecture is designed for AI from day one.

Supports:

- Prompt Library
- Vector Search
- RAG
- Knowledge Base
- AI Conversations
- Agent Memory
- AI Usage Analytics

---

# Database Lifecycle

```text
Development
      │
Migration
      │
Testing
      │
Staging
      │
Production
      │
Monitoring
      │
Optimization
      │
Archiving
```

---

# Guiding Principles

The database architecture shall always prioritize:

1. Data Integrity
2. Performance
3. Scalability
4. Maintainability
5. Security
6. Auditability
7. Extensibility
8. AI Readiness
9. Cloud Compatibility
10. Enterprise Reliability

---

# Related Documents

- NamingConventions.md
- EntityRelationshipDiagram.md
- Tables.md
- IndexingStrategy.md
- Auditing.md
- Versioning.md
- MultiTenancy.md
- BackupAndRecovery.md
- Archiving.md
- DataDictionary.md
