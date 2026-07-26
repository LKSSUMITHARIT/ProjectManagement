# ADR-004: Resource Allocation Engine

**ADR ID:** ADR-004

**Title:** Centralized Resource Allocation & Capacity Planning Engine

**Status:** Accepted

**Date:** 2026-07-26

**Decision Makers:**

- Solution Architect
- Product Owner
- Delivery Manager
- PMO Team
- Resource Management Team

---

# Context

The platform is designed to support organizations that execute projects through shared human resources, including:

- Software Developers
- QA Engineers
- UI/UX Designers
- 2D/3D Artists
- Animators
- VFX Artists
- Technical Writers
- DevOps Engineers
- Business Analysts
- AI Agents

Resources are often shared across multiple projects simultaneously and have varying:

- Skills
- Availability
- Capacity
- Cost
- Calendars
- Time Zones
- Departments

Traditional project management systems allocate resources manually, often resulting in:

- Over-allocation
- Under-utilization
- Schedule conflicts
- Missed deadlines
- Inaccurate forecasting

The platform requires a centralized allocation engine that provides intelligent planning, workload balancing, forecasting, and AI-assisted recommendations.

---

# Problem Statement

Embedding allocation logic inside individual modules causes:

- Duplicate scheduling logic
- No global visibility
- Conflicting assignments
- Manual planning
- Poor forecasting
- Difficult reporting
- Limited optimization

A single allocation engine is required for all planning activities.

---

# Decision

The platform will implement a **Centralized Resource Allocation Engine** responsible for planning, scheduling, monitoring, and optimizing all human and non-human resources.

Every module requiring resources (Project, Task, Batch, Workflow, Review, etc.) must request assignments through this engine.

No module may directly assign resources without using the Allocation Engine.

---

# Architectural Principles

The Allocation Engine follows:

- Single Source of Truth
- Capacity-Based Planning
- Skill-Based Assignment
- Calendar Awareness
- Event-Driven Updates
- AI-Assisted Recommendations
- Complete Auditability
- Configurable Allocation Policies

---

# High-Level Architecture

```text
Project

      │

Task / Batch / Review

      │

Allocation Request

      │

▼

Resource Allocation Engine

      │

Capacity Validation

      │

Skill Matching

      │

Availability Check

      │

AI Recommendation

      │

Assignment

      │

Notifications
```

---

# Core Components

The Allocation Engine consists of

- Resource
- Skill
- Availability Calendar
- Working Calendar
- Allocation Request
- Allocation
- Capacity Engine
- Forecast Engine
- Utilization Engine
- AI Recommendation Engine

---

# Resource Types

Supported resource categories

### Human Resources

- Employees
- Contractors
- Freelancers
- Vendors
- Consultants

---

### Digital Resources

- AI Agents
- Automation Bots
- Virtual Machines
- Build Servers

---

### Physical Resources

- Devices
- Studios
- Labs
- Equipment

---

# Allocation Types

Supports

- Full-Time Allocation
- Part-Time Allocation
- Hourly Allocation
- Daily Allocation
- Percentage Allocation
- Shift-Based Allocation
- On-Demand Allocation

---

# Capacity Model

Each resource defines

- Daily Capacity
- Weekly Capacity
- Monthly Capacity
- Maximum Concurrent Projects
- Working Hours
- Holidays
- Leave Schedule

Example

```text
John Doe

Capacity

8 Hours / Day

↓

Project A

4 Hours

↓

Project B

3 Hours

↓

Training

1 Hour
```

---

# Skill Matching

Assignments consider

- Primary Skills
- Secondary Skills
- Experience Level
- Certifications
- Department
- Seniority
- Preferred Technologies

Example

```text
Task

↓

Requires

Blender

↓

Resources

Skill Match

↓

Top Candidates
```

---

# Availability Management

Availability factors include

- Working Hours
- Public Holidays
- Leave
- Time Zone
- Existing Allocations
- Overtime Policy

---

# Allocation Workflow

```text
Resource Requested

↓

Capacity Check

↓

Skill Match

↓

Availability Check

↓

Manager Approval (Optional)

↓

Assignment

↓

Notification
```

---

# Conflict Detection

Automatically detects

- Double Booking
- Over Allocation
- Skill Mismatch
- Calendar Conflicts
- Leave Conflicts
- Time Zone Overlap
- Project Priority Conflicts

---

# Utilization Tracking

Measures

- Planned Hours
- Actual Hours
- Billable Hours
- Non-Billable Hours
- Idle Time
- Overtime

---

# Forecasting

Supports forecasting for

- Resource Demand
- Capacity Requirements
- Hiring Needs
- Project Staffing
- Budget Impact

---

# AI Integration

The Allocation Engine integrates with the AI Platform.

---

## AI Resource Recommendation

Suggests

- Best Available Resource
- Alternate Resources
- Skill Gap Analysis
- Estimated Assignment Risk

---

## AI Capacity Forecast

Predicts

- Future Demand
- Capacity Shortage
- Idle Resources
- Hiring Requirements

---

## AI Workload Balancing

Automatically recommends

- Resource Redistribution
- Task Reassignment
- Priority Adjustments
- Schedule Optimization

---

## AI Delivery Risk

Analyzes

- Team Capacity
- Skill Availability
- Allocation Conflicts
- Deadline Risk

---

# Calendar Management

Supports

- Company Calendar
- Department Calendar
- Personal Calendar
- Holiday Calendar
- Shift Calendar

---

# Approval Rules

Optional approval may be required based on

- Allocation Duration
- Department
- Budget
- Resource Cost
- Project Priority

---

# Functional Requirements

Users shall be able to

- Request resources.
- View availability.
- Allocate resources.
- Modify allocations.
- Cancel allocations.
- View utilization.
- View capacity.
- Forecast staffing.

Managers shall be able to

- Approve allocations.
- Reassign resources.
- Balance workloads.
- Monitor utilization.
- Plan future capacity.

---

# Database Entities

Primary entities include

- Resource
- Skill
- ResourceSkill
- ResourceCalendar
- WorkingCalendar
- AllocationRequest
- Allocation
- CapacitySnapshot
- UtilizationRecord
- Forecast
- LeaveRequest

---

# Events

Published events include

- Resource Allocated
- Resource Released
- Allocation Updated
- Allocation Cancelled
- Capacity Exceeded
- Skill Gap Detected
- Allocation Approved
- Allocation Rejected

---

# APIs

Representative endpoints

```http
GET    /api/resources

GET    /api/resources/{id}

GET    /api/resources/availability

POST   /api/allocations

PUT    /api/allocations/{id}

DELETE /api/allocations/{id}

GET    /api/utilization

GET    /api/capacity

GET    /api/forecast

POST   /api/resources/recommend
```

---

# Reporting

Available reports

- Resource Utilization
- Capacity Planning
- Allocation Summary
- Over Allocation Report
- Idle Resource Report
- Skill Availability
- Department Workload
- Forecast Report
- Hiring Forecast
- AI Allocation Recommendations

---

# Security

Supports

- Role-Based Access Control
- Department-Level Visibility
- Resource Ownership
- Audit Logging
- Tenant Isolation
- Approval Permissions

---

# Performance Requirements

- Allocation validation < 500 ms
- Resource search < 1 second
- Capacity calculation < 2 seconds
- Utilization dashboard < 3 seconds
- Forecast generation < 10 seconds
- Support 100,000+ resources

---

# Alternatives Considered

## Manual Allocation

Rejected because

- Error-prone
- No optimization
- Difficult forecasting
- No conflict detection

---

## Module-Specific Allocation

Rejected because

- Duplicate logic
- Inconsistent planning
- Poor reporting
- No global capacity view

---

## Third-Party Resource Planning Tool

Rejected because

- Integration complexity
- Additional licensing
- Limited customization
- Fragmented user experience

---

# Consequences

## Positive

- Centralized allocation logic.
- Better utilization.
- Accurate capacity planning.
- AI-assisted recommendations.
- Reduced scheduling conflicts.
- Improved delivery forecasting.
- Enterprise scalability.

## Negative

- Higher implementation complexity.
- Requires accurate resource master data.
- AI recommendations depend on data quality.

---

# Future Evolution

The Allocation Engine is designed to support

- Automatic resource scheduling
- AI autonomous staffing
- Cross-organization resource sharing
- Marketplace-based contractor allocation
- Predictive hiring
- Digital twin workforce simulation
- Cost optimization
- Real-time workload balancing
- Multi-region workforce planning

---

# Decision Summary

The platform adopts a **Centralized Resource Allocation Engine** responsible for all resource planning, capacity management, utilization tracking, and assignment decisions. Every business module interacts with this engine rather than implementing allocation logic independently, ensuring consistent planning, optimized utilization, enterprise scalability, and AI-assisted workforce management.
