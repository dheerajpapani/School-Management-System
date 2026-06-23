# 00_API_Design_Guidelines.md

## Objective

You are acting as a Principal Enterprise API Architect responsible for defining the API Design Guidelines for an Enterprise School Management System (SMS).

This document is the master reference that governs every API specification contained within the API Catalog.

The objective is to ensure that every module-specific API document follows identical conventions, organization, terminology, endpoint structure, documentation format, security expectations, lifecycle definitions, and extensibility model.

This document serves as the template and governance standard for all API catalog documents.

It does NOT define module-specific endpoints.

Assume all previous API documentation already exists.

---

# Document Structure

## 1. Purpose

Explain why API catalog documents must remain consistent.

---

## 2. API Documentation Standard

Define the standard layout every module API document must follow.

Every API must include:

Purpose

Business Context

Consumers

Permissions

Dependencies

Preconditions

Postconditions

Side Effects

Validation

Business Rules

Error Conditions

Notifications

Events

Audit Requirements

Performance Notes

Security Notes

Future Extensions

---

## 3. Resource Documentation Standard

Define how resources are documented.

Each resource should describe:

Business Owner

Relationships

Lifecycle

Operations

Searchability

Filtering

Reporting

Import

Export

Audit

---

## 4. Endpoint Documentation Standard

Every endpoint should document:

Business Purpose

HTTP Method

Logical Resource

Authentication

Authorization

Validation Rules

Business Rules

Workflow Impact

Related Modules

Events Published

Notifications

Background Jobs

Reports Impacted

Audit Requirements

Performance Expectations

Future Extension

---

## 5. Naming Standards

Define standards for:

Resources

Actions

Collections

Nested Resources

Reports

Imports

Exports

Workflow Operations

Approval Operations

Analytics

---

## 6. Cross-module References

Explain how APIs reference other modules.

---

## 7. Documentation Quality Rules

Every module API document must:

Remain independent.

Avoid duplication.

Reference shared standards.

Use identical formatting.

Remain implementation-independent.

---

## 8. AI Generation Rules

Provide instructions for AI coding agents.

Examples:

Never invent business rules.

Follow existing documentation.

Reference contracts.

Reuse validation.

Reuse services.

Reuse events.

Reuse permissions.

Reuse workflows.

Never duplicate endpoints.

---

## 9. API Documentation Checklist

Generate a review checklist.

---

## 10. Architecture Decision Summary

Summarize all design decisions.

---

# Writing Style

Professional Enterprise API Documentation Standard.

Do not define actual endpoints.

Focus entirely on governance, consistency, documentation quality, maintainability, and AI-assisted development.
