# 09_SQL_Schema.md

## Objective

You are acting as a Principal Enterprise Database Architect responsible for designing the complete SQL Schema Specification for an Enterprise School Management System (SMS).

This document is the authoritative physical database specification derived from the previously completed architecture documents including:

- Database Architecture
- Entity Catalog
- Entity Relationships
- Normalization Strategy
- Indexing Strategy
- Partitioning Strategy
- Audit Strategy
- Migration Strategy

This document translates the logical database model into a complete physical relational schema specification while remaining implementation-independent.

It is NOT intended to generate SQL statements.

Instead, it defines every physical database design decision required before implementation.

Assume every business module, entity catalog, API catalog, contracts, workflows, and security documents already exist.

Reference previous documentation rather than duplicating it.

---

# Scope

Generate the complete SQL Schema Specification covering:

Entire Enterprise School Management System including:

Master Administration

Student

Academic

Attendance

Examination

Fees

Timetable

Homework

LMS

Communication

Parent Portal

Transport

Hostel

Library

Inventory

HRMS

Discipline

Events

Alumni

Audit

Reporting

Background Processing

Configuration

Future Extensions

---

# Enterprise Database Principles

Database remains normalized.

Every table has a single ownership domain.

Primary keys remain immutable.

Business identifiers remain version-safe.

Audit information is standardized.

Soft deletion follows institutional policies.

Foreign key relationships remain explicit.

Historical data is preserved.

Large transactional tables support partitioning.

Indexes follow the indexing strategy.

Database remains vendor-neutral.

---

# Document Structure

## 1. Physical Database Overview

Describe:

Database Purpose

Physical Architecture

Logical vs Physical Mapping

Database Boundaries

Naming Standards

Object Organization

Storage Philosophy

Normalization Level

Historical Data Strategy

Future Growth

---

## 2. Schema Organization

Define database schemas such as:

Administration

Academic

Student

Attendance

Examination

Fees

Learning

Communication

Operations

Reporting

Audit

Security

Configuration

Integration

Background Jobs

Future Extensions

For every schema explain:

Purpose

Contained Tables

Ownership

Dependencies

Security Classification

Growth Expectations

---

## 3. Physical Table Catalog

Generate the complete physical table catalog.

For every table define:

Owning Module

Schema

Business Purpose

Primary Key

Business Keys

Foreign Keys

Unique Constraints

Nullable Rules

Audit Columns

Soft Delete Strategy

Partition Strategy

Archive Strategy

Growth Characteristics

Retention Policy

Dependencies

Expected Relationships

Read Patterns

Write Patterns

Reporting Usage

Future Extension Notes

Generate for every table across all modules.

---

## 4. Standard Column Conventions

Define standard columns including:

Primary Keys

Foreign Keys

Business Codes

Created By

Created At

Updated By

Updated At

Deleted At

Deleted By

Version

Status

Lifecycle State

Approval State

Audit Identifier

Tenant Identifier (future)

Synchronization Identifier

Correlation Identifier

External Identifier

Import Identifier

Explain usage standards.

---

## 5. Constraint Standards

Define standards for:

Primary Keys

Foreign Keys

Unique Constraints

Composite Keys

Business Constraints

Check Constraints

Nullable Rules

Default Values

Referential Integrity

Cascade Rules

Historical Constraints

Soft Delete Constraints

Version Constraints

---

## 6. Relationship Standards

Describe standards for:

One-to-One

One-to-Many

Many-to-Many

Bridge Tables

Hierarchy Tables

Lookup Tables

Reference Tables

Temporal Relationships

Versioned Relationships

Historical Relationships

Ownership Relationships

---

## 7. Data Type Standards

Define enterprise standards for:

Identifiers

Codes

Names

Descriptions

Money

Percentages

Dates

Times

DateTime

Time Zone

Boolean

JSON Readiness

Binary Files

Large Text

Version Numbers

Status Values

Enumerations

UUID Readiness

Future Globalization

---

## 8. Naming Standards

Define standards for:

Schemas

Tables

Columns

Indexes

Constraints

Views

Sequences

Triggers

Functions

Materialized Views

Bridge Tables

History Tables

Temporary Tables

Archive Tables

Import Tables

Export Tables

---

## 9. Database Object Standards

Describe standards for:

Tables

Views

Materialized Views

History Tables

Archive Tables

Bridge Tables

Lookup Tables

Reference Tables

Temporary Tables

Import Tables

Export Tables

Sequences

Synonyms (future)

---

## 10. Reporting Model

Describe:

Reporting Views

Aggregated Views

Materialized Views

Operational Views

Executive Views

Analytics Views

Dashboard Views

Historical Views

Snapshot Views

Security Views

Read-only Views

Future Data Warehouse Readiness

---

## 11. Performance Considerations

Discuss:

Partition Alignment

Index Alignment

Large Tables

Historical Tables

Archiving

Compression Readiness

Read Optimization

Write Optimization

Reporting Optimization

Concurrency

Future Horizontal Scaling

---

## 12. Migration Readiness

Describe:

Schema Evolution

Backward Compatibility

Forward Compatibility

Migration Order

Reference Data

Seed Data

Versioning

Rollback Strategy

Deployment Strategy

Validation

Verification

---

## 13. AI Coding Agent Guidance

Provide implementation guidance covering:

Database creation order

Schema order

Lookup tables

Reference tables

Master tables

Transactional tables

History tables

Bridge tables

Indexes

Constraints

Views

Reporting

Migration sequencing

Avoiding circular references

Repository mapping

Entity mapping

Future ORM generation

---

## 14. Architecture Decision Summary

Generate a summary table.

Columns:

Area

Decision

Reason

Business Impact

Technical Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise SQL Schema Specification.

Do NOT generate:

- SQL CREATE TABLE statements

- DDL

- Database vendor syntax

- Stored procedures

- Functions

- Triggers

Instead describe the complete physical schema architecture in implementation-independent language.

This document should become the definitive blueprint from which SQL Server, PostgreSQL, MySQL, Oracle, MariaDB, or any enterprise RDBMS schema can be generated without additional architectural decisions.
