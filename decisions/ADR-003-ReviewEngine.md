# ADR-003: Review & Approval Engine Architecture

**ADR ID:** ADR-003

**Title:** Centralized Review & Approval Engine

**Status:** Accepted

**Date:** 2026-07-26

**Decision Makers:**

- Solution Architect
- Product Owner
- Technical Architect
- Production Team
- QA Team

---

# Context

The platform manages work that requires formal reviews before completion.

Examples include

- Creative Asset Review
- Source Code Review
- Document Review
- Design Approval
- QA Verification
- Client Approval
- Financial Approval
- AI Generated Content Review

Most enterprise project management systems implement reviews differently across modules, resulting in inconsistent approval processes, duplicated logic, and limited reporting.

The platform requires a reusable review engine that can support every module while maintaining complete traceability and audit history.

---

# Problem Statement

Embedding review logic directly into modules introduces several issues:

- Duplicate approval logic
- Different review behaviors
- Difficult maintenance
- Poor reporting
- Limited configurability
- Weak audit trails
- Difficult AI integration

A centralized review engine is required to standardize the review lifecycle.

---

# Decision

The platform will implement a **centralized Review & Approval Engine** responsible for managing all review processes regardless of business domain.

Business modules will create review requests and delegate review management to the engine.

The Review Engine will manage:

- Review Requests
- Review Rounds
- Review Assignments
- Comments
- Markups
- Decisions
- Approval Rules
- Escalations
- Notifications
- Audit History

---

# Architectural Principles

The Review Engine follows

- Separation of Concerns
- Metadata Driven Design
- Workflow Integration
- Immutable Review History
- Human-in-the-Loop Validation
- AI-Assisted Review
- Event Driven Architecture

---

# High-Level Architecture

```text
Business Module

        │

Create Review

        │

        ▼

Review Engine

        │

Review Assignment

        │

Reviewer Actions

        │

Decision

        │

Workflow Engine

        │

Business Module
```

---

# Supported Review Types

The engine supports

- Technical Review
- Creative Review
- QA Review
- Security Review
- Architecture Review
- Financial Approval
- Legal Review
- Client Review
- AI Validation Review
- Final Delivery Review

New review types can be added without code changes.

---

# Core Components

The Review Engine consists of

- Review Definition
- Review Instance
- Review Round
- Reviewer Assignment
- Review Comment
- Review Decision
- Review Attachment
- Review Markup
- Review Checklist
- Review History

---

# Review Lifecycle

A standard review follows

```text
Draft

↓

Submitted

↓

Assigned

↓

In Review

↓

Approved

↓

Completed
```

Alternative path

```text
In Review

↓

Changes Requested

↓

Rework

↓

Resubmitted

↓

Review
```

---

# Review Rounds

A review may contain multiple iterations.

Example

```text
Round 1

↓

Changes Requested

↓

Round 2

↓

Changes Requested

↓

Round 3

↓

Approved
```

Every round is preserved permanently.

---

# Reviewer Assignment

Reviewers may be assigned

- Manually
- Automatically
- By Department
- By Team
- By Role
- By Workflow Rule
- By AI Recommendation

---

# Review Modes

Supported modes

## Single Reviewer

One reviewer makes the decision.

---

## Parallel Review

Multiple reviewers evaluate simultaneously.

---

## Sequential Review

Reviewer B receives the item only after Reviewer A completes.

---

## Consensus Review

All reviewers must approve.

---

## Majority Review

Approval requires a configurable percentage.

Example

```text
5 Reviewers

↓

3 Approvals

↓

Approved
```

---

# Review Decisions

Supported decisions

- Approve
- Reject
- Request Changes
- Approve with Comments
- Escalate
- Delegate
- Cancel Review

---

# Review Comments

Supports

- Rich Text
- Markdown
- Images
- Attachments
- Hyperlinks
- Code Snippets
- Threaded Discussions

Every comment is timestamped.

---

# Asset Markup

For documents, images, videos and design assets.

Supports

- Drawing
- Highlighting
- Pin Comments
- Bounding Boxes
- Shapes
- Region Selection
- Timeline Comments (Video)

---

# Review Checklists

Review templates may include checklists.

Example

```text
✓ Naming Standards

✓ Coding Standards

✓ Documentation

✓ Security

✓ Performance

✓ Accessibility
```

---

# Workflow Integration

The Review Engine integrates with the Workflow Engine.

Example

```text
Task

↓

Ready for Review

↓

Review Engine

↓

Approved

↓

Workflow Continues
```

Modules never implement approval logic themselves.

---

# AI Integration

The Review Engine includes AI-assisted capabilities.

---

## AI Pre-Review

AI analyzes submissions before humans review them.

Checks include

- Missing Information
- Quality Issues
- Formatting
- Compliance
- Best Practices

---

## AI Review Assistant

Suggests

- Potential Issues
- Missing Requirements
- Risk Areas
- Similar Previous Reviews

---

## AI Reviewer

For supported scenarios, AI may perform an initial review and produce recommendations.

Human approval remains mandatory where configured.

---

## AI Summary

Automatically generates

- Review Summary
- Changes Requested
- Risk Assessment
- Suggested Decision

---

# SLA Management

Each review type defines

- Review Deadline
- Reminder Interval
- Escalation Time

Example

```text
Review Assigned

↓

24 Hours

↓

Reminder

↓

48 Hours

↓

Escalation
```

---

# Escalation

Escalation actions include

- Notify Reviewer
- Notify Manager
- Reassign Reviewer
- Escalate to Team Lead
- Trigger Workflow Escalation

---

# Audit Trail

Every review action is recorded.

Stored information

- Reviewer
- Timestamp
- Decision
- Comments
- Attachments
- Review Round
- Previous State
- Current State

History cannot be modified.

---

# Notifications

Generated events

- Review Assigned
- Review Started
- Comment Added
- Review Completed
- Changes Requested
- Review Approved
- Review Rejected
- SLA Warning
- Escalation Triggered

Channels

- Email
- In-App
- Microsoft Teams
- Slack
- Mobile Push

---

# Functional Requirements

Users shall be able to

- Submit reviews.
- Assign reviewers.
- Add comments.
- Upload attachments.
- Annotate assets.
- Approve submissions.
- Reject submissions.
- Request changes.
- View review history.
- Compare review rounds.

Administrators shall be able to

- Configure review templates.
- Configure approval rules.
- Configure reviewer assignment.
- Configure SLAs.
- Configure escalation rules.

---

# Database Entities

Primary entities include

- ReviewDefinition
- ReviewInstance
- ReviewRound
- ReviewerAssignment
- ReviewDecision
- ReviewComment
- ReviewAttachment
- ReviewMarkup
- ReviewChecklist
- ReviewHistory

---

# APIs

Representative endpoints

```http
GET    /api/reviews

POST   /api/reviews

GET    /api/reviews/{id}

POST   /api/reviews/{id}/assign

POST   /api/reviews/{id}/approve

POST   /api/reviews/{id}/reject

POST   /api/reviews/{id}/requestchanges

POST   /api/reviews/{id}/comments

GET    /api/reviews/{id}/history
```

---

# Reporting

Available reports

- Review Cycle Time
- Average Review Duration
- Reviewer Productivity
- Approval Rate
- Rejection Rate
- Review Backlog
- SLA Compliance
- AI Recommendation Accuracy
- Review Round Statistics

---

# Security

Supports

- Role-Based Access Control
- Reviewer Permissions
- Client Visibility Rules
- Immutable Review History
- Secure Attachments
- Audit Logging
- Tenant Isolation

---

# Performance Requirements

- Review creation < 1 second
- Reviewer assignment < 500 ms
- Comment posting < 300 ms
- Annotation rendering < 1 second
- Support millions of reviews
- Asynchronous notification delivery

---

# Alternatives Considered

## Module-Specific Review Logic

Rejected because

- Duplicate implementation
- Inconsistent behavior
- Difficult maintenance
- Limited reporting

---

## External Review Platform

Rejected because

- Integration complexity
- Additional licensing costs
- Poor workflow integration
- Limited customization

---

## Simple Approval Status Field

Rejected because

- No history
- No review rounds
- No comments
- No SLA support
- No auditability

---

# Consequences

## Positive

- Consistent review process across the platform.
- Reusable approval mechanism.
- Complete audit trail.
- AI-assisted quality improvements.
- Rich reporting and analytics.
- Supports future expansion.

## Negative

- Higher implementation complexity.
- Additional metadata management.
- Requires careful governance of review templates.

---

# Future Evolution

The Review Engine is designed to support

- Real-time collaborative reviews
- Video timeline annotations
- 3D asset reviews
- BIM/CAD review support
- AI automatic approvals (configurable)
- Machine Learning quality scoring
- Digital signatures
- Electronic approval certificates
- External client review portals

---

# Decision Summary

The platform adopts a **centralized Review & Approval Engine** that standardizes all review processes across business modules. It provides configurable review workflows, multi-round approvals, annotations, AI-assisted recommendations, SLA monitoring, and immutable audit history while remaining fully integrated with the Workflow Engine and overall platform architecture.
