# 01_Service_Contracts.md

## Objective

You are acting as a Principal Software Architect responsible for defining the complete Service Layer Contract for an Enterprise School Management System (SMS).

This document defines every application service that will exist in the backend.

It is the authoritative specification describing:

- Service responsibilities
- Ownership
- Public operations
- Dependencies
- Consumed services
- Published events
- Transaction ownership
- Validation ownership
- Error handling
- Concurrency expectations
- Idempotency
- Security expectations

It is **NOT** an API specification.

It is **NOT** PHP code.

It is **NOT** a database specification.

Instead, it defines the backend service architecture that every future PHP class must follow.

Assume all previous documentation already exists.

Do not duplicate previous documents.

---

# Scope

Define every backend service required across all modules.

Every business capability should belong to exactly one service.

Avoid "God Services."

Avoid duplicated responsibilities.

---

# Service Definition Format

Every service must contain:

---

Service Name

---

Business Purpose

---

Owning Module

---

Responsibilities

---

Public Operations

Describe conceptual operations only.

Examples:

Create Student

Approve Admission

Assign Section

Generate Invoice

Collect Payment

Generate Result

Publish Attendance

Issue Book

Allocate Hostel

etc.

Do not define code.

---

Consumes

Which services it depends upon.

---

Produces

What records or events it creates.

---

Transaction Ownership

Describe transaction boundary.

---

Validation Ownership

Business validations owned.

---

Security Responsibilities

---

Audit Responsibilities

---

Published Events

---

Consumed Events

---

Failure Handling

---

Retry Expectations

---

Concurrency Expectations

---

Caching Opportunities

---

Future Extensibility

---

# Generate Complete Service Catalog

Generate services including but not limited to:

InstitutionService

AcademicYearService

BranchService

DepartmentService

RoleService

PermissionService

AuthenticationService

AuthorizationService

StudentService

AdmissionService

GuardianService

MedicalProfileService

StudentLifecycleService

DocumentService

AttendanceService

AttendanceAnalyticsService

CurriculumService

SubjectService

LessonPlanService

TeacherAssignmentService

ExaminationService

AssessmentService

MarksService

ResultService

ReportCardService

FeeStructureService

InvoiceService

PaymentService

ScholarshipService

RefundService

LedgerService

TimetableService

SchedulingService

ConflictDetectionService

HomeworkService

AssignmentService

LMSService

CourseService

QuizService

NotificationService

EmailService

SMSService

PushNotificationService

TransportService

VehicleService

GPSService

HostelService

RoomAllocationService

LibraryService

BookIssueService

InventoryService

PurchaseService

AssetService

EmployeeService

LeaveService

PayrollReadyService

EventService

CertificateService

DisciplineService

BehaviorAnalyticsService

AlumniService

AuditService

ConfigurationService

SearchService

FileStorageService

ImportService

ExportService

ReportService

BackgroundJobService

IntegrationService

WebhookService

HealthMonitoringService

CacheService

LoggingService

SystemSettingsService

Generate every additional service required.

---

# Cross-Service Matrix

Generate a matrix.

Columns:

Service

Depends On

Used By

Transaction Owner

Criticality

Scalability

---

# Event Publication Matrix

Generate:

Service

Publishes

Consumes

Priority

Delivery Strategy

Retry

---

# Transaction Ownership Matrix

Generate:

Transaction

Owning Service

Supporting Services

Rollback Owner

Compensation Strategy

---

# Writing Style

Maintain the tone of an Enterprise Software Architecture Specification.

Avoid:

SQL

PHP

APIs

Database

UI

Focus entirely on backend service boundaries.

This document must ensure every future PHP service class has a single, well-defined responsibility with minimal coupling and maximum cohesion.

It should eliminate ambiguity for AI coding agents regarding where business logic belongs.
