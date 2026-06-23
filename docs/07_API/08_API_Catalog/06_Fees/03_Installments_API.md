# 03_Installments_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Installment Management domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to fee installment planning, installment schedules, payment plans, due dates, installment revisions, installment restructuring, overdue processing, penalties, installment governance, and payment lifecycle management.

The Installment Management domain defines how fee obligations are divided into payable schedules and integrates with Fee Structure, Fee Collection, Scholarships, Student Lifecycle, Admissions, Transport, Hostel, Parent Portal, Communication, Finance Reports, Accounting, Reporting, Analytics, Notifications, and Audit.

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
- Accounting implementation
- Payment gateway implementation

Assume all previously generated architecture, contracts, validation rules, workflows, security documentation, API standards, Fee Structure APIs, Fee Collection APIs, and Finance documentation already exist.

Reference previous documentation instead of duplicating it.

---

# Enterprise Financial Principles

Treat installments as contractual payment schedules.

Once an installment becomes financially active, preserve historical integrity.

Future changes must occur through:

- Revised Installment Plans
- Schedule Amendments
- Installment Adjustments
- Deferred Installments
- Waivers
- Extensions
- Settlement Transactions

Never overwrite financial history.

Every installment lifecycle action must be auditable.

---

# Scope

Generate the complete API specification for:

## Installment Plans

Academic Installments

Admission Installments

Recurring Installments

Monthly Plans

Quarterly Plans

Half-yearly Plans

Annual Plans

Custom Payment Plans

Student-specific Plans

Bulk Installment Plans

Installment Templates

Version Management

---

## Installment Scheduling

Due Dates

Grace Periods

Installment Calendar

Payment Windows

Installment Sequencing

Dependency Rules

Schedule Validation

Holiday Handling

Automatic Schedule Generation

Academic Calendar Synchronization

---

## Installment Lifecycle

Draft

Pending Approval

Approved

Published

Active

Partially Paid

Fully Paid

Overdue

Deferred

Cancelled

Closed

Archived

Version History

---

## Installment Adjustments

Due Date Extension

Payment Deferral

Installment Merge

Installment Split

Rescheduling

Waivers

Penalty Removal

Restructuring

Settlement

Adjustment Audit

---

## Penalties & Charges

Late Fee Calculation

Penalty Rules

Interest Calculation

Grace Period Validation

Penalty Waiver

Penalty Reversal

Compliance Validation

---

## Payment Tracking

Outstanding Installments

Paid Installments

Partial Payments

Advance Payments

Overdue Tracking

Installment Ledger

Installment Status

Collection Readiness

---

## Governance

Approval

Review

Publication

Versioning

Compliance

Retention

Audit

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

Due Schedule

Outstanding Schedule

Installment Calendar

History

Statistics

Analytics

Dashboard

Generate every retrieval API.

---

### Creation

Create Installment Plan

Generate Installments

Clone Installment Plan

Bulk Generate

Import

Initialize

Generate every creation API.

---

### Modification

Approve

Reject

Activate

Suspend

Revise

Reschedule

Extend

Merge

Split

Adjust

Waive

Lock

Unlock

Archive

Restore

Validate

Generate every modification API.

---

### Workflow Operations

Generate Payment Schedule

Calculate Due Dates

Calculate Penalties

Synchronize Fee Collection

Synchronize Student Ledger

Synchronize Scholarships

Generate Notifications

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Reschedule

Bulk Waiver

Bulk Activation

Rollback

Compliance Review

Conflict Resolution

Generate every administrative API.

---

### Reporting & Analytics

Installment Reports

Overdue Reports

Collection Forecast Reports

Penalty Reports

Payment Plan Reports

Executive Dashboards

Operational Dashboards

Financial Analytics

Generate every reporting API.

---

## 4. API Specification Template

Document every API using the standardized enterprise template.

---

## 5. Cross-module Integration

Explain integrations with:

Master Administration

Student

Admissions

Student Lifecycle

Fee Structure

Fee Collection

Scholarships

Transport

Hostel

Finance Reports

Accounting

Communication

Parent Portal

Reporting

Audit

Notifications

Background Processing

Search

Import/Export

Generate every integration dependency.

---

## 6. Security Considerations

Cover:

Installment Integrity

Schedule Protection

Penalty Controls

Waiver Controls

Administrative Override

Bulk Operations

Financial Compliance

Audit Requirements

Future Regulatory Readiness

---

## 7. Performance Considerations

Discuss:

Bulk Installment Generation

Penalty Calculation

Schedule Resolution

Outstanding Calculation

Caching

Analytics

Scalability

Future Large-scale Financial Planning

---

## 8. Monitoring

Define:

Installment Creation

Due Date Changes

Penalty Processing

Waivers

Overdue Accounts

Bulk Operations

Operational KPIs

Financial KPIs

Collection KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

Dynamic Payment Plans

AI Payment Prediction

Subscription Billing

Recurring Payment Engines

Flexible Installments

Government Financial Aid

Multi-currency

Cross-campus Payment Plans

ERP Integration

Real-time Banking APIs

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including:

InstallmentPlanCreated

InstallmentsGenerated

InstallmentApproved

InstallmentActivated

InstallmentRescheduled

InstallmentDeferred

InstallmentMerged

InstallmentSplit

PenaltyCalculated

PenaltyWaived

InstallmentPaid

InstallmentOverdue

PaymentScheduleGenerated

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

- Installment services
- Scheduling engine
- Penalty engine
- Repository ownership
- Event publication
- Background jobs
- Transaction handling
- Validation sequencing
- Notification orchestration
- Concurrency handling

---

## 13. Error & Exception Catalog

Define business exceptions including:

InstallmentAlreadyPaid

InstallmentLocked

InvalidPaymentPlan

ScheduleConflict

PenaltyCalculationFailed

DueDateViolation

InstallmentAlreadyClosed

WaiverConflict

DeferredInstallmentConflict

OutstandingMismatch

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Installment Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Accounting implementation
- Payment gateway implementation

Focus entirely on payment scheduling, installment governance, financial workflows, immutable schedule management, reporting, monitoring, auditability, event-driven architecture, compliance, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Installment Management subsystem—including controllers, services, repositories, scheduling engines, penalty engines, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
