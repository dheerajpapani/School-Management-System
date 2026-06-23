# 03_RBAC.md

## Objective

You are acting as a Principal Enterprise Security Architect responsible for defining the complete Role-Based Access Control (RBAC) Architecture for an Enterprise School Management System (SMS).

This document is the authoritative specification governing all roles, permissions, permission groups, resource access, scope restrictions, delegated authority, policy mapping, and future authorization extensibility throughout the School Management System.

The objective is to establish a centralized, scalable, auditable, configurable, and reusable RBAC framework that enforces consistent access control across every module.

This document defines RBAC architecture only.

It does NOT define:

- Authentication
- Authorization implementation
- SQL schema
- PHP implementation
- APIs
- UI implementation

Assume all previously generated documentation already exists.

Do not duplicate previous documents.

For every RBAC definition specify:

- Owner
- Consumers
- Allowed Dependencies
- Forbidden Dependencies
- Lifecycle
- Security Requirements
- Related Contracts

---

# Scope

Define RBAC for every module and every user category.

Include:

Platform

Administration

Student

Parent

Teacher

Class Teacher

Department Head

Vice Principal

Principal

Finance

HR

Library

Transport

Hostel

Inventory

Events

Discipline

Alumni

Generate every required role.

---

# Document Structure

## 1. Purpose

Explain:

Why RBAC exists.

Difference between:

Role

Permission

Permission Group

Policy

Scope

Capability

Privilege

Ownership

Delegation

Explain why RBAC must remain configurable.

---

## 2. RBAC Principles

Describe principles including:

Least Privilege

Role Separation

Permission Reuse

Permission Grouping

Scope Isolation

Inheritance Readiness

Delegation

Auditability

Configuration Driven

Future Extensibility

Explain each principle.

---

## 3. RBAC Model

Describe conceptual RBAC architecture.

Define:

Roles

Permission Groups

Permissions

Scopes

Resource Types

Operations

Hierarchical Roles

Future Dynamic Roles

Explain evaluation order.

---

## 4. Role Catalog

Generate complete enterprise role catalog.

Examples:

Super Administrator

System Administrator

Institution Administrator

Principal

Vice Principal

Department Head

Academic Coordinator

Teacher

Class Teacher

Exam Coordinator

Finance Manager

Accountant

Librarian

Transport Manager

Hostel Warden

HR Manager

Inventory Manager

Event Coordinator

Discipline Officer

Student

Parent

Guardian

Alumni

Guest

API Client (future)

Service Account (future)

Generate every additional role required.

---

## 5. Permission Group Catalog

Generate permission groups.

Examples:

Institution Management

Academic Management

Student Management

Attendance

Examinations

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

Reports

Administration

Configuration

Audit

Notification

Import/Export

System Management

Generate every additional group.

---

## 6. Permission Catalog

Define conceptual permissions.

Use CRUD plus business actions.

Examples:

Create

Read

Update

Delete

Approve

Reject

Publish

Archive

Restore

Assign

Transfer

Promote

Generate

Export

Import

Verify

Lock

Unlock

Override

View Sensitive Data

Generate every additional business permission required.

---

## 7. Scope Model

Describe scope restrictions.

Examples:

Institution

Branch

Academic Year

Department

Class

Section

Subject

Assigned Students

Assigned Employees

Owned Records

Generated Records

Self Only

Future Context Scopes

Explain evaluation order.

---

## 8. Delegation Model

Describe:

Temporary Delegation

Permanent Delegation

Emergency Delegation

Approval Delegation

Administrative Override

Delegation Expiration

Audit

---

## 9. Cross-Module Permission Matrix

Generate a conceptual matrix covering all modules.

For each module define:

Roles

Permission Groups

Typical Permissions

Scope Restrictions

Sensitive Operations

Approval Requirements

Audit Requirements

Future Extensions

---

## 10. Sensitive Permissions

Define permissions for:

Financial Data

Medical Records

Examination Results

Payroll

Audit Logs

System Configuration

User Management

Role Management

Permission Management

Security Settings

Government Reports

Data Export

Bulk Operations

Administrative Override

Break-glass Access

---

## 11. Monitoring & Auditing

Describe monitoring for:

Permission Changes

Role Assignment

Role Removal

Privilege Escalation

Delegation

Unauthorized Attempts

Sensitive Permission Usage

Operational KPIs

Compliance

---

## 12. Future Extensibility

Support future:

Attribute-Based Access Control (ABAC)

Policy-Based Access Control (PBAC)

Dynamic Roles

Context-aware Permissions

Time-based Access

Location-based Access

Risk-based Access

AI-assisted Authorization

Government Compliance

External Identity Providers

---

## 13. RBAC Matrix

Create a matrix.

Columns:

Role

Permission Groups

Scope

Sensitive Permissions

Delegation

Audit

Future Extension

---

## 14. Architecture Decision Summary

Create a summary table.

Columns:

Area

Decision

Reason

Security Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise RBAC Architecture Specification.

Do not include:

- SQL
- PHP
- Permission IDs
- Role IDs
- API implementation
- UI implementation

Focus entirely on RBAC governance, role hierarchy, permission organization, scope evaluation, delegation, monitoring, auditing, and extensibility.

This document should enable AI coding agents to implement a centralized, configurable, enterprise-grade RBAC system across the entire School Management System.
