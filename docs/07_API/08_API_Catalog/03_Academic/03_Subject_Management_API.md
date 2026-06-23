# 03_Subject_Management_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Subject Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to subject definition, subject hierarchy, subject offerings, electives, prerequisites, teacher assignments, curriculum mapping, academic planning, and subject governance.

The Subject Management domain acts as the academic bridge between Curriculum, Classes, Lesson Planning, Timetable, Attendance, Homework, LMS, Examinations, and Report Cards.

This document must remain implementation-independent.

The architecture must support both:

- Server-rendered PHP MVC
- Headless REST API

through a common business service layer.

Do NOT generate:

- PHP
- SQL
- JSON payloads
- OpenAPI specifications
- Endpoint URLs
- Infrastructure
- Implementation details

Assume all previously generated architecture, contracts, validation rules, workflows, security documents, API standards, Master Administration APIs, Student APIs, Curriculum APIs, and Class Management APIs already exist.

Reference previous documentation instead of duplicating it.

For every business API explicitly identify:

- API Category
  - Command
  - Query
  - Workflow API
  - Administrative API
  - Integration API
  - Reporting API
  - Background Operation API
- Execution Type
- Idempotency
- Transaction Boundary
- Audit Requirements
- Cacheability
- Concurrency Strategy
- System of Record
- Read Ownership
- Write Ownership
- Master vs Operational Data
- Reference vs Transactional Data
- Lifecycle Owner
- Data Retention Classification

---

# Scope

Generate the complete API specification for:

## Subject Catalog

Subject Creation

Subject Code

Subject Naming

Subject Categories

Subject Groups

Subject Classification

Subject Status

Subject Versioning

Subject Templates

Subject Archive

---

## Subject Structure

Core Subjects

Elective Subjects

Optional Subjects

Language Subjects

Laboratory Subjects

Practical Subjects

Theory Subjects

Integrated Subjects

Interdisciplinary Subjects

Bridge Courses

Foundation Courses

Remedial Subjects

Advanced Subjects

---

## Subject Mapping

Curriculum Mapping

Board Mapping

Program Mapping

Class Mapping

Section Mapping

Academic Year Mapping

Semester Mapping

Teacher Mapping

Department Mapping

Learning Outcome Mapping

Assessment Mapping

Credit Mapping

---

## Elective Management

Elective Groups

Elective Rules

Elective Capacity

Student Elective Selection

Elective Approval

Elective Allocation

Elective Changes

Elective Analytics

---

## Subject Prerequisites

Prerequisite Definition

Prerequisite Validation

Equivalent Subjects

Subject Dependency

Progression Rules

Replacement Subjects

Bridge Requirements

---

## Subject Allocation

Teacher Assignment

Multiple Teacher Assignment

Co-Teacher Assignment

Substitute Teacher

Guest Faculty

Teaching Load Distribution

Allocation History

Availability Validation

---

## Subject Lifecycle

Create

Activate

Deactivate

Suspend

Archive

Restore

Copy

Clone

Merge

Split

Version Upgrade

Review

Approval

Retirement

---

## Academic Analytics

Subject Utilization

Enrollment

Popularity

Pass Percentage

Performance Trends

Teaching Load

Subject Capacity

Academic Coverage

Generate every API required.

---

# Document Structure

## 1. Domain Overview

Describe:

Business Responsibilities

Business Objectives

Primary Consumers

Dependencies

Cross-module Relationships

Security Classification

Business Criticality

Operational Importance

Future Extensions

---

## 2. Resource Catalog

For every resource define:

Business Purpose

System of Record

Read Ownership

Write Ownership

Data Classification

Reference vs Transactional

Lifecycle

Dependencies

Validation Dependencies

Workflow Dependencies

Audit Requirements

Retention Classification

Future Extensions

---

## 3. API Catalog

For every resource generate conceptual APIs covering:

### Retrieval

Get

List

Lookup

Search

Advanced Search

Hierarchy

Version History

Availability

Statistics

Analytics

Dashboard

Generate every retrieval API.

---

### Creation

Create

Clone

Copy

Template Creation

Bulk Create

Import

Initialize

Generate every creation API.

---

### Modification

Update

Partial Update

Bulk Update

Activate

Deactivate

Archive

Restore

Merge

Split

Version

Approve

Reject

Review

Validate

Synchronize

Generate every modification API.

---

### Workflow Operations

Assign Teachers

Allocate Electives

Validate Prerequisites

Synchronize Curriculum

Synchronize Timetable

Synchronize LMS

Synchronize Assessment

Synchronize Learning Outcomes

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Assignment

Bulk Activation

Bulk Retirement

Conflict Resolution

Rollback

Review

Approval

Generate every administrative API.

---

### Reporting & Analytics

Subject Reports

Teacher Workload Reports

Elective Reports

Enrollment Reports

Performance Reports

Coverage Reports

Curriculum Reports

Executive Dashboards

Operational Dashboards

Academic Analytics

Generate every reporting API.

---

## 4. API Specification Template

Every API must document:

API Category

Execution Type

Business Purpose

Business Owner

Primary Consumers

Authentication Requirements

Authorization Requirements

Required Permissions

Business Preconditions

Validation Dependencies

Business Rule Dependencies

Workflow Dependencies

Cross-module Dependencies

Affected Resources

Published Events

Consumed Events

Background Jobs

Notifications

Audit Requirements

Transaction Scope

Concurrency Strategy

System of Record

Read Ownership

Write Ownership

Cacheability

Retention Classification

Failure Scenarios

Performance Expectations

Future Extensions

Reference Documentation

---

## 5. Cross-module Integration

Explain interactions with:

Master Administration

Student

Admission

Student Lifecycle

Curriculum

Class Management

Lesson Planning

Attendance

Timetable

Homework

LMS

Examination

Communication

Reporting

Audit

Notification

Search

Import/Export

Background Processing

Generate every integration dependency.

---

## 6. Security Considerations

Define:

Academic Governance

Subject Approval

Elective Integrity

Teacher Assignment Controls

Administrative Override

Bulk Operations

Curriculum Compliance

Audit Requirements

Regulatory Readiness

Future Multi-board Support

---

## 7. Performance Considerations

Discuss:

Subject Search

Elective Allocation

Teacher Assignment

Curriculum Synchronization

Bulk Operations

Caching Readiness

Analytics

Scalability

Future Distributed Curriculum Services

---

## 8. Monitoring

Define:

Subject Changes

Teacher Assignments

Elective Allocation

Version Changes

Curriculum Mapping

Bulk Operations

Operational KPIs

Academic KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support future:

Competency-based Subjects

Micro-Credentials

Cross-institution Subject Sharing

AI Subject Recommendations

Dynamic Elective Planning

International Credit Transfer

Online Subjects

Virtual Laboratories

Industry Certification Mapping

Digital Academic Catalogs

---

## 10. API Dependency Matrix

Create a matrix.

Columns:

Resource

Primary APIs

API Category

Execution Type

System of Record

Read Ownership

Write Ownership

Dependencies

Published Events

Consumed Events

Transaction Scope

Concurrency Strategy

Retention Classification

Security Level

Business Criticality

Future Extension

---

## 11. Architecture Decision Summary

Create a summary table.

Columns:

Area

Decision

Reason

Business Impact

Operational Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Subject Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Implementation details

Focus entirely on subject governance, curriculum integration, teacher allocation, elective management, academic workflows, reporting, monitoring, auditability, security, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Subject Management subsystem—including controllers, services, repositories, validators, allocation engines, curriculum synchronizers, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
