# SignalR Real-Time Communication

**Document Version:** 1.0  
**Module:** Real-Time Communication Architecture  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Backend Developers, Frontend Developers, Solution Architects, DevOps Engineers, AI Agents

---

# Purpose

This document defines the real-time communication architecture for the Project & Asset Management Platform using **ASP.NET Core SignalR**.

SignalR enables instant communication between the server and connected clients without requiring continuous polling.

The objectives are to:

- Provide real-time updates
- Reduce API polling
- Improve user experience
- Synchronize multiple users
- Support collaborative workflows
- Enable AI event notifications
- Scale across multiple application servers

---

# Why SignalR?

Traditional applications require polling.

```text
Browser

↓

Every 10 Seconds

↓

GET /notifications
```

This generates unnecessary network traffic.

SignalR provides:

```text
Server

↓

Push Event

↓

Connected Browser
```

No polling required.

---

# SignalR Architecture

```text
                Browser

                    │

              SignalR Client

                    │

                WebSocket

                    │

             SignalR Hub Server

                    │

             Event Dispatcher

                    │

Business Modules / Workflow Engine

                    │

                PostgreSQL
```

---

# Supported Transport Protocols

SignalR automatically selects the best available transport.

Priority

```text
WebSocket

↓

Server Sent Events

↓

Long Polling
```

WebSocket is preferred.

---

# Core Components

The real-time platform consists of:

- SignalR Hub
- Hub Context
- Connection Manager
- Notification Service
- Event Dispatcher
- Redis Backplane (Multi-Server)

---

# SignalR Hubs

The platform defines dedicated hubs.

---

## Notification Hub

Endpoint

```text
/api/hubs/notifications
```

Purpose

- User notifications
- Alerts
- Toast messages

---

## Workflow Hub

Endpoint

```text
/api/hubs/workflows
```

Purpose

- Workflow updates
- Status changes
- Approval notifications

---

## Task Hub

Endpoint

```text
/api/hubs/tasks
```

Purpose

- Task assignment
- Task completion
- Progress updates

---

## Asset Hub

Endpoint

```text
/api/hubs/assets
```

Purpose

- Asset upload
- Version changes
- Lock/Unlock events

---

## Review Hub

Endpoint

```text
/api/hubs/reviews
```

Purpose

- Review status
- Comments
- Approval workflow

---

## Dashboard Hub

Endpoint

```text
/api/hubs/dashboard
```

Purpose

- KPI refresh
- Charts
- Live statistics

---

## AI Hub

Endpoint

```text
/api/hubs/ai
```

Purpose

- AI processing progress
- Document generation
- AI assistant updates
- Background AI jobs

---

# Hub Naming Convention

Every hub ends with

```text
Hub
```

Example

```text
NotificationHub

TaskHub

WorkflowHub

AIHub
```

---

# Client Connection

Example

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/api/hubs/notifications")
    .build();
```

Connections should automatically reconnect.

---

# Automatic Reconnection

Enabled by default.

Example

```text
Disconnected

↓

Retry

↓

Reconnect

↓

Restore Subscription
```

---

# Authentication

SignalR connections require JWT authentication.

Browser

```http
Authorization: Bearer <token>
```

The authenticated user identity is available inside the Hub.

---

# Authorization

Each Hub enforces authorization policies.

Example

```text
NotificationHub

↓

Notification.Read
```

Workflow Hub

```text
Workflow.Execute
```

---

# Connection Lifecycle

```text
Connect

↓

Authenticate

↓

Authorize

↓

Join Groups

↓

Receive Events

↓

Disconnect
```

---

# Connection Events

SignalR handles

```text
Connected

Disconnected

Reconnected

Connection Lost
```

These events are logged.

---

# User Mapping

Each connection maps to

```text
User ID

↓

Connection ID
```

Users may have multiple active connections.

Example

```text
Desktop

Mobile

Tablet
```

---

# Group Management

Groups organize users.

Examples

```text
Tenant

Project

Batch

Team

Workflow

Review
```

---

# Tenant Groups

Example

```text
Tenant-100
```

Only users within Tenant-100 receive those events.

---

# Project Groups

Example

```text
Project-ERP
```

Project members automatically join.

---

# Team Groups

Example

```text
Team-Design
```

Only design team receives updates.

---

# Workflow Groups

Example

```text
Workflow-455
```

Participants receive workflow progress.

---

# Sending Messages

Server

↓

Hub

↓

Group

↓

Users

↓

Clients

---

# Broadcast

Example

```text
All Users
```

Use sparingly.

---

# User Notification

Example

```text
User

↓

Notification

↓

Single User
```

---

# Group Notification

Example

```text
Task Completed

↓

Project Group

↓

All Members
```

---

# Tenant Broadcast

Example

```text
Maintenance Notice

↓

Entire Tenant
```

---

# Real-Time Events

---

## Task Events

```text
TaskAssigned

TaskCompleted

TaskUpdated

TaskDeleted
```

---

## Project Events

```text
ProjectCreated

ProjectUpdated

ProjectArchived
```

---

## Asset Events

```text
AssetUploaded

AssetLocked

AssetUnlocked

AssetVersionCreated
```

---

## Workflow Events

```text
WorkflowStarted

WorkflowCompleted

WorkflowFailed

WorkflowTransition
```

---

## Review Events

```text
ReviewSubmitted

ReviewApproved

ReviewRejected

ReviewCommentAdded
```

---

## Notification Events

```text
NotificationCreated

NotificationRead
```

---

## Dashboard Events

```text
DashboardRefresh

KPIUpdated

ChartUpdated
```

---

## AI Events

```text
DocumentGenerated

PromptCompleted

AgentFinished

ModelCompleted

VectorIndexed
```

---

# Event Payload

Example

```json
{
  "event": "TaskAssigned",
  "taskId": 105,
  "projectId": 20,
  "assignedTo": "USR-102",
  "timestamp": "2026-07-28T08:00:00Z"
}
```

---

# Message Format

Every message contains

```text
Event

Timestamp

Data

CorrelationId

TenantId
```

---

# Hub Methods

Examples

```text
JoinProject()

LeaveProject()

JoinTeam()

LeaveTeam()

SubscribeDashboard()

UnsubscribeDashboard()
```

---

# Server Push Only

Business updates originate from server-side services.

Example

```text
Workflow Completed

↓

Workflow Engine

↓

SignalR Hub

↓

Connected Clients
```

---

# Background Services

Background workers can publish events.

Examples

- Notification Worker
- AI Worker
- Workflow Processor
- Scheduler

They use

```text
IHubContext
```

instead of direct Hub instances.

---

# Offline Users

If user is offline

↓

Create Notification

↓

Store Database

↓

Deliver On Login

SignalR is not used as permanent storage.

---

# Message Persistence

SignalR messages are transient.

Persistent notifications are stored in

```text
Notifications Table
```

---

# Redis Backplane

For multiple application servers

```text
Server 1

↓

Redis

↓

Server 2

↓

Server 3
```

Ensures messages reach all connected users.

---

# Scaling

Supports

- Horizontal Scaling
- Kubernetes
- Load Balancers
- Multiple SignalR Servers

Sticky sessions are not required when using a Redis backplane or Azure SignalR Service.

---

# Performance

Recommended practices

- Small payloads
- Event-driven updates
- Avoid unnecessary broadcasts
- Use groups
- Compress payloads when appropriate

---

# Error Handling

Errors include

- Connection Failure
- Authentication Failure
- Authorization Failure
- Serialization Error

Errors are logged.

---

# Logging

Log

- Connect
- Disconnect
- Reconnect
- Group Join
- Group Leave
- Errors
- Broadcast Events

---

# Monitoring

Monitor

- Active Connections
- Messages/Second
- Failed Connections
- Reconnection Rate
- Hub Exceptions
- Average Latency

---

# Security

SignalR requires

- HTTPS
- JWT Authentication
- Authorization Policies
- Tenant Isolation
- Input Validation
- Rate Limiting

Never expose sensitive information through hub messages.

---

# Rate Limiting

Protect against abuse.

Examples

```text
Maximum Connections

Messages / Minute

Subscriptions / Minute
```

---

# AI Integration

AI Agents publish updates through SignalR.

Examples

```text
Document Ready

AI Review Complete

Code Generation Finished

Requirement Analysis Complete
```

Users receive updates instantly without refreshing the page.

---

# Client Behavior

Clients should

- Auto reconnect
- Resubscribe after reconnect
- Handle duplicate messages safely
- Gracefully handle temporary disconnections

---

# Development Guidelines

Developers should

- Use strongly typed hubs where practical
- Keep hub methods lightweight
- Perform business logic in services
- Use asynchronous methods
- Send events only after successful transactions

---

# AI Development Guidelines

AI-generated SignalR code must

- Use Hub classes
- Use dependency injection
- Authenticate every connection
- Authorize every hub
- Use groups instead of broadcasting
- Use async methods
- Publish only successful business events
- Log connection events

AI must never

- Embed business logic directly inside hubs
- Broadcast sensitive data
- Trust client identity without validation
- Use SignalR as persistent storage

---

# SignalR Checklist

Before deployment verify:

- ✓ Authentication enabled
- ✓ Authorization policies applied
- ✓ HTTPS enforced
- ✓ Groups implemented
- ✓ Auto reconnect enabled
- ✓ Redis Backplane configured (multi-server)
- ✓ Logging enabled
- ✓ Monitoring enabled
- ✓ Offline notification fallback implemented
- ✓ Tenant isolation validated

---

# Future Enhancements

Planned capabilities include:

- Azure SignalR Service
- Presence Detection
- Typing Indicators
- Collaborative Editing
- Live Cursor Sharing
- WebRTC Integration
- Push Notifications for Mobile
- Event Streaming via Kafka
- Real-Time Analytics Dashboard

---

# Summary

The Project & Asset Management Platform uses **ASP.NET Core SignalR** to provide secure, scalable, real-time communication across web clients, background services, AI agents, and business modules. The architecture is built around dedicated hubs, authenticated connections, authorization policies, tenant-aware groups, and server-driven events. By combining SignalR with a Redis backplane (or Azure SignalR Service for cloud deployments), the platform delivers reliable low-latency updates while maintaining security, scalability, and a clean separation between business logic and real-time messaging.
