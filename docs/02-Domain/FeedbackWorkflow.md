# Feedback Workflow

> **Purpose**
>
> The Feedback Workflow defines how review observations, comments, defects, suggestions, and client requests are captured, managed, implemented, and verified throughout the production lifecycle.
>
> Feedback is an independent business entity that bridges the gap between Review and Production.
>
> Reviewers never create implementation work directly. Instead, they create Feedback Items that are later analyzed and converted into one or more SubTasks by the Team Lead or Project Manager.

---

# Overview

Feedback represents work that needs to be performed following a review.

Feedback exists independently from:

- Reviews
- SubTasks
- Deliverables
- Workflow State

One Review may generate multiple Feedback Items.

One Feedback Item may generate multiple SubTasks.

Multiple Feedback Items may also be resolved by a single SubTask.

---

# Objectives

The Feedback Workflow provides:

- Structured review observations
- Separation of review and implementation
- Feedback traceability
- Unlimited review rounds
- Implementation tracking
- Audit history
- Client communication
- Analytics

---

# Architecture

```text
Review

↓

Feedback

↓

Lead Analysis

↓

SubTask Creation

↓

Production

↓

Verification

↓

Resolved
```

---

# Feedback Sources

Feedback may originate from:

- WIP Review
- Lead Review
- Final Review
- QC Review
- Client Review
- Internal Audit
- Production Team
- AI Review (Future)

---

# Feedback Lifecycle

```text
Created

↓

Open

↓

Analyzed

↓

Mapped to SubTasks

↓

In Progress

↓

Implemented

↓

Verified

↓

Closed
```

---

# Feedback Status

| Status | Description |
|----------|-------------|
| Open | Newly created |
| Under Analysis | Lead reviewing feedback |
| Planned | SubTasks created |
| In Progress | Implementation started |
| Waiting Verification | Ready for review |
| Resolved | Verified |
| Closed | Completed |
| Rejected | Invalid feedback |
| Cancelled | No longer required |

---

# Feedback Types

Examples

- Visual
- Animation
- Modeling
- Texture
- Rigging
- Lighting
- Rendering
- Documentation
- Technical
- Client Request
- Enhancement
- Quality
- Performance
- Compliance

---

# Feedback Severity

Suggested values

- Critical
- High
- Medium
- Low
- Suggestion

Severity helps prioritize implementation.

---

# Feedback Priority

Possible values

- Urgent
- High
- Medium
- Low

Priority may differ from Severity.

---

# Feedback Creation

Feedback is created during Reviews.

Example

```text
Reviewer

↓

Adds Feedback

↓

Feedback Item Created

↓

Assigned to Lead

↓

Review Completed
```

Feedback is **never assigned directly to Artists**.

---

# Lead Analysis

The Team Lead (or Project Manager):

- Reviews Feedback
- Groups similar Feedback
- Splits large Feedback
- Merges duplicate Feedback
- Decides implementation strategy
- Creates SubTasks

---

# Feedback to SubTask Mapping

One Feedback Item

↓

Multiple SubTasks

```text
Feedback

Improve Character Armor

↓

Model Update

↓

Texture Update

↓

Material Update
```

---

Multiple Feedback Items

↓

Single SubTask

```text
Feedback

Fix Eye

Improve Face

Correct Nose

↓

SubTask

Face Refinement
```

---

# Feedback Categories

Each Feedback may belong to:

- Functional
- Artistic
- Technical
- Client Change
- Pipeline
- Documentation

---

# Review Round Association

Every Feedback belongs to a Review Round.

Example

```text
Round 1

↓

Feedback 001

Feedback 002

Feedback 003
```

Round 2 creates new Feedback Items.

Existing Feedback history remains unchanged.

---

# Attachments

Feedback may include:

- Images
- Videos
- PDFs
- Drawings
- Screenshots
- Reference Assets
- Audio Notes

---

# Rich Text Support

Feedback supports:

- Rich Text
- Bullet Lists
- Hyperlinks
- Tables
- Code Blocks
- Mentions

Future

- Image Annotation
- Video Timeline Comments

---

# Implementation Tracking

Each Feedback records:

- Number of SubTasks
- Completion Percentage
- Remaining Work
- Verification Status

---

# Verification

After implementation

```text
Feedback

↓

Implemented

↓

Review

↓

Verified

↓

Closed
```

If verification fails

↓

New Feedback

↓

Next Review Round

---

# Traceability

The system maintains complete traceability.

```text
Review

↓

Feedback

↓

SubTask

↓

Deliverable Version

↓

Review

↓

Approval
```

---

# Notifications

Notifications are generated when:

- Feedback Created
- Feedback Assigned
- Feedback Implemented
- Feedback Verified
- Feedback Closed

---

# Audit

Every Feedback records:

- Created By
- Review
- Review Round
- Comments
- Attachments
- Status Changes
- Linked SubTasks
- Verification

History is immutable.

---

# Business Rules

## BR-001

Feedback belongs to exactly one Review.

---

## BR-002

Feedback belongs to exactly one Review Round.

---

## BR-003

Reviewers never assign implementation work.

---

## BR-004

Only Team Leads or Project Managers create implementation SubTasks.

---

## BR-005

One Feedback may generate multiple SubTasks.

---

## BR-006

One SubTask may resolve multiple Feedback Items.

---

## BR-007

Closed Feedback cannot be modified.

---

## BR-008

Feedback history is immutable.

---

## BR-009

Every Feedback must be linked to at least one Review.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| FeedbackId | Primary Key |
| ReviewId | Parent Review |
| ReviewRound | Review Round |
| FeedbackType | Visual / Technical / Client |
| Severity | Critical / High / Medium / Low |
| Priority | High / Medium / Low |
| Status | Current Status |
| Title | Summary |
| Description | Rich Text |
| CreatedBy | Reviewer |
| CreatedOn | Date |
| VerifiedOn | Date |

---

# Reporting

Typical reports include:

- Feedback by Reviewer
- Feedback by Project
- Feedback by Asset
- Feedback by Severity
- Average Resolution Time
- Open Feedback
- Reopened Feedback
- Client Change Requests
- Feedback Trend Analysis

---

# Future Enhancements

Future releases may include:

- AI Feedback Grouping
- AI Duplicate Detection
- AI Suggested SubTasks
- Image Annotation
- Video Annotation
- Voice Feedback
- OCR Integration
- Smart Priority Recommendation

---

# Design Principles

The Feedback Workflow follows these principles:

- Feedback is independent of implementation.
- Feedback is a business entity, not a comment.
- Implementation responsibility belongs to Leads and Project Managers.
- Complete traceability is maintained from Review to Deliverable.
- Unlimited review rounds are supported.
- Feedback history is immutable.
- Feedback drives production improvements while preserving review integrity.

---

# Related Documents

- ReviewWorkflow.md
- ReviewRounds.md
- Workflow.md
- Task.md
- SubTask.md
- DeliverableManagement.md
- WorkflowTransition.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Feedback Workflow specification |
