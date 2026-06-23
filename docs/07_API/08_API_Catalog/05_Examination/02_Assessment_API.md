# 02_Assessment_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Assessment Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to academic assessments, continuous evaluation, formative assessments, summative assessments, assignments, projects, practicals, laboratory evaluations, viva examinations, rubrics, competency-based assessments, assessment scheduling, moderation, approvals, grading readiness, and assessment governance.

The Assessment Management domain bridges curriculum delivery with academic evaluation and integrates with Curriculum, Subject Management, Lesson Planning, Student Lifecycle, Examination Setup, Attendance, Homework, LMS, Marks, Results, Report Cards, Communication, Parent Portal, Reporting, and Analytics.

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

Assume all previous architecture, contracts, validation rules, workflows, security documents, API standards, and Examination Setup APIs already exist.

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

## Assessment Framework

Assessment Categories

Assessment Types

Assessment Components

Assessment Templates

Assessment Weightages

Continuous Assessment

Internal Assessment

External Assessment

Diagnostic Assessment

Competency Assessment

Outcome-based Assessment

---

## Assessment Planning

Assessment Calendar

Assessment Schedule

Assessment Windows

Assessment Publication

Assessment Revision

Assessment Versioning

Assessment Approval

Assessment Lifecycle

---

## Assessment Activities

Written Tests

Assignments

Projects

Laboratory Assessments

Practical Examinations

Oral Examinations

Presentations

Seminars

Case Studies

Portfolio Assessment

Observation Assessment

Peer Assessment

Self Assessment

---

## Rubrics

Rubric Templates

Evaluation Criteria

Scoring Guides

Performance Indicators

Competency Mapping

Rubric Versioning

Rubric Approval

---

## Student Assessment

Student Registration

Assessment Allocation

Submission Tracking

Attendance Validation

Assessment Completion

Late Submission

Resubmission

Exemptions

Special Accommodation

---

## Moderation

Assessment Review

Internal Moderation

External Moderation

Score Verification

Quality Assurance

Approval Workflow

Appeals Readiness

---

## Assessment Governance

Approval

Publication

Locking

Unlocking

Revision

Compliance

Audit

Version Control

Generate every API required.

---

# Document Structure

## 1. Domain Overview

## 2. Resource Catalog

Include:

Business Purpose

System of Record

Read Ownership

Write Ownership

Lifecycle

Dependencies

Validation

Workflow Dependencies

Audit

Retention

Future Extensions

---

## 3. API Catalog

Generate APIs for:

### Retrieval

Get

List

Search

Advanced Search

Calendar

Dashboard

History

Statistics

Analytics

Generate every retrieval API.

---

### Creation

Create Assessment

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

Generate every modification API.

---

### Workflow Operations

Schedule Assessment

Allocate Students

Allocate Teachers

Assign Rubrics

Validate Eligibility

Moderate Assessment

Approve Assessment

Publish Assessment

Synchronize LMS

Synchronize Homework

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Approval

Bulk Publication

Bulk Revision

Rollback

Conflict Resolution

Compliance Review

Generate every administrative API.

---

### Reporting & Analytics

Assessment Reports

Rubric Reports

Teacher Reports

Student Reports

Outcome Reports

Compliance Reports

Operational Dashboards

Executive Dashboards

Assessment Analytics

Generate every reporting API.

---

## 4. API Specification Template

Document every API with the standardized enterprise template.

---

## 5. Cross-module Integration

Explain integrations with:

Master Administration

Academic

Student

Attendance

Examination Setup

Marks

Results

Report Cards

Homework

LMS

Communication

Parent Portal

Reporting

Audit

Notifications

Background Processing

Generate every integration dependency.

---

## 6. Security Considerations

Cover:

Assessment Integrity

Rubric Security

Approval Controls

Assessment Locking

Moderation Controls

Administrative Override

Compliance

Audit

Future Digital Assessment Security

---

## 7. Performance Considerations

Discuss:

Bulk Assessment Creation

Large-scale Scheduling

Rubric Evaluation

Analytics

Caching

Scalability

Future Online Assessments

---

## 8. Monitoring

Include:

Assessment Creation

Assessment Updates

Moderation

Approvals

Publication

Bulk Operations

Operational KPIs

Academic KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

Online Assessment

AI-assisted Evaluation

Adaptive Assessment

Competency-based Education

Remote Assessment

Digital Rubrics

AI Plagiarism Detection

Government Assessment Standards

International Curriculum Support

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Include events such as:

AssessmentCreated

AssessmentScheduled

AssessmentApproved

AssessmentPublished

AssessmentAllocated

AssessmentSubmitted

AssessmentModerated

RubricAssigned

AssessmentLocked

AssessmentUnlocked

AssessmentCompleted

AssessmentAnalyticsGenerated

Generate every relevant business event.

---

## 12. AI Coding Agent Guidance

Provide implementation guidance for:

Assessment orchestration

Scheduling

Rubric engines

Workflow sequencing

Repository ownership

Events

Notifications

Transactions

Background jobs

Concurrency

---

## 13. Error & Exception Catalog

Define business exceptions including:

AssessmentAlreadyPublished

AssessmentLocked

AssessmentWindowClosed

DuplicateAssessment

RubricMissing

StudentNotEligible

ModerationPending

ApprovalRequired

InvalidAssessmentConfiguration

SchedulingConflict

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Assessment Management API Catalog Specification.

Do not include implementation details.

Focus entirely on business APIs, governance, workflow orchestration, assessment lifecycle management, event-driven architecture, auditability, reporting, monitoring, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Assessment subsystem without making any business assumptions.
