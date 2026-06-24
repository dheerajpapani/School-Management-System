# 16_HRMS_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Human Resource Management System (HRMS) domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to employee lifecycle management, recruitment readiness, onboarding, employment records, organizational hierarchy, attendance integration, leave management, payroll readiness, shift scheduling, performance management, professional development, document management, separation, compliance, reporting, governance, and institutional workforce administration.

The HRMS domain manages the complete lifecycle of teaching and non-teaching employees including administrators, teachers, support staff, librarians, transport staff, hostel staff, laboratory staff, security personnel, finance staff, maintenance staff, and future institutional workforce categories.

The HRMS domain integrates with Master Administration, Attendance, Academic, Timetable, Examination, Transport, Hostel, Library, Inventory, Communication, Events, Reporting, Analytics, Audit, Notification Center, Payroll readiness, Identity Management, and future ERP modules.

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
- Payroll engine implementation
- Biometric implementation
- ERP implementation

Assume all previously generated architecture, contracts, validation rules, workflows, security documentation, API standards, Attendance APIs, Communication APIs, Timetable APIs, Inventory APIs, and Reporting APIs already exist.

Reference previous documentation instead of duplicating it.

---

# Enterprise HRMS Principles

Employees follow a complete institutional lifecycle.

Employment records remain historically immutable.

Organizational hierarchy remains versioned.

Attendance integrates through authoritative attendance services.

Payroll remains an external financial concern.

Every HR action remains auditable.

Organizational changes preserve historical reporting relationships.

Professional history remains permanently traceable.

---

# Scope

Generate the complete API specification for:

## Organization Management

Institution Structure

Departments

Designations

Job Grades

Reporting Hierarchy

Employment Categories

Employment Types

Cost Centers

Work Locations

Organization History

---

## Employee Lifecycle

Recruitment Readiness

Candidate Conversion

Employee Registration

Onboarding

Probation

Confirmation

Transfer

Promotion

Demotion

Role Change

Contract Renewal

Resignation

Retirement

Termination

Exit Management

Alumni Staff Readiness

---

## Employee Profile

Personal Information

Employment Information

Qualifications

Certifications

Experience

Skills

Emergency Contacts

Identity Documents

Bank Details Readiness

Professional Licenses

Employee Documents

Document Expiry

Profile History

---

## Attendance & Leave

Attendance Integration

Shift Assignment

Roster Management

Leave Request

Leave Approval

Leave Balance

Holiday Calendar

Compensatory Leave

Overtime Readiness

Attendance Exceptions

Attendance Corrections

Leave History

---

## Performance Management

Goal Setting

Performance Reviews

Appraisals

Competency Evaluation

Training Recommendations

Professional Development

Career Progression

Recognition

Awards

Performance History

---

## Workforce Operations

Duty Assignment

Timetable Assignment

Class Allocation

Subject Allocation

Committee Assignment

Event Assignment

Hostel Assignment

Transport Assignment

Library Assignment

Inventory Responsibility

Asset Assignment

---

## Compliance

Document Compliance

Certification Tracking

Background Verification Readiness

Medical Readiness

Contract Compliance

Policy Acceptance

Mandatory Training

Audit Compliance

---

## Governance

Approval

Administrative Override

Audit

Compliance

Retention

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

Employee Lookup

Department Lookup

Hierarchy Lookup

Attendance Summary

Leave Summary

Performance Summary

Dashboard

Statistics

Analytics

Generate every retrieval API.

---

### Creation

Register Employee

Create Department

Assign Position

Create Shift

Submit Leave

Register Qualification

Register Certification

Bulk Import

Generate every creation API.

---

### Modification

Update Employee

Transfer Employee

Promote Employee

Approve Leave

Assign Manager

Assign Department

Update Shift

Suspend Employee

Reactivate Employee

Lock

Unlock

Validate

Generate every modification API.

---

### Workflow Operations

Onboard Employee

Confirm Employment

Assign Timetable

Assign Assets

Assign Duties

Process Leave

Synchronize Attendance

Generate Notifications

Generate Reports

Generate Analytics

Manage Separation

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Bulk Employee Update

Bulk Transfers

Bulk Promotions

Compliance Review

Audit Review

Rollback

Generate every administrative API.

---

### Reporting & Analytics

Employee Reports

Department Reports

Attendance Reports

Leave Reports

Performance Reports

Training Reports

Organizational Dashboards

Executive Dashboards

HR Analytics

Workforce Analytics

Generate every reporting API.

---

## 4. API Specification Template

Document every API using the standardized enterprise template.

---

## 5. Cross-module Integration

Explain integrations with:

Master Administration

Attendance

Academic

Timetable

Examination

Transport

Hostel

Library

Inventory

Communication

Events

Reporting

Analytics

Audit

Notification Center

Payroll Readiness

Identity Management

Background Processing

Search

Import/Export

Generate every integration dependency.

---

## 6. Security Considerations

Cover:

Employee Authorization

Personnel Privacy

Role Integrity

Hierarchy Controls

Administrative Override

Document Security

Audit Requirements

Future Identity Federation

---

## 7. Performance Considerations

Discuss:

Large Employee Directories

Hierarchy Resolution

Attendance Synchronization

Bulk Imports

Performance Analytics

Caching

Scalability

Future Multi-campus Workforce

---

## 8. Monitoring

Define:

Employee Lifecycle

Attendance Synchronization

Leave Processing

Performance Reviews

Compliance Status

Operational KPIs

HR KPIs

Workforce KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

Payroll Integration

Biometric Attendance

Identity Federation

SSO

AI Workforce Planning

Competency Intelligence

Learning Recommendations

Digital Employee Files

Succession Planning

ERP Integration

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including:

EmployeeRegistered

EmployeeOnboarded

EmployeeConfirmed

EmployeeTransferred

EmployeePromoted

EmployeeSuspended

LeaveRequested

LeaveApproved

ShiftAssigned

PerformanceReviewed

TrainingAssigned

EmployeeSeparated

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

- Employee lifecycle services

- Organizational hierarchy services

- Leave management services

- Performance services

- Assignment services

- Repository ownership

- Event publication

- Background jobs

- Validation sequencing

- Notification orchestration

- Transaction handling

- Concurrency handling

---

## 13. Error & Exception Catalog

Define business exceptions including:

EmployeeAlreadyExists

DuplicateEmployeeCode

InvalidReportingHierarchy

DepartmentInactive

LeaveBalanceExceeded

EmployeeSuspended

QualificationExpired

CertificationExpired

PromotionConflict

TransferConflict

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Human Resource Management API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- Payroll implementation
- Biometric implementation

Focus entirely on employee lifecycle management, organizational administration, workforce governance, reporting, monitoring, auditability, event-driven architecture, scalability, compliance, and extensibility.

This document should enable an AI coding agent to generate the complete HRMS subsystem—including controllers, services, repositories, employee lifecycle managers, hierarchy services, leave managers, performance services, events, notifications, reports, background jobs, tests, and documentation—without making any business assumptions.
