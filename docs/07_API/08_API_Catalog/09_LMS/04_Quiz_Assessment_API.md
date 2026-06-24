# 04_Quiz_Assessment_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the LMS Quiz & Assessment Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to quizzes, online assessments, question banks, attempts, grading, proctoring readiness, adaptive quizzes, continuous assessment, learner evaluation, assessment governance, and institutional digital learning assessments.

The LMS Quiz & Assessment domain provides formative assessments inside the Learning Management System and integrates with Course Management, Learning Content Management, Learning Activities, Homework, Examination, Student Lifecycle, Learning Progress, Parent Portal, Communication, Reporting, Analytics, Certification, and Digital Learning.

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
- Online proctoring implementation
- AI grading implementation

Assume all previously generated architecture, contracts, validation rules, workflows, security documentation, API standards, Homework APIs, Examination APIs, LMS APIs, Academic APIs, and Reporting APIs already exist.

Reference previous documentation instead of duplicating it.

---

# Enterprise Learning Assessment Principles

LMS Assessments are formative by default.

Institutional Examinations remain part of the Examination module.

Assessment attempts never overwrite previous attempts.

Assessments remain versioned.

Questions remain reusable.

Question Banks remain reusable.

Assessment results contribute to Learning Progress.

Every assessment interaction remains auditable.

---

# Scope

Generate the complete API specification for:

## Assessment Lifecycle

Assessment Creation

Draft

Review

Approval

Publication

Revision

Versioning

Archive

Restore

Retirement

Clone

---

## Assessment Types

Quiz

Practice Quiz

Timed Quiz

Adaptive Quiz

Self Assessment

Peer Assessment

Coding Assessment

Practical Assessment

Assignment-linked Quiz

Lesson Quiz

Module Quiz

Course Quiz

Certification Quiz

Survey

Diagnostic Assessment

---

## Question Bank

Question Categories

Question Types

MCQ

Multiple Select

True/False

Fill in the Blank

Matching

Ordering

Short Answer

Essay

Coding Question

Case Study

Numerical

File Upload

Rubric Question

Question Pools

Randomization

Difficulty Levels

Tagging

Versioning

---

## Attempt Management

Start Attempt

Resume Attempt

Pause Attempt

Submit Attempt

Auto Submit

Retry Attempt

Retake Rules

Time Limit

Attempt Limit

Attempt History

---

## Evaluation

Automatic Grading

Manual Grading

Rubric Evaluation

Partial Scoring

Negative Marking

Bonus Marks

Feedback

Hints

Answer Review

Moderation

Appeals Readiness

---

## Governance

Approval

Publication

Version Control

Review

Audit

Compliance

Retention

Generate every API required.

---

# Document Structure

## 1. Domain Overview

## 2. Resource Catalog

## 3. API Catalog

Generate APIs covering:

### Retrieval

Get

List

Search

Advanced Search

Question Bank

Assessment Catalog

Attempt History

Statistics

Analytics

Dashboard

Generate every retrieval API.

---

### Creation

Create Assessment

Create Question

Create Question Bank

Clone Assessment

Bulk Import

Initialize Assessment

Generate every creation API.

---

### Modification

Update

Approve

Reject

Publish

Archive

Restore

Version

Revise

Assign Questions

Randomize Questions

Lock

Unlock

Validate

Generate every modification API.

---

### Workflow Operations

Publish Assessment

Start Attempt

Resume Attempt

Submit Assessment

Evaluate Assessment

Synchronize Learning Progress

Synchronize Homework

Synchronize Examination

Notify Learners

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Publication

Bulk Evaluation

Rollback

Compliance Review

Conflict Resolution

Generate every administrative API.

---

### Reporting & Analytics

Assessment Reports

Question Analysis

Attempt Reports

Difficulty Analysis

Performance Reports

Teacher Reports

Operational Dashboards

Executive Dashboards

Learning Analytics

Generate every reporting API.

---

## 4. API Specification Template

Document every API using the standardized enterprise template.

---

## 5. Cross-module Integration

Explain integrations with:

Course Management

Content Management

Learning Activities

Homework

Examination

Learning Progress

Academic

Student

Communication

Parent Portal

Reporting

Analytics

Audit

Notification

Background Processing

Search

Import/Export

Generate every integration dependency.

---

## 6. Security Considerations

Cover:

Assessment Integrity

Question Bank Protection

Attempt Security

Evaluation Security

Administrative Override

Bulk Operations

Audit Requirements

Learner Privacy

Future Online Proctoring Readiness

---

## 7. Performance Considerations

Discuss:

Large Question Banks

High Concurrent Quiz Attempts

Automatic Grading

Question Randomization

Caching

Analytics

Scalability

Future Massive Online Learning

---

## 8. Monitoring

Define:

Assessment Creation

Attempts

Submissions

Evaluation

Synchronization

Bulk Operations

Operational KPIs

Learning KPIs

Assessment KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

AI Question Generation

AI Evaluation

Adaptive Assessment

Online Proctoring

Remote Invigilation

Question Marketplace

SCORM

xAPI

Competency-based Assessment

Digital Certification

Gamification

Micro-Credentials

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including:

AssessmentCreated

AssessmentPublished

QuestionCreated

QuestionBankUpdated

AttemptStarted

AttemptPaused

AttemptResumed

AssessmentSubmitted

AssessmentEvaluated

GradeCalculated

FeedbackGenerated

QuestionRandomized

AssessmentCompleted

Generate every event with:

- Event Category
- Business Purpose
- Producer
- Consumers
- Ordering
- Retry
- Idempotency
- Background Jobs
- Notifications
- Audit Impact

---

## 12. AI Coding Agent Guidance

Provide implementation guidance covering:

- Assessment services

- Question bank services

- Attempt engine

- Evaluation engine

- Repository ownership

- Event publication

- Background jobs

- Validation sequencing

- Notification orchestration

- Transaction handling

- Concurrency handling

---

## 13. Error & Exception Catalog

Define business exceptions including:

AssessmentAlreadyPublished

DuplicateQuestion

QuestionBankConflict

AttemptAlreadySubmitted

AttemptLimitExceeded

TimeLimitExceeded

AssessmentLocked

EvaluationPending

QuestionRandomizationFailed

AssessmentSynchronizationFailed

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise LMS Quiz & Assessment API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Online proctoring implementation
- AI grading implementation

Focus entirely on assessment lifecycle management, question bank governance, learner assessment, reporting, monitoring, auditability, event-driven architecture, scalability, compliance, and extensibility.

This document should enable an AI coding agent to generate the complete LMS Quiz & Assessment subsystem—including controllers, services, repositories, question bank services, attempt engines, evaluation services, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
