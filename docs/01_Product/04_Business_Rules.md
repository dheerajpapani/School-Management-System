# 04_Business_Rules.md

## Objective

You are acting as a Senior Business Analyst and Enterprise Domain Expert responsible for defining the complete Business Rules Specification (BRS) for an Enterprise School Management System (SMS).

This document defines the **business policies, constraints, validations, calculations, approvals, and decision logic** that govern system behavior.

It is **NOT** a functional requirements document.

It is **NOT** a database specification.

It is **NOT** an API specification.

It defines **how the business operates**.

Every future validation, workflow, service, controller, API, database constraint, and UI validation must derive from this document.

Assume the following documents already exist:

- Module Structure
- Blueprint
- Functional Requirements
- Non-Functional Requirements
- System Architecture
- Database Architecture
- Entity Catalog
- Domain Model

Do not duplicate them.

---

# Scope

Document every business rule required by every module of the School Management System.

Each rule must be uniquely identifiable.

---

# Document Structure

## 1. Purpose

Explain the purpose of Business Rules.

Describe how they differ from Functional Requirements.

---

## 2. Rule Categories

Classify rules into categories.

Examples:

Validation Rules

Calculation Rules

Eligibility Rules

Approval Rules

Assignment Rules

Scheduling Rules

Financial Rules

Academic Rules

Security Rules

Lifecycle Rules

Notification Rules

Reporting Rules

Retention Rules

Integration Rules

Explain each category.

---

## 3. Rule Definition Format

Every rule must use the following format.

---

Business Rule ID

---

Name

---

Category

---

Business Purpose

---

Applicable Modules

---

Trigger

---

Preconditions

---

Decision Logic

Describe exactly how the rule evaluates.

---

Outcome

---

Exceptions

---

Priority

Critical

High

Medium

Low

---

Dependencies

---

Audit Requirements

---

Future Configuration

State whether the rule should be configurable in future.

---

## 4. Academic Rules

Generate rules for:

Academic Year

Terms

Classes

Sections

Subjects

Curriculum

Promotion

Demotion

Transfers

Graduation

Alumni conversion

---

## 5. Admission Rules

Rules for:

Application

Eligibility

Duplicate detection

Age validation

Admission tests

Interview

Approval

Enrollment

Seat allocation

Waiting list

Cancellation

---

## 6. Student Rules

Rules governing:

Student status

Guardian relationships

Medical records

Document requirements

Identity uniqueness

Academic assignment

Lifecycle transitions

---

## 7. Attendance Rules

Rules including:

Attendance submission

Editing

Correction

Bulk attendance

Attendance locking

Minimum attendance

Defaulter calculation

Holiday handling

Leave handling

Biometric reconciliation

QR attendance

RFID attendance

Exam eligibility

---

## 8. Examination Rules

Rules for:

Exam creation

Scheduling

Assessment

Marks entry

Marks editing

Result calculation

Result approval

Result publication

Grade calculation

CGPA

Ranking

Tie handling

Grace marks

Revaluation

Supplementary exams

---

## 9. Fee Rules

Rules for:

Fee structure

Invoices

Installments

Late fees

Discounts

Scholarships

Concessions

Refunds

Payment allocation

Partial payment

Overpayment

Payment reversal

Receipt generation

Outstanding calculation

Financial holds

---

## 10. Timetable Rules

Teacher availability

Room availability

Period limits

Break rules

Subject frequency

Teacher workload

Conflict detection

Substitution

Temporary schedules

---

## 11. Homework Rules

Publishing

Submission

Late submission

Grading

Resubmission

Attachments

Deadlines

---

## 12. LMS Rules

Course enrollment

Completion

Quiz attempts

Passing score

Certificates

Learning progress

---

## 13. Communication Rules

Notifications

Circulars

Messages

Emergency alerts

Read status

Retry logic

Opt-out policies

---

## 14. Transport Rules

Vehicle assignment

Route capacity

Stop assignment

GPS tracking

Attendance reconciliation

Vehicle maintenance holds

---

## 15. Hostel Rules

Room allocation

Bed allocation

Capacity

Leave

Mess billing

Vacating

Inspection

---

## 16. Library Rules

Book issue

Return

Renewal

Reservations

Fine calculation

Lost books

Damaged books

Maximum issue limits

---

## 17. Inventory Rules

Procurement

Stock movement

Approvals

Asset assignment

Maintenance

Depreciation

Vendor rules

---

## 18. HR Rules

Joining

Probation

Attendance

Leave

Approvals

Exit

Employee status

---

## 19. Discipline Rules

Incident recording

Warnings

Counseling

Suspension

Behavior scoring

Appeals

---

## 20. Event Rules

Registration

Capacity

Certificates

Participation

Approvals

---

## 21. Alumni Rules

Eligibility

Migration

Donations

Mentorship

Communication

---

## 22. Cross-Module Rules

Examples:

Attendance affects Exam Eligibility

Fees affect Report Card Release

Promotion requires Published Results

Transport assignment affects Fee Structure

Hostel allocation affects Billing

Library dues affect Clearance

Disciplinary actions affect Certificates

Inventory requests require Approval

Employee Leave affects Timetable

Generate every possible interaction.

---

## 23. Calculation Rules

Describe formulas conceptually.

Examples:

Attendance Percentage

Late Fee

CGPA

Merit Ranking

Scholarship Amount

Invoice Total

Outstanding Balance

Behavior Score

Do not include code.

---

## 24. Rule Dependency Matrix

Create a matrix.

Columns:

Rule

Depends On

Impacts

Priority

Configurable

---

## 25. Business Rule Summary

Provide a master summary table.

Columns:

Rule ID

Name

Module

Category

Priority

Future Configuration

---

# Writing Style

Maintain the tone of a professional Business Rules Specification.

Avoid implementation.

Avoid SQL.

Avoid APIs.

Avoid UI.

Focus entirely on deterministic business logic.

Every rule must be uniquely identifiable.

Write so that AI coding agents can implement validations, workflows, services, and automated decisions directly from this specification.
