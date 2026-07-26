# Workflow Template

> **Purpose**
>
> Workflow Templates provide reusable definitions for business workflows.
>
> Instead of designing a Workflow for every Project or Batch, administrators create reusable Workflow Templates that can be instantiated multiple times.
>
> Templates standardize business processes while allowing controlled customization where required.

---

# Overview

A Workflow Template is the blueprint for creating Workflow instances.

```text
Workflow Template

↓

Create Workflow

↓

Assign to Project

↓

Assign to Batch

↓

Workflow Instance
```

Templates themselves never execute.

Only Workflow Instances execute.

---

# Objectives

Workflow Templates provide:

- Process standardization
- Reusability
- Faster project setup
- Version control
- Organization-wide consistency
- Reduced configuration effort
- Governance

---

# Architecture

```text
Workflow Template
        │
        ├── Processes
        ├── States
        ├── Transitions
        ├── Permissions
        ├── Validations
        ├── Automations
        ├── Notifications
        ├── SLA
        ├── Rules
        └── Metadata
                │
                ▼
        Workflow Instance
```

---

# Template Components

Each template contains:

- Template Information
- Workflow Definition
- Processes
- States
- Transitions
- Actions
- Validation Rules
- Permission Rules
- Automation Rules
- Notification Rules
- SLA Rules
- Custom Fields
- Tags

---

# Template Lifecycle

```text
Draft

↓

Testing

↓

Approved

↓

Published

↓

Deprecated

↓

Archived
```

Only Published templates may be used.

---

# Template Types

Examples

- Asset Production
- Character Pipeline
- Environment Pipeline
- Animation Pipeline
- UI Design
- Software Development
- Marketing Approval
- HR Approval
- Procurement

---

# Template Structure

Example

```text
Character Production

↓

Production

↓

Lead Review

↓

Final Review

↓

QC

↓

Client Review

↓

Completed
```

---

# Template Parameters

Templates may define configurable parameters.

Examples

- Default Priority
- SLA
- Working Calendar
- Review Required
- QC Required
- Client Review Required
- Review Types
- Auto Assignment Rules

---

# Template Variables

Variables are replaced during Workflow creation.

Example

```text
{{ProjectName}}

{{ClientName}}

{{TeamLead}}

{{WorkflowOwner}}
```

---

# Template Inheritance

Templates may inherit from another template.

Example

```text
Asset Production

↓

Character Production

↓

Hero Character Production
```

Child templates inherit all parent configuration unless overridden.

---

# Version Support

Every published template is versioned.

Example

```
Asset Workflow

Version 1.0

↓

Version 1.1

↓

Version 2.0
```

Existing workflows continue using the version from which they were created unless migrated.

---

# Template Cloning

Templates may be cloned.

Example

```text
Character Workflow

↓

Clone

↓

Creature Workflow
```

---

# Customizations

Organizations may customize:

- Process names
- States
- Permissions
- Notifications
- Automations
- SLA
- Forms
- Custom Fields

Core template integrity remains protected.

---

# Template Validation

Before publishing, the system validates:

- Duplicate States
- Missing Transitions
- Circular References
- Missing Permissions
- Missing Validations
- Invalid SLA Rules
- Broken Automation References

---

# Template Deployment

Templates may be deployed to:

- Single Project
- Multiple Projects
- Business Unit
- Organization
- Tenant

---

# Import / Export

Supported formats

- JSON
- YAML
- XML (Future)

Allows sharing templates across environments.

---

# Business Rules

## BR-001

Only Published Templates can create Workflow Instances.

---

## BR-002

Templates are immutable after publication.

Changes require a new Template Version.

---

## BR-003

Workflow Instances maintain a reference to the originating Template Version.

---

## BR-004

Templates may inherit from other Templates.

---

## BR-005

Template validation must succeed before publication.

---

## BR-006

Template deletion is prohibited while active Workflow Instances exist.

---

## BR-007

Templates support import and export.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| TemplateId | Primary Key |
| Name | Template Name |
| Description | Description |
| Category | Asset / Software / HR |
| Version | Current Version |
| ParentTemplateId | Optional Parent |
| Status | Draft / Published |
| PublishedOn | Publication Date |
| CreatedBy | Creator |

---

# Reporting

Typical reports include:

- Template Usage
- Most Used Templates
- Template Versions
- Active Workflow Instances
- Deprecated Templates
- Workflow Creation Time

---

# Future Enhancements

Future releases may include:

- AI Template Generator
- AI Workflow Optimization
- Marketplace for Templates
- Industry Template Library
- Low-Code Workflow Builder
- Visual Template Comparison
- Template Dependency Analysis

---

# Design Principles

The Workflow Template module follows these principles:

- Templates define structure, not execution.
- Templates are reusable across projects.
- Published templates are immutable.
- Every Workflow Instance records its source template.
- Versioning ensures long-term stability.
- Templates encourage consistency while supporting controlled customization.

---

# Related Documents

- Workflow.md
- WorkflowVersion.md
- WorkflowDesigner.md
- WorkflowProcess.md
- WorkflowState.md
- WorkflowTransition.md
- WorkflowValidation.md
- WorkflowAutomation.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow Template specification |
