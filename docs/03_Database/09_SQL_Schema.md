# 09_SQL_Schema.md

## Objective

You are acting as a Principal Database Architect and Senior MySQL Engineer responsible for generating the production-ready SQL schema for an Enterprise School Management System (SMS).

This document is the authoritative physical database specification for the entire School Management System.

It must implement every architectural decision defined in all previously generated documentation.

Assume every previous document is authoritative.

Do not invent business rules.

Do not simplify the schema.

This SQL is intended to be production-ready.

---

## Target Platform

- PHP 8.1+
- MySQL 8.0+
- InnoDB
- utf8mb4
- utf8mb4_unicode_ci

---

## General Rules

Before generating any SQL:

1. Review all previously generated SQL.
2. Validate consistency.
3. Validate naming.
4. Validate FK references.
5. Validate indexes.
6. Validate normalization.
7. Report inconsistencies before generating new SQL.

Never regenerate previous tables.

Only append new tables.

Never modify previous SQL unless explicitly instructed.

---

## Table Standards

Every table must use:

CREATE TABLE IF NOT EXISTS

Every table should include wherever applicable:

- id
- uuid
- created_at
- updated_at
- deleted_at
- created_by
- updated_by
- deleted_by
- version
- status

Use:

PRIMARY KEY

UNIQUE

INDEX

FOREIGN KEY

CHECK constraints where appropriate

Comments

Soft Delete compatibility

Audit compatibility

Future extensibility

---

## Naming Convention

Tables

sms_

Example

sms_students

Columns

snake_case

Foreign Keys

entity_id

Indexes

idx_

Unique

uq_

Foreign Keys

fk_

Checks

chk_

---

## SQL Requirements

Generate:

Production-quality SQL

Normalized schema

Proper data types

Proper constraints

Proper FK relationships

Proper indexes

Consistent naming

Scalable design

No TODOs

No placeholders

No incomplete tables

---

## Output Format

Every generation must contain:

1. Scope
2. SQL
3. Dependency Notes
4. Validation Checklist
5. Completed Tables
6. Remaining Tables

---part-1---
Continue building

03_Database/09_SQL_Schema.md

using the previously generated SQL.

Do NOT regenerate previous tables.

Generate only the Core Platform schema.

Include:

Institution

Academic Years

Academic Terms

Branches

Departments

Classes

Sections

Users

Authentication

Roles

Permissions

Permission Groups

Role Permissions

User Roles

Menus

Menu Permissions

Application Settings

Configurations

Countries

States

Cities

Currencies

Languages

Timezones

Academic Calendar metadata

Lookup Tables

Reference Tables

Notification Templates

Feature Flags

Application Metadata

System Metadata

Background Job Metadata

File Metadata

Generate complete CREATE TABLE statements.

Include:

Indexes

Unique Constraints

Foreign Keys

Comments

Soft Delete

Audit fields

Versioning

Status

Use production-quality MySQL 8 SQL.

Finish with:

Completed Tables

Dependencies

Validation Checklist

Remaining Tables.

---part-2---
Continue generating the existing document:

docs/03_Database/09_SQL_Schema.md

This is **Part 2** of the complete production SQL schema.

Do NOT regenerate or modify any SQL generated in previous parts unless a consistency issue is detected.

---

## Step 1 — Review Previous SQL

Before generating any new SQL:

Review all previously generated SQL from Part 1.

Validate:

- Naming conventions
- Table prefixes (`sms_`)
- Primary keys
- UUID usage
- Audit fields
- Soft delete support
- Foreign key consistency
- Unique constraints
- Index naming
- Normalization
- Status fields
- Version fields
- Timestamp consistency

If any inconsistency is found:

- Report it first.
- Explain the impact.
- Propose the smallest correction.
- Do not silently change previous SQL.

Only continue if validation passes.

---

## Step 2 — Generate ONLY the Student Information System schema

Do NOT generate any tables outside this scope.

Generate complete production-ready SQL for:

### Admission

- Admission Enquiries
- Admission Applications
- Online Applications
- Admission Status Tracking
- Admission Tests
- Test Results
- Interview Scheduling
- Interview Evaluation
- Merit Lists
- Admission Approvals
- Admission Documents

### Student Core

- Students
- Student Academic Assignment
- Student Roll Number History
- Student Status History
- Student Promotion History
- Student Transfer History
- Student Exit Records
- Student Graduation Records

### Parent & Guardian

- Parents
- Guardians
- Parent-Student Relationship
- Guardian Authorization
- Emergency Contacts

### Student Profile

- Personal Information
- Family Information
- Academic Information
- Medical Information
- Hostel Information
- Transport Information

### Student Documents

Generate document tables for:

- Birth Certificate
- Aadhaar
- Transfer Certificate
- Previous Marksheets
- Medical Records
- Identity Proofs
- Passport Photos
- Custom Documents

Support:

- Document Type
- Verification Status
- Expiry Date
- Version
- Upload Metadata
- Verification History

### Student Notes

Generate tables for:

- Counseling Notes
- Administrative Notes
- Teacher Notes
- Parent Meeting Notes

### Student Lifecycle

Generate lifecycle support tables for:

- Promotion
- Section Change
- Branch Transfer
- Graduation
- Alumni Preparation
- Withdrawal
- Suspension
- Reinstatement

### Student History

Generate historical tracking tables for:

- Class History
- Section History
- Academic Year History
- Status History
- Roll Number History

---

## SQL Requirements

Every table must use:

CREATE TABLE IF NOT EXISTS

Use:

ENGINE=InnoDB

utf8mb4

utf8mb4_unicode_ci

Include wherever applicable:

- id
- uuid
- created_at
- updated_at
- deleted_at
- created_by
- updated_by
- deleted_by
- version
- status

Include:

- Primary Keys
- Foreign Keys
- Unique Constraints
- Composite Indexes
- Lookup Indexes
- Check Constraints where appropriate
- Comments
- Audit compatibility

Do NOT omit foreign keys.

Do NOT leave placeholder columns.

Do NOT leave TODOs.

Do NOT simplify the schema.

Design for production use.

Support:

- 10,000+ students
- Multi-academic year history
- High-performance queries
- Auditability
- Future extensibility

---

## Finish with

### Completed Tables

List every table created.

### Dependencies

List all referenced tables from Part 1.

### Validation Checklist

Confirm:

- FK integrity
- Naming consistency
- Normalization
- Index coverage
- Audit compatibility
- Soft delete compatibility

### Remaining SQL

List what will be generated in Part 3 only.

Do not generate Part 3.

---part-3---
