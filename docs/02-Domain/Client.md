# Client Domain

> **Purpose**
>
> The Client domain represents the organizations for whom the company delivers services. It is the highest business entity in the operational hierarchy and serves as the financial and contractual owner of Projects.
>
> Although invoices are generated **against Projects**, every invoice ultimately belongs to a Client through its associated Project.

---

# Overview

A Client represents a customer organization that engages the company for one or more Projects.

The Client module provides a centralized location to manage:

- Client Information
- Contacts
- Addresses
- Billing Information
- Project Portfolio
- Financial Summary
- Communication
- Activity History

The Client itself does **not** participate in production workflows but acts as the business owner of Projects.

---

# Business Hierarchy

```text
Client
│
├── Contacts
├── Addresses
├── Projects
│      │
│      ├── Batches
│      ├── Assets
│      ├── Tasks
│      └── Deliverables
│
├── Financial Summary
├── Communication
├── Documents
└── Activity Timeline
```

---

# Objectives

The Client module should enable the organization to:

- Maintain a centralized customer database
- Track all active and historical Projects
- Monitor client revenue
- Track outstanding payments
- Manage billing information
- Maintain communication history
- Generate client-level reports

---

# Business Ownership

| Property | Value |
|----------|-------|
| Domain Owner | Sales / Business Development |
| Operational Owner | Project Management Office |
| Financial Owner | Finance Department |

---

# Entity Relationship

```text
Parent Client (Optional)
        │
        ▼
     Client
        │
        ├─────────────┐
        ▼             ▼
   Contacts       Addresses
        │
        ▼
    Projects
        │
        ▼
   Financial Summary
```

---

# Core Information

## Basic Information

The Client stores the primary business identity.

Typical information includes:

- Client Name
- Display Name
- Short Code
- Parent Client
- Business Type
- Industry
- Status

---

## Geographic Information

Location information includes:

- Country
- State / Province
- Region
- City
- Postal Code
- Time Zone

---

## Address Information

A Client may maintain multiple addresses.

Examples:

- Corporate Office
- Billing Address
- Shipping Address
- Regional Office

One address may be marked as the default billing address.

---

## Contact Management

A Client may have multiple contacts.

Typical contacts include:

- Account Manager
- Producer
- Finance Contact
- Technical Contact
- Legal Contact

Each contact may have:

- Email
- Phone
- Designation
- Department

---

# Parent Client

Large organizations often consist of multiple business units.

Example:

```text
Microsoft
│
├── Xbox Studios
├── Mojang
├── Bethesda
└── Activision
```

Projects may belong to any child Client while reports can be aggregated at the Parent Client level.

---

# Project Relationship

A Client may own multiple Projects.

```text
Client

↓

Project A

Project B

Project C
```

Projects cannot exist without a Client.

---

# Financial Relationship

Financial ownership is organized as follows:

```text
Client
      │
      ▼
Project
      │
      ▼
Invoice
      │
      ▼
Payment
```

Important business rule:

> Invoices are generated **against Projects**, not directly against Clients.

The Client Financial Summary aggregates information from all associated Project invoices.

---

# Financial Summary

The platform automatically calculates client-level financial metrics.

Examples include:

- Total Revenue
- Total Invoiced Amount
- Outstanding Amount
- Total Payments Received
- Discounts
- Waivers
- Average Collection Time
- Active Projects
- Completed Projects

These values are calculated rather than manually maintained.

---

# Communication

The Client maintains a centralized communication history.

Supported features:

- Discussions
- Rich Text Notes
- Attachments
- Mentions
- Activity Timeline

This communication is intended for account-level discussions and is separate from Project-specific communication.

---

# Documents

Client-level documents may include:

- Master Service Agreements
- Contracts
- Non-Disclosure Agreements
- Tax Documents
- Purchase Orders
- Billing Instructions

These documents are administrative and not production deliverables.

---

# Activity Timeline

Every significant business action is recorded.

Examples include:

- Client Created
- Information Updated
- Contact Added
- Address Changed
- Project Created
- Invoice Generated
- Payment Recorded
- Client Archived

---

# Business Rules

## BR-001

A Client must have a unique Name.

---

## BR-002

Every Project must belong to exactly one Client.

---

## BR-003

A Client may have multiple Projects.

---

## BR-004

A Client may optionally belong to a Parent Client.

---

## BR-005

A Client may have multiple Contacts.

---

## BR-006

A Client may have multiple Addresses.

---

## BR-007

Financial information displayed at the Client level is derived from Project-level transactions.

---

## BR-008

Deleting a Client is not permitted if Projects exist.

Clients should instead be marked as Inactive or Archived.

---

## BR-009

Inactive Clients remain available for historical reporting.

---

## BR-010

Communication and activity history must never be deleted.

---

# Lifecycle

```text
Draft
    │
Active
    │
Inactive
    │
Archived
```

---

# Status Definitions

| Status | Description |
|----------|-------------|
| Draft | Client record under preparation |
| Active | Available for new Projects |
| Inactive | No new Projects can be created |
| Archived | Historical reference only |

---

# Permissions

Typical permissions include:

| Permission | Description |
|------------|-------------|
| View Client | View client information |
| Create Client | Create new client |
| Edit Client | Modify client details |
| Delete Client | Archive or deactivate client |
| Manage Contacts | Add/Edit contacts |
| Manage Addresses | Add/Edit addresses |
| View Financial Summary | Access financial metrics |
| View Communication | Read discussions |
| Manage Communication | Create discussions |

---

# Reporting

The Client module supports reports such as:

- Client Directory
- Active Clients
- Inactive Clients
- Revenue by Client
- Outstanding Payments
- Project Portfolio
- Client Growth
- Top Clients by Revenue
- Collection Summary

---

# Future Enhancements

Future versions may include:

- CRM Integration
- Client Portal
- Client Satisfaction Tracking
- Contract Renewal Management
- SLA Management
- Automated Credit Limits
- Customer Health Score
- Multi-Currency Billing
- Multi-Legal Entity Support

---

# Related Documents

- EntityRelationship.md
- Project.md
- Finance.md
- CommunicationModel.md
- AuditModel.md
- BusinessRules.md

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | TBD | Project Team | Initial Client domain specification |
