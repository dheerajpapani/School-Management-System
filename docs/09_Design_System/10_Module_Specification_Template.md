# 10_Module_Specification_Template.md

## Objective

You are acting as a Principal Enterprise Solution Architect responsible for producing the complete functional, technical, UX, workflow, security, reporting, integration, and implementation specification for a single module of the Enterprise School Management System (SMS).

This document acts as the **master template** for every module specification throughout the platform.

It must be reusable for:

* Master Administration
* Student
* Academic
* Attendance
* Examination
* Fees
* Timetable
* Homework
* LMS
* Communication
* Parent Portal
* Transport
* Hostel
* Library
* Inventory
* HRMS
* Discipline
* Events
* Alumni
* Reporting
* Analytics
* Future Modules

This template must remain implementation-independent.

Do NOT generate:

* Source Code
* SQL
* API Endpoints
* HTML
* CSS
* JavaScript
* Framework-specific implementations

Reference previously completed documentation instead of duplicating it.

---

# Module Document Structure

---

# 1. Module Overview

Describe:

* Business Purpose
* Objectives
* Scope
* Responsibilities
* Domain Boundaries
* Primary Users
* Stakeholders
* Business Value
* Dependencies
* Assumptions
* Constraints
* Future Vision

---

# 2. Business Capabilities

Document:

Core Capabilities

Supporting Capabilities

Administrative Capabilities

Operational Capabilities

Reporting Capabilities

Analytics Capabilities

Configuration Capabilities

Future Capabilities

For every capability define:

* Purpose
* Inputs
* Outputs
* Consumers
* Dependencies

---

# 3. Resource Catalog

List every business resource owned by the module.

For each resource describe:

* Purpose
* Business Owner
* System of Record
* Lifecycle
* Relationships
* Dependencies
* Security Classification
* Retention Policy

---

# 4. Business Rules

Document:

Validation Rules

Processing Rules

Calculation Rules

Approval Rules

Lifecycle Rules

State Rules

Security Rules

Visibility Rules

Data Ownership Rules

Retention Rules

Compliance Rules

Future Rules

---

# 5. Business Workflows

Document every workflow.

For every workflow define:

* Purpose
* Trigger
* Preconditions
* Actors
* Steps
* Decision Points
* Exceptions
* Completion Criteria
* Notifications
* Background Jobs
* Audit Requirements
* Published Events
* Consumed Events

---

# 6. User Experience

Describe:

Primary Screens

Navigation

Workspace

Forms

Tables

Reports

Dashboards

Approval Screens

Search Experience

Filters

Bulk Operations

Accessibility

Mobile Experience

Future Enhancements

---

# 7. Security

Document:

Authentication

Authorization

Permissions

RBAC

Data Visibility

Sensitive Data

Approval Controls

Audit Logging

Compliance

Privacy

Future Security

---

# 8. Reporting & Analytics

Define:

Operational Reports

Management Reports

Executive Reports

Dashboards

KPIs

Analytics

Historical Reports

Scheduled Reports

Exports

Future Analytics

---

# 9. Notifications

Document:

Email

SMS

Push Notifications

In-app Notifications

Approval Notifications

Reminders

Escalations

Failures

Success Messages

Background Notifications

---

# 10. Integrations

Document integrations with:

Master Administration

Student

Academic

Attendance

Examination

Fees

Timetable

Homework

LMS

Communication

Parent Portal

Transport

Hostel

Library

Inventory

HRMS

Discipline

Events

Alumni

Reporting

Analytics

Audit

Background Jobs

Import/Export

Search

Future Systems

For every integration define:

* Purpose
* Direction
* Resources
* Business Events
* Criticality

---

# 11. Domain Events

Generate:

Published Events

Consumed Events

For every event define:

* Business Purpose
* Producer
* Consumers
* Trigger
* Ordering
* Retry
* Idempotency
* Notifications
* Background Jobs
* Audit Impact

---

# 12. Error & Exception Catalog

Categorize:

Validation Errors

Business Errors

Authorization Errors

Workflow Errors

Data Errors

Configuration Errors

External Integration Errors

Concurrency Errors

Recovery Strategy

Audit Impact

---

# 13. AI Coding Agent Guidance

Provide implementation guidance covering:

* Recommended module architecture
* Layer responsibilities
* Controllers
* Services
* Repositories
* Validation
* Events
* Background Jobs
* Transactions
* Concurrency
* Testing Strategy
* Documentation Strategy
* Future Extensions

---

# 14. Architecture Decision Summary

Generate a summary table.

Columns:

| Area | Decision | Reason | Business Benefit | Technical Benefit | Future Extension |

---

# Writing Style

Maintain the tone of a professional Enterprise Module Specification.

Focus on:

* Business architecture
* Domain design
* Workflow ownership
* Security
* Integrations
* Scalability
* Maintainability
* Extensibility

Avoid implementation details and technology-specific guidance.

This template should be reusable for every present and future module within the Enterprise School Management System and should enable consistent, architecture-first module documentation across the entire platform.
