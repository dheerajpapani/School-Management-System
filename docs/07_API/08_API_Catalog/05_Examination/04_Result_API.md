# 03_Marks_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Marks Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to mark entry, mark validation, mark moderation, grade calculation, normalization, scaling, moderation, grace marks, mark publishing readiness, auditability, and academic evaluation governance.

The Marks Management domain is responsible for collecting, validating, processing, securing, and governing all academic marks produced from examinations and assessments before result generation.

This domain integrates with Examination Setup, Assessment Management, Curriculum, Subject Management, Student Lifecycle, Attendance, Result Processing, Report Cards, Parent Portal, Communication, Reporting, Analytics, and Audit.

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

Assume all previously generated architecture, contracts, validation rules, workflows, security documentation, API standards, and Examination Setup + Assessment APIs already exist.

Reference previous documentation instead of duplicating it.

For every business API explicitly identify:

- API Category
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

## Mark Entry

Manual Mark Entry

Bulk Mark Entry

Online Mark Entry

Offline Mark Entry

Teacher Mark Entry

Examiner Mark Entry

Practical Marks

Laboratory Marks

Project Marks

Assignment Marks

Internal Marks

External Marks

Attendance Marks

Grace Marks

Extra Credit

Negative Marks

---

## Mark Validation

Range Validation

Eligibility Validation

Maximum Marks Validation

Minimum Marks Validation

Attendance Validation

Assessment Validation

Duplicate Validation

Missing Marks Validation

Incomplete Evaluation Detection

Consistency Validation

---

## Moderation

Internal Moderation

External Moderation

Department Moderation

Board Moderation

Scaling

Normalization

Grace Marks

Special Consideration

Review Workflow

Approval Workflow

---

## Mark Processing

Grade Calculation Readiness

Percentage Calculation

Weighted Scores

Credit Calculation

CGPA Readiness

GPA Readiness

Ranking Preparation

Merit Preparation

Pass/Fail Readiness

---

## Publishing Control

Draft Marks

Submitted Marks

Verified Marks

Approved Marks

Locked Marks

Published Marks

Rollback

Versioning

Audit History

---

## Re-evaluation

Rechecking

Revaluation

Mark Challenge

Appeal

Correction

Revision

Approval

Audit Trail

---

## Governance

Approval

Publication

Compliance

Audit

Locking

Unlocking

Retention

Version Control

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

Lifecycle

Dependencies

Validation Dependencies

Workflow Dependencies

Audit Requirements

Retention Classification

Future Extensions

---

## 3. API Catalog

Generate APIs covering:

### Retrieval

Get

List

Search

Advanced Search

Dashboard

Statistics

Analytics

History

Timeline

Audit History

Generate every retrieval API.

---

### Creation

Create Mark Entry

Bulk Import

Offline Synchronization

Initialize Mark Sheet

Generate Mark Register

Generate every creation API.

---

### Modification

Update

Bulk Update

Submit

Verify

Approve

Reject

Moderate

Scale

Normalize

Apply Grace Marks

Apply Extra Credit

Correct

Revise

Lock

Unlock

Archive

Restore

Rollback

Validate

Generate every modification API.

---

### Workflow Operations

Record Marks

Validate Marks

Moderate Marks

Normalize Marks

Scale Marks

Calculate Grades

Calculate Percentage

Calculate Credits

Generate Ranking

Generate Merit

Prepare Results

Synchronize Assessment

Synchronize Examination

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Approval

Bulk Lock

Bulk Unlock

Bulk Publication Readiness

Conflict Resolution

Rollback

Compliance Review

Generate every administrative API.

---

### Reporting & Analytics

Mark Registers

Subject Reports

Teacher Reports

Department Reports

Moderation Reports

Grade Distribution

Pass Percentage

Merit Reports

Operational Dashboards

Executive Dashboards

Assessment Analytics

Generate every reporting API.

---

## 4. API Specification Template

Document every API using the enterprise standard:

- API Category
- Execution Type
- Business Purpose
- Business Owner
- Primary Consumers
- Authentication Requirements
- Authorization Requirements
- Required Permissions
- Business Preconditions
- Validation Dependencies
- Business Rule Dependencies
- Workflow Dependencies
- Cross-module Dependencies
- Affected Resources
- Published Events
- Consumed Events
- Background Jobs
- Notifications
- Audit Requirements
- Transaction Scope
- Concurrency Strategy
- System of Record
- Read Ownership
- Write Ownership
- Cacheability
- Retention Classification
- Failure Scenarios
- Performance Expectations
- Future Extensions
- Reference Documentation

---

## 5. Cross-module Integration

Explain integrations with:

Master Administration

Student

Student Lifecycle

Curriculum

Subject Management

Assessment

Examination Setup

Results

Report Cards

Attendance

LMS

Homework

Communication

Parent Portal

Reporting

Audit

Notification

Background Processing

Search

Import/Export

Generate every integration dependency.

---

## 6. Security Considerations

Cover:

Mark Confidentiality

Teacher Authorization

Department Authorization

Moderation Security

Grade Integrity

Publication Controls

Administrative Override

Bulk Operations

Audit Requirements

Compliance Readiness

Future Digital Signatures

---

## 7. Performance Considerations

Discuss:

Bulk Mark Entry

Bulk Validation

Large-scale Grade Calculation

Moderation

Ranking Generation

Caching

Analytics

Scalability

Future Distributed Evaluation

---

## 8. Monitoring

Define:

Mark Entry

Corrections

Moderation

Approval

Publication

Bulk Operations

Operational KPIs

Academic KPIs

Quality KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

AI-assisted Evaluation

Automated Moderation

Digital Answer Sheets

OCR Mark Capture

Online Evaluation

Government Board Integration

International Grading Systems

Competency-based Scoring

Blockchain Audit Trail

Cross-campus Evaluation

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including (but not limited to):

MarkEntryCreated

MarksImported

MarksSubmitted

MarksVerified

MarksApproved

MarksRejected

MarksCorrected

MarksModerated

MarksScaled

MarksNormalized

GraceMarksApplied

GradeCalculated

MeritGenerated

MarksLocked

MarksUnlocked

MarksReadyForResults

Generate every event defining:

- Event Category
- Business Purpose
- Producer
- Consumers
- Trigger
- Ordering
- Retry
- Idempotency
- Background Jobs
- Notifications
- Audit Impact

---

## 12. AI Coding Agent Guidance

Provide implementation guidance covering:

- Mark entry services
- Validation engines
- Moderation engines
- Grade calculation sequencing
- Repository ownership
- Event publication
- Transaction handling
- Background jobs
- Notification orchestration
- Concurrency handling

---

## 13. Error & Exception Catalog

Define business exceptions including:

MarksAlreadyPublished

MarksLocked

DuplicateMarkEntry

InvalidMarkRange

StudentNotEligible

AssessmentIncomplete

ModerationPending

ApprovalRequired

GradeCalculationFailed

NormalizationConflict

RankingCalculationFailed

ResultGenerationBlocked

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Marks Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Implementation details

Focus entirely on mark governance, validation, moderation, processing, workflow orchestration, event-driven architecture, reporting, monitoring, security, auditability, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Marks Management subsystem—including controllers, services, repositories, validators, moderation engines, grading engines, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
