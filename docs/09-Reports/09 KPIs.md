# Key Performance Indicators (KPIs)

**Document Version:** 1.0  
**Module:** KPI Framework  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Executives, Project Managers, Delivery Managers, Resource Managers, Finance Team, Operations Team, Business Analysts

---

# Purpose

The Key Performance Indicator (KPI) framework defines the standard business metrics used throughout the Project & Asset Management Platform.

KPIs provide measurable insights into organizational performance, project health, operational efficiency, financial performance, workforce productivity, quality, customer satisfaction, and AI effectiveness.

Every dashboard, report, and analytics screen should derive metrics from this centralized KPI framework to ensure consistency across the platform.

---

# Objectives

The KPI framework enables organizations to:

- Measure business performance
- Track project execution
- Monitor operational efficiency
- Evaluate financial health
- Optimize resource utilization
- Improve production quality
- Monitor customer satisfaction
- Measure AI effectiveness
- Enable data-driven decision making

---

# KPI Categories

The platform groups KPIs into the following categories.

| Category | Description |
|----------|-------------|
| Executive | Organization-wide performance |
| Financial | Revenue, cost, profitability |
| Project | Project execution metrics |
| Production | Production efficiency |
| Resource | Workforce metrics |
| Workflow | Business process metrics |
| Quality | Quality assurance metrics |
| Client | Customer metrics |
| AI | Artificial Intelligence metrics |
| Operational | Daily operational metrics |

---

# Executive KPIs

## Revenue

Measures total earned revenue.

Formula

```text
Sum(Invoice Amount)
```

Frequency

- Daily
- Monthly
- Quarterly
- Annual

---

## Gross Margin

Formula

```text
Revenue - Direct Cost
```

---

## Net Margin

Formula

```text
Revenue - Total Cost
```

---

## Active Clients

Definition

Number of clients with at least one active project.

---

## Active Projects

Definition

Projects whose status is not Closed, Cancelled, or Archived.

---

## Delivery Success Rate

Formula

```text
Delivered On Time

÷

Total Deliveries
```

---

# Financial KPIs

## Budget Utilization

Formula

```text
Actual Cost

÷

Approved Budget
```

---

## Profitability

Formula

```text
Revenue

-

Total Cost
```

---

## Cost Variance

Formula

```text
Planned Cost

-

Actual Cost
```

---

## Revenue Growth

Formula

```text
(Current Revenue

-

Previous Revenue)

÷

Previous Revenue
```

---

## Cash Flow

Formula

```text
Cash Inflow

-

Cash Outflow
```

---

## Collection Efficiency

Formula

```text
Collected Amount

÷

Total Invoiced Amount
```

---

# Project KPIs

## Project Health Score

Composite score calculated from

- Schedule
- Budget
- Resource Utilization
- Risks
- Quality
- Client Feedback

Scale

```text
0 - 100
```

---

## Schedule Variance

Formula

```text
Planned Progress

-

Actual Progress
```

---

## Cost Performance Index (CPI)

Formula

```text
Earned Value

÷

Actual Cost
```

---

## Schedule Performance Index (SPI)

Formula

```text
Earned Value

÷

Planned Value
```

---

## Milestone Completion Rate

Formula

```text
Completed Milestones

÷

Total Milestones
```

---

## On-Time Delivery Rate

Formula

```text
Deliveries On Time

÷

Total Deliveries
```

---

# Production KPIs

## Asset Throughput

Formula

```text
Assets Completed

÷

Time Period
```

---

## Production Efficiency

Formula

```text
Planned Hours

÷

Actual Hours
```

---

## Cycle Time

Definition

Average time required to complete one asset.

---

## Work In Progress (WIP)

Definition

Assets currently under production.

---

## Batch Completion Rate

Formula

```text
Completed Batches

÷

Total Batches
```

---

# Resource KPIs

## Resource Utilization

Formula

```text
Billable Hours

÷

Available Hours
```

---

## Capacity Utilization

Formula

```text
Allocated Capacity

÷

Total Capacity
```

---

## Bench Percentage

Formula

```text
Bench Resources

÷

Total Resources
```

---

## Average Workload

Formula

```text
Assigned Hours

÷

Active Resources
```

---

## Overtime Percentage

Formula

```text
Overtime Hours

÷

Worked Hours
```

---

# Workflow KPIs

## Workflow Success Rate

Formula

```text
Successful Workflows

÷

Total Workflows
```

---

## Average Workflow Duration

Definition

Average time from workflow start to completion.

---

## SLA Compliance

Formula

```text
SLA Met

÷

Total Workflow Instances
```

---

## Automation Rate

Formula

```text
Automated Steps

÷

Total Workflow Steps
```

---

## Approval Time

Definition

Average approval duration.

---

# Quality KPIs

## First Pass Approval Rate

Formula

```text
Approved First Review

÷

Total Reviews
```

---

## Rework Percentage

Formula

```text
Reworked Assets

÷

Total Assets
```

---

## QA Pass Rate

Formula

```text
QA Passed

÷

QA Executed
```

---

## Defect Density

Formula

```text
Defects

÷

Assets Produced
```

---

## Review Rejection Rate

Formula

```text
Rejected Reviews

÷

Total Reviews
```

---

# Client KPIs

## Client Satisfaction Score

Collected from

- Surveys
- Ratings
- Feedback

Scale

```text
1 – 5
```

---

## Client Retention Rate

Formula

```text
Returning Clients

÷

Total Clients
```

---

## Average Response Time

Definition

Average time taken to respond to client requests.

---

## Client Escalations

Definition

Number of client escalations during a reporting period.

---

## Net Promoter Score (NPS)

Collected through customer surveys.

---

# AI KPIs

## AI Utilization

Formula

```text
AI Assisted Tasks

÷

Total Tasks
```

---

## AI Acceptance Rate

Formula

```text
Accepted AI Suggestions

÷

Generated Suggestions
```

---

## AI Productivity Gain

Formula

```text
Estimated Hours Saved
```

---

## AI Automation Rate

Formula

```text
AI Executed Processes

÷

Eligible Processes
```

---

## AI Accuracy

Formula

```text
Successful AI Results

÷

Total AI Executions
```

---

# Operational KPIs

## Open Tasks

Definition

Tasks not yet completed.

---

## Overdue Tasks

Definition

Tasks whose due date has passed.

---

## Pending Reviews

Definition

Reviews awaiting completion.

---

## Pending Approvals

Definition

Approvals waiting for action.

---

## System Availability

Formula

```text
System Uptime

÷

Total Time
```

---

# KPI Thresholds

Each KPI should support configurable thresholds.

Example

| KPI | Green | Yellow | Red |
|------|--------|---------|------|
| Utilization | 75–90% | 60–74% / 91–95% | <60% / >95% |
| On-Time Delivery | ≥95% | 85–94% | <85% |
| Gross Margin | ≥30% | 20–29% | <20% |
| SLA Compliance | ≥98% | 90–97% | <90% |
| First Pass Approval | ≥90% | 80–89% | <80% |

Thresholds should be configurable per organization.

---

# KPI Visualization

Supported widgets

- KPI Card
- Gauge
- Trend Line
- Bar Chart
- Pie Chart
- Heat Map
- Bullet Chart
- Progress Ring
- Scorecard

---

# KPI Refresh Frequency

| KPI Type | Refresh |
|----------|----------|
| Operational | Real-Time |
| Production | Every 5 Minutes |
| Resource | Every 15 Minutes |
| Workflow | Every 5 Minutes |
| Financial | Every 15 Minutes |
| Executive | Hourly |
| AI | Hourly |

---

# KPI Drill-Down

Every KPI should support drill-down navigation.

Example

```text
Revenue

↓

Client

↓

Project

↓

Batch

↓

Invoice
```

Example

```text
Resource Utilization

↓

Department

↓

Team

↓

Employee

↓

Task
```

---

# KPI Ownership

Each KPI should define an owner.

Example

| KPI | Owner |
|------|-------|
| Revenue | Finance |
| Margin | Finance |
| Project Health | Project Manager |
| Resource Utilization | Resource Manager |
| Production Efficiency | Production Manager |
| Workflow SLA | Operations |
| AI Productivity | AI Operations |
| Client Satisfaction | Customer Success |

---

# KPI History

The platform should retain KPI history for trend analysis.

Recommended retention

| Data | Retention |
|------|-----------|
| Daily | 2 Years |
| Monthly | 5 Years |
| Yearly | Lifetime |

---

# KPI Security

KPIs should respect:

- Tenant Isolation
- Role-Based Access Control (RBAC)
- Department-Level Security
- Financial Visibility Rules
- Row-Level Security

Users should only see KPI values derived from data they are authorized to access.

---

# AI KPI Recommendations

The AI engine should continuously analyze KPI trends and provide recommendations.

Examples

- Reduce review cycle time
- Improve resource utilization
- Optimize workflow bottlenecks
- Increase first-pass approval rate
- Improve project profitability
- Reduce overtime
- Increase automation

Example

> "Project profitability has decreased by 8% over the last month due to increased rework. Improving the first-pass approval rate by 10% could restore the planned margin."

---

# Performance Targets

| Operation | Target |
|-----------|---------|
| KPI Calculation | < 2 Seconds |
| KPI Refresh | < 2 Seconds |
| Dashboard KPI Load | < 3 Seconds |
| Historical Trend Query | < 5 Seconds |

---

# Development Guidelines

Developers should:

- Define KPIs using centralized metadata
- Avoid duplicate KPI calculation logic
- Use pre-aggregated summary tables where possible
- Cache frequently requested KPI values
- Support configurable thresholds and targets
- Maintain historical KPI snapshots for trend analysis

---

# Future Enhancements

Planned capabilities include:

- KPI Benchmarking
- Industry Comparison
- Predictive KPIs
- AI Goal Tracking
- Smart KPI Recommendations
- Executive KPI Scorecards
- Balanced Scorecard Framework
- ESG & Sustainability KPIs
- Custom KPI Formula Designer

---

# Summary

The KPI Framework establishes a standardized and centralized approach for measuring business performance across the Project & Asset Management Platform. By defining consistent calculations, thresholds, ownership, visualization standards, and security rules, it ensures that dashboards, reports, and analytics deliver accurate, actionable, and organization-wide insights. Combined with AI-driven recommendations and predictive analysis, the KPI framework supports continuous improvement and strategic decision-making.
