# 01_Curriculum_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Curriculum Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to curriculum planning, academic structures, education boards, learning outcomes, curriculum mapping, academic policies, progression rules, and curriculum governance.

The Curriculum domain is the academic foundation consumed by Admissions, Class Management, Subjects, Lesson Planning, Attendance, Examinations, Timetable, LMS, Homework, Report Cards, Analytics, and Academic Administration.

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

Assume all previously generated architecture, contracts, validation rules, workflows, security documents, API standards, Student APIs, and Master Administration APIs already exist.

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

## Curriculum

Curriculum Creation

Curriculum Revision

Curriculum Versioning

Curriculum Activation

Curriculum Retirement

Curriculum Comparison

Curriculum Copy

Curriculum Templates

Curriculum History

---

## Education Boards

Board Management

Board Mapping

Board Activation

Board Migration

Board Rules

Board Policies

National Boards

International Boards

Custom Boards

---

## Academic Programs

Program Management

Streams

Specializations

Academic Levels

Program Duration

Program Structure

Program Versioning

---

## Academic Policies

Promotion Policy

Progression Policy

Assessment Policy

Attendance Policy

Elective Policy

Subject Policy

Academic Calendar Policy

---

## Learning Outcomes

Outcome Framework

Competencies

Skill Framework

Bloom's Taxonomy Mapping

Outcome Versioning

Outcome Validation

Outcome Analytics

---

## Curriculum Mapping

Board Mapping

Class Mapping

Subject Mapping

Outcome Mapping

Assessment Mapping

Teacher Mapping

Academic Year Mapping

---

## Curriculum Governance

Approval Workflow

Review Workflow

Publication

Deprecation

Compliance

Audit

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

Comparison

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

Import

Bulk Import

Initialize

Generate every creation API.

---

### Modification

Update

Partial Update

Bulk Update

Version

Publish

Approve

Reject

Activate

Deactivate

Archive

Restore

Lock

Unlock

Validate

Review

Generate every modification API.

---

### Workflow Operations

Curriculum Approval

Policy Approval

Board Migration

Curriculum Publication

Outcome Validation

Curriculum Synchronization

Version Upgrade

Compliance Review

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Approval

Bulk Publication

Bulk Activation

Bulk Deactivation

Merge

Split

Conflict Resolution

Rollback

Generate every administrative API.

---

### Reporting & Analytics

Curriculum Reports

Policy Reports

Outcome Reports

Board Reports

Program Reports

Compliance Reports

Version Reports

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

Class Management

Subject Management

Lesson Planning

Attendance

Examination

Timetable

Homework

LMS

Communication

Reporting

Audit

Configuration

Search

Import/Export

Background Processing

Generate every integration dependency.

---

## 6. Security Considerations

Define:

Curriculum Governance

Approval Security

Version Protection

Policy Protection

Administrative Override

Academic Integrity

Bulk Operations

Audit Requirements

Compliance Readiness

Future Regulatory Alignment

---

## 7. Performance Considerations

Discuss:

Curriculum Lookup

Version Comparison

Outcome Mapping

Hierarchy Resolution

Caching Readiness

Bulk Updates

Analytics

Scalability

Future Multi-board Support

---

## 8. Monitoring

Define:

Curriculum Changes

Policy Changes

Version Changes

Publication

Approval

Board Updates

Outcome Changes

Bulk Operations

Operational KPIs

Academic KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support future:

International Curriculum Standards

Competency-based Education

AI Curriculum Recommendations

Outcome Prediction

Government Curriculum APIs

Cross-campus Curriculum Sharing

Curriculum Marketplace

Academic Accreditation Integration

Digital Curriculum Publishing

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

Maintain the tone of a professional Enterprise Curriculum Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Implementation details

Focus entirely on curriculum governance, business APIs, workflow orchestration, versioning, compliance, reporting, monitoring, security, and extensibility.

This document should enable an AI coding agent to generate the complete Curriculum Management subsystem—including controllers, services, repositories, validators, workflow engines, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
