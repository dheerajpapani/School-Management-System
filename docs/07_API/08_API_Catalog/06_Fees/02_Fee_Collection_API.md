# 02_Fee_Collection_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Fee Collection domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to fee demand generation, fee collection, receipts, refunds, adjustments, reversals, payment reconciliation, payment allocation, outstanding balances, financial compliance, and collection governance.

The Fee Collection domain manages the operational lifecycle of collecting student fees and integrates with Fee Structures, Installments, Scholarships, Student Lifecycle, Admissions, Transport, Hostel, Parent Portal, Communication, Finance Reports, Accounting, Reporting, Notifications, and Audit.

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

Assume all previous architecture, contracts, validation rules, workflows, security documentation, API standards, and Fee Structure APIs already exist.

Reference previous documentation instead of duplicating it.

---

# Enterprise Financial Principles

Model all financial transactions as immutable business records.

Never modify finalized financial transactions.

Support corrections through:

- Adjustment Transactions
- Reversal Transactions
- Refund Transactions
- Waiver Transactions
- Credit Notes
- Debit Notes
- Reconciliation Entries

Every financial operation must be fully auditable.

For every business API explicitly identify:

- API Category
- Execution Type
- Idempotency
- Transaction Boundary
- Audit Requirements
- Financial Integrity Requirements
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

## Fee Demand

Demand Generation

Demand Revision

Demand Cancellation

Demand Synchronization

Outstanding Balance

Opening Balance

Closing Balance

Demand History

---

## Fee Collection

Cash Collection

Cheque Collection

Online Collection

Bank Transfer

UPI

Card Payment

Wallet Payment

Mixed Payment

Advance Collection

Partial Payment

Bulk Collection

Offline Collection

---

## Receipt Management

Receipt Generation

Receipt Reprint

Duplicate Receipt

Receipt Cancellation

Receipt Reversal

Receipt Verification

Receipt History

Receipt Audit

Digital Receipt

---

## Payment Allocation

Fee Head Allocation

Installment Allocation

Transport Allocation

Hostel Allocation

Fine Allocation

Late Fee Allocation

Scholarship Adjustment

Credit Adjustment

Generate every allocation API.

---

## Refund Management

Refund Request

Refund Approval

Refund Processing

Partial Refund

Full Refund

Refund Adjustment

Refund Audit

Generate every refund API.

---

## Financial Adjustments

Adjustment Entry

Credit Note

Debit Note

Reversal

Correction

Manual Adjustment

Write-off

Recovery

Generate every adjustment API.

---

## Collection Governance

Approval

Verification

Lock

Unlock

Daily Closing

Cash Reconciliation

Bank Reconciliation

Compliance

Audit

Generate every governance API.

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

Outstanding Balance

Ledger

Payment History

Receipt History

Transaction History

Analytics

Dashboard

Generate every retrieval API.

---

### Creation

Generate Demand

Collect Fee

Generate Receipt

Generate Refund

Generate Credit Note

Generate Debit Note

Bulk Collection

Import Collections

Initialize Collection

Generate every creation API.

---

### Modification

Approve

Reject

Reverse

Refund

Adjust

Allocate

Verify

Lock

Unlock

Close Day

Reconcile

Validate

Generate every modification API.

---

### Workflow Operations

Generate Demand

Collect Payment

Allocate Payment

Generate Receipt

Process Refund

Reverse Transaction

Reconcile Cash

Reconcile Bank

Synchronize Parent Portal

Synchronize Student Ledger

Generate Reports

Generate Analytics

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Verification

Bulk Collection

Bulk Reconciliation

Rollback

Compliance Review

Conflict Resolution

Generate every administrative API.

---

### Reporting & Analytics

Collection Reports

Outstanding Reports

Refund Reports

Cash Reports

Bank Reports

Collection Trends

Executive Dashboards

Operational Dashboards

Financial Analytics

Generate every reporting API.

---

## 4. API Specification Template

Use the standardized enterprise template.

---

## 5. Cross-module Integration

Explain integrations with:

Master Administration

Student

Admissions

Student Lifecycle

Fee Structure

Installments

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

Financial Integrity

Receipt Security

Refund Controls

Adjustment Controls

Administrative Override

Cash Handling

Reconciliation Controls

Audit Requirements

Regulatory Compliance

Future Payment Gateway Security

---

## 7. Performance Considerations

Discuss:

Bulk Collection

Receipt Generation

Ledger Queries

Outstanding Calculation

Payment Allocation

Caching

Analytics

Scalability

Future Distributed Payment Processing

---

## 8. Monitoring

Define:

Collections

Refunds

Adjustments

Reconciliation

Daily Closing

Bulk Operations

Operational KPIs

Financial KPIs

Collection KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

Payment Gateway Integration

Recurring Payments

Auto Collection

Subscription Billing

Digital Wallet

Government Fee Collection

Multi-currency

Cross-campus Collection

ERP Accounting Integration

Real-time Banking APIs

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including:

FeeDemandGenerated

FeeCollected

ReceiptGenerated

ReceiptCancelled

PaymentAllocated

RefundRequested

RefundApproved

RefundProcessed

CreditNoteIssued

DebitNoteIssued

CollectionReconciled

DailyClosingCompleted

OutstandingUpdated

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

- Collection services
- Ledger services
- Allocation engine
- Receipt engine
- Refund engine
- Adjustment engine
- Repository ownership
- Transaction boundaries
- Event publication
- Background jobs
- Notification orchestration

---

## 13. Error & Exception Catalog

Define business exceptions including:

DuplicatePayment

ReceiptAlreadyCancelled

RefundAlreadyProcessed

OutstandingMismatch

AllocationFailure

LedgerOutOfBalance

DailyClosingCompleted

CashMismatch

BankReconciliationFailed

CreditAdjustmentConflict

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Fee Collection API Catalog Specification.

Do not include implementation details.

Focus entirely on financial workflows, immutable transaction management, governance, reconciliation, auditability, event-driven architecture, reporting, monitoring, compliance, scalability, and extensibility.

This document should enable an AI coding agent to generate the complete Fee Collection subsystem—including controllers, services, repositories, ledger services, receipt engines, reconciliation services, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
