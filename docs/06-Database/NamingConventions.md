# Database Naming Conventions

**Document ID:** DB-002

**Version:** 1.0

**Status:** Approved

**Owner:** Solution Architecture Team

---

# Purpose

This document defines the standard naming conventions for all database objects within the **AI Project & Asset Management Platform**.

The objectives are to:

- Maintain consistency
- Improve readability
- Simplify development
- Support automation
- Reduce ambiguity
- Improve maintainability
- Enable AI-assisted code generation

These conventions are mandatory for every database object.

---

# General Principles

All database objects shall follow these principles.

- Use **PascalCase**
- Use singular nouns for entities
- Names shall be meaningful
- Avoid abbreviations unless standardized
- Avoid spaces
- Avoid special characters
- Avoid reserved SQL keywords
- Keep names concise but descriptive

Example

```
Project
Client
WorkflowState
TaskAssignment
```

Avoid

```
tbl_project
proj
TBL_CLIENT
PJT
```

---

# Case Convention

Use **PascalCase** for all object names.

Examples

```
Project
ProjectTask
WorkflowTransition
NotificationTemplate
```

---

# Singular vs Plural

Use **singular** names for all tables.

Correct

```
Project
Task
Asset
Review
```

Incorrect

```
Projects
Tasks
Assets
Reviews
```

Reason

Each row represents one entity.

---

# Prefixes

Do not use prefixes such as

```
tbl_
tb_
dbo_
TBL_
```

Incorrect

```
tblProject
tblTask
```

Correct

```
Project
Task
```

---

# Table Naming

Tables shall represent business entities.

Examples

```
Organization
Client
Project
Batch
Asset
Task
SubTask
Review
Invoice
Payment
```

---

# Lookup Tables

Lookup tables end with **Type**, **Category**, or **Status**.

Examples

```
TaskStatus
ProjectStatus
AssetType
NotificationType
PriorityLevel
```

---

# Junction Tables

Many-to-many relationships shall combine entity names.

Examples

```
UserRole
ProjectTeam
RolePermission
TaskTag
AssetCategory
```

---

# Primary Keys

Every table shall have one primary key.

Naming format

```
<TableName>Id
```

Examples

```
ProjectId
TaskId
AssetId
ClientId
ReviewId
```

Avoid

```
Id
PID
Project_ID
```

---

# Foreign Keys

Foreign keys shall use the referenced table name.

Examples

```
ProjectId
ClientId
WorkflowId
UserId
BatchId
```

---

# Composite Keys

Use the participating key names.

Example

```
ProjectId
UserId
```

---

# Unique Keys

Naming format

```
UK_<Table>_<Columns>
```

Examples

```
UK_User_Email
UK_Client_Code
UK_Project_Number
```

---

# Primary Key Constraints

Naming format

```
PK_<Table>
```

Examples

```
PK_Project
PK_Task
PK_Asset
```

---

# Foreign Key Constraints

Naming format

```
FK_<Child>_<Parent>
```

Examples

```
FK_Task_Project
FK_Project_Client
FK_Asset_Batch
FK_Review_Task
```

---

# Index Naming

Naming format

```
IX_<Table>_<Columns>
```

Examples

```
IX_Task_Status
IX_Project_ClientId
IX_Asset_BatchId
```

---

# Unique Index

Naming

```
UX_<Table>_<Columns>
```

Examples

```
UX_User_Email
UX_Client_Code
```

---

# Check Constraints

Naming

```
CK_<Table>_<Rule>
```

Examples

```
CK_Task_Priority
CK_Project_Dates
CK_Invoice_Total
```

---

# Default Constraints

Naming

```
DF_<Table>_<Column>
```

Examples

```
DF_Task_Status
DF_Project_IsActive
DF_User_CreatedOn
```

---

# Views

Views begin with **vw**.

Examples

```
vwProjectSummary
vwTaskDashboard
vwInvoiceSummary
```

---

# Materialized Views

Prefix

```
mv
```

Examples

```
mvProjectStatistics
mvRevenueSummary
```

---

# Stored Procedures

Prefix

```
sp
```

Examples

```
spCreateProject
spAssignTask
spApproveReview
spGenerateInvoice
```

---

# Functions

Scalar Functions

```
fnCalculateRevenue
fnGenerateProjectCode
```

Table Functions

```
fnProjectTasks
fnResourceUtilization
```

---

# Sequences

Naming

```
SEQ_<Entity>
```

Examples

```
SEQ_Project
SEQ_Invoice
```

---

# Triggers

Naming

```
TR_<Table>_<Action>
```

Examples

```
TR_Task_Insert
TR_Project_Update
TR_Review_Delete
```

---

# Columns

Columns use PascalCase.

Examples

```
ProjectName
TaskTitle
EstimatedHours
CreatedDate
ModifiedDate
```

---

# Boolean Columns

Use positive names.

Correct

```
IsActive
IsDeleted
IsApproved
IsCompleted
CanEdit
CanDelete
HasAttachment
```

Avoid

```
NotActive
DeletedFlag
Disable
```

---

# Date Columns

Standard names

```
CreatedDate
ModifiedDate
DeletedDate
ApprovedDate
CompletedDate
DueDate
StartDate
EndDate
```

---

# User Reference Columns

Examples

```
CreatedBy
ModifiedBy
DeletedBy
AssignedTo
ApprovedBy
ReviewedBy
```

---

# Audit Columns

Every transactional table should contain

```
CreatedDate
CreatedBy
ModifiedDate
ModifiedBy
IsDeleted
DeletedDate
DeletedBy
```

---

# Status Columns

Naming

```
Status
StatusId
WorkflowStateId
ApprovalStatus
```

---

# Numeric Columns

Examples

```
Quantity
Amount
Budget
Cost
Revenue
Percentage
Priority
DisplayOrder
```

---

# Text Columns

Examples

```
Name
Title
Description
Remarks
Comments
Notes
Summary
```

---

# File Columns

Examples

```
FileName
OriginalFileName
StoragePath
ContentType
FileSize
Checksum
```

---

# AI Columns

Examples

```
EmbeddingVector
PromptVersion
ModelName
TokenCount
AIProvider
ConfidenceScore
```

---

# Enumeration Tables

Examples

```
TaskPriority
TaskStatus
AssetStatus
WorkflowStatus
ReviewStatus
```

---

# Naming Reserved Columns

These names are standardized.

```
Id
Code
Name
Description
Status
CreatedDate
CreatedBy
ModifiedDate
ModifiedBy
DeletedDate
DeletedBy
IsDeleted
IsActive
Version
RowVersion
TenantId
```

---

# File Storage Convention

Assets are stored outside the database.

Database stores

```
AssetId
StorageProvider
StoragePath
OriginalFileName
ContentType
Checksum
FileSize
```

---

# JSON Columns

Use only when necessary.

Examples

```
MetadataJson
ConfigurationJson
SettingsJson
AdditionalDataJson
```

Avoid excessive JSON storage when relational modeling is appropriate.

---

# Temporary Tables

Prefix

```
Tmp
```

Examples

```
TmpProjectImport
TmpTaskCalculation
```

---

# Archive Tables

Suffix

```
Archive
```

Examples

```
ProjectArchive
TaskArchive
ReviewArchive
```

---

# History Tables

Suffix

```
History
```

Examples

```
ProjectHistory
WorkflowHistory
AssetHistory
ReviewHistory
```

---

# AI Knowledge Tables

Examples

```
KnowledgeDocument
KnowledgeChunk
PromptLibrary
PromptTemplate
Conversation
ConversationMessage
Embedding
```

---

# Examples

## Good

```
Project
ProjectId
ProjectName
ClientId
CreatedDate
CreatedBy
```

---

## Poor

```
tblProject
PID
projname
CreateDt
Flg
```

---

# Reserved Abbreviations

The following abbreviations are permitted because they are industry standards.

| Abbreviation | Meaning |
|-------------|---------|
| API | Application Programming Interface |
| AI | Artificial Intelligence |
| URL | Uniform Resource Locator |
| URI | Uniform Resource Identifier |
| UUID | Universally Unique Identifier |
| IP | Internet Protocol |
| UI | User Interface |
| KPI | Key Performance Indicator |
| SLA | Service Level Agreement |
| OTP | One-Time Password |
| MFA | Multi-Factor Authentication |
| SSO | Single Sign-On |

---

# Naming Checklist

Before creating any database object, verify:

- PascalCase used
- Singular noun
- Business terminology
- No prefixes
- No reserved keywords
- Meaningful name
- Consistent with domain model
- AI-readable
- Matches documentation
- Follows enterprise standards

---

# Summary

Following these conventions ensures:

- Consistent database design
- Easier onboarding of developers
- Cleaner Entity Framework models
- Better SQL readability
- Improved maintainability
- Predictable API models
- Simplified AI-assisted development
- Long-term enterprise scalability
