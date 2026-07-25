# Product Modules

> **Purpose**
>
> This document provides a high-level overview of all functional modules that make up the Project Management Platform. It describes the responsibility, ownership, and interaction of each module without going into implementation details.
>
> Detailed functional specifications for every module are documented in the **03-Modules** section.

---

# Overview

The Project Management Platform is designed using a **modular architecture**, where each module owns a specific business capability while collaborating with other modules through well-defined interfaces and business workflows.

This approach provides:

- Clear separation of responsibilities
- Independent module evolution
- Better maintainability
- Easier scalability
- Future plugin support
- AI integration readiness

---

# Module Hierarchy

```text
Platform
│
├── Administration
├── User & Security
├── Client Management
├── Project Management
├── Batch Management
├── Resource Management
├── Asset Management
├── Task Management
├── Workflow Management
├── Review Management
├── Deliverable Management
├── Finance
├── Communication
├── Reporting
├── Notification
└── AI Services (Future)
```

---

# Core Business Modules

## Client Management

### Purpose

Manage organizations for whom projects are executed.

### Responsibilities

- Client Master
- Parent Client Hierarchy
- Contact Information
- Address Management
- Region & Country
- Client Financial Summary
- Active Projects
- Outstanding Payments

### Primary Users

- Sales
- Project Managers
- Finance
- Management

### Depends On

- Finance
- Project Management

---

## Project Management

### Purpose

Manage contractual engagements and overall project execution.

### Responsibilities

- Project Master
- Project Team
- Required Software
- Project Settings
- Project Communication
- Project Dashboard
- Project Timeline

### Primary Users

- Project Managers
- Delivery Managers
- Leads

### Depends On

- Client Management
- Batch Management

---

## Batch Management

### Purpose

Organize production work into manageable execution units.

### Responsibilities

- Batch Master
- Batch Team
- Batch Workflow
- Batch Stages
- Batch Dashboard
- Batch Communication

### Primary Users

- Production Managers
- Leads
- Project Managers

### Depends On

- Project Management
- Workflow Management

---

## Resource Management

### Purpose

Plan, allocate, approve, and monitor production resources.

### Responsibilities

- Resource Allocation
- Allocation Requests
- Allocation Approval
- Capacity Planning
- Utilization Tracking
- Allocation Calendar
- Workload Visualization

### Primary Users

- Resource Managers
- Batch Managers
- Project Managers

### Depends On

- Batch Management
- User Management

---

## Asset Management

### Purpose

Manage production deliverables within each Batch.

### Responsibilities

- Asset Master
- Asset Categories
- Asset Assignment
- Asset Progress
- Asset Timeline

### Primary Users

- Leads
- Artists
- Project Managers

### Depends On

- Batch Management

---

## Task Management

### Purpose

Manage production activities performed on Assets.

### Responsibilities

- Task Creation
- Task Assignment
- Task Workflow
- Task Progress
- Kanban Board
- Task Timeline

### Primary Users

- Leads
- Artists
- Project Managers

### Depends On

- Asset Management
- Workflow Engine

---

## Subtask Management

### Purpose

Manage individual units of production work assigned to resources.

### Responsibilities

- General Subtasks
- FR Fix Subtasks
- Client Fix Subtasks
- Round Tracking
- Assignment
- Status Tracking

### Primary Users

- Leads
- Artists

### Depends On

- Task Management

---

## Workflow Management

### Purpose

Define and execute production workflows.

### Responsibilities

- Workflow Definition
- Process Definition
- State Definition
- Transition Rules
- Workflow Validation
- Workflow Versioning *(Future)*

### Primary Users

- Administrators
- Business Analysts

### Used By

Nearly every production module.

---

## Review Management

### Purpose

Manage all review stages within production.

### Responsibilities

- WIP Review
- Final Review
- Quality Control
- Client Review
- Feedback
- Review History
- Review Rounds

### Primary Users

- Leads
- Reviewers
- QC
- Clients *(Future Portal)*

### Depends On

- Workflow Management
- Task Management

---

## Deliverable Management

### Purpose

Track production deliverables and source control references.

### Responsibilities

- Repository
- File Path
- Branch
- Version
- Changeset
- Delivery History

### Important

The platform stores metadata only.

Actual production files remain in external source control systems.

---

## Finance

### Purpose

Manage project billing and payment tracking.

### Responsibilities

- Project Invoices
- Client Billing
- Payments
- Outstanding Balance
- Discounts
- Waivers
- Revenue Tracking

### Primary Users

- Finance
- Management

### Depends On

- Project Management
- Client Management

---

## Communication

### Purpose

Provide contextual collaboration throughout the platform.

### Responsibilities

- Discussions
- Rich Text Comments
- Mentions
- Attachments
- Activity Feed

Supported Levels:

- Project
- Batch
- Asset
- Task

---

## Reporting

### Purpose

Provide operational and executive visibility.

### Responsibilities

- Dashboards
- KPI Reporting
- Production Reports
- Financial Reports
- Resource Reports
- Executive Reports

Consumes data from all business modules.

---

# Platform Modules

---

## User Management

### Responsibilities

- User Profiles
- Departments
- Designations
- Teams
- Employee Information

---

## Authentication

### Responsibilities

- Login
- Session Management
- Password Policies
- Multi-Factor Authentication *(Future)*
- Single Sign-On *(Future)*

---

## Authorization

### Responsibilities

- Roles
- Permissions
- Access Policies
- Entity Security

---

## Administration

### Responsibilities

- Master Data
- Organization Settings
- Business Configuration
- System Parameters
- Lookup Tables

---

## Notification

### Responsibilities

- In-App Notifications
- Email Notifications
- Push Notifications *(Future)*
- Reminder Rules
- Escalations

---

## Audit & Activity

### Responsibilities

- Activity Timeline
- Audit Logs
- Change History
- Security Logs

Every important business action is recorded.

---

## Search

### Responsibilities

- Global Search
- Entity Search
- Full Text Search
- Saved Searches *(Future)*

---

## Tag Management

### Responsibilities

- Tags
- Classification
- Filtering
- Reporting

---

## Custom Fields

### Responsibilities

Allow organizations to extend entities without changing application code.

Phase 1 supports approximately 15 configurable custom fields per supported entity.

---

# Future Modules

These modules are planned for future phases.

---

## Client Portal

- Project Progress
- Deliverables
- Client Reviews
- Downloads
- Communication

---

## Vendor Portal

- Outsourced Work
- Deliverables
- External Communication

---

## Mobile Application

- Android
- iOS
- Push Notifications
- Offline Support

---

## Integration Hub

- REST APIs
- Webhooks
- ERP Integration
- HR Integration
- Identity Providers

---

## AI Services

Future AI capabilities include:

- AI Project Manager
- AI Resource Planner
- AI Review Assistant
- AI Reporting Assistant
- AI Business Analyst
- AI Knowledge Assistant

---

# Module Dependency Overview

```text
Client
    │
    ▼
Project
    │
    ▼
Batch
    │
    ▼
Asset
    │
    ▼
Task
    │
    ▼
Subtask
    │
    ▼
Workflow
    │
    ▼
Reviews
    │
    ▼
Deliverable
    │
    ▼
Finance
```

Supporting every module:

- Security
- Notifications
- Communication
- Reporting
- Audit
- Search
- Tags
- Custom Fields

---

# Cross-Cutting Features

The following capabilities are shared across multiple modules:

- Role-Based Security
- Workflow Engine
- Activity Timeline
- Audit Logging
- Notifications
- Attachments
- Rich Text Comments
- Search
- Tags
- Custom Fields
- APIs
- Reporting

---

# Module Documentation

Each module described here has a dedicated specification under the **03-Modules** section, including:

- Business Purpose
- Functional Requirements
- Business Rules
- UI Screens
- Workflows
- Database Design
- APIs
- Permissions
- Reports
- Future Enhancements

---

# Related Documents

- ProductOverview.md
- ProductArchitecture.md
- ProductPrinciples.md
- 02-Domain/*
- 03-Modules/*
- 04-Workflow/*
- 06-Database/*
- 07-API/*

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Product Modules Overview |
