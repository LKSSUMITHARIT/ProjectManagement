# Workflow Validation

> **Purpose**
>
> Workflow Validation defines the business conditions that must be satisfied before a Workflow Transition (Workflow Action) can be successfully executed.
>
> Validation ensures that Tasks move through the workflow only when all required business, production, review, and quality conditions are met.
>
> The validation engine is completely configuration-driven and independent of application code.

---

# Overview

Every Workflow Action executes a Validation Pipeline before performing the Transition.

```text
User Action

↓

Permission Validation

↓

Workflow Validation

↓

Business Validation

↓

Execute Transition

↓

Automation
```

If any validation fails, the Transition is rejected.

---

# Objectives

The Validation Engine provides:

- Business Rule Enforcement
- Production Quality Assurance
- Review Integrity
- Data Consistency
- Deliverable Verification
- Source Control Validation
- Workflow Integrity

---

# Validation Architecture

```text
Workflow Action
        │
        ▼
Validation Engine
        │
 ├── Required Fields
 ├── Workflow Validation
 ├── Business Validation
 ├── Review Validation
 ├── Deliverable Validation
 ├── Source Control Validation
 ├── Dependency Validation
 └── Custom Validation
```

---

# Validation Categories

Workflow Validation consists of several categories.

---

## 1. Required Field Validation

Ensures mandatory information exists.

Examples

- Title
- Description
- Due Date
- Assigned Lead
- Priority
- Workflow

---

## 2. Workflow Validation

Ensures workflow consistency.

Examples

- Valid Current State
- Transition Exists
- Workflow Active
- Workflow Version Valid

---

## 3. SubTask Validation

Examples

- General SubTasks Completed
- Mandatory SubTasks Completed
- No Active Blocking SubTask
- Required SubTask Types Exist

Example

```text
Submit To Lead Review

↓

All General SubTasks

Status = Closed
```

---

## 4. Deliverable Validation

Examples

- Deliverable Uploaded
- Version Exists
- Repository Path Present
- File Linked
- Mandatory File Type Uploaded

---

## 5. Source Control Validation

Examples

- Repository Selected
- Branch Exists
- Changeset Number
- Commit ID
- Version Tag
- File Path

---

## 6. Review Validation

Examples

- Lead Review Completed
- FR Review Completed
- QC Passed
- Client Review Enabled

---

## 7. Feedback Validation

Examples

- Feedback Recorded
- Review Decision Selected
- Feedback Linked
- Comment Mandatory

---

## 8. Communication Validation

Examples

- Mandatory Comment
- Mandatory Attachment
- Discussion Closed

---

## 9. Approval Validation

Examples

- Required Reviewer Approved
- Client Approved
- QC Passed

---

## 10. Custom Validation

Organization-specific validation.

Examples

- Naming Convention
- File Structure
- Asset Standard
- Production Checklist

---

# Validation Levels

Validation may execute at different levels.

| Level | Example |
|---------|----------|
| Workflow | Workflow Active |
| Process | Review Enabled |
| State | State Valid |
| Transition | Transition Allowed |
| Task | Task Complete |
| SubTask | Artist Completed |
| Deliverable | Version Exists |

---

# Validation Execution Order

The engine evaluates validations in order.

```text
Permission

↓

Workflow

↓

State

↓

Task

↓

SubTask

↓

Deliverables

↓

Review

↓

Business Rules

↓

Custom Rules

↓

Success
```

Execution stops on the first critical failure.

---

# Validation Severity

Each validation has a severity level.

| Severity | Behaviour |
|----------|-----------|
| Error | Transition Blocked |
| Warning | User Confirmation Required |
| Information | Logged Only |

---

# Example Validation

## Submit for Lead Review

Requirements

✓ Workflow Active

✓ Task Assigned

✓ All General SubTasks Closed

✓ Deliverables Uploaded

✓ Repository Path Exists

✓ Changeset Entered

If any validation fails:

```text
Transition Rejected
```

---

## Submit for Final Review

Requirements

✓ Lead Review Approved

✓ Deliverables Versioned

✓ Review Package Created

✓ Production Complete

---

## Client Approval

Requirements

✓ QC Passed

✓ Final Review Approved

✓ Client Package Uploaded

---

## Close Task

Requirements

✓ Workflow Completed

✓ Client Approved

✓ All Reviews Closed

✓ No Active SubTasks

---

# Validation Response

Every validation returns:

```json
{
    "IsValid": true,
    "Severity": "Error",
    "Message": "",
    "Rule": "AllSubTasksCompleted"
}
```

---

# Batch Validation

The Validation Engine supports validating multiple rules together.

```text
Task

↓

Validate

↓

12 Rules

↓

10 Passed

↓

2 Failed

↓

Display Errors
```

---

# User Experience

Validation failures should display:

- Validation Name
- Error Description
- Resolution Suggestion
- Related Entity

Example

```
Cannot submit to Lead Review.

Reason:
Three General SubTasks are still In Progress.

Remaining SubTasks

• Texture Face
• Weapon Polish
• Hair Cleanup
```

---

# Validation Logging

Every validation execution should record:

- Workflow
- Transition
- Rule
- Result
- User
- Date
- Duration

---

# Business Rules

## BR-001

Validation executes after Permission Validation.

---

## BR-002

Validation executes before Workflow Transition.

---

## BR-003

Critical validation failures block Transition.

---

## BR-004

Warnings may allow user confirmation.

---

## BR-005

Validation Rules are versioned with the Workflow.

---

## BR-006

Validation Rules must be reusable.

---

## BR-007

Validation execution must be fully auditable.

---

## BR-008

Custom validation plugins may be registered.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| ValidationId | Primary Key |
| WorkflowId | Workflow |
| TransitionId | Transition |
| Name | Validation Name |
| Category | Workflow / Review / Deliverable |
| Severity | Error / Warning / Info |
| Priority | Execution Order |
| Enabled | Boolean |
| Error Message | Display Message |

---

# Reporting

Typical reports include:

- Validation Failures
- Most Common Errors
- Transition Failure Rate
- Review Validation Statistics
- Workflow Health
- Validation Performance

---

# Future Enhancements

Future releases may include:

- Expression Builder
- Scripted Validators
- AI Validation Suggestions
- Validation Simulator
- Dynamic Rule Engine
- Low-Code Validation Designer
- External Validation APIs

---

# Design Principles

The Workflow Validation module follows these principles:

- Validation is configuration-driven.
- Validation is independent of permissions.
- Validation is reusable across workflows.
- Validation rules are version-controlled.
- Business logic should never be hard-coded.
- Every validation execution is auditable.
- Validation failures should provide actionable feedback to users.

---

# Related Documents

- Workflow.md
- WorkflowTransition.md
- WorkflowRule.md
- WorkflowPermission.md
- WorkflowAutomation.md
- WorkflowEvent.md
- WorkflowNotification.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow Validation specification |
