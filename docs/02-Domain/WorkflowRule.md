# Workflow Rules

> **Purpose**
>
> Workflow Rules define the configurable business logic executed by the Workflow Engine during Task lifecycle events.
>
> Instead of embedding business logic in application code, Workflow Rules allow administrators to configure validations, approvals, automation, notifications, and review behavior without modifying the system.
>
> Workflow Rules are the heart of the configurable Workflow Engine.

---

# Overview

A Workflow consists of:

```text
Workflow
    │
    ├── Process
    ├── State
    ├── Transition
    └── Rules
```

Whenever a Transition is executed, the Workflow Engine evaluates every applicable Rule before allowing the Task to proceed.

---

# Objectives

Workflow Rules provide:

- Configurable business logic
- Validation without coding
- Flexible workflow behavior
- Production standardization
- Organization-specific customization
- Future no-code workflow configuration

---

# Rule Categories

Workflow Rules are grouped into the following categories.

## Validation Rules

Determine whether a Transition is allowed.

Examples:

- All mandatory SubTasks completed
- Deliverable uploaded
- Repository path provided
- Changeset entered
- Comments required
- Attachments required

---

## Permission Rules

Determine who can execute a Transition.

Examples

- Artist
- Team Lead
- Project Manager
- Reviewer
- QC
- Client

---

## Automation Rules

Automatically perform system actions.

Examples

- Send notification
- Create activity log
- Create review record
- Create feedback
- Increment review round
- Generate deliverable version

---

## Review Rules

Configure review behavior.

Examples

- WIP Review required
- Lead Review mandatory
- FR Review enabled
- QC enabled
- Client Review enabled

---

## Transition Rules

Control movement between States.

Examples

```text
Production

↓

Lead Review
```

Allowed

```text
Lead Review

↓

Completed
```

Not Allowed

---

## Deliverable Rules

Control production file submission.

Examples

- Repository required
- File path mandatory
- Version required
- Change Number required

---

## Notification Rules

Automatically notify users.

Examples

- Email
- In-App
- Teams
- Slack
- Webhook

---

## SLA Rules

Examples

- Review within 24 Hours
- QC within 12 Hours
- Client Review within 5 Days

---

# Rule Evaluation Order

The engine evaluates Rules in a predictable order.

```text
User Action

↓

Permission Rules

↓

Validation Rules

↓

Business Rules

↓

Automation Rules

↓

Notification Rules

↓

Audit

↓

Transition Complete
```

---

# Rule Scope

Rules may be applied at different levels.

| Scope | Description |
|---------|-------------|
| Workflow | Entire Workflow |
| Process | Specific Process |
| State | Specific State |
| Transition | Specific Transition |
| Task Type | Specific Task Category |
| Batch Stage | Specific Batch Stage |

---

# Validation Examples

## Example 1

Submit for Lead Review

Requirements

- All General SubTasks Closed
- Deliverables Uploaded
- Repository Path Present

---

## Example 2

Submit to Client

Requirements

- QC Passed
- Final Review Approved
- Version Tagged

---

## Example 3

Close Task

Requirements

- Workflow Complete
- Client Approved
- All Review Records Closed

---

# Review Rules

## Minor Fix

```text
Review

↓

Minor Fix

↓

Create Feedback

↓

Lead Creates New SubTasks

↓

Return Production
```

---

## Major Fix

```text
Review

↓

Major Fix

↓

Increase Review Round

↓

Lead Creates New SubTasks

↓

Production

↓

Review Again
```

---

# Business Rules

Examples

### BR-001

Task cannot enter Lead Review until mandatory General SubTasks are completed.

---

### BR-002

Final Review cannot begin until Lead Review is approved.

---

### BR-003

Client Review cannot begin until QC has passed.

---

### BR-004

Minor Fix does not require repeating the same review stage unless configured.

---

### BR-005

Major Fix always starts a new review round.

---

### BR-006

Completed Tasks cannot be modified.

---

### BR-007

Discarded SubTasks remain in history.

---

### BR-008

Reviewers cannot create SubTasks.

Only Team Leads or Project Managers may create implementation SubTasks.

---

### BR-009

A Task may have multiple active Artists through SubTasks.

---

### BR-010

Every Rule execution must generate an Audit Log entry.

---

# Rule Priority

Rules execute in priority order.

| Priority | Purpose |
|----------|----------|
| 1 | Permission |
| 2 | Validation |
| 3 | Business |
| 4 | Automation |
| 5 | Notification |

---

# Rule Configuration

Typical properties include:

- Rule Name
- Rule Type
- Description
- Enabled
- Priority
- Workflow
- Process
- State
- Transition
- Error Message

---

# Rule Failure

If any mandatory Rule fails:

```text
Validation Failed

↓

Rollback

↓

Display Error

↓

Remain In Current State
```

No workflow data is modified.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| RuleId | Primary Key |
| WorkflowId | Parent Workflow |
| TransitionId | Related Transition |
| RuleType | Validation / Permission / Automation |
| Name | Rule Name |
| Priority | Execution Order |
| IsMandatory | Boolean |
| IsEnabled | Boolean |
| ErrorMessage | User Message |

---

# Reporting

Typical reports include:

- Rule Execution History
- Validation Failures
- Permission Denials
- Workflow Errors
- Rule Usage
- SLA Violations

---

# Future Enhancements

Future releases may include:

- Expression Builder
- No-Code Rule Designer
- JavaScript/C# Script Rules
- AI Rule Recommendation
- Rule Templates
- Dynamic Rule Engine
- Rule Testing Sandbox
- Rule Version Comparison

---

# Design Principles

The Workflow Rule Engine follows these principles:

- Business logic must be configuration-driven.
- Rules should be reusable across Workflows.
- Rule execution must be deterministic.
- Rules must be independently versioned with the Workflow.
- Validation occurs before automation.
- Every Rule execution is fully auditable.
- Rules should minimize hard-coded workflow behavior.

---

# Related Documents

- Workflow.md
- WorkflowTransition.md
- WorkflowValidation.md
- WorkflowPermission.md
- WorkflowAutomation.md
- WorkflowNotification.md
- WorkflowEvent.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow Rule specification |
