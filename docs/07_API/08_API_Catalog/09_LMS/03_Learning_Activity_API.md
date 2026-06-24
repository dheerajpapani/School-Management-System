# 03_Learning_Activity_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Learning Activity Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to digital learning activities, learner interactions, practice exercises, collaborative learning, discussions, virtual classrooms, coding exercises, laboratory activities, simulations, activity completion, participation tracking, engagement analytics, and institutional learning experiences.

The Learning Activity Management domain orchestrates learner engagement with educational content and integrates with Course Management, Learning Content Management, Homework, Quiz Assessment, Learning Progress, Student Lifecycle, Timetable, Parent Portal, Communication, Reporting, Analytics, Certification, and Digital Learning.

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
- Live streaming implementation
- Video conferencing implementation
- Collaboration engine implementation

Assume all previously generated architecture, contracts, validation rules, workflows, security documentation, API standards, Homework APIs, Course Management APIs, Content Management APIs, Academic APIs, and Reporting APIs already exist.

Reference previous documentation instead of duplicating it.

---

# Enterprise Learning Principles

Learning Activities represent learner interactions.

Activities must be reusable.

Activities may belong to:

- Courses
- Modules
- Units
- Lessons
- Learning Paths

Activities support multiple delivery modes.

Activity completion contributes to learning progress.

Activities remain versioned.

Every learner interaction must remain auditable.

---

# Scope

Generate the complete API specification for:

## Activity Lifecycle

Activity Creation

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

## Activity Types

Reading Activity

Video Activity

Audio Activity

Interactive Activity

Practice Exercise

Coding Exercise

Simulation

Virtual Laboratory

Discussion Forum

Reflection

Assignment Activity

Peer Collaboration

Case Study

Project Activity

Presentation Activity

Workshop

Live Session

Offline Activity

Gamified Activity

Microlearning Activity

---

## Learner Participation

Start Activity

Resume Activity

Pause Activity

Complete Activity

Retry Activity

Abandon Activity

Group Participation

Collaborative Learning

Peer Interaction

Instructor Interaction

Participation Timeline

---

## Activity Rules

Availability Window

Completion Rules

Passing Rules

Attempt Limits

Time Limits

Sequential Learning

Prerequisites

Mandatory Activities

Optional Activities

Adaptive Release

---

## Engagement

Time Spent

Interaction Metrics

Participation Score

Activity Score

Completion Status

Engagement Analytics

Learning Behavior

Activity History

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

Activity Catalog

Timeline

History

Dashboard

Statistics

Analytics

Generate every retrieval API.

---

### Creation

Create Activity

Clone Activity

Create Activity Template

Bulk Import

Initialize Activity

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

Assign Activity

Unassign Activity

Lock

Unlock

Validate

Generate every modification API.

---

### Workflow Operations

Assign Activity

Start Activity

Resume Activity

Complete Activity

Synchronize Learning Progress

Synchronize Homework

Synchronize Quiz Assessment

Notify Learners

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Assignment

Bulk Publication

Rollback

Compliance Review

Conflict Resolution

Generate every administrative API.

---

### Reporting & Analytics

Activity Reports

Participation Reports

Engagement Reports

Completion Reports

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

Homework

Quiz Assessment

Learning Progress

Academic

Student

Timetable

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

Activity Integrity

Learner Authorization

Instructor Authorization

Participation Privacy

Administrative Override

Bulk Operations

Audit Requirements

Learning Privacy

Future Digital Classroom Governance

---

## 7. Performance Considerations

Discuss:

High Concurrent Learners

Activity Tracking

Participation Recording

Progress Synchronization

Caching

Analytics

Scalability

Future Large-scale Online Learning

---

## 8. Monitoring

Define:

Activity Creation

Participation

Completion

Synchronization

Bulk Operations

Operational KPIs

Learning KPIs

Engagement KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

AI Tutors

Adaptive Activities

Virtual Reality

Augmented Reality

Digital Laboratories

Collaborative Whiteboards

Live Class Integration

Learning Recommendations

Gamification

Social Learning

Competency-based Learning

Learning Experience API (xAPI)

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including:

ActivityCreated

ActivityPublished

ActivityAssigned

ActivityStarted

ActivityPaused

ActivityResumed

ActivityCompleted

ParticipationRecorded

EngagementCalculated

ActivityRetired

LearningInteractionRecorded

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

- Activity services

- Participation services

- Engagement engine

- Completion engine

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

ActivityAlreadyPublished

DuplicateActivity

ActivityLocked

VersionConflict

PrerequisiteNotSatisfied

AttemptLimitExceeded

TimeLimitExceeded

ActivityUnavailable

ParticipationConflict

CompletionValidationFailed

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Learning Activity Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Streaming implementation
- Video conferencing implementation
- Collaboration engine details

Focus entirely on learning activity lifecycle, learner engagement, participation management, governance, reporting, monitoring, auditability, event-driven architecture, scalability, compliance, and extensibility.

This document should enable an AI coding agent to generate the complete Learning Activity Management subsystem—including controllers, services, repositories, participation services, engagement engines, completion managers, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
