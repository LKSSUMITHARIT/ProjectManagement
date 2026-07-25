# Frequently Asked Questions (FAQ)

> **Purpose**
>
> This document answers common questions about the Project Management Platform. It provides a high-level understanding of the product, its architecture, design decisions, scope, and future direction.

---

# General Questions

## What is the Project Management Platform?

The Project Management Platform is an enterprise-grade **Production Management System** designed to manage the complete lifecycle of production projects.

Unlike traditional project management tools, it understands production concepts such as:

- Clients
- Projects
- Batches
- Assets
- Tasks
- Subtasks
- Reviews
- Deliverables
- Resource Allocation
- Production Workflows

---

## Is this another Jira or Azure DevOps?

No.

While the platform shares some concepts with Jira and Azure DevOps, its primary focus is **production management**, not software issue tracking.

The platform is designed specifically for industries where production work moves through multiple review stages before delivery.

---

## Which industries can use this platform?

The platform is designed to be configurable and can support:

- Game Development
- Game Art Outsourcing
- Animation
- VFX
- Architecture Visualization
- Creative Agencies
- Digital Production Studios
- Engineering Design Teams
- Software Teams (with custom workflows)

---

## Why build a new platform instead of using Jira?

Generic project management tools primarily manage issues and tickets.

This platform manages complete production workflows including:

- Batch Planning
- Asset Production
- Resource Allocation
- Review Cycles
- Client Approvals
- Deliverables
- Financial Tracking
- Production Analytics

These capabilities require a domain-specific production model rather than generic issue tracking.

---

# Product Questions

## What is the primary goal of the platform?

To provide a single system that manages:

- Planning
- Production
- Reviews
- Delivery
- Communication
- Finance
- Reporting
- Operational Intelligence

---

## Is the platform workflow driven?

Yes.

Every production activity is controlled through configurable workflows consisting of:

- Workflow
- Process
- State
- Transition Rules
- Permissions

Business logic is driven by workflows rather than hardcoded application logic.

---

## Can workflows be customized?

Yes.

Organizations can configure:

- Workflows
- Processes
- States
- Transition Rules
- Notifications
- Review Stages
- Custom Fields
- Tags

without changing application code.

---

## Can different projects use different workflows?

Yes.

Each Batch Stage can reference a different Workflow, allowing projects to support different production pipelines while using the same platform.

---

# Production Questions

## What is a Batch?

A Batch is a logical production group within a Project.

It contains:

- Assets
- Team Members
- Workflow Configuration
- Resource Allocation
- Production Schedule

---

## Why use Assets?

Assets represent the actual production deliverables.

Examples include:

- Character
- Vehicle
- Environment
- Animation
- UI Screen
- Prop
- Weapon

Tasks are performed on Assets.

---

## Can an Asset have multiple Tasks?

Yes.

Each Asset can contain one or more Tasks depending on the production pipeline.

---

## Can a Task have multiple Artists?

Not directly.

A Task is executed through one or more **Subtasks**, and each Subtask is assigned to a single Artist.

This allows multiple Artists to collaborate on the same Task while maintaining clear ownership.

---

## Can a Subtask be reassigned?

No.

Once assigned, a Subtask cannot be reassigned.

If ownership changes:

1. The existing Subtask is discarded or closed.
2. A new Subtask is created.
3. The new Subtask is assigned to the new Artist.

This preserves production history and accountability.

---

## What Subtask types are supported?

Phase 1 supports:

- General
- Final Review Fix
- Client Fix

Additional types may be introduced in future releases.

---

## What are Review Rounds?

Every time a review requests changes, a new Review Round is created.

All Subtasks generated from that feedback belong to the same Round Number.

This allows complete traceability of the review history.

---

# Workflow Questions

## What is the difference between Workflow, Process, and State?

### Workflow

Defines the complete lifecycle of a Task.

Example:

```
Game Asset Workflow
```

---

### Process

Represents a major business stage.

Examples:

- Production
- WIP Review
- Final Review
- QC
- Client Review
- Closed

---

### State

Represents the current condition within a Process.

Example:

```
Process:
Final Review

States:
Waiting
Under Review
Approved
Rejected
```

---

## Why separate Process and State?

This allows:

- Cleaner Kanban Boards
- Better reporting
- Simpler workflow visualization
- More flexible workflow configuration

The Kanban board uses **Process** as swimlanes or columns, while **State** provides finer operational detail.

---

# Review Questions

## What review stages are supported?

The production workflow supports:

- WIP Review
- Final Review
- Quality Control (QC)
- Client Review

Each stage can be enabled or disabled depending on the workflow configuration.

---

## Is WIP Review mandatory?

No.

A Workflow may choose whether WIP Review is included.

---

## Does every project require QC?

No.

QC is configurable and can be omitted for workflows that do not require it.

---

## What happens when Final Review requests changes?

The reviewer provides feedback only.

The Lead or Project Manager then converts that feedback into one or more new **Final Review Fix Subtasks**.

The reviewer does not create production subtasks directly.

---

## What happens when the Client requests changes?

The process is similar to Final Review.

The Client provides feedback.

The Lead or Project Manager analyzes the feedback and creates the required **Client Fix Subtasks**.

---

## Why don't reviewers create subtasks directly?

Reviewers evaluate quality.

Leads understand:

- Work distribution
- Artist ownership
- Production planning
- Task decomposition

Separating feedback from execution improves production management and accountability.

---

# Resource Management Questions

## Can a Resource work on multiple Batches?

Yes.

Resources may be allocated across multiple Batches simultaneously.

Allocations are managed using percentages and require approval through the Resource Allocation workflow.

---

## How are allocations approved?

1. Batch Manager requests allocation.
2. Resource Manager reviews availability.
3. Allocation is approved or rejected.
4. Approved allocation becomes active.

---

## Can allocation exceed 100%?

This depends on organization policy.

The platform can highlight overallocation, but the business may choose whether to allow it.

---

# Deliverable Questions

## Does the platform store production files?

No.

Production files remain in external repositories such as:

- Git
- Perforce
- SVN
- Cloud Storage

The platform stores metadata and references only.

---

## What information is stored for a Deliverable?

Examples include:

- Repository
- Branch
- File Path
- Version
- Changeset
- Delivery Date
- Workflow Transition

---

# Finance Questions

## Are invoices generated against Clients?

Invoices are **issued to Clients** but are **created against Projects**.

Each Project belongs to a Client, allowing project-level billing while maintaining client-level financial reporting.

---

## Can invoices be partially settled?

Yes.

Outstanding balances can be reduced through:

- Payments
- Approved Discounts
- Approved Waivers

Each adjustment is recorded for audit purposes.

---

# Reporting Questions

## What dashboards are available?

Phase 1 includes:

- Executive Dashboard
- Project Dashboard
- Batch Dashboard
- Resource Dashboard
- Finance Dashboard

Additional dashboards will be added in future releases.

---

## Can reports be customized?

Yes.

The reporting framework is designed to support configurable filters, saved views, and custom dashboards.

Advanced report designers are planned for future phases.

---

# Security Questions

## Does the platform support Role-Based Access Control?

Yes.

Permissions are assigned through roles, allowing organizations to control access to modules, entities, and business operations.

---

## Is every action audited?

Yes.

Important business events—including workflow transitions, assignments, reviews, comments, approvals, and financial changes—are recorded in the activity and audit logs.

---

# AI Questions

## Will AI replace Project Managers?

No.

AI is designed to assist users by providing recommendations, analytics, and automation.

Business ownership and approvals remain with human users.

---

## What AI capabilities are planned?

Future AI features include:

- AI Project Manager
- AI Resource Planner
- AI Production Assistant
- AI Review Assistant
- AI Business Analyst
- AI Reporting Assistant
- Predictive Scheduling
- Risk Detection

---

# Technical Questions

## Is the platform cloud-only?

No.

The architecture is designed to support:

- Cloud Deployment
- On-Premises Deployment
- Hybrid Deployment

---

## Is the platform API-first?

Yes.

All business capabilities are intended to be accessible through APIs, enabling integrations, mobile applications, automation, and AI agents.

---

## Will mobile applications be available?

Yes.

Native Android and iOS applications are planned as part of a future release.

---

# Future Questions

## What major features are planned after Phase 1?

Future releases include:

- Visual Workflow Designer
- AI Agents
- Client Portal
- Plugin Marketplace
- Mobile Applications
- Advanced Analytics
- Workflow Automation
- Production Forecasting
- Enterprise Integrations

---

# Where can I learn more?

Refer to the following documents:

- Vision.md
- ProblemStatement.md
- BusinessObjectives.md
- ProductGoals.md
- ProductScope.md
- ProductRoadmap.md
- ProductPrinciples.md
- SuccessMetrics.md
- Glossary.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial FAQ |
