# 03_Academic_Management.md

## Objective

You are acting as a Principal Enterprise Solution Architect responsible for producing the definitive Module Specification for the Academic Management module of an Enterprise School Management System (SMS).

This document defines the complete academic domain, including curriculum, academic structure, class organization, subject management, teacher allocation, lesson planning, syllabus planning, learning outcomes, and academic governance.

It is the authoritative specification for all future implementation related to academic operations.

This document must guide backend development, frontend implementation, database design, reporting, testing, APIs, workflows, and AI-assisted code generation.

Assume the following documents already exist:

- Module Structure
- Blueprint
- Functional Requirements
- Non-Functional Requirements
- Business Rules
- System Architecture
- Domain Model
- Database Architecture
- Entity Catalog
- Master Administration Module Specification
- Student Information System Module Specification

Reference them where appropriate without duplicating content.

---

# Scope

Cover the complete Academic Management module.

Include:

## Curriculum Management

Curriculum Framework

Academic Programs

Curriculum Versions

Subject Allocation

Learning Outcomes

Course Mapping

Credits

Academic Calendar Integration

Curriculum Publishing

Curriculum Archival

---

## Class Management

Class Creation

Section Assignment

Student Allocation

Teacher Allocation

Homeroom/Class Teacher Assignment

Class Capacity

Promotion Readiness

Section Balancing

Multi-Branch Support

---

## Subject Management

Core Subjects

Elective Subjects

Optional Subjects

Practical Subjects

Language Subjects

Lab Subjects

Subject Groups

Subject Dependencies

Subject Credits

Subject Prerequisites

Subject Status

---

## Lesson Planning

Annual Plans

Term Plans

Unit Plans

Chapter Plans

Daily Lesson Plans

Learning Objectives

Teaching Resources

Assessment Mapping

Progress Tracking

Lesson Completion

---

# Document Structure

## 1. Module Overview

Purpose

Business Objectives

Responsibilities

Module Boundaries

Business Owner

Dependencies

Consumers

---

## 2. Functional Scope

Describe every capability within each submodule.

Explain expected business behavior.

---

## 3. Academic Structure Workflow

Describe the complete workflow for creating and maintaining:

Programs

Curriculum

Classes

Sections

Subjects

Teacher Assignments

Academic Calendar Mapping

Activation

Closure

Archival

Alternative flows

---

## 4. Curriculum Lifecycle

Draft

Review

Approval

Published

Active

Revised

Retired

Archived

Allowed transitions

Invalid transitions

Approval requirements

Version management

Historical retention

---

## 5. Subject Management

Ownership

Subject hierarchy

Grouping

Dependencies

Credits

Prerequisites

Assessment mapping

Cross-class mapping

Cross-branch reuse

Versioning

---

## 6. Teacher Allocation

Assignment rules

Maximum workload

Minimum workload

Primary teacher

Secondary teacher

Substitute readiness

Department ownership

Approval process

Historical tracking

---

## 7. Lesson Planning

Planning hierarchy

Annual → Term → Unit → Chapter → Daily Lesson

Learning outcomes mapping

Teaching resources

Assessment linkage

Completion tracking

Approval workflow

Revision handling

Progress monitoring

---

## 8. Business Capabilities

Generate a complete capability list.

Examples:

Create Curriculum

Clone Curriculum

Publish Curriculum

Archive Curriculum

Create Subject

Assign Subject

Deactivate Subject

Create Class

Create Section

Merge Sections

Split Sections

Assign Teacher

Transfer Teacher

Assign Class Teacher

Generate Academic Calendar

Approve Lesson Plan

Clone Lesson Plan

Track Progress

Generate Coverage Report

etc.

---

## 9. Validation Rules

Curriculum validations

Subject uniqueness

Credit rules

Teacher workload

Section capacity

Learning outcome mapping

Lesson approval

Academic calendar consistency

Version conflicts

Cross-branch restrictions

---

## 10. Permissions Matrix

Define permissions for:

View

Create

Edit

Delete

Archive

Restore

Approve

Reject

Assign

Publish

Clone

Transfer

Import

Export

Generate Reports

Track Progress

Specify role granularity.

---

## 11. Cross Module Dependencies

Describe interactions with:

Master Administration

Student Information System

Attendance

Examination

Timetable

Homework

LMS

Communication

HRMS

Transport

Library

Events

For each interaction define:

Dependency direction

Read ownership

Write ownership

Domain ownership

Trigger events

Failure handling

---

## 12. Notifications

List all notifications.

Curriculum Published

Teacher Assigned

Lesson Plan Approved

Lesson Plan Rejected

Subject Changed

Academic Calendar Updated

Class Assignment Changed

Recipients

Priority

Retry expectations

---

## 13. Reports

List every report.

Curriculum Coverage

Teacher Workload

Subject Allocation

Class Allocation

Lesson Progress

Learning Outcome Coverage

Academic Calendar

Section Strength

Teacher Assignment

Subject Matrix

Curriculum Versions

Custom Reports

Describe purpose, filters, consumers, and export capabilities.

---

## 14. Import / Export

Curriculum import

Subject import

Teacher allocation import

Lesson plan import

Bulk updates

Validation

Rollback

Preview

Templates

Duplicate handling

---

## 15. Performance Expectations

Large curriculum management

Teacher allocation

Lesson plan search

Progress analytics

Bulk operations

Caching opportunities

Pagination

Scalability expectations

---

## 16. Error Scenarios

Duplicate curriculum

Teacher overload

Invalid subject mapping

Capacity exceeded

Approval conflicts

Version conflicts

Concurrent edits

Academic year mismatch

Recovery expectations

---

## 17. Future Enhancements

Competency-based education

Outcome-based education

AI lesson planning

AI curriculum recommendations

Bloom's taxonomy integration

Adaptive curriculum

Learning pathway analytics

National curriculum synchronization

External LMS synchronization

---

## 18. Module Decision Summary

Create a summary table.

Columns:

Capability

Owner

Dependencies

Criticality

Future Expansion

Implementation Complexity

---

# Writing Style

Maintain a professional enterprise module specification.

Do not include SQL.

Do not include APIs.

Do not include PHP code.

Do not include UI layouts.

Focus on business behavior, ownership, workflows, validations, permissions, lifecycle, reporting, and cross-module interactions.

The document should be sufficiently detailed that an AI coding agent can implement the Academic Management module with minimal assumptions while remaining consistent with all previously generated documentation.
