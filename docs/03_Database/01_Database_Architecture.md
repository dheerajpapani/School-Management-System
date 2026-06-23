# 01_Database_Architecture.md

## Objective

You are a Principal Database Architect designing the database architecture for an enterprise-grade School Management System (SMS).

This document defines the architectural principles, organization, ownership, conventions, and design philosophy of the database.

This is **NOT** a SQL document.

This is **NOT** a table catalog.

This is **NOT** an ER diagram.

Instead, it defines how the database should be designed so that every future entity, table, relationship, migration, and query follows consistent engineering standards.

Assume the following documents already exist:

* Module Structure
* Blueprint
* System Architecture
* Functional Requirements
* Non-Functional Requirements

Do not duplicate those documents.

---

# Scope

Describe the complete database architecture that will support an enterprise School Management System containing all modules defined in the project.

Focus on architectural decisions rather than physical implementation.

---

# Document Structure

## 1. Purpose

Explain the goals of the database architecture.

Discuss:

* consistency
* maintainability
* scalability
* performance
* reliability
* auditability
* future extensibility

---

## 2. Database Philosophy

Describe the overall philosophy.

Examples:

Single relational database

Normalized core data

Controlled denormalization

Single source of truth

Soft delete strategy

Immutable historical records

Business-driven data ownership

Minimal redundancy

Configuration-driven behavior

Explain why these principles are used.

---

## 3. Database Scope

Describe what the database stores.

Examples:

Academic data

Students

Parents

Employees

Fees

Finance

Attendance

Library

Transport

Hostel

Inventory

Events

Audit

Notifications

Configuration

Files

Reference data

Explain what is intentionally outside the database (temporary cache, generated files, logs stored elsewhere, etc.).

---

## 4. Domain Separation

Organize the database into logical domains.

Examples:

Administration

Academic

Student

Attendance

Examination

Finance

Communication

Transport

Hostel

Library

Inventory

HRMS

Events

Discipline

Alumni

System

For every domain describe:

Responsibilities

Owned data

Dependencies

Isolation rules

---

## 5. Data Ownership

Define ownership rules.

Every entity must have exactly one owner.

Examples:

Student module owns student profile.

Attendance owns attendance records.

Fees owns invoices.

HR owns employee records.

No other module may directly modify another module's master data.

Describe synchronization rules.

---

## 6. Entity Categories

Classify future entities.

Examples:

Master Data

Reference Data

Transactional Data

Configuration Data

Historical Data

Audit Data

Reporting Data

Temporary Data

Derived Data

Integration Data

Explain lifecycle expectations for each category.

---

## 7. Naming Standards

Define naming conventions.

Tables

Columns

Indexes

Foreign keys

Unique constraints

Views

Stored procedures (if any)

Triggers (if any)

Sequences

Migration files

Primary keys

Junction tables

Audit tables

Temporary tables

Configuration tables

Include examples.

---

## 8. Key Strategy

Define how identifiers work.

Primary Keys

Business Keys

Natural Keys

Surrogate Keys

Composite Keys

UUID readiness

External IDs

Public IDs

Sequence generation philosophy

Never define SQL.

Only define standards.

---

## 9. Relationship Strategy

Describe relationship philosophy.

One-to-One

One-to-Many

Many-to-Many

Self-referencing

Hierarchical data

Reference tables

Lookup tables

Bridge tables

Ownership vs reference

Cascading strategy

Orphan prevention

---

## 10. Historical Data Strategy

Describe handling of historical information.

Academic years

Student lifecycle

Fee history

Attendance history

Result history

Transfer history

Promotion history

Versioned records

Immutable records

Archival strategy

---

## 11. Soft Delete Strategy

Define:

Which entities support soft delete

Which require hard delete

Recovery expectations

Retention rules

Audit implications

---

## 12. Audit Strategy

Describe database audit philosophy.

Who changed data

When

Previous values

New values

Affected module

Reason

Traceability

Compliance expectations

---

## 13. Configuration Strategy

Describe handling of configurable behavior.

Global configuration

Branch configuration

Academic configuration

Feature flags

Workflow settings

Notification settings

Validation rules

Grading systems

Explain inheritance strategy.

---

## 14. Performance Strategy

Describe database-level performance philosophy.

Normalization

Controlled denormalization

Index-first thinking

Query optimization

Pagination

Partition readiness

Archival

Reporting optimization

Materialized summary readiness

Read-heavy optimization

Write-heavy optimization

---

## 15. Transaction Strategy

Describe transactional expectations.

Atomic operations

Financial transactions

Admission workflow

Promotion workflow

Attendance submission

Bulk imports

Rollback philosophy

Consistency guarantees

Isolation expectations

Deadlock handling

Idempotency readiness

---

## 16. Data Integrity Strategy

Define integrity expectations.

Referential integrity

Business integrity

Validation ownership

Unique constraints

Mandatory relationships

Consistency rules

Duplicate prevention

Orphan prevention

Cross-domain integrity

---

## 17. Storage Strategy

Describe storage expectations.

Text

Images

Documents

Generated PDFs

Large files

External storage readiness

Temporary uploads

Metadata storage

Retention

Cleanup

---

## 18. Reporting Strategy

Describe how the database supports reporting.

Operational reports

Analytical reports

Historical reports

Aggregations

Summary data

Read-only reporting

Future BI readiness

---

## 19. Scalability Strategy

Describe future scalability.

10,000+

students

Future 100,000+

students

Multiple branches

Future multi-school

Cloud deployment

Read replicas

Partition readiness

Sharding readiness

Data archival

Future distributed architecture

---

## 20. Migration Strategy

Describe database evolution.

Migration philosophy

Versioning

Rollback

Forward-only migrations

Seed data

Reference data

Environment synchronization

Deployment considerations

---

## 21. Database Decision Summary

Create a concise summary table.

Columns:

Decision

Reason

Impact

Future Consideration

This section becomes the quick reference for database architects.

---

# Writing Style

Maintain a professional enterprise database architecture specification.

Avoid SQL.

Avoid CREATE TABLE statements.

Avoid entity definitions.

Avoid ER diagrams.

Focus on architectural decisions, conventions, and long-term maintainability.

Write with enough precision that future AI coding agents can design every table consistently without needing additional architectural clarification.
