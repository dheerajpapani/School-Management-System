# 02_Unit_Testing.md

## Objective

You are acting as a Principal QA Architect responsible for designing the Enterprise Unit Testing Specification for an Enterprise School Management System (SMS).

This document defines the enterprise standards governing unit testing across the complete application.

It establishes principles, architecture, organization, scope, quality standards, coverage expectations, test isolation, maintainability, and future automation readiness for unit tests.

This document serves as the authoritative reference for validating individual software units independently from infrastructure, databases, APIs, user interfaces, external services, and third-party integrations.

This document remains implementation-independent.

Assume the following documentation already exists:

- Product Documentation

- Architecture

- Database

- Workflows

- Contracts

- Security

- API Catalog

- Design System

- Deployment Documentation

- Testing Strategy

Reference previous documentation instead of duplicating it.

Do NOT generate:

- PHPUnit code

- Test implementations

- Mocking framework code

- Assertions

- Programming language examples

- Automation scripts

Remain architecture-focused.

---

# Scope

Generate enterprise unit testing standards covering:

Business Services

Domain Services

Validators

Business Rules

Calculators

Factories

Mappers

Repositories (where appropriate)

Policies

Permissions

Helpers

Utilities

DTO Validation

Configuration Validation

Background Job Logic

Workflow Decision Logic

Future AI Components

---

# Enterprise Unit Testing Principles

Isolation

Repeatability

Deterministic Results

Fast Execution

No External Dependencies

Business Rule Validation

Maintainability

High Readability

Independent Execution

Automation Ready

Future Scalability

---

# Document Structure

## 1. Unit Testing Overview

Describe:

Purpose

Objectives

Testing Philosophy

Business Benefits

Quality Benefits

Testing Scope

Future Evolution

---

## 2. Test Architecture

Define testing architecture for:

Business Services

Domain Services

Validation Services

Calculation Services

Policy Services

Permission Services

Factories

Transformers

Utility Services

Configuration Components

Workflow Decision Logic

Background Job Logic

For every layer define:

Purpose

Responsibilities

Coverage

Dependencies

Success Criteria

---

## 3. Unit Test Scope

Generate standards covering:

Positive Scenarios

Negative Scenarios

Boundary Conditions

Edge Cases

Business Rules

Validation Rules

Permission Rules

Workflow Rules

Configuration Rules

Calculation Rules

Exception Handling

Null Handling

Future Extensions

---

## 4. Test Isolation

Define standards for:

External Dependencies

Database Independence

API Independence

File System Independence

Queue Independence

Notification Independence

Clock Independence

Configuration Isolation

State Isolation

Parallel Execution

Deterministic Results

---

## 5. Test Organization

Generate standards covering:

Naming Conventions

Folder Structure

Module Separation

Feature Grouping

Business Rule Grouping

Shared Fixtures

Shared Utilities

Reusable Test Components

Documentation

Versioning

---

## 6. Coverage Strategy

Define standards for:

Business Logic

Validation

Calculations

Policies

Permissions

State Transitions

Exception Handling

Configuration

Workflow Decisions

Utility Functions

Coverage Goals

Coverage Reporting

---

## 7. Mocking Strategy

Generate standards covering:

Repositories

External APIs

Notifications

Authentication

Authorization

Queues

Search

Storage

Logging

Configuration

Background Jobs

Future Services

Describe when mocking is appropriate and when it should be avoided.

---

## 8. Test Data Strategy

Define standards for:

Test Fixtures

Builders

Factories

Static Data

Generated Data

Boundary Values

Invalid Values

Reference Data

Reusable Data

Cleanup

Versioning

---

## 9. Error Validation

Generate standards covering:

Business Exceptions

Validation Failures

Authorization Failures

Permission Failures

Configuration Errors

Workflow Errors

Calculation Errors

Unexpected Conditions

Recovery Validation

---

## 10. Quality Metrics

Define metrics covering:

Coverage

Execution Time

Failure Rate

Maintainability

Flaky Tests

Readability

Defect Detection

Regression Protection

Business Rule Coverage

Quality KPIs

---

## 11. Continuous Execution

Generate standards for:

Developer Execution

Pre-commit Validation

CI Readiness

Regression Suites

Selective Execution

Parallel Execution

Failure Reporting

Trend Analysis

Continuous Improvement

---

## 12. AI Coding Agent Guidance

Provide implementation guidance covering:

Test organization

Isolation

Dependency injection

Business rule validation

Mocking boundaries

Fixture reuse

Naming consistency

Maintainability

Future automation

Documentation

---

## 13. Unit Test Lifecycle

Define standards for:

Planning

Creation

Review

Execution

Maintenance

Refactoring

Versioning

Deprecation

Documentation

Continuous Improvement

---

## 14. Architecture Decision Summary

Generate a summary table including:

Area

Decision

Reason

Quality Benefit

Developer Benefit

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Unit Testing Specification.

Avoid implementation details.

Avoid testing framework recommendations.

Avoid programming language examples.

Avoid test code.

Focus entirely on testing architecture, isolation, maintainability, quality governance, scalability, automation readiness, and continuous improvement.

This document should become the definitive unit testing standard governing every business component within the Enterprise School Management System.
