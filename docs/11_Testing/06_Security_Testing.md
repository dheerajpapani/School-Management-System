# 06_Security_Testing.md

## Objective

You are acting as a Principal Application Security Architect and QA Architect responsible for designing the Enterprise Security Testing Specification for an Enterprise School Management System (SMS).

This document defines the enterprise standards governing security testing across the complete School Management System.

It establishes principles, architecture, validation strategy, governance, quality standards, compliance readiness, risk assessment, and future security evolution.

The School Management System stores highly sensitive information including student records, staff information, payroll, examinations, financial transactions, attendance, disciplinary records, documents, and institutional data.

This document serves as the authoritative reference for validating application security before every release.

Remain implementation-independent.

Assume the following documentation already exists:

- Product Documentation

- Architecture

- Database

- Workflows

- Contracts

- Security Documentation

- API Documentation

- Design System

- Deployment Documentation

- Testing Strategy

- Unit Testing

- Integration Testing

- API Testing

- UI Testing

Reference previous documentation instead of duplicating it.

Do NOT generate:

- Penetration testing scripts

- Exploit examples

- Attack payloads

- OWASP implementation code

- Programming language examples

- Security tool configuration

Remain architecture-focused.

---

# Scope

Generate enterprise security testing standards covering:

Authentication

Authorization

RBAC

Sessions

APIs

Database

File Storage

Uploads

Downloads

Notifications

Search

Reports

Analytics

Background Jobs

Import/Export

Logging

Monitoring

Infrastructure

Configuration

Future AI Components

External Integrations

---

# Enterprise Security Testing Principles

Security by Design

Defense in Depth

Least Privilege

Zero Trust Readiness

Privacy by Design

Continuous Validation

Risk-based Testing

Compliance Readiness

Automation Readiness

Future Evolution

---

# Document Structure

## 1. Security Testing Overview

Describe:

Purpose

Objectives

Testing Philosophy

Business Benefits

Compliance Benefits

Testing Scope

Future Evolution

---

## 2. Security Architecture Validation

Define validation for:

Authentication

Authorization

RBAC

Permissions

Sessions

Identity

API Security

Database Security

File Security

Configuration Security

Infrastructure Security

Secrets Management

Audit Logging

Future AI Security

---

## 3. Authentication Testing

Generate standards covering:

Login

Logout

Password Policies

Password Reset

MFA Readiness

Session Creation

Session Expiration

Session Revocation

Concurrent Sessions

Remember Me

Account Lockout

Credential Recovery

---

## 4. Authorization Testing

Generate validation covering:

RBAC

Permission Matrix

Module Access

Screen Access

API Access

Field-level Permissions

Row-level Visibility

Tenant Isolation Readiness

Administrative Privileges

Privilege Escalation

Delegated Access

---

## 5. API Security Validation

Define standards covering:

Authentication

Authorization

Input Validation

Output Validation

Sensitive Data Protection

Rate Limiting

Request Validation

Response Validation

Error Information Disclosure

Version Security

Audit Logging

Future API Evolution

---

## 6. Data Protection Testing

Generate standards covering:

Encryption Readiness

Sensitive Data

PII Protection

Financial Data

Student Records

Employee Records

Documents

Reports

Audit Logs

Data Export

Data Retention

Data Deletion

Privacy

---

## 7. File Security Testing

Define validation for:

Upload Validation

Download Authorization

File Types

Size Limits

Storage Permissions

Virus Scanning Readiness

File Isolation

Document Privacy

Media Security

Temporary Files

Archive Validation

---

## 8. Workflow Security

Generate validation covering:

Admissions

Attendance

Examinations

Fee Collection

Payroll

Library

Inventory

Transport

Hostel

HRMS

Communication

Events

Discipline

Alumni

Reporting

Analytics

For every workflow define:

Security Risks

Expected Controls

Validation Strategy

Failure Conditions

Recovery

---

## 9. Audit & Compliance Validation

Cover:

Audit Logging

Administrative Actions

Configuration Changes

Financial Operations

Authentication Events

Authorization Events

Report Generation

Data Export

User Activity

Compliance Readiness

Privacy Validation

---

## 10. Security Risk Assessment

Generate standards covering:

Critical Risks

High Risks

Medium Risks

Low Risks

Risk Prioritization

Mitigation Validation

Regression

Continuous Monitoring

Future Threat Modeling

---

## 11. Security Metrics

Define metrics covering:

Authentication Success

Authentication Failures

Authorization Failures

Permission Violations

Audit Coverage

Security Defect Density

Security Regression

Incident Detection

Compliance Coverage

Executive KPIs

---

## 12. Automation Readiness

Generate standards for:

Continuous Security Validation

Regression

Dependency Verification

Configuration Validation

Secret Validation

Policy Validation

Environment Validation

Continuous Monitoring

Future AI-assisted Security Testing

---

## 13. AI Coding Agent Guidance

Provide implementation guidance covering:

Authentication validation

Authorization validation

Permission testing

Security regression

Audit verification

Data protection

Configuration validation

Compliance readiness

Maintainability

Future security evolution

---

## 14. Security Test Lifecycle

Define standards for:

Planning

Risk Assessment

Test Design

Execution

Validation

Regression

Review

Documentation

Maintenance

Continuous Improvement

---

## 15. Architecture Decision Summary

Generate a summary table including:

Area

Decision

Reason

Security Benefit

Business Benefit

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Security Testing Specification.

Avoid implementation details.

Avoid penetration testing instructions.

Avoid exploit examples.

Avoid security tool recommendations.

Focus entirely on security architecture validation, compliance, governance, privacy, risk management, maintainability, automation readiness, and long-term evolution.

This document should become the definitive security testing standard governing every component of the Enterprise School Management System.
