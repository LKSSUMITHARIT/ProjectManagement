# Design Patterns

**Document Version:** 1.0  
**Module:** Development Standards  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Solution Architects, Software Architects, Developers, AI Agents

---

# Purpose

This document defines the approved software design patterns for the Project & Asset Management Platform.

The objectives are to:

- Standardize software architecture
- Promote reusable code
- Improve maintainability
- Reduce coupling
- Increase extensibility
- Improve testability
- Guide AI-generated code
- Prevent inconsistent implementations

Only approved design patterns should be introduced into the codebase.

---

# Design Philosophy

The platform follows these principles:

- SOLID
- Clean Architecture
- Domain Driven Design (DDD)
- Composition over Inheritance
- Dependency Injection
- Explicit Dependencies
- High Cohesion
- Loose Coupling
- Separation of Concerns

Patterns should solve real architectural problems.

Avoid using patterns simply because they exist.

---

# Pattern Categories

The platform uses the following pattern categories:

- Architectural Patterns
- Creational Patterns
- Structural Patterns
- Behavioral Patterns
- Enterprise Patterns
- Integration Patterns
- Cloud Patterns
- AI Patterns

---

# Architectural Patterns

## 1. Clean Architecture

**Status:** Mandatory

All modules follow Clean Architecture.

```text
Presentation

↓

Application

↓

Domain

↑

Infrastructure
```

### Benefits

- Testable
- Independent
- Maintainable
- Framework Independent

---

## 2. Domain Driven Design (DDD)

**Status:** Mandatory

Every business module represents a bounded context.

Examples

- Client Management
- Project Management
- Workflow Engine
- Review Engine
- Resource Management

DDD components

- Entities
- Value Objects
- Aggregates
- Domain Services
- Domain Events
- Repositories

---

## 3. Modular Monolith

**Status:** Phase 1–3

Business domains are isolated into independent modules.

```text
Client

Project

Task

Workflow

Review

Finance
```

Communication occurs only through public contracts.

---

## 4. Event-Driven Architecture

**Status:** Mandatory

Business events are published instead of calling modules directly.

```text
Task Created

↓

Domain Event

↓

Notification

↓

Reporting

↓

Workflow
```

Benefits

- Loose coupling
- Better scalability
- Easy extensibility

---

# Creational Patterns

## 5. Dependency Injection

**Status:** Mandatory

Constructor Injection only.

Good

```csharp
public ProjectService(
    IRepository repository,
    ILogger<ProjectService> logger)
```

Never use

- Service Locator
- Static Dependencies

---

## 6. Factory Pattern

Used when object creation becomes complex.

Examples

- Workflow Factory
- Notification Factory
- AI Provider Factory
- Repository Factory

Example

```text
NotificationFactory

↓

Email

SMS

Teams

Slack
```

---

## 7. Abstract Factory

Used for provider-independent services.

Examples

- Storage Providers
- Authentication Providers
- AI Providers
- Source Control Providers

```text
IAIProvider

↓

OpenAI

Claude

Gemini

Ollama
```

---

## 8. Builder Pattern

Used for constructing complex objects.

Examples

- Report Builder
- Workflow Builder
- Dashboard Builder
- Query Builder

---

# Structural Patterns

## 9. Adapter Pattern

Mandatory for external integrations.

Examples

```text
GitHub Adapter

GitLab Adapter

Azure DevOps Adapter
```

Also used for

- Payment Providers
- Storage Providers
- AI Providers

---

## 10. Facade Pattern

Used to simplify complex subsystems.

Example

```text
AI Platform

↓

Facade

↓

Prompt

↓

RAG

↓

Memory

↓

Model
```

Business modules call only the facade.

---

## 11. Proxy Pattern

Used for

- Authorization
- Lazy Loading
- Caching
- Remote Services

---

## 12. Decorator Pattern

Used to extend functionality without modifying classes.

Examples

```text
Logging

Caching

Retry

Authorization
```

---

# Behavioral Patterns

## 13. Strategy Pattern

Used when multiple algorithms exist.

Examples

- Pricing Strategy
- Allocation Strategy
- AI Routing Strategy
- Notification Strategy

Example

```text
Notification

↓

Email Strategy

SMS Strategy

Push Strategy
```

---

## 14. State Pattern

Mandatory for Workflow Engine.

```text
Task

↓

Assigned

↓

In Progress

↓

Review

↓

Completed
```

State transitions encapsulate behavior.

---

## 15. Command Pattern

Mandatory for CQRS.

Examples

```text
CreateProjectCommand

UpdateTaskCommand

DeleteAssetCommand
```

Commands modify state.

---

## 16. Query Pattern

Used with CQRS.

Examples

```text
GetProjectQuery

SearchAssetsQuery

GetDashboardQuery
```

Queries never modify state.

---

## 17. Observer Pattern

Used for internal notifications.

Example

```text
Task Updated

↓

Subscribers

↓

Notification

Reporting

Audit

Analytics
```

Implemented through Domain Events.

---

## 18. Mediator Pattern

Used to reduce component dependencies.

Implemented using MediatR.

```text
Controller

↓

Mediator

↓

Handler
```

---

## 19. Chain of Responsibility

Used for request processing.

Examples

```text
Authentication

↓

Authorization

↓

Validation

↓

Logging

↓

Business Logic
```

Also used for middleware.

---

## 20. Template Method

Used for workflows with common steps.

Examples

- Import Process
- Export Process
- Approval Process

---

# Enterprise Patterns

## 21. Repository Pattern

Mandatory.

Repositories

- Retrieve Aggregates
- Persist Aggregates
- Abstract Data Access

Repositories never contain business rules.

---

## 22. Unit of Work

Managed through Entity Framework Core.

Coordinates

- Transactions
- Save Changes
- Rollback

---

## 23. Specification Pattern

Used for complex business filtering.

Example

```text
Active Projects

AND

Client = ABC

AND

Priority = High
```

Reusable specifications improve maintainability.

---

## 24. Domain Events

Mandatory.

Business changes publish immutable events.

Examples

```text
ProjectCreated

TaskAssigned

ReviewCompleted
```

---

## 25. Aggregate Pattern

Business consistency boundaries.

Examples

```text
Project

↓

Tasks

↓

Deliverables
```

Only the Aggregate Root controls modifications.

---

## 26. Value Objects

Used for immutable concepts.

Examples

- Money
- Address
- DateRange
- EmailAddress
- PhoneNumber

---

# Integration Patterns

## 27. API Gateway Pattern

All external requests pass through the API Gateway.

Responsibilities

- Authentication
- Routing
- Rate Limiting
- Logging

---

## 28. Publish–Subscribe

Used for asynchronous communication.

```text
Publisher

↓

Message Bus

↓

Subscribers
```

---

## 29. Retry Pattern

Used for transient failures.

Examples

- Email
- Storage
- AI APIs
- External APIs

Use exponential backoff.

---

## 30. Circuit Breaker

Protects external dependencies.

Used for

- AI Providers
- Payment Gateways
- Git Providers
- Cloud Storage

---

## 31. Bulkhead Pattern

Isolates failures between subsystems.

Example

AI failures must not affect:

- Workflow
- Authentication
- Reporting

---

# Cloud Patterns

## 32. Health Check Pattern

Every service exposes

```text
/health
```

Checks include

- Database
- Cache
- Queue
- AI
- Storage

---

## 33. Background Worker Pattern

Used for

- Imports
- Exports
- AI Processing
- Notifications
- Report Generation

---

## 34. Cache Aside Pattern

Preferred caching strategy.

```text
Request

↓

Cache

↓

Database

↓

Update Cache
```

---

## 35. Outbox Pattern

Used for reliable event publishing.

Flow

```text
Business Transaction

↓

Outbox Table

↓

Event Publisher

↓

Message Bus
```

Ensures database changes and event publication remain consistent.

---

# AI Patterns

## 36. Multi-Agent Pattern

Multiple specialized AI agents collaborate.

```text
Planner

↓

Reviewer

↓

Risk Analyzer

↓

Documentation Agent
```

---

## 37. RAG Pattern

Retrieval-Augmented Generation.

```text
Question

↓

Embedding

↓

Vector Search

↓

Context

↓

LLM
```

---

## 38. Provider Strategy Pattern

AI providers are interchangeable.

```text
IAIProvider

↓

OpenAI

Claude

Gemini

Ollama
```

---

## 39. Prompt Template Pattern

Prompts are stored separately from code.

Benefits

- Versioning
- Reusability
- Governance

---

## 40. Human-in-the-Loop Pattern

Critical AI decisions require approval.

Examples

- Financial Approval
- Workflow Approval
- Production Deployment
- Permission Changes

---

# Patterns Explicitly Avoided

The following patterns are **not approved** unless justified through an ADR.

## Singleton

Reason

- Global State
- Difficult Testing
- Hidden Dependencies

Dependency Injection already manages object lifetime.

---

## Active Record

Reason

- Violates DDD
- Mixes persistence with business logic
- Poor separation of concerns

---

## Anemic Domain Model

Reason

Business rules must remain inside the Domain.

---

## God Object

Reason

- Difficult maintenance
- High coupling
- Poor scalability

---

## Service Locator

Reason

- Hidden dependencies
- Difficult testing
- Violates Dependency Injection principles

---

# Pattern Selection Guidelines

Choose patterns based on the problem:

| Problem | Recommended Pattern |
|----------|---------------------|
| Business lifecycle | State |
| Complex object creation | Builder |
| External system integration | Adapter |
| Multiple algorithms | Strategy |
| Business events | Observer / Domain Events |
| Cross-module communication | Publish–Subscribe |
| Data persistence | Repository |
| Command execution | Command |
| Read operations | Query |
| Complex filtering | Specification |
| AI provider abstraction | Strategy + Abstract Factory |
| Background processing | Worker |
| Reliable messaging | Outbox |

---

# AI Development Rules

AI-generated code must:

- Use approved patterns only
- Reuse existing abstractions
- Avoid introducing unnecessary patterns
- Follow module boundaries
- Respect Clean Architecture
- Produce testable implementations
- Document any new pattern usage

If a new pattern is required, an **Architecture Decision Record (ADR)** must be created before adoption.

---

# Summary

The Project & Asset Management Platform adopts a carefully selected set of proven enterprise design patterns centered on **Clean Architecture**, **Domain-Driven Design**, **Event-Driven Communication**, and **Dependency Injection**. These patterns provide a consistent foundation for human developers and AI agents, enabling the platform to remain maintainable, scalable, secure, and adaptable while avoiding unnecessary complexity and architectural drift.
