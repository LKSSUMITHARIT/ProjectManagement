# REST Endpoints

**Document Version:** 1.0  
**Module:** API Reference  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Backend Developers, Frontend Developers, Mobile Developers, Integration Developers, AI Agents

---

# Purpose

This document provides the standard REST API endpoint structure for the Project & Asset Management Platform.

The objectives are to:

- Standardize API naming
- Define available resources
- Maintain consistency
- Simplify frontend development
- Support third-party integrations
- Provide a reference for AI-generated APIs

This document defines endpoint contracts only. Detailed request and response models are documented in **APIRequirements.md** and the generated OpenAPI (Swagger) specification.

---

# Base URL

Development

```text
https://localhost:5001/api/v1
```

Production

```text
https://api.company.com/api/v1
```

---

# Common HTTP Methods

| Method | Purpose |
|----------|----------|
| GET | Read |
| POST | Create |
| PUT | Replace |
| PATCH | Partial Update |
| DELETE | Delete |

---

# Authentication Endpoints

| Method | Endpoint | Description |
|----------|----------|-------------|
| POST | /auth/login | Login |
| POST | /auth/logout | Logout |
| POST | /auth/refresh | Refresh Token |
| POST | /auth/forgot-password | Forgot Password |
| POST | /auth/reset-password | Reset Password |
| POST | /auth/change-password | Change Password |
| POST | /auth/mfa/verify | Verify MFA |
| GET | /auth/profile | Current User |
| GET | /auth/sessions | Active Sessions |

---

# Tenant Endpoints

| Method | Endpoint |
|----------|----------|
| GET | /tenants |
| GET | /tenants/{tenantId} |
| POST | /tenants |
| PUT | /tenants/{tenantId} |
| DELETE | /tenants/{tenantId} |

---

# User Management

| Method | Endpoint |
|----------|----------|
| GET | /users |
| GET | /users/{userId} |
| POST | /users |
| PUT | /users/{userId} |
| PATCH | /users/{userId} |
| DELETE | /users/{userId} |
| GET | /users/{userId}/roles |
| PUT | /users/{userId}/roles |
| GET | /users/{userId}/permissions |

---

# Role Management

| Method | Endpoint |
|----------|----------|
| GET | /roles |
| GET | /roles/{roleId} |
| POST | /roles |
| PUT | /roles/{roleId} |
| DELETE | /roles/{roleId} |
| GET | /roles/{roleId}/permissions |
| PUT | /roles/{roleId}/permissions |

---

# Permission Management

| Method | Endpoint |
|----------|----------|
| GET | /permissions |
| GET | /permissions/{permissionId} |

---

# Client Management

| Method | Endpoint |
|----------|----------|
| GET | /clients |
| GET | /clients/{clientId} |
| POST | /clients |
| PUT | /clients/{clientId} |
| DELETE | /clients/{clientId} |
| GET | /clients/{clientId}/projects |
| GET | /clients/search |

---

# Project Management

| Method | Endpoint |
|----------|----------|
| GET | /projects |
| GET | /projects/{projectId} |
| POST | /projects |
| PUT | /projects/{projectId} |
| PATCH | /projects/{projectId} |
| DELETE | /projects/{projectId} |
| GET | /projects/{projectId}/batches |
| GET | /projects/{projectId}/tasks |
| GET | /projects/{projectId}/assets |
| POST | /projects/{projectId}/archive |
| POST | /projects/{projectId}/restore |

---

# Batch Management

| Method | Endpoint |
|----------|----------|
| GET | /batches |
| GET | /batches/{batchId} |
| POST | /batches |
| PUT | /batches/{batchId} |
| DELETE | /batches/{batchId} |
| GET | /batches/{batchId}/tasks |
| GET | /batches/{batchId}/assets |
| POST | /batches/{batchId}/close |
| POST | /batches/{batchId}/reopen |

---

# Task Management

| Method | Endpoint |
|----------|----------|
| GET | /tasks |
| GET | /tasks/{taskId} |
| POST | /tasks |
| PUT | /tasks/{taskId} |
| PATCH | /tasks/{taskId} |
| DELETE | /tasks/{taskId} |
| POST | /tasks/{taskId}/assign |
| POST | /tasks/{taskId}/complete |
| POST | /tasks/{taskId}/reopen |
| POST | /tasks/bulk-update |
| GET | /tasks/my |

---

# Asset Management

| Method | Endpoint |
|----------|----------|
| GET | /assets |
| GET | /assets/{assetId} |
| POST | /assets |
| PUT | /assets/{assetId} |
| DELETE | /assets/{assetId} |
| GET | /assets/{assetId}/download |
| POST | /assets/{assetId}/upload-version |
| GET | /assets/{assetId}/versions |
| POST | /assets/{assetId}/lock |
| POST | /assets/{assetId}/unlock |

---

# Review Management

| Method | Endpoint |
|----------|----------|
| GET | /reviews |
| GET | /reviews/{reviewId} |
| POST | /reviews |
| PUT | /reviews/{reviewId} |
| POST | /reviews/{reviewId}/submit |
| POST | /reviews/{reviewId}/approve |
| POST | /reviews/{reviewId}/reject |
| GET | /reviews/{reviewId}/comments |

---

# Workflow Engine

| Method | Endpoint |
|----------|----------|
| GET | /workflows |
| GET | /workflows/{workflowId} |
| POST | /workflows |
| PUT | /workflows/{workflowId} |
| DELETE | /workflows/{workflowId} |
| POST | /workflows/{workflowId}/start |
| POST | /workflows/{workflowId}/pause |
| POST | /workflows/{workflowId}/resume |
| POST | /workflows/{workflowId}/cancel |

---

# Workflow Instances

| Method | Endpoint |
|----------|----------|
| GET | /workflow-instances |
| GET | /workflow-instances/{instanceId} |
| GET | /workflow-instances/{instanceId}/history |
| POST | /workflow-instances/{instanceId}/transition |

---

# Team Management

| Method | Endpoint |
|----------|----------|
| GET | /teams |
| GET | /teams/{teamId} |
| POST | /teams |
| PUT | /teams/{teamId} |
| DELETE | /teams/{teamId} |
| GET | /teams/{teamId}/members |
| POST | /teams/{teamId}/members |

---

# Resource Management

| Method | Endpoint |
|----------|----------|
| GET | /resources |
| GET | /resources/{resourceId} |
| POST | /resources |
| PUT | /resources/{resourceId} |
| DELETE | /resources/{resourceId} |
| GET | /resources/availability |
| POST | /resources/allocate |
| POST | /resources/release |

---

# Communication

| Method | Endpoint |
|----------|----------|
| GET | /messages |
| POST | /messages |
| GET | /conversations |
| GET | /conversations/{conversationId} |
| POST | /conversations/{conversationId}/messages |

---

# Notifications

| Method | Endpoint |
|----------|----------|
| GET | /notifications |
| GET | /notifications/unread |
| POST | /notifications/mark-read |
| POST | /notifications/mark-all-read |
| DELETE | /notifications/{notificationId} |

---

# Finance

| Method | Endpoint |
|----------|----------|
| GET | /invoices |
| GET | /invoices/{invoiceId} |
| POST | /invoices |
| PUT | /invoices/{invoiceId} |
| POST | /invoices/{invoiceId}/approve |
| GET | /timesheets |
| POST | /timesheets |
| GET | /budgets |

---

# Reporting

| Method | Endpoint |
|----------|----------|
| GET | /reports |
| GET | /reports/{reportId} |
| POST | /reports/generate |
| POST | /reports/export |
| GET | /dashboards |
| GET | /dashboards/{dashboardId} |

---

# AI Services

| Method | Endpoint |
|----------|----------|
| POST | /ai/chat |
| POST | /ai/prompts |
| POST | /ai/summarize |
| POST | /ai/estimate |
| POST | /ai/review |
| POST | /ai/generate-document |
| GET | /ai/agents |
| GET | /ai/models |

---

# File Management

| Method | Endpoint |
|----------|----------|
| POST | /files |
| GET | /files/{fileId} |
| DELETE | /files/{fileId} |
| GET | /files/{fileId}/download |
| GET | /files/{fileId}/metadata |

---

# Audit

| Method | Endpoint |
|----------|----------|
| GET | /audit |
| GET | /audit/{auditId} |
| GET | /audit/entity/{entityType}/{entityId} |

---

# Administration

| Method | Endpoint |
|----------|----------|
| GET | /settings |
| PUT | /settings |
| GET | /system-info |
| GET | /licenses |
| POST | /maintenance/start |
| POST | /maintenance/stop |

---

# Source Control Integration

| Method | Endpoint |
|----------|----------|
| GET | /repositories |
| GET | /repositories/{repositoryId} |
| POST | /repositories |
| GET | /repositories/{repositoryId}/branches |
| GET | /repositories/{repositoryId}/commits |
| GET | /repositories/{repositoryId}/pull-requests |

---

# Search

| Method | Endpoint |
|----------|----------|
| GET | /search |
| GET | /search/projects |
| GET | /search/tasks |
| GET | /search/assets |
| GET | /search/users |

---

# Dashboard

| Method | Endpoint |
|----------|----------|
| GET | /dashboard |
| GET | /dashboard/kpis |
| GET | /dashboard/charts |
| GET | /dashboard/workload |
| GET | /dashboard/recent-activity |

---

# Health

| Method | Endpoint |
|----------|----------|
| GET | /health |
| GET | /health/live |
| GET | /health/ready |

---

# Query Parameters

Common query parameters supported across collection endpoints:

| Parameter | Description |
|-----------|-------------|
| page | Page number |
| pageSize | Records per page |
| sort | Sort field |
| order | asc / desc |
| search | Free-text search |
| filter | Custom filter |
| expand | Include related resources |
| fields | Partial response fields |

Example

```http
GET /projects?page=1&pageSize=25&sort=name&order=asc&search=ERP
```

---

# Standard Response Codes

| Status | Meaning |
|---------|---------|
| 200 | Success |
| 201 | Created |
| 202 | Accepted |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 500 | Internal Server Error |

---

# Endpoint Naming Rules

All endpoints must:

- Use plural resource names
- Use lowercase URLs
- Use hyphens for multi-word resources
- Avoid verbs in resource names
- Be versioned
- Follow REST conventions
- Return consistent response models

Examples

```text
/projects

/project-members

/workflow-instances

/review-comments
```

---

# Summary

The Project & Asset Management Platform exposes a comprehensive REST API organized around business resources such as Clients, Projects, Batches, Tasks, Assets, Reviews, Workflows, Teams, Resources, Finance, AI Services, and Administration. All endpoints follow consistent REST conventions, support versioning, use standardized HTTP methods and response models, and are secured through the platform's authentication and authorization architecture. This endpoint catalog serves as the canonical reference for application development, mobile clients, third-party integrations, and AI agents.
