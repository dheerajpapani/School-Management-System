# 05_Academic_Index.md

## Objective

You are acting as a Principal Enterprise Solution Architect responsible for creating the Academic Domain API Index for an Enterprise School Management System (SMS).

This document serves as the authoritative navigation guide, architecture reference, dependency map, workflow index, resource catalog, and AI implementation guide for the complete Academic API Catalog.

This document is NOT an API specification.

Its purpose is to consolidate all Academic domain documentation into a single architecture index that enables architects, developers, QA engineers, business analysts, AI coding agents, and maintainers to quickly understand the Academic domain without duplicating previous documentation.

This document must remain implementation-independent.

Do NOT generate:

- PHP
- SQL
- JSON
- OpenAPI specifications
- Endpoint definitions
- Infrastructure
- Implementation details

Reference existing documentation rather than duplicating it.

Assume all Academic API documents already exist.

---

# Scope

Create the master index for:

Curriculum Management

Class Management

Subject Management

Lesson Planning

Include future Academic domain extensions.

---

# Document Structure

## 1. Domain Overview

Describe:

Business Purpose

Business Objectives

Business Scope

Business Responsibilities

Domain Boundaries

Primary Consumers

Supporting Modules

Dependent Modules

Security Classification

Operational Criticality

Business Criticality

Future Evolution

Academic Governance Model

---

## 2. Domain Catalog

For every domain include:

Curriculum Management

Class Management

Subject Management

Lesson Planning

For each define:

Purpose

Primary Resources

Primary Workflows

Primary APIs

Dependencies

Consumers

Security Classification

Business Criticality

System of Record

Lifecycle Ownership

Future Extensions

Related Documents

---

## 3. Resource Catalog

Generate a comprehensive resource catalog including:

Curriculum

Curriculum Version

Curriculum Policy

Education Board

Academic Program

Academic Stream

Academic Level

Learning Outcome

Competency

Academic Calendar

Promotion Policy

Assessment Policy

Class

Section

Class Teacher

Subject

Subject Category

Elective

Elective Group

Prerequisite

Teaching Assignment

Lesson Plan

Teaching Schedule

Unit Plan

Topic Plan

Teaching Resource

Learning Resource

Worksheet

Learning Outcome Mapping

Teaching Progress

Coverage

Lesson Review

Lesson Approval

Academic Analytics

Generate every major academic resource.

For every resource define:

Business Purpose

Owning Document

System of Record

Read Ownership

Write Ownership

Lifecycle Owner

Dependencies

Business Criticality

Retention Classification

---

## 4. Workflow Index

Generate an index covering every major academic workflow.

Examples:

Curriculum Creation

Curriculum Approval

Curriculum Publication

Curriculum Version Upgrade

Board Mapping

Academic Program Setup

Policy Management

Class Creation

Section Allocation

Teacher Assignment

Student Allocation

Subject Creation

Elective Selection

Prerequisite Validation

Subject Assignment

Academic Planning

Lesson Planning

Lesson Approval

Lesson Delivery

Coverage Tracking

Outcome Tracking

Teaching Review

Generate every workflow.

For each workflow define:

Purpose

Owning Document

Participating Resources

Participating APIs

Business Rules

Published Events

Consumed Events

Notifications

Background Jobs

Audit Requirements

---

## 5. Dependency Matrix

Create a matrix.

Columns:

Domain

Depends On

Consumed By

Published Events

Consumed Events

Primary Resources

Criticality

Security Level

Future Extension

---

## 6. Cross-module Integration Matrix

Describe integrations with:

Master Administration

Student

Attendance

Examination

Timetable

Homework

LMS

Communication

Fees

Transport

Hostel

Library

Inventory

HRMS

Events

Discipline

Parent Portal

Reporting

Audit

Notification

Search

Configuration

Import/Export

Background Processing

Analytics

For every integration define:

Purpose

Direction

Criticality

Primary Resources

Primary APIs

Primary Workflows

Primary Events

---

## 7. Document Navigation

Create a navigation table.

Columns:

Document

Purpose

Primary Resources

Dependencies

Status

Future Extensions

Include:

01_Curriculum_API.md

02_Class_Management_API.md

03_Subject_Management_API.md

04_Lesson_Planning_API.md

---

## 8. Domain Event Index

Generate an index of every major Academic domain event.

Examples include:

CurriculumCreated

CurriculumUpdated

CurriculumApproved

CurriculumPublished

BoardMapped

ProgramCreated

ClassCreated

ClassCapacityUpdated

SectionCreated

TeacherAssigned

StudentAllocated

SubjectCreated

SubjectUpdated

ElectiveApproved

LessonPlanCreated

LessonApproved

LessonPublished

LessonDelivered

CoverageUpdated

LearningOutcomeMapped

LearningOutcomeAchieved

TeachingProgressUpdated

AcademicReviewCompleted

Generate every major event.

For every event define:

Business Purpose

Producer

Consumers

Ordering

Retry Expectations

Audit Impact

Related Background Jobs

Related Notifications

---

## 9. API Coverage Summary

Summarize:

Business Domains Covered

Resources Covered

CRUD Coverage

Workflow Coverage

Reporting Coverage

Analytics Coverage

Bulk Operations

Imports

Exports

Administration

Configuration

Audit

Monitoring

Security

Compliance

Domain Events

Future Readiness

---

## 10. AI Coding Agent Guidance

Provide implementation guidance.

Include guidance such as:

Always begin from this index.

Respect System of Record ownership.

Respect lifecycle ownership.

Reuse validation contracts.

Reuse business rules.

Reuse services.

Reuse repositories.

Reuse events.

Reuse permissions.

Reuse workflows.

Never duplicate business logic.

Maintain dependency order.

Implement one academic domain at a time.

Respect transaction boundaries.

Respect event ordering.

Generate deterministic implementations.

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

Maintain the tone of a professional Enterprise Academic Domain Architecture Index.

This document must function as:

- Navigation guide
- Architecture map
- Dependency map
- Resource catalog
- Workflow index
- Event index
- AI coding reference
- Documentation entry point

Do not duplicate previous documents.

Instead organize, classify, summarize, and relate them into a single authoritative Academic domain index.

This document should become the primary entry point for the complete Academic API Catalog.
