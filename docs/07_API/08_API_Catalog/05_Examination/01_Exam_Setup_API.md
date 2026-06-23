# 01_Exam_Setup_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Examination Setup domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to examination configuration, academic examination planning, exam schedules, examination policies, grading structures, exam sessions, invigilation planning, hall allocation, examination governance, and institutional examination administration.

The Examination Setup domain establishes the complete operational foundation for assessments, marks, results, report cards, certificates, transcripts, analytics, and academic progression.

It integrates with Curriculum Management, Class Management, Subject Management, Lesson Planning, Student Lifecycle, Attendance, Timetable, Communication, Parent Portal, Reporting, and Academic Administration.

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

Assume all previously generated architecture, contracts, validation rules, workflows, security documents, API standards, Master Administration APIs, Student APIs, Academic APIs, Attendance APIs, and Examination architecture documentation already exist.

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

## Examination Sessions

Academic Examination Sessions

Internal Examination Sessions

External Examination Sessions

Board Examination Sessions

Term Examinations

Semester Examinations

Annual Examinations

Supplementary Examinations

Improvement Examinations

Re-examinations

Session Lifecycle

---

## Examination Configuration

Exam Types

Exam Categories

Exam Templates

Exam Policies

Passing Rules

Grading Policies

Weightage Rules

Moderation Rules

Scaling Rules

Rounding Rules

Publication Rules

Eligibility Rules

Academic Regulations

---

## Examination Scheduling

Exam Timetable

Exam Calendar

Subject Scheduling

Practical Scheduling

Laboratory Scheduling

Viva Scheduling

Project Evaluation Schedule

Rescheduling

Conflict Resolution

Holiday Validation

Resource Validation

---

## Hall Management

Hall Allocation

Room Capacity

Seat Allocation

Seating Plans

Candidate Allocation

Special Accommodation

Accessibility Planning

Hall Supervision

Capacity Validation

---

## Invigilation Management

Invigilator Assignment

Chief Superintendent

Observer Assignment

Substitute Invigilators

Duty Rotation

Availability Validation

Conflict Detection

Duty Approval

---

## Examination Eligibility

Attendance Eligibility

Fee Clearance

Academic Eligibility

Subject Registration

Backlog Eligibility

Special Permission

Conditional Eligibility

Approval Workflow

---

## Examination Governance

Approval Workflow

Review Workflow

Publication Workflow

Locking

Unlocking

Audit

Compliance

Version Management

Generate every API required.

---

# Document Structure

## 1. Domain Overview

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

Generate conceptual APIs covering:

### Retrieval

Get

List

Lookup

Search

Advanced Search

Calendar

Schedule

Timeline

Availability

Eligibility

Statistics

Analytics

Dashboard

Generate every retrieval API.

---

### Creation

Create Examination

Create Session

Create Schedule

Create Hall Plan

Create Seating Plan

Create Invigilation Plan

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

Approve

Reject

Review

Publish

Archive

Restore

Lock

Unlock

Version

Revise

Synchronize

Validate

Reschedule

Generate every modification API.

---

### Workflow Operations

Generate Exam Schedule

Generate Seating Plan

Generate Hall Allocation

Generate Invigilation Plan

Generate Eligibility

Generate Candidate Lists

Validate Timetable

Validate Resources

Validate Eligibility

Approve Examination

Publish Examination

Synchronize Timetable

Synchronize Attendance

Synchronize Communication

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Emergency Rescheduling

Bulk Approval

Bulk Publication

Bulk Lock

Bulk Unlock

Conflict Resolution

Rollback

Compliance Review

Generate every administrative API.

---

### Reporting & Analytics

Examination Schedule Reports

Hall Reports

Invigilation Reports

Eligibility Reports

Compliance Reports

Capacity Reports

Operational Dashboards

Executive Dashboards

Institution Analytics

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

Student Lifecycle

Curriculum

Class Management

Subject Management

Lesson Planning

Attendance

Timetable

Assessment

Marks

Results

Report Cards

Fees

Communication

Parent Portal

LMS

Reporting

Audit

Notification

Background Processing

Search

Import/Export

Generate every integration dependency.

---

## 6. Security Considerations

Define:

Exam Governance

Schedule Integrity

Hall Allocation Security

Invigilation Controls

Eligibility Validation

Administrative Override

Publication Controls

Bulk Operation Security

Audit Requirements

Compliance Readiness

Future Digital Examination Security

---

## 7. Performance Considerations

Discuss:

Large Examination Scheduling

Bulk Hall Allocation

Eligibility Calculation

Timetable Synchronization

Caching Readiness

Analytics

Scalability

Future Distributed Examination Processing

---

## 8. Monitoring

Define:

Exam Creation

Schedule Changes

Hall Allocation

Invigilator Assignment

Eligibility Changes

Publication

Bulk Operations

Operational KPIs

Academic KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support future:

Online Examinations

AI-based Scheduling

Computer-based Testing

Remote Proctoring

Digital Hall Tickets

QR-based Verification

Cross-campus Examinations

Government Board Integration

International Examination Boards

Adaptive Examination Scheduling

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

## 11. Domain Event Catalog

Generate events including (but not limited to):

ExaminationSessionCreated

ExaminationConfigured

ExaminationApproved

ExaminationPublished

ExamScheduleGenerated

ExamRescheduled

HallAllocated

SeatingPlanGenerated

InvigilatorAssigned

EligibilityCalculated

ExaminationLocked

ExaminationUnlocked

ExaminationComplianceValidated

Generate every event with:

Event Category

Business Purpose

Producer

Consumers

Trigger

Ordering

Retry

Idempotency

Background Jobs

Notifications

Audit Impact

---

## 12. AI Coding Agent Guidance

Provide implementation guidance covering:

- Examination setup service boundaries
- Scheduling engine responsibilities
- Hall allocation orchestration
- Eligibility validation sequencing
- Event publication
- Background jobs
- Repository ownership
- Transaction handling
- Notification orchestration
- Concurrency handling

---

## 13. Architecture Decision Summary

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

Maintain the tone of a professional Enterprise Examination Setup API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Implementation details

Focus entirely on examination governance, scheduling, eligibility, hall planning, business workflows, reporting, monitoring, security, auditability, event-driven architecture, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Examination Setup subsystem—including controllers, services, repositories, validators, scheduling engines, hall allocation engines, workflow managers, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
