# 01_Parent_Dashboard_API.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for designing the complete API Catalog for the Parent Dashboard domain of an Enterprise School Management System (SMS).

This document is the authoritative specification governing every business API related to the Parent Dashboard, student summaries, academic overview, attendance overview, fee overview, examination overview, homework overview, LMS overview, announcements, notifications, actionable insights, dashboard personalization, and parent-specific institutional visibility.

The Parent Dashboard domain provides parents with a consolidated, role-based view of information originating from multiple institutional systems.

The Parent Dashboard is NOT a system of record.

It consumes authoritative data from Student, Academic, Attendance, Examination, Fees, Timetable, Homework, LMS, Communication, Events, Transport, Hostel, Library, HRMS (limited), and future institutional modules.

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
- Dashboard UI implementation

Assume all previously generated architecture, contracts, validation rules, workflows, security documentation, API standards, Student APIs, Attendance APIs, Examination APIs, Fees APIs, LMS APIs, Homework APIs, Communication APIs, and Reporting APIs already exist.

Reference previous documentation instead of duplicating it.

---

# Parent Portal Principles

The Parent Dashboard is a read-optimized aggregation layer.

Parents never modify institutional records directly unless explicitly permitted by business rules.

Every dashboard widget consumes authoritative data from its owning module.

Dashboard data may be cached.

Every dashboard interaction remains auditable.

Dashboard personalization never changes institutional data.

---

# Scope

Generate the complete API specification for:

## Dashboard Overview

Dashboard Summary

Student Summary

Academic Summary

Attendance Summary

Fee Summary

Homework Summary

Examination Summary

LMS Summary

Announcement Summary

Notification Summary

Upcoming Events

Calendar Overview

Quick Actions

Widgets

Personalized Dashboard

---

## Student Overview

Multiple Children

Student Switching

Academic Profile

Current Class

Current Section

Roll Number

Academic Status

Admission Status

Profile Snapshot

---

## Academic Snapshot

Current Subjects

Current Teachers

Current Timetable

Current Academic Session

Current Performance

Learning Progress

Competencies

Achievements

---

## Institutional Alerts

Attendance Alerts

Fee Alerts

Homework Alerts

Examination Alerts

Transport Alerts

Emergency Alerts

Administrative Alerts

Academic Alerts

---

## Dashboard Personalization

Widget Preferences

Layout Preferences

Notification Preferences

Pinned Widgets

Quick Links

Language Preferences

Accessibility Preferences

---

## Governance

Privacy

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

Get Dashboard

Get Student Summary

Get Attendance Summary

Get Fee Summary

Get Homework Summary

Get LMS Summary

Get Examination Summary

Get Notification Summary

Search Dashboard

Analytics

Statistics

Timeline

Generate every retrieval API.

---

### Creation

Create Dashboard Preference

Create Widget Configuration

Create Quick Link

Initialize Dashboard

Generate every creation API.

---

### Modification

Update Preferences

Pin Widget

Unpin Widget

Reorder Widgets

Reset Layout

Update Language

Update Accessibility

Validate Configuration

Generate every modification API.

---

### Workflow Operations

Load Dashboard

Refresh Dashboard

Aggregate Student Data

Aggregate Academic Data

Aggregate Fee Data

Aggregate Attendance Data

Aggregate LMS Data

Generate Alerts

Synchronize Parent Portal

Generate Reports

Generate every workflow API.

---

### Administrative Operations

Administrative Override

Reset Dashboard

Bulk Preference Update

Compliance Review

Audit Review

Generate every administrative API.

---

### Reporting & Analytics

Dashboard Usage Reports

Widget Usage Reports

Parent Engagement Reports

Portal Analytics

Operational Dashboards

Executive Dashboards

Generate every reporting API.

---

## 4. API Specification Template

Document every API using the standardized enterprise template.

---

## 5. Cross-module Integration

Explain integrations with:

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

Transport

Hostel

Library

Events

Reporting

Analytics

Audit

Notification

Background Processing

Search

Import/Export

Generate every integration dependency.

---

## 6. Security Considerations

Cover:

Parent Authorization

Student Visibility Rules

Data Aggregation Security

Dashboard Privacy

Administrative Override

Audit Requirements

Multi-child Access

Future Guardian Delegation

---

## 7. Performance Considerations

Discuss:

Dashboard Aggregation

Caching

Widget Loading

Large Families

Analytics

Scalability

Future Real-time Dashboards

---

## 8. Monitoring

Define:

Dashboard Loads

Widget Performance

Cache Performance

Portal Usage

Operational KPIs

Parent Engagement KPIs

Security KPIs

Audit KPIs

---

## 9. Future Extensibility

Support:

AI Parent Assistant

Predictive Academic Alerts

Smart Dashboard

Personalized Recommendations

Digital Consent

Guardian Collaboration

Cross-campus Families

Voice Assistant Integration

Mobile Widgets

Family Analytics

---

## 10. API Dependency Matrix

Generate the standardized dependency matrix.

---

## 11. Domain Event Catalog

Generate events including:

ParentDashboardLoaded

DashboardRefreshed

WidgetConfigured

DashboardPreferenceUpdated

StudentSwitched

AcademicSummaryGenerated

AttendanceSummaryGenerated

FeeSummaryGenerated

HomeworkSummaryGenerated

DashboardAlertGenerated

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

- Dashboard aggregation services

- Widget services

- Preference services

- Read-model orchestration

- Repository ownership

- Event publication

- Background jobs

- Validation sequencing

- Transaction handling

- Concurrency handling

---

## 13. Error & Exception Catalog

Define business exceptions including:

DashboardUnavailable

StudentAccessDenied

WidgetConfigurationInvalid

DashboardPreferenceConflict

DataAggregationFailed

DashboardRefreshFailed

ParentNotLinked

PermissionValidationFailed

CacheUnavailable

Generate every major business exception.

---

## 14. Architecture Decision Summary

Generate the standard architecture summary table.

---

# Writing Style

Maintain the tone of a professional Enterprise Parent Dashboard API Catalog Specification.

Do not include:

- PHP
- SQL
- JSON
- OpenAPI
- Endpoint URLs
- Infrastructure
- UI implementation

Focus entirely on dashboard aggregation, read-model orchestration, personalization, governance, reporting, monitoring, auditability, event-driven architecture, scalability, compliance, and extensibility.

This document should enable an AI coding agent to generate the complete Parent Dashboard subsystem—including controllers, aggregation services, repositories, widget managers, preference services, events, reports, background jobs, tests, and documentation—without making any business assumptions.
