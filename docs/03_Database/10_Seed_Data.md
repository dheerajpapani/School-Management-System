# 10_Seed_Data.md

## Objective

You are acting as a Principal Database Architect responsible for defining the complete Seed Data Strategy for an Enterprise School Management System (SMS).

This document is the authoritative specification governing how the application is initialized with mandatory system data required for a fresh installation.

It defines what data must exist before the application can function correctly.

It does NOT define SQL INSERT statements.

It does NOT define demo/sample data.

It defines the governance, organization, ownership, lifecycle, versioning, and validation of seed data across all modules.

Assume all previous documentation already exists.

Do not duplicate previous documents.

---

# Scope

Define every mandatory seed dataset required for a production-ready School Management System.

Include:

- Application Configuration
- Institution Defaults
- Academic Defaults
- Countries
- States
- Languages
- Time Zones
- Currency
- Role Definitions
- Permission Definitions
- Menu Definitions
- Lookup Values
- Workflow Statuses
- Attendance Statuses
- Student Statuses
- Employee Statuses
- Fee Categories
- Payment Methods
- Document Types
- Notification Channels
- Notification Templates
- Exam Types
- Grade Definitions
- Leave Types
- Transport Statuses
- Hostel Statuses
- Asset Categories
- Library Categories
- Discipline Categories
- Audit Categories
- Feature Flags
- Dashboard Widgets
- Default Reports
- Search Metadata

Generate every additional seed category required.

---

# Document Structure

## 1. Purpose

Explain:

- Why seed data exists.
- Difference between seed data, reference data, configuration data, transactional data, and demo data.
- Why seed data must be deterministic and idempotent.

---

## 2. Seed Data Principles

Define principles such as:

- Idempotent Initialization
- Environment Independence
- Version Compatibility
- Configuration Driven
- No Transactional Records
- Extensible Design
- Repeatable Execution
- Minimal Mandatory Dataset
- Localization Ready
- Upgrade Safe

Explain each principle.

---

## 3. Seed Data Classification

Group seed data into categories:

- System
- Security
- Academic
- Finance
- Communication
- Student
- Employee
- Library
- Transport
- Hostel
- Inventory
- Reporting
- Workflow
- Lookup
- Localization
- Platform

Explain ownership and purpose.

---

## 4. Module-wise Seed Data

For every module define:

Purpose

Mandatory datasets

Optional datasets

Ownership

Dependencies

Versioning

Validation

Future extensibility

Cover all 19 modules.

---

## 5. Security Seed Data

Define default:

Roles

Permission Groups

Permissions

Menu Hierarchy

Authentication Policies

Password Policies

Session Policies

Approval Levels

Default Administrator

System Users

---

## 6. Configuration Seed Data

Define conceptual initialization for:

Institution

Academic Calendar

Academic Terms

Working Days

Attendance Configuration

Grading Configuration

Fee Configuration

Notification Configuration

Email Configuration

SMS Configuration

File Storage Configuration

Audit Configuration

Logging Configuration

Application Settings

Generate all required configuration groups.

---

## 7. Workflow Seed Data

Describe default workflows and statuses for:

Admissions

Attendance

Examinations

Fees

Library

Transport

Hostel

Inventory

HRMS

Events

Discipline

Alumni

Communication

Approvals

Notifications

---

## 8. Notification Seed Data

Define categories for:

Email Templates

SMS Templates

Push Templates

WhatsApp Templates

Reminder Templates

System Alerts

Approval Notifications

Academic Notifications

Financial Notifications

Operational Notifications

Do not write actual templates.

---

## 9. Reporting Seed Data

Describe initialization of:

Report Categories

Dashboard Widgets

KPIs

Charts

Export Formats

Scheduled Reports

Analytics Groups

Default Filters

---

## 10. Localization

Describe seed data for:

Languages

Currencies

Date Formats

Time Zones

Address Formats

Regional Settings

Future Localization Packs

---

## 11. Validation Strategy

Describe validation for:

Duplicate Seeds

Dependency Validation

Missing Seeds

Reference Integrity

Configuration Integrity

Version Compatibility

Upgrade Safety

Environment Validation

---

## 12. Future Extensibility

Support:

Multi-School

Multi-Tenant

Plugin Modules

Regional Packs

Government Integrations

Marketplace Extensions

Custom Modules

AI Configuration

---

## 13. Seed Data Matrix

Create a matrix.

Columns:

Category

Purpose

Mandatory

Owner

Versioned

Dependencies

Future Extension

---

## 14. Architecture Decision Summary

Create a summary table.

Columns:

Area

Decision

Reason

Operational Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Database Initialization Specification.

Do not include:

- SQL INSERT statements
- Sample records
- Demo data
- Migration scripts
- Database engine specifics

Focus on governance, ownership, versioning, validation, initialization, and long-term maintainability.

This document should enable AI coding agents and DevOps engineers to initialize a production-ready School Management System consistently across all supported environments.
