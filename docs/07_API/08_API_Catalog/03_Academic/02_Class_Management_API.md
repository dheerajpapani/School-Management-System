# 02_Class_Management_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Class Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to academic class organization, section management, class assignments, capacity planning, teacher allocation, student allocation, class hierarchy, and academic operational management.

The Class Management domain orchestrates how students, teachers, subjects, sections, classrooms, and academic years are organized into operational teaching units.

This domain is consumed by Admissions, Student Lifecycle, Timetable, Attendance, Examination, Homework, LMS, Communication, Transport, Hostel, Parent Portal, Reporting, and Analytics.

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

Assume all previous architecture, contracts, workflows, validation rules, security documents, API standards, Curriculum APIs, Student APIs, and Master Administration APIs already exist.

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

## Academic Classes

Class Creation

Class Levels

Academic Streams

Academic Batches

Class Capacity

Class Categories

Class Templates

Class Activation

Class Archive

---

## Section Management

Section Creation

Section Capacity

Section Allocation

Section Merge

Section Split

Section Closure

Section Transfer

Section History

---

## Student Allocation

Student Allocation

Bulk Allocation

Automatic Allocation

Manual Allocation

Reallocation

Seat Availability

Capacity Validation

Student Distribution

Allocation Analytics

---

## Teacher Allocation

Class Teacher Assignment

Subject Teacher Assignment

Co-Teacher Assignment

Temporary Assignment

Substitute Assignment

Teacher Workload

Teacher Allocation History

Teacher Availability

---

## Classroom Allocation

Room Assignment

Room Capacity

Room Availability

Lab Assignment

Special Room Assignment

Shared Classroom

Room Transfer

---

## Academic Structure

Class Hierarchy

Section Hierarchy

Academic Year Mapping

Curriculum Mapping

Branch Mapping

Department Mapping

Program Mapping

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

Availability

Capacity

Statistics

Analytics

Dashboard

History

Generate every retrieval API.

---

### Creation

Create

Clone

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

Transfer

Validate

Lock

Unlock

Generate every modification API.

---

### Workflow Operations

Allocate Students

Allocate Teachers

Allocate Rooms

Capacity Validation

Student Redistribution

Teacher Redistribution

Room Optimization

Academic Year Initialization

Promotion Preparation

Synchronization

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Allocation

Bulk Transfer

Conflict Resolution

Rollback

Approval

Review

Generate every administrative API.

---

### Reporting & Analytics

Class Reports

Section Reports

Capacity Reports

Teacher Allocation Reports

Student Allocation Reports

Occupancy Reports

Utilization Reports

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

Subject Management

Lesson Planning

Attendance

Examination

Timetable

Homework

LMS

Communication

Transport

Hostel

Library

Inventory

Parent Portal

Reporting

Notification

Audit

Search

Import/Export

Background Processing

Generate every integration dependency.

---

## 6. Security Considerations

Define:

Academic Structure Governance

Capacity Enforcement

Teacher Assignment Security

Student Allocation Controls

Administrative Override

Bulk Operation Controls

Approval Requirements

Audit Requirements

Compliance Readiness

Future Multi-campus Academic Structures

---

## 7. Performance Considerations

Discuss:

Bulk Student Allocation

Bulk Teacher Allocation

Capacity Calculation

Hierarchy Resolution

Room Availability

Caching Readiness

Analytics

Scalability

Future Distributed Academic Structures

---

## 8. Monitoring

Define:

Class Creation

Section Changes

Teacher Assignments

Student Allocations

Room Allocations

Capacity Changes

Bulk Operations

Operational KPIs

Academic KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support future:

AI-based Class Balancing

AI Teacher Workload Optimization

Dynamic Classroom Allocation

Hybrid Learning Structures

Cross-campus Class Sharing

International Academic Programs

Virtual Classrooms

Smart Classroom Integration

Academic Digital Twins

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

Maintain the tone of a professional Enterprise Class Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Implementation details

Focus entirely on academic organization, allocation workflows, governance, reporting, monitoring, auditability, security, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Class Management subsystem—including controllers, services, repositories, validators, allocation engines, workflow managers, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
