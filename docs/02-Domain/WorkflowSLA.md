# Workflow SLA

> **Purpose**
>
> The Workflow SLA (Service Level Agreement) module defines the expected completion time for Workflow Processes, Workflow States, Reviews, and Tasks.
>
> It provides automatic tracking, breach detection, escalations, notifications, and performance reporting to ensure production targets are met.
>
> SLA rules are fully configurable and independent of business logic.

---

# Overview

Workflow SLA monitors the time spent within a Workflow.

```text
Task Created

↓

Workflow Started

↓

SLA Timer Started

↓

Workflow Progress

↓

SLA Evaluated

↓

Completed
OR
Breached
```

SLA applies to:

- Workflow
- Process
- State
- Review
- Task
- SubTask

---

# Objectives

The SLA Engine provides:

- Production monitoring
- Deadline tracking
- Automatic escalations
- Performance measurement
- Bottleneck identification
- Team accountability
- Client commitment tracking

---

# SLA Architecture

```text
Workflow

↓

SLA Engine

├── SLA Rules
├── Timer Engine
├── Working Calendar
├── Escalation Rules
├── Notification Engine
└── Reporting
```

---

# SLA Scope

An SLA may be configured for:

| Level | Example |
|--------|----------|
| Workflow | Asset Production |
| Process | Final Review |
| State | Waiting for Approval |
| Task | Character Modeling |
| SubTask | UV Mapping |
| Review | Client Review |

---

# SLA Components

Each SLA defines:

- Name
- Target Duration
- Warning Threshold
- Breach Threshold
- Working Calendar
- Escalation Rules
- Notification Rules
- Pause Conditions
- Resume Conditions

---

# SLA Lifecycle

```text
Created

↓

Running

↓

Paused

↓

Resumed

↓

Completed

OR

Breached
```

---

# SLA States

Possible values:

- Not Started
- Running
- Paused
- Warning
- Breached
- Completed
- Cancelled

---

# Timer Behavior

The SLA timer starts automatically when:

- Workflow starts
- Process entered
- State entered
- Review assigned
- Task created

The timer stops when:

- Task completed
- Process exited
- State changed
- Review approved
- Workflow completed

---

# Pause Conditions

The timer may pause when:

- Waiting for Client
- Waiting for External Vendor
- Holiday
- Weekend
- Manual Hold
- Dependency Hold

Paused time is excluded from SLA calculations.

---

# Working Calendar

The SLA Engine supports:

- Business Hours
- Working Days
- Public Holidays
- Team Calendars
- Regional Calendars
- Shift-Based Calendars

Example

```
Monday - Friday

09:00 AM - 06:00 PM

Saturday

Half Day

Sunday

Non-working
```

---

# Warning Threshold

Warnings notify users before an SLA breach.

Example

```
Target SLA

24 Hours

↓

Warning

20 Hours

↓

Breach

24 Hours
```

---

# Escalation Levels

Example

| Time | Action |
|------|---------|
| 80% | Notify Assignee |
| 90% | Notify Team Lead |
| 100% | Notify Project Manager |
| 120% | Notify Delivery Manager |

---

# Notifications

Automatic notifications may be sent for:

- SLA Started
- SLA Warning
- SLA Breached
- SLA Resumed
- SLA Completed

---

# Breach Handling

When breached:

- Update SLA Status
- Record Breach Time
- Notify Stakeholders
- Generate Timeline Event
- Trigger Automation
- Raise Escalation

---

# SLA Metrics

The engine calculates:

- Elapsed Time
- Working Time
- Paused Time
- Remaining Time
- Breach Duration
- Average Resolution Time

---

# Example SLA

## Final Review

Target

```
16 Working Hours
```

Warning

```
12 Hours
```

Escalation

```
16 Hours

↓

Notify Project Manager
```

---

## Client Review

Target

```
3 Working Days
```

Paused when:

- Waiting for Client Response

---

# Dashboard

Typical widgets

- Active SLAs
- SLA Warnings
- Breached SLAs
- Average Resolution Time
- Team SLA Performance
- Review SLA Compliance

---

# Business Rules

## BR-001

Each Workflow may have multiple SLA definitions.

---

## BR-002

Only one active SLA instance exists per configured scope.

---

## BR-003

Paused time does not count toward SLA duration.

---

## BR-004

Working calendars determine elapsed time.

---

## BR-005

Breach events are immutable.

---

## BR-006

Escalations are configuration-driven.

---

## BR-007

Workflow completion automatically completes active SLA instances.

---

# Suggested Data Model

| Field | Description |
|------|-------------|
| SLAId | Primary Key |
| WorkflowId | Workflow |
| ProcessId | Optional Process |
| StateId | Optional State |
| TargetDuration | SLA Target |
| WarningDuration | Warning Threshold |
| CalendarId | Working Calendar |
| EscalationPolicyId | Escalation Policy |
| Status | Current Status |

---

# Reporting

Typical reports include:

- SLA Compliance
- SLA Breaches
- Average Resolution Time
- Review SLA Performance
- Team SLA Performance
- Process Bottlenecks
- Workflow Efficiency

---

# Future Enhancements

Future releases may include:

- AI Breach Prediction
- Dynamic SLA Adjustment
- Capacity-Based SLA Forecasting
- SLA Simulation
- Intelligent Escalation
- Executive SLA Dashboard
- Customer SLA Portal

---

# Design Principles

The Workflow SLA module follows these principles:

- SLA rules are configuration-driven.
- Working calendars determine elapsed time.
- SLA tracking is independent of task due dates.
- Escalations are automatic and auditable.
- SLA metrics support continuous process improvement.
- Every SLA event is recorded for reporting and analytics.

---

# Related Documents

- Workflow.md
- WorkflowState.md
- WorkflowProcess.md
- WorkflowTransition.md
- WorkflowNotification.md
- WorkflowAutomation.md
- Dashboard.md
- Reporting.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Workflow SLA specification |
