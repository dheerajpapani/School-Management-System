# 02_Validation_Contracts.md

## Objective

You are acting as a Principal Software Architect responsible for defining the complete Validation Layer Contract for an Enterprise School Management System (SMS).

This document defines the architecture, ownership, lifecycle, responsibilities, and standards for all validation performed within the system.

It is the authoritative specification governing:

- Field validation
- Business validation
- Cross-module validation
- Workflow validation
- Authorization validation
- State validation
- Import validation
- Export validation
- Integration validation

It defines **where validation belongs** and **who owns each validation**.

This document must eliminate duplicated validation logic and ensure consistency across controllers, services, APIs, imports, background jobs, scheduled tasks, and integrations.

Assume all previous documentation already exists.

Do not duplicate previous documents.

---

# Scope

Define every validation category required throughout the School Management System.

Avoid implementation.

Do not write PHP.

Do not write SQL.

Do not define API payloads.

---

# Document Structure

## 1. Purpose

Explain why validation must be centralized.

Explain the difference between:

- UI validation
- Application validation
- Business validation
- Database constraints

---

## 2. Validation Architecture

Describe the validation philosophy.

Include:

- Fail Fast
- Layered Validation
- Reusable Validators
- Stateless Validators
- Immutable Validation Results
- Validation Composition
- Rule Reuse
- Separation from Business Logic

---

## 3. Validation Categories

Define:

### Input Validation

### Format Validation

### Required Field Validation

### Business Rule Validation

### State Validation

### Cross-Module Validation

### Workflow Validation

### Permission Validation

### Financial Validation

### Academic Validation

### Attendance Validation

### Examination Validation

### Import Validation

### Export Validation

### File Upload Validation

### Integration Validation

### Background Job Validation

Describe each category.

---

## 4. Validation Ownership

For every module define:

Validation Owner

Shared Validators

Module Validators

Cross-module Validators

Reusable Validators

---

## 5. Validator Definition Format

Every validator must include:

Validator Name

Purpose

Owner

Inputs

Outputs

Dependencies

Validation Rules

Failure Conditions

Success Conditions

Consumed Services

Published Events (if any)

Audit Expectations

Performance Expectations

Future Extension

---

## 6. Shared Validators

Generate shared validators.

Examples:

EmailValidator

PhoneValidator

DateValidator

MoneyValidator

PercentageValidator

AcademicYearValidator

SectionCapacityValidator

AttendanceEligibilityValidator

ExamEligibilityValidator

FeeEligibilityValidator

StudentStatusValidator

GuardianValidator

DocumentValidator

IdentityValidator

PaymentValidator

InvoiceValidator

ResultValidator

GradeValidator

TimetableConflictValidator

RoomAvailabilityValidator

TeacherAvailabilityValidator

LeaveOverlapValidator

FileValidator

RoleValidator

PermissionValidator

ConfigurationValidator

Generate all reusable validators.

---

## 7. Module Validation Matrix

Generate a matrix.

Columns:

Module

Validation

Owner

Shared

Criticality

Reusable

---

## 8. Validation Execution Order

Describe:

Request Validation

Business Validation

Authorization Validation

Workflow Validation

Transaction Validation

Persistence Validation

Post-Processing Validation

Background Validation

---

## 9. Cross-Module Validation Rules

Describe validations requiring multiple modules.

Examples:

Attendance → Examination

Fees → Report Card

Transport → Student

Hostel → Fees

Library → Student Exit

Promotion → Results

Promotion → Attendance

Promotion → Fee Clearance

Employee Leave → Timetable

Inventory → Procurement

Generate all cross-module validation scenarios.

---

## 10. Validation Failure Strategy

Describe:

Validation Errors

Business Errors

Warnings

Recoverable Errors

Blocking Errors

Retryable Errors

Partial Validation

Batch Validation

Bulk Import Validation

Conflict Resolution

---

## 11. Performance Strategy

Describe:

Validation Caching

Reusable Results

Bulk Validation

Parallel Validation

Background Validation

Large Imports

Scalability

---

## 12. Security Considerations

Validation against:

SQL Injection

XSS

File Uploads

Malicious Content

Duplicate Requests

Replay Attacks

Permission Escalation

Invalid State Changes

Data Tampering

---

## 13. Future Extensibility

Support future:

Dynamic Validation Rules

Configuration-driven Validation

AI-assisted Validation

Regional Validation Packs

Government Compliance Rules

Plugin Validators

Custom Validators

---

## 14. Validation Summary

Generate a summary table.

Columns:

Validator

Owner

Category

Reusable

Criticality

Future Configuration

---

# Writing Style

Maintain the tone of a professional Enterprise Software Architecture Specification.

Do not include:

- PHP code
- SQL
- Database schemas
- APIs
- UI validation code

Focus entirely on validation architecture, ownership, execution order, reuse, consistency, and governance.

This document should enable AI coding agents to implement a unified validation layer across the entire application without duplicated logic or inconsistent behavior.
