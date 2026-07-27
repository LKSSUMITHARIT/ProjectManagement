# Coding Standards

**Document Version:** 1.0  
**Module:** Development Standards  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Developers, AI Agents, Architects, Code Reviewers, DevOps Engineers

---

# Purpose

This document defines the mandatory coding standards for the Project & Asset Management Platform.

Its objectives are to:

- Maintain a consistent codebase
- Improve readability
- Reduce technical debt
- Increase maintainability
- Improve security
- Simplify onboarding
- Enable AI-generated code consistency
- Support long-term scalability

These standards apply equally to:

- Human Developers
- AI Coding Agents
- Code Generation Tools
- Automated Refactoring Tools

---

# Technology Stack

## Backend

- .NET 10
- ASP.NET Core
- C#
- Entity Framework Core
- PostgreSQL
- Redis
- SignalR

---

## Frontend

- Blazor
- HTML5
- CSS3
- TailwindCSS
- JavaScript (ES2023)
- TypeScript (Optional)

---

## Infrastructure

- Docker
- Kubernetes
- GitHub
- GitHub Actions
- Azure
- Nginx

---

# General Principles

The project follows these principles:

- Clean Code
- SOLID
- KISS
- DRY
- YAGNI
- Separation of Concerns
- Dependency Injection
- Domain Driven Design
- CQRS (where applicable)
- Event Driven Architecture

---

# Coding Philosophy

Every piece of code should be

- Easy to understand
- Easy to modify
- Easy to test
- Secure
- Performant
- Well documented
- Predictable

Code is written for humans first.

---

# Naming Conventions

## Projects

```text
ProjectManagement.API

ProjectManagement.Core

ProjectManagement.Domain

ProjectManagement.Infrastructure
```

---

## Namespaces

```csharp
ProjectManagement.Domain.Entities

ProjectManagement.Application.Services

ProjectManagement.Infrastructure.Persistence
```

---

## Classes

Use PascalCase.

```csharp
ProjectService

TaskManager

NotificationProcessor
```

---

## Interfaces

Prefix with I.

```csharp
IProjectService

IRepository

ILogger
```

---

## Methods

Use PascalCase.

```csharp
CreateProject()

UpdateTask()

DeleteAsset()
```

Method names must describe actions.

---

## Variables

Use camelCase.

```csharp
project

taskCount

currentUser
```

---

## Constants

Use PascalCase.

```csharp
MaxRetryCount

DefaultTimeout
```

---

## Enums

Use PascalCase.

```csharp
ProjectStatus

TaskPriority
```

Enum values

```csharp
Pending

Approved

Rejected
```

---

## Files

One public class per file.

File name must match class name.

```text
ProjectService.cs

Task.cs

InvoiceRepository.cs
```

---

# Folder Organization

Feature-based organization is preferred.

Example

```text
Projects

    Commands

    Queries

    DTOs

    Validators

    Services

    Controllers
```

Avoid dumping unrelated classes into shared folders.

---

# Code Formatting

Indentation

- 4 Spaces
- No Tabs

Maximum line length

120 characters

Use UTF-8 encoding.

Always end files with a newline.

---

# Comments

Code should be self-explanatory.

Comments explain **why**, not **what**.

Good

```csharp
// Prevent duplicate invoice generation
```

Bad

```csharp
// Increment i
i++;
```

---

# XML Documentation

Public APIs require XML documentation.

```csharp
/// <summary>
/// Creates a new project.
/// </summary>
public Task<ProjectDto> CreateAsync(...)
```

---

# Regions

Avoid excessive use.

Allowed only for

- Constructors
- Public Methods
- Private Methods

Do not create nested regions.

---

# Method Design

Methods should

- Perform one responsibility
- Be short
- Be readable
- Avoid side effects

Ideal length

20–40 lines

Maximum

100 lines

---

# Parameters

Maximum recommended parameters

5

Otherwise use DTOs.

Bad

```csharp
CreateProject(name, client, manager, startDate, endDate, budget, status)
```

Good

```csharp
CreateProject(CreateProjectRequest request)
```

---

# Class Design

Classes should follow the Single Responsibility Principle.

Avoid God Classes.

Recommended maximum

300–500 lines

---

# Exception Handling

Never swallow exceptions.

Bad

```csharp
catch
{
}
```

Good

```csharp
catch(Exception ex)
{
    _logger.LogError(ex, "Unable to create project.");

    throw;
}
```

---

# Logging

Use structured logging.

Good

```csharp
_logger.LogInformation(
    "Project {ProjectId} created by {UserId}",
    project.Id,
    userId);
```

Avoid string concatenation.

---

# Dependency Injection

Always use constructor injection.

Good

```csharp
public ProjectService(
    IRepository repository,
    ILogger<ProjectService> logger)
```

Never use Service Locator.

---

# Asynchronous Programming

Prefer async/await.

Bad

```csharp
.Result

.Wait()
```

Good

```csharp
await repository.SaveAsync();
```

Always propagate async.

---

# LINQ

Prefer readability over cleverness.

Avoid deeply nested LINQ.

Break into multiple statements when necessary.

---

# Nullable Reference Types

Nullable Reference Types must be enabled.

Avoid

```csharp
string Name;
```

Prefer

```csharp
string? Description;
```

when nullable.

---

# DTO Usage

Never expose EF entities directly.

Always use

- DTO
- Request
- Response
- ViewModel

---

# Repository Pattern

Repositories should only access data.

Business logic belongs in Services.

---

# Entity Framework

Always use

```csharp
AsNoTracking()
```

for read-only queries.

Use eager loading carefully.

Avoid unnecessary Include chains.

---

# Validation

Use FluentValidation.

Validation never belongs inside Controllers.

---

# Controllers

Controllers should

- Validate
- Authorize
- Call Service
- Return Result

Controllers should never contain business logic.

---

# API Responses

Use consistent response models.

Example

```json
{
  "success": true,
  "message": "Project created.",
  "data": {}
}
```

---

# JavaScript Standards

Use ES2023.

Avoid global variables.

Use modules.

Prefer

```javascript
const

let
```

Avoid

```javascript
var
```

---

# CSS Standards

Use TailwindCSS utilities.

Avoid inline CSS.

Maintain reusable components.

---

# Database Standards

Never use

```sql
SELECT *
```

Always specify columns.

Use parameterized queries.

Never concatenate SQL.

---

# Security Standards

Always

- Validate input
- Encode output
- Parameterize SQL
- Use HTTPS
- Protect secrets
- Authorize every request

Never trust client input.

---

# Performance Standards

Avoid

- N+1 queries
- Blocking calls
- Large object allocations
- Duplicate database calls

Measure before optimizing.

---

# Unit Testing

Every business service should have unit tests.

Recommended coverage

Minimum

80%

Critical modules

90%+

---

# Code Reviews

Every Pull Request must review

- Naming
- Readability
- Security
- Performance
- Testing
- Documentation
- Architecture
- Coding Standards

---

# AI Coding Standards

AI-generated code must

- Follow all project standards
- Produce compilable code
- Avoid deprecated APIs
- Include meaningful names
- Generate XML documentation
- Follow architecture
- Avoid unnecessary abstractions
- Produce deterministic results

AI must never:

- Invent APIs
- Skip validation
- Ignore security
- Introduce hidden dependencies
- Bypass architecture

---

# Pull Request Requirements

Every Pull Request must include

- Purpose
- Related Work Item
- Testing Performed
- Breaking Changes
- Screenshots (UI)
- Database Changes
- Rollback Notes

---

# Static Analysis

Mandatory tools

- Roslyn Analyzers
- StyleCop
- SonarQube
- CodeQL
- Dependabot

Build fails on critical violations.

---

# Definition of Clean Code

Good code is

- Readable
- Predictable
- Secure
- Tested
- Documented
- Maintainable
- Performant
- Reusable

---

# Code Quality Checklist

Before merging, verify:

- ✓ Builds successfully
- ✓ No compiler warnings
- ✓ No critical analyzer issues
- ✓ Unit tests pass
- ✓ Integration tests pass
- ✓ Documentation updated
- ✓ Security reviewed
- ✓ Performance reviewed
- ✓ Logging implemented
- ✓ Error handling implemented
- ✓ Naming standards followed
- ✓ Architecture respected

---

# Summary

These coding standards establish a consistent engineering foundation for both human developers and AI coding agents. Adhering to these standards ensures that the platform remains maintainable, secure, scalable, and easy to evolve throughout its lifecycle while enabling high-quality AI-assisted software development.
