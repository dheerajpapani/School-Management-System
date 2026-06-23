# 03_Entity_Relationships.md

## Objective

You are acting as a Principal Data Architect responsible for defining the complete Entity Relationship Architecture for an Enterprise School Management System (SMS).

This document is the authoritative specification describing every relationship that exists between business entities throughout the platform.

It is NOT a SQL document.

It is NOT a table definition document.

It is NOT an ER diagram image.

Instead, it defines the logical data model that every future database schema, ORM model, repository, API, report, and AI-generated implementation must follow.

Assume all previous documentation already exists.

Do not duplicate previous documents.

---

# Scope

Generate the complete conceptual and logical relationship model for the School Management System.

Cover every entity defined in the Entity Catalog.

Describe ownership, dependency, relationship cardinality, lifecycle dependency, cascading behavior, and business meaning.

Avoid implementation.

---

# Document Structure

## 1. Purpose

Explain:

Why relationship modeling exists.

Difference between:

Entity Catalog

Entity Relationships

Normalization

SQL Schema

Explain why relationships are defined before physical tables.

---

## 2. Relationship Modeling Principles

Describe principles including:

Single Ownership

Aggregate Boundaries

Strong Relationships

Weak Relationships

Composition

Aggregation

Association

Reference Relationships

Lifecycle Dependency

Mandatory Relationships

Optional Relationships

Inheritance Readiness

Extensibility

Historical Tracking

Soft Delete Compatibility

Referential Integrity

Explain each principle.

---

## 3. Relationship Definition Standard

Every relationship must define:

Relationship ID

Relationship Name

Parent Entity

Child Entity

Business Purpose

Relationship Type

Cardinality

Ownership

Lifecycle Dependency

Cascade Expectations

Optional / Mandatory

Business Constraints

Deletion Strategy

Historical Considerations

Future Extensibility

---

## 4. Core Relationship Groups

Generate complete relationship definitions for:

### Administration

Institution

↓

Branches

↓

Departments

↓

Classes

↓

Sections

↓

Academic Years

↓

Academic Terms

↓

Curriculum

↓

Subjects

↓

Teachers

↓

Roles

↓

Permissions

---

### Student

Student

↓

Guardian

↓

Medical Profile

↓

Academic Assignment

↓

Attendance

↓

Results

↓

Fee Profile

↓

Transport

↓

Hostel

↓

Library

↓

Discipline

↓

Documents

↓

Communication

↓

Alumni

---

### Academic

Curriculum

↓

Subjects

↓

Lessons

↓

Learning Outcomes

↓

Assessments

↓

Examinations

---

### Attendance

Attendance Session

↓

Attendance Records

↓

Attendance Summary

↓

Attendance Analytics

---

### Examination

Examination

↓

Assessment

↓

Marks

↓

Results

↓

Report Cards

↓

Transcripts

---

### Fee

Fee Structure

↓

Invoice

↓

Invoice Items

↓

Payments

↓

Scholarships

↓

Refunds

↓

Ledger

---

### Timetable

Timetable

↓

Periods

↓

Teacher Allocation

↓

Room Allocation

↓

Substitutions

---

### Homework

Homework

↓

Submission

↓

Evaluation

↓

Attachments

---

### LMS

Course

↓

Modules

↓

Resources

↓

Quizzes

↓

Progress

↓

Certificates

---

### Communication

Notification

↓

Recipients

↓

Delivery Status

↓

Templates

↓

Channels

---

### Transport

Vehicle

↓

Route

↓

Stops

↓

Student Assignment

↓

GPS Tracking

---

### Hostel

Building

↓

Floor

↓

Room

↓

Bed

↓

Allocation

↓

Billing

---

### Library

Book

↓

Copy

↓

Issue

↓

Reservation

↓

Fine

---

### Inventory

Inventory

↓

Purchase

↓

Vendor

↓

Asset

↓

Maintenance

---

### HRMS

Employee

↓

Attendance

↓

Leave

↓

Department

↓

Assignments

---

### Events

Event

↓

Registration

↓

Participation

↓

Certificate

---

### Discipline

Incident

↓

Investigation

↓

Action

↓

Behavior Record

---

### Alumni

Alumni

↓

Events

↓

Mentorship

↓

Donations

---

Generate every additional relationship required.

---

## 5. Cardinality Matrix

Generate a matrix showing:

Parent

Child

Cardinality

Ownership

Optional

Lifecycle Dependency

Cascade

Business Criticality

---

## 6. Ownership Matrix

Generate:

Entity

Owner

References

Consumers

Shared

Historical

Read Model

---

## 7. Lifecycle Dependency Matrix

Describe:

Which entities cannot exist independently.

Examples:

Invoice Item requires Invoice

Attendance Record requires Attendance Session

Student Document requires Student

Payment requires Invoice

Result requires Examination

Book Issue requires Book Copy

Bed Allocation requires Room

Generate every lifecycle dependency.

---

## 8. Cascade Strategy

Conceptually define:

Cascade Create

Cascade Update

Cascade Archive

Cascade Restore

Cascade Delete (Logical)

Cascade Validation

Cascade Notifications

Cascade Audit

Do NOT define SQL ON DELETE rules.

---

## 9. Circular Dependency Prevention

Describe:

Forbidden relationships

Reference-only relationships

Aggregate boundaries

Cross-module ownership

Relationship anti-patterns

---

## 10. Historical Relationships

Describe entities requiring history.

Examples:

Student Class History

Teacher Assignment History

Fee History

Attendance History

Promotion History

Timetable History

Role History

Room Allocation History

Vehicle Assignment History

Generate all historical relationships.

---

## 11. Future Extensibility

Support future:

Multi-school

Multi-campus

Multi-currency

Government Integration

External LMS

Identity Providers

Plugin Modules

Microservices

Regional Extensions

AI Modules

---

## 12. Relationship Decision Summary

Create a summary table.

Columns:

Relationship

Type

Cardinality

Owner

Lifecycle

Criticality

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Data Architecture Specification.

Do not include:

- SQL
- CREATE TABLE statements
- Foreign Keys
- Indexes
- Database engine specifics
- ORM mappings

Focus entirely on conceptual and logical entity relationships, ownership, lifecycle, cardinality, dependencies, extensibility, and governance.

This document should enable AI coding agents and database architects to generate a consistent relational model before physical schema design.
