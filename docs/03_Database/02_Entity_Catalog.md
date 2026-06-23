# 02_Entity_Catalog.md

## Objective

You are acting as a Principal Enterprise Data Architect responsible for defining the complete conceptual data model of an Enterprise School Management System (SMS).

This document is the **authoritative catalog of all business entities** that exist in the system.

It is **NOT** a SQL document.

It is **NOT** a database schema.

It is **NOT** an ER diagram.

It is **NOT** an API specification.

Its purpose is to define every business entity before any physical database tables are designed.

Future SQL, APIs, PHP Models, DTOs, Services, Validation Rules, Reports, and UI components must derive from this document.

Assume the following documents already exist:

* Module Structure
* Blueprint
* System Architecture
* Functional Requirements
* Non-Functional Requirements
* Database Architecture

Do not duplicate their contents.

---

# Scope

Identify every conceptual business entity required across every module of the School Management System.

Every entity should exist exactly once in this document.

Do not omit supporting entities.

Do not create implementation-specific entities.

---

# Document Structure

## 1. Purpose

Explain why a centralized Entity Catalog is required.

Describe its role in maintaining consistency across architecture, database design, APIs, backend models, and frontend development.

---

## 2. Entity Classification

Classify all entities into logical categories.

Examples include:

* Master Entities
* Transactional Entities
* Configuration Entities
* Reference Entities
* Workflow Entities
* Audit Entities
* Integration Entities
* Reporting Entities
* Historical Entities
* Temporary Entities

Explain the purpose of each category.

---

## 3. Entity Definition Format

Every entity throughout this document must follow the exact structure below.

---

### Entity Name

---

### Business Purpose

Describe why this entity exists.

---

### Business Owner

Which module owns this entity.

---

### Description

Explain what the entity represents.

---

### Responsibilities

What information this entity is responsible for.

---

### What This Entity MUST Contain

Business-level attributes only.

Do **NOT** list SQL columns.

Examples:

Student

* Personal Identity
* Admission Information
* Current Academic Assignment
* Guardian References
* Medical Summary
* Status

---

### What This Entity MUST NOT Contain

Clearly define boundaries.

Example:

Student must not contain

* Attendance Records
* Fee Transactions
* Exam Marks

Those belong to other entities.

---

### Relationships

Conceptual relationships only.

Example:

Student

has many Attendance Records

has many Fee Invoices

belongs to one Current Section

belongs to one Current Class

has many Guardians

---

### Lifecycle

Describe:

Creation

Updates

State Changes

Archival

Deletion

Historical retention

---

### States

Examples:

Draft

Pending

Approved

Active

Suspended

Completed

Cancelled

Archived

Explain transitions conceptually.

---

### Business Rules

List rules affecting this entity.

No implementation.

---

### Dependencies

Other conceptual entities.

---

### Security Classification

Public

Internal

Confidential

Highly Confidential

Restricted

Explain access expectations.

---

### Audit Requirements

Describe required audit expectations.

---

### Future Extensibility

How this entity may evolve.

---

## 4. Complete Entity Catalog

Generate every business entity required by the project.

Include all conceptual entities for every module.

Examples include (but are not limited to):

Institution

Branch

Academic Year

Academic Term

Department

Class

Section

House

Club

Committee

User

Role

Permission

Student

Guardian

Admission Application

Admission Test

Interview

Student Lifecycle Event

Student Document

Medical Profile

Teacher

Employee

Attendance Session

Attendance Record

Subject

Curriculum

Lesson Plan

Learning Outcome

Homework

Assignment

Project

Learning Material

Quiz

Question

Quiz Attempt

Exam

Assessment

Mark Entry

Result

Report Card

Grade Scale

Fee Head

Fee Structure

Installment Plan

Invoice

Invoice Item

Payment

Scholarship

Concession

Ledger Entry

Timetable

Timetable Slot

Teacher Substitution

Notification

Message

Circular

Announcement

Vehicle

Route

Stop

Transport Assignment

GPS Position

Hostel

Room

Bed

Hostel Allocation

Library Item

Book Copy

Loan

Reservation

Inventory Item

Vendor

Purchase Order

Asset

Asset Assignment

Maintenance Record

Employee Leave

Event

Registration

Certificate

Discipline Incident

Corrective Action

Behavior Record

Alumni

Donation

Mentorship

Audit Log

Configuration

System Setting

File Attachment

Background Job

Integration Event

and every additional entity necessary to fully represent the system.

No entity should be omitted because it appears "small."

---

## 5. Entity Ownership Matrix

Create a matrix showing:

Entity

Owning Module

Primary Responsibility

Shared Consumers

Read Access

Write Access

---

## 6. Cross-Entity Rules

Describe conceptual rules governing interactions between entities.

Examples:

Student references Guardian.

Attendance references Student.

Fee Invoice references Student.

Payment references Invoice.

Result references Assessment.

Report Card references Result.

Focus on conceptual integrity.

---

## 7. Entity Lifecycle Matrix

Create a matrix listing:

Entity

Created By

Updated By

Archived By

Deleted By

Retention Requirement

Historical Requirement

---

## 8. Security Classification Matrix

For every entity classify sensitivity.

Examples:

Public

Internal

Confidential

Highly Confidential

Restricted

Describe expected access level.

---

## 9. Entity Summary

Create a concise table.

Columns:

Entity

Business Owner

Category

Lifecycle

Security Classification

Future Expansion

This table becomes the quick-reference catalog for architects and developers.

---

# Writing Style

Maintain a professional enterprise data architecture style.

Do not include SQL.

Do not include column definitions.

Do not include APIs.

Do not include implementation details.

Focus entirely on business entities and their conceptual meaning.

Write with enough precision that every future database table, PHP model, REST resource, GraphQL type, DTO, validation rule, report, and UI form can be derived directly from this document without ambiguity.
