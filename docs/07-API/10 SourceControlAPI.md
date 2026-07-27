# Source Control API

**Document Version:** 1.0  
**Module:** Source Control Integration API  
**Applies To:** Entire Project & Asset Management Platform  
**Audience:** Backend Developers, DevOps Engineers, Solution Architects, AI Agents, Integration Developers

---

# Purpose

This document defines the Source Control API abstraction layer used by the Project & Asset Management Platform.

The platform is designed to integrate with multiple Source Control Management (SCM) systems through a common interface, allowing projects, tasks, reviews, AI agents, and workflows to interact with repositories without being tightly coupled to a specific provider.

---

# Objectives

The Source Control API enables:

- Repository Management
- Branch Management
- Commit Tracking
- Pull / Merge Requests
- Tag Management
- Release Tracking
- Code Review Integration
- AI Code Analysis
- Build Pipeline Integration
- Deployment Tracking

---

# Supported Providers

Version 1 supports:

- GitHub
- Azure DevOps Repositories
- GitLab
- Bitbucket

Future support:

- AWS CodeCommit
- Gitea
- Gogs
- Perforce (Metadata Integration)

---

# Architecture

```text
Application

        │

Source Control Service

        │

SCM Provider Adapter

        │

─────────────────────────────

GitHub

Azure DevOps

GitLab

Bitbucket

─────────────────────────────
```

The application communicates only with the **Source Control Service**.

---

# Design Principles

The integration layer should:

- Be provider independent
- Support dependency injection
- Be asynchronous
- Support multiple repositories
- Be event-driven
- Cache metadata when appropriate
- Support future providers without changing business logic

---

# Authentication

Supported authentication mechanisms:

- OAuth 2.0
- Personal Access Token (PAT)
- GitHub App
- Azure Service Principal
- GitLab Access Token
- Bitbucket App Password

Credentials are stored securely in the platform's secret management system.

---

# Repository Model

A repository contains:

- Repository ID
- Name
- Provider
- Organization
- Default Branch
- Clone URL
- Visibility
- Status

---

# Supported Operations

## Repository

| Method | Endpoint | Description |
|---------|----------|-------------|
| GET | /repositories | List repositories |
| GET | /repositories/{id} | Repository details |
| POST | /repositories | Register repository |
| PUT | /repositories/{id} | Update repository |
| DELETE | /repositories/{id} | Remove repository |
| POST | /repositories/{id}/sync | Synchronize metadata |

---

## Branches

| Method | Endpoint |
|---------|----------|
| GET | /repositories/{id}/branches |
| GET | /repositories/{id}/branches/{branch} |
| POST | /repositories/{id}/branches |
| DELETE | /repositories/{id}/branches/{branch} |

---

## Commits

| Method | Endpoint |
|---------|----------|
| GET | /repositories/{id}/commits |
| GET | /repositories/{id}/commits/{commitId} |
| GET | /repositories/{id}/commits/latest |

---

## Pull Requests

| Method | Endpoint |
|---------|----------|
| GET | /repositories/{id}/pull-requests |
| GET | /repositories/{id}/pull-requests/{prId} |
| POST | /repositories/{id}/pull-requests |
| PUT | /repositories/{id}/pull-requests/{prId} |
| POST | /repositories/{id}/pull-requests/{prId}/approve |
| POST | /repositories/{id}/pull-requests/{prId}/merge |

---

## Tags

| Method | Endpoint |
|---------|----------|
| GET | /repositories/{id}/tags |
| POST | /repositories/{id}/tags |

---

## Releases

| Method | Endpoint |
|---------|----------|
| GET | /repositories/{id}/releases |
| GET | /repositories/{id}/releases/{releaseId} |

---

# Repository Registration

Each repository registration includes:

- Provider
- Organization
- Repository Name
- Default Branch
- Credentials Reference
- Project Mapping
- Active Status

---

# Branch Strategy

Recommended strategy:

```text
main

develop

feature/*

bugfix/*

release/*

hotfix/*
```

The platform validates branch names against configured policies.

---

# Repository Mapping

Projects may link to one or more repositories.

```text
Project

↓

Repositories

↓

Branches

↓

Pull Requests

↓

Commits
```

---

# Commit Metadata

Stored metadata includes:

- Commit ID
- Author
- Committer
- Branch
- Message
- Timestamp
- Repository
- Linked Task (Optional)

---

# Commit Message Convention

Recommended format:

```text
[PROJECT-123] Added workflow validation

[TASK-445] Fixed asset upload issue

[BUG-52] Corrected approval logic
```

Allows automatic linkage between commits and work items.

---

# Pull Request Metadata

The platform tracks:

- PR Number
- Title
- Source Branch
- Target Branch
- Status
- Reviewers
- Approval Count
- Merge Status

---

# Task Integration

Tasks may reference:

- Repository
- Branch
- Pull Request
- Commit
- Release

Example:

```text
Task

↓

Feature Branch

↓

Commit

↓

Pull Request

↓

Merge

↓

Task Completed
```

---

# AI Integration

AI Agents can:

- Analyze commits
- Review pull requests
- Generate commit summaries
- Detect coding standards violations
- Recommend reviewers
- Suggest release notes
- Generate documentation

AI Agents never push code directly without explicit authorization.

---

# Events

The Source Control module publishes events such as:

```text
RepositoryRegistered

BranchCreated

CommitReceived

PullRequestCreated

PullRequestMerged

ReleasePublished
```

Consumers include:

- Workflow Engine
- Notification Service
- AI Platform
- Reporting
- Audit Service

---

# Webhooks

Supported incoming webhook events:

GitHub

- Push
- Pull Request
- Release
- Issue
- Branch

Azure DevOps

- Push
- Pull Request
- Build Completed
- Release Completed

GitLab

- Push
- Merge Request
- Pipeline
- Tag

---

# Synchronization

Synchronization modes:

## Manual

Administrator triggers synchronization.

---

## Scheduled

Runs periodically.

Example

```text
Every 15 Minutes
```

---

## Event Driven

Triggered immediately by SCM webhooks.

Preferred option.

---

# Caching

Frequently accessed metadata may be cached.

Examples

- Repository List
- Branches
- Recent Commits
- Open Pull Requests

Cache invalidation occurs after webhook events or scheduled synchronization.

---

# Security

Every operation requires authorization.

Example permissions:

```text
SourceControl.Read

SourceControl.Manage

SourceControl.Sync

SourceControl.Merge

SourceControl.Admin
```

---

# Audit Logging

Log:

- Repository Registration
- Synchronization
- Branch Creation
- Pull Request Approval
- Merge
- Configuration Changes

Each log includes:

- User
- Tenant
- Repository
- Timestamp
- Correlation ID

---

# Error Handling

Common error codes:

```text
REPOSITORY_NOT_FOUND

BRANCH_NOT_FOUND

INVALID_PROVIDER

AUTHENTICATION_FAILED

SYNC_FAILED

MERGE_CONFLICT

PULL_REQUEST_NOT_FOUND
```

Errors follow the platform's standard error response model.

---

# Performance Targets

| Operation | Target |
|-----------|---------|
| Repository List | < 2 seconds |
| Branch List | < 2 seconds |
| Commit Synchronization | < 30 seconds |
| Pull Request Retrieval | < 5 seconds |
| Webhook Processing | < 2 seconds |

---

# Extensibility

New SCM providers should only require implementing the common adapter interface.

Business modules remain unchanged.

---

# AI Development Guidelines

AI-generated source control integrations must:

- Use the abstraction layer
- Avoid provider-specific logic in business modules
- Validate webhook signatures
- Handle retries safely
- Log synchronization operations
- Respect repository permissions

AI must never:

- Store credentials in source code
- Push directly to protected branches
- Automatically merge pull requests without policy approval
- Bypass branch protection rules

---

# Development Guidelines

Developers should:

- Program against interfaces
- Use asynchronous APIs
- Handle rate limits
- Cache metadata responsibly
- Validate provider responses
- Publish domain events after synchronization

---

# Source Control Checklist

Before deployment verify:

- ✓ Repository abstraction implemented
- ✓ Provider adapters configured
- ✓ Authentication secured
- ✓ Webhooks configured
- ✓ Synchronization enabled
- ✓ Branch strategy enforced
- ✓ Audit logging enabled
- ✓ Permissions configured
- ✓ Event publishing enabled
- ✓ AI integration validated

---

# Future Enhancements

Planned capabilities include:

- Repository Analytics
- Code Ownership Tracking
- Branch Protection Management
- Automatic Release Notes
- Security Vulnerability Scanning
- Dependency Analysis
- Multi-Repository Projects
- Commit Quality Metrics
- AI-Assisted Code Review
- AI-Generated Pull Requests

---

# Summary

The Project & Asset Management Platform provides a provider-independent Source Control API that abstracts GitHub, Azure DevOps, GitLab, and Bitbucket behind a unified interface. The architecture supports repository management, branches, commits, pull requests, releases, webhooks, synchronization, workflow integration, and AI-assisted development while maintaining strong security, auditability, scalability, and extensibility for future SCM providers.
