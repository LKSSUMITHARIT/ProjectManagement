# Review Workflow

> **Purpose**
>
> The Review Workflow governs how production deliverables are reviewed, approved, rejected, and returned for corrections throughout the asset production lifecycle.
>
> Unlike traditional task management systems, reviews are independent workflow stages with their own lifecycle, permissions, review rounds, feedback management, and audit history.
>
> A Review never directly modifies production work. Instead, it generates structured Feedback Items, which are converted into implementation SubTasks by the Team Lead or Project Manager.

---

# Overview

The Review Workflow ensures production quality before deliverables progress to the next stage.

Typical Review Stages include:

- WIP Review (Optional)
- Lead Review
- Final Review (FR)
- Quality Control (QC)
- Client Review

Each stage may be enabled or disabled independently.

---

# Objectives

The Review Workflow provides:

- Multi-stage review process
- Review history
- Unlimited review rounds
- Structured feedback
- Separation of review and implementation
- Audit compliance
- Quality assurance
- Client collaboration

---

# Review Architecture

```text
Production

↓

Review Request

↓

Review Assignment

↓

Review

↓

Decision

↓

Approved

OR

Feedback

↓

Production
```

---

# Review Types

## Work In Progress (WIP)

Purpose

Early quality check before completion.

Typical Reviewer

- Senior Artist
- Team Lead

---

## Lead Review

Purpose

Internal approval before Final Review.

Reviewer

- Team Lead

---

## Final Review (FR)

Purpose

Creative and technical approval.

Reviewer

- Final Reviewer

Output

- Approved
- Minor Fix
- Major Fix

---

## Quality Control (QC)

Purpose

Technical validation.

Examples

- Naming
- File Format
- Packaging
- Export Validation

---

## Client Review

Purpose

Customer approval.

Possible outcomes

- Approved
- Minor Fix
- Major Fix

---

# Review Lifecycle

```text
Review Requested

↓

Waiting

↓

Assigned

↓

In Review

↓

Decision

↓

Completed
```

---

# Review Status

Possible Review Status values:

- Waiting
- Assigned
- In Progress
- Approved
- Minor Fix
- Major Fix
- Rejected
- Cancelled
- Completed

---

# Review Decisions

A reviewer may choose:

## Approve

Task proceeds to next Process.

---

## Minor Fix

Creates Feedback Items.

Lead creates FR/Client Fix SubTasks.

Workflow returns to Production.

Review Round remains linked.

---

## Major Fix

Creates Feedback Items.

Creates new Review Round.

Returns to Production.

Entire Review repeats.

---

## Reject

Terminates Review.

Returns Task.

Requires comments.

---

# Review Assignment

A Review may be assigned to:

- Individual Reviewer
- Reviewer Group
- Client
- QC Team

Assignments are tracked separately from Task ownership.

---

# Feedback Generation

A Review generates Feedback Items.

Example

```text
Review

↓

Feedback Item

↓

Lead Review

↓

Create SubTasks

↓

Artists
```

Reviewers never assign Artists directly.

---

# Review Rounds

Unlimited review rounds are supported.

Example

```text
Round 1

↓

Minor Fix

↓

Production

↓

Round 2

↓

Major Fix

↓

Production

↓

Round 3

↓

Approved
```

Each round stores:

- Round Number
- Reviewer
- Decision
- Date
- Feedback

---

# Review Attachments

Each Review may contain:

- Images
- Videos
- Documents
- Reference Files
- Markups
- Screen Recordings

---

# Review Comments

Supports:

- Rich Text
- Markdown (Future)
- Image Annotation (Future)
- File Attachments
- Mentions

---

# Review Notifications

Automatic notifications are sent when:

- Review Requested
- Reviewer Assigned
- Decision Recorded
- Feedback Created
- Review Completed

---

# Review Audit

Every Review records:

- Reviewer
- Assignment
- Decision
- Time
- Comments
- Attachments
- Round
- Previous Decision

Review history is immutable.

---

# Business Rules

## BR-001

Every Review belongs to one Task.

---

## BR-002

Reviews never directly create SubTasks.

---

## BR-003

Only Team Leads or Project Managers create implementation SubTasks.

---

## BR-004

Unlimited Review Rounds are supported.

---

## BR-005

Each Review Round maintains its own history.

---

## BR-006

Minor Fix and Major Fix always generate Feedback Items.

---

## BR-007

Approved Reviews cannot be modified.

---

## BR-008

Review history cannot be deleted.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| ReviewId | Primary Key |
| TaskId | Parent Task |
| ReviewType | WIP / Lead / FR / QC / Client |
| ReviewRound | Round Number |
| ReviewerId | Assigned Reviewer |
| Status | Current Status |
| Decision | Final Decision |
| RequestedOn | Date Requested |
| CompletedOn | Completion Date |

---

# Reporting

Typical reports include:

- Review Turnaround Time
- Average Review Duration
- Review Round Analysis
- Approval Rate
- Rejection Rate
- Reviewer Productivity
- Feedback Volume
- Client Revision Analysis

---

# Future Enhancements

Future versions may include:

- AI Pre-Review
- AI Image Comparison
- Annotation Tools
- Video Timeline Comments
- Automated Review Assignment
- Review Templates
- Parallel Reviews
- Review Checklists

---

# Design Principles

The Review Workflow follows these principles:

- Reviews are independent workflow entities.
- Reviews generate Feedback, not implementation work.
- Feedback implementation is managed by Leads.
- Review history is immutable.
- Unlimited review rounds are supported.
- Review outcomes are fully auditable.
- Reviews integrate seamlessly with the Workflow Engine.

---

# Related Documents

- Workflow.md
- WorkflowProcess.md
- WorkflowState.md
- FeedbackWorkflow.md
- ReviewRounds.md
- Task.md
- SubTask.md
- WorkflowTransition.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Review Workflow specification |
