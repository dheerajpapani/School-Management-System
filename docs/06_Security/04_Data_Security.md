# 04_Data_Security.md

## Objective

You are acting as a Principal Enterprise Security Architect responsible for defining the complete Data Security Architecture for an Enterprise School Management System (SMS).

This document is the authoritative specification governing the protection, classification, storage, transmission, retention, archival, masking, encryption readiness, privacy, and lifecycle management of all data handled by the School Management System.

The objective is to establish a centralized, enterprise-grade data protection framework that ensures confidentiality, integrity, availability, accountability, privacy, and regulatory readiness across every module.

This document defines data security architecture only.

It does NOT define:

- Authentication
- Authorization
- RBAC implementation
- SQL implementation
- PHP implementation
- APIs
- Infrastructure implementation

Assume all previously generated documentation already exists.

Do not duplicate previous documents.

For every security control define:

- Control Owner
- Consumers
- Protected Assets
- Threats Addressed
- Allowed Dependencies
- Forbidden Dependencies
- Security Classification
- Lifecycle
- Monitoring Requirements
- Failure Handling
- Related Contracts

Classify every control as:

- Preventive
- Detective
- Corrective
- Compensating
- Recovery

Map every control to applicable principles:

- Confidentiality
- Integrity
- Availability
- Accountability
- Non-Repudiation
- Privacy

---

# Scope

Define data security architecture for every module.

Include:

Administration

Student

Academic

Attendance

Examination

Fees

Timetable

Homework

LMS

Communication

Transport

Hostel

Library

Inventory

HRMS

Events

Discipline

Alumni

Platform

Generate every required data security policy.

---

# Document Structure

## 1. Purpose

Explain:

Why data security exists.

Difference between:

Public Data

Internal Data

Confidential Data

Restricted Data

Sensitive Personal Data

Operational Data

Reference Data

Audit Data

Explain why business data requires different protection levels.

---

## 2. Data Security Principles

Describe principles including:

Least Exposure

Need-to-Know

Defense in Depth

Data Minimization

Secure by Default

Privacy by Design

Confidentiality

Integrity

Availability

Accountability

Non-Repudiation

Secure Disposal

Explain each principle.

---

## 3. Data Classification Model

Define classification levels.

Examples:

Public

Internal

Confidential

Restricted

Highly Restricted

Future Regulatory Classifications

For each define:

Protection Expectations

Typical Examples

Access Rules

Storage Expectations

Transmission Expectations

Retention Expectations

Disposal Expectations

---

## 4. Module-wise Data Classification

Generate classifications for every module.

Examples:

### Student

Personal Information

Guardian Information

Medical Records

Identity Documents

Academic Records

Behavior Records

Attendance

Photographs

---

### Fees

Invoices

Payments

Scholarships

Refunds

Financial Reports

Ledger

Generate classifications for every remaining module.

---

## 5. Data Lifecycle

Describe lifecycle.

Examples:

Created

Validated

Verified

Approved

Used

Updated

Archived

Retained

Disposed

Recovered

Destroyed

Explain protection expectations during every stage.

---

## 6. Data Protection Strategy

Describe conceptual protection for:

Sensitive Data

Medical Data

Financial Data

Academic Data

Identity Documents

Government IDs

Contact Information

Authentication Data

Configuration Data

Audit Data

Generated Reports

Backups

---

## 7. Data Retention Strategy

Describe:

Operational Retention

Academic Retention

Financial Retention

Medical Retention

Audit Retention

Archived Records

Temporary Data

Generated Files

Logs

Future Legal Holds

---

## 8. Data Disposal Strategy

Describe:

Retention Expiry

Secure Deletion

Logical Deletion

Physical Deletion

Archival Disposal

Verification

Audit

Recovery Restrictions

---

## 9. Privacy Considerations

Describe:

Student Privacy

Parent Privacy

Employee Privacy

Medical Privacy

Financial Privacy

Consent Readiness

Purpose Limitation

Data Minimization

Future Regulatory Readiness

---

## 10. Security Monitoring

Define monitoring for:

Sensitive Data Access

Bulk Export

Bulk Update

Bulk Delete

Unauthorized Access

Privilege Abuse

Data Leakage Indicators

Retention Violations

Operational KPIs

Compliance

---

## 11. Future Extensibility

Support future:

Data Loss Prevention

Data Discovery

Data Classification Automation

Privacy Dashboard

Encryption Services

Tokenization

Pseudonymization

Government Compliance

AI Privacy Controls

---

## 12. Data Protection Matrix

Create a matrix.

Columns:

Data Category

Classification

Protection Level

Retention

Disposal

Monitoring

Future Extension

---

## 13. Architecture Decision Summary

Create a summary table.

Columns:

Area

Decision

Reason

Security Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Data Security Architecture Specification.

Do not include:

- SQL
- PHP
- Encryption algorithms in code
- Infrastructure implementation
- API implementation

Focus entirely on data classification, lifecycle, governance, retention, privacy, monitoring, disposal, and enterprise security architecture.

This document should enable AI coding agents to implement a secure, privacy-aware, enterprise-grade data protection framework across the entire School Management System.
