# 04_Event_Driven_Architecture.md

## Objective

You are acting as a Principal Enterprise Solution Architect responsible for defining the Event-Driven Architecture (EDA) for an Enterprise School Management System (SMS).

This document is the authoritative specification for how business events are generated, published, consumed, persisted, monitored, retried, audited, and extended across the entire platform.

This is **NOT** an API document.

This is **NOT** a module specification.

This is **NOT** a database specification.

This document defines the event model used internally by the application.

Assume the following documents already exist and must not be duplicated:

* Module Structure
* Blueprint
* Functional Requirements
* Non-Functional Requirements
* Business Rules
* System Architecture
* Domain Model
* Module Interaction Matrix
* End-to-End Business Workflows
* Service Contracts
* Validation Contracts
* All completed Module Specifications

Reference them where appropriate without repeating their contents.

---

# Scope

Define the complete Event-Driven Architecture for the School Management System.

Describe how business events coordinate workflows across modules while maintaining loose coupling.

Avoid implementation details.

---

# Document Structure

## 1. Purpose

Explain:

* Why Event-Driven Architecture is used.
* Difference between synchronous service calls and domain events.
* When events should and should not be used.
* Benefits for scalability, maintainability and extensibility.

---

## 2. Event Architecture Principles

Define principles including:

* Business Events
* Domain Events
* Application Events
* Integration Events
* Immutable Events
* Event Naming Standards
* Event Versioning
* Event Ordering
* Event Idempotency
* Event Replay
* Event Correlation
* Event Traceability

Explain each principle.

---

## 3. Event Lifecycle

Describe the complete lifecycle:

Business Action

↓

Event Creation

↓

Validation

↓

Publication

↓

Event Queue (conceptually)

↓

Consumers

↓

Processing

↓

Completion

↓

Audit

↓

Archival

Include:

* Retry flow
* Failure flow
* Dead event handling
* Duplicate handling

---

## 4. Event Definition Standard

Every event must include:

* Event Name
* Event ID
* Category
* Source Module
* Owning Service
* Trigger
* Business Meaning
* Producer
* Consumers
* Preconditions
* Postconditions
* Expected Processing
* Retry Strategy
* Failure Strategy
* Audit Requirements
* Security Classification
* Future Compatibility

---

## 5. Domain Event Catalog

Generate a comprehensive catalog of business events.

Examples include (but are not limited to):

### Administration

InstitutionCreated

AcademicYearActivated

AcademicYearClosed

BranchCreated

DepartmentCreated

RoleAssigned

PermissionChanged

---

### Student

AdmissionSubmitted

AdmissionApproved

AdmissionRejected

StudentCreated

StudentActivated

StudentTransferred

StudentPromoted

StudentGraduated

StudentWithdrawn

StudentArchived

GuardianLinked

DocumentVerified

---

### Academic

CurriculumPublished

SubjectAssigned

TeacherAssigned

LessonPlanApproved

LessonCompleted

---

### Attendance

AttendanceSessionOpened

AttendanceSubmitted

AttendanceLocked

AttendanceCorrected

AttendanceFinalized

AttendanceShortageDetected

---

### Examination

ExamCreated

ExamScheduled

HallTicketGenerated

MarksSubmitted

MarksVerified

ResultCalculated

ResultPublished

ReportCardGenerated

PromotionRecommended

---

### Fee

InvoiceGenerated

PaymentReceived

PaymentFailed

ScholarshipApproved

RefundProcessed

FinancialYearClosed

---

### Timetable

TimetablePublished

TeacherSubstituted

ConflictDetected

---

### Homework

HomeworkAssigned

AssignmentSubmitted

AssignmentEvaluated

---

### LMS

CourseCompleted

QuizCompleted

CertificateIssued

---

### Communication

NotificationSent

EmailDelivered

SMSDelivered

PushDelivered

---

### Transport

RouteAssigned

VehicleMaintenanceDue

GPSAlertGenerated

---

### Hostel

RoomAllocated

RoomVacated

HostelFeeGenerated

---

### Library

BookIssued

BookReturned

FineCalculated

ReservationCreated

---

### Inventory

PurchaseApproved

AssetAssigned

MaintenanceCompleted

---

### HRMS

EmployeeJoined

LeaveApproved

EmployeeExited

---

### Events

EventPublished

CertificateGenerated

---

### Discipline

IncidentReported

WarningIssued

SuspensionApproved

---

### Alumni

AlumniRegistered

DonationReceived

MentorshipAssigned

Generate every additional event necessary for a complete enterprise system.

---

## 6. Producer–Consumer Matrix

Create a matrix showing:

Event

Producer

Primary Consumers

Secondary Consumers

Business Criticality

Retry Required

Audit Required

---

## 7. Event Categories

Classify events:

* Academic
* Financial
* Administrative
* Security
* Communication
* Operational
* Analytics
* Audit
* Integration
* Notification
* Background Processing

Explain the purpose of each.

---

## 8. Event Processing Rules

Describe:

* Immediate Events
* Deferred Events
* Scheduled Events
* Batch Events
* Chained Events
* Conditional Events
* Manual Replay
* Event Ordering
* Duplicate Detection
* Idempotent Processing

---

## 9. Failure Handling

Define:

* Retry policies
* Poison event handling
* Dead-letter strategy (conceptually)
* Partial failures
* Compensation workflows
* Recovery procedures
* Monitoring expectations

---

## 10. Security Considerations

Describe:

* Event authorization
* Sensitive payload handling
* Data minimization
* Encryption readiness
* Audit logging
* Access control
* Privacy considerations

---

## 11. Monitoring & Observability

Describe:

* Event metrics
* Processing latency
* Failure monitoring
* Retry monitoring
* Consumer health
* Event tracing
* Correlation IDs
* Operational dashboards

---

## 12. Future Extensibility

Explain readiness for:

* Message brokers
* Distributed services
* Microservices
* External integrations
* Third-party subscribers
* Event streaming
* Real-time analytics

---

## 13. Architecture Decision Summary

Create a summary table with:

* Decision
* Reason
* Impact
* Future Consideration

---

# Writing Style

Maintain the tone of a professional Enterprise Architecture Specification.

Do not include:

* SQL
* PHP
* API endpoints
* Queue implementation
* UI
* Database schema

Focus entirely on event architecture, business events, orchestration, reliability, extensibility, and governance.

This document should enable AI coding agents to implement a consistent event-driven backend while preserving the architectural decisions defined in all previous documentation.
