# 02_Authorization.md

## Objective

You are acting as a Principal Enterprise Security Architect responsible for defining the complete Authorization Architecture for an Enterprise School Management System (SMS).

This document is the authoritative specification governing how access decisions are made throughout the School Management System.

The objective is to establish a centralized, policy-driven, secure, auditable, extensible, and consistent authorization framework that determines whether an authenticated identity is allowed to perform a requested business action.

This document defines authorization architecture only.

It does NOT define:

- Authentication
- RBAC implementation
- SQL schema
- PHP implementation
- APIs
- UI implementation

Assume all previously generated documentation already exists.

Do not duplicate previous documents.

For every authorization policy define:

- Policy Owner
- Consumers
- Allowed Dependencies
- Forbidden Dependencies
- Evaluation Lifecycle
- Security Requirements
- Related Contracts

---

# Scope

Define authorization architecture for every module.

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

Generate every authorization policy required.

---

# Document Structure

## 1. Purpose

Explain:

Why authorization exists.

Difference between:

Authentication

Authorization

Permission

Privilege

Capability

Policy

Ownership

Delegation

Explain why authorization decisions should be centralized.

---

## 2. Authorization Principles

Describe principles including:

Default Deny

Least Privilege

Need to Know

Policy-based Evaluation

Ownership Validation

Context Awareness

Department Isolation

Branch Isolation

Academic Year Isolation

Resource Ownership

Auditability

Extensibility

Explain each principle.

---

## 3. Authorization Model

Describe conceptual authorization layers.

Examples:

Platform Level

Institution Level

Branch Level

Department Level

Academic Year Level

Class Level

Section Level

Resource Level

Operation Level

Field Level

Future Context-aware Authorization

Explain evaluation order.

---

## 4. Authorization Lifecycle

Describe:

Request

Policy Evaluation

Permission Evaluation

Context Evaluation

Decision

Audit

Response

Override

Revocation

Re-evaluation

---

## 5. Module-wise Authorization Policies

Generate policies for every module.

### Administration

Institution Management

Academic Year Management

Configuration

Role Administration

Permission Administration

Branch Management

---

### Student

Admission

Profile Update

Promotion

Transfer

Graduation

Medical Records

Student Documents

Guardian Records

---

### Academic

Curriculum

Subject Assignment

Teacher Assignment

Lesson Planning

Learning Outcomes

---

### Attendance

Attendance Entry

Attendance Correction

Attendance Lock

Attendance Reports

---

### Examination

Exam Setup

Marks Entry

Marks Approval

Result Publication

Report Card

---

### Fees

Invoice Creation

Payment Collection

Refund

Scholarship

Financial Reports

Fee Waiver

---

### Timetable

Creation

Publication

Substitution

Conflict Resolution

---

### Homework

Creation

Submission

Evaluation

Publication

---

### LMS

Course Management

Quiz Management

Progress Tracking

Certificates

---

### Communication

Messages

Circulars

Announcements

Broadcasts

---

### Parent Portal

Requests

Certificates

Leave

Transport Requests

---

### Transport

Vehicle Management

Route Management

Assignments

GPS Monitoring

---

### Hostel

Room Allocation

Billing

Attendance

Leave

---

### Library

Book Issue

Return

Reservation

Fine

Inventory

---

### Inventory

Purchase

Assets

Maintenance

Stock

Vendor

---

### HRMS

Employee

Attendance

Leave

Payroll

Promotion

Termination

---

### Events

Planning

Registration

Participation

Certificates

Budget

---

### Discipline

Incidents

Warnings

Suspensions

Appeals

---

### Alumni

Membership

Donations

Mentorship

Generate every additional policy required.

---

## 6. Resource Ownership

Describe authorization based on:

Creator

Department

Branch

Class Teacher

Subject Teacher

Principal

Finance

HR

Librarian

Hostel Warden

Transport Manager

Future Ownership Models

---

## 7. Delegated Authorization

Describe:

Temporary Delegation

Permanent Delegation

Emergency Delegation

Approval Delegation

Administrative Override

Delegation Expiry

Audit

---

## 8. Security Considerations

Describe:

Privilege Escalation

Horizontal Access

Vertical Access

Sensitive Records

Medical Data

Financial Data

Configuration

Emergency Override

Break-glass Access

---

## 9. Monitoring & Auditing

Define monitoring for:

Denied Requests

Override Usage

Privilege Escalation Attempts

Delegation Usage

Unauthorized Access Attempts

Sensitive Resource Access

Policy Violations

Operational KPIs

---

## 10. Future Extensibility

Support future:

ABAC

PBAC

Context-aware Policies

Location-based Authorization

Time-based Authorization

Risk-based Authorization

AI Authorization

Government Policies

External Identity Providers

---

## 11. Authorization Matrix

Create a matrix.

Columns:

Resource

Operation

Required Policy

Context

Audit

Future Extension

---

## 12. Architecture Decision Summary

Create a summary table.

Columns:

Area

Decision

Reason

Security Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Authorization Architecture Specification.

Do not include:

- SQL
- PHP
- API implementation
- UI implementation

Focus entirely on authorization policies, decision flow, resource ownership, policy evaluation, governance, monitoring, and extensibility.

This document should enable AI coding agents to implement a centralized authorization framework across the entire School Management System.
