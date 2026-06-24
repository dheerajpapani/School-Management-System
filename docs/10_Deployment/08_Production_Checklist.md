# 08_Production_Checklist.md

## Objective

You are acting as a Principal Enterprise DevOps Architect, Site Reliability Engineer (SRE), and Release Manager responsible for designing the Production Readiness & Go-Live Checklist Specification for an Enterprise School Management System (SMS).

This document defines the complete enterprise production readiness framework governing release validation, infrastructure readiness, application readiness, operational readiness, security validation, performance verification, disaster recovery verification, deployment approval, post-deployment monitoring, rollback readiness, and continuous operational excellence.

This document serves as the final validation gate before every production deployment.

It is not merely a checklist.

It is an enterprise production governance specification.

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

Reference previous documentation instead of duplicating it.

Remain implementation-independent.

Do NOT generate:

- CI/CD pipelines

- Deployment scripts

- Shell commands

- Kubernetes manifests

- Vendor-specific deployment procedures

- Cloud-provider instructions

---

# Scope

Generate enterprise production readiness standards covering:

Application

Infrastructure

Database

Security

Storage

Network

Cache

Search

Background Workers

Monitoring

Logging

Reporting

Analytics

Authentication

Notifications

Backup

Recovery

Operations

Support

Future SaaS Deployment

---

# Enterprise Go-live Principles

Production deployments must be:

Repeatable

Auditable

Predictable

Recoverable

Secure

Observable

Validated

Reversible

Documented

Business Approved

---

# Document Structure

## 1. Production Readiness Overview

Describe:

Purpose

Objectives

Release Philosophy

Business Benefits

Operational Benefits

Deployment Governance

Future Evolution

---

## 2. Release Readiness

Generate standards covering:

Business Approval

Technical Approval

Architecture Validation

Documentation Validation

Version Validation

Dependency Validation

Release Notes

Known Issues

Change Requests

Deployment Window

Communication Plan

---

## 3. Infrastructure Readiness

Define validation for:

Servers

Networking

Storage

Database

Cache

Search

Queues

Background Workers

Monitoring

Logging

Backups

Disaster Recovery

Environment Configuration

Secrets

Certificates

Capacity

Scalability

High Availability

---

## 4. Application Readiness

Generate standards covering:

Application Version

Database Compatibility

Configuration Validation

Feature Flags

Business Rules

Workflows

API Compatibility

User Permissions

Localization

Accessibility

Future Module Readiness

---

## 5. Database Readiness

Describe validation for:

Schema

Indexes

Constraints

Views

Seed Data

Reference Data

Migration Validation

Rollback Validation

Performance Validation

Data Integrity

---

## 6. Security Validation

Cover:

Authentication

Authorization

RBAC

Secrets

Encryption

Certificates

Audit Logging

Session Management

API Security

Security Headers Readiness

Vulnerability Review

Compliance

Privacy

---

## 7. Performance Validation

Generate standards covering:

Response Time

API Performance

Database Performance

Search Performance

Cache Performance

Queue Performance

Import Performance

Export Performance

Report Generation

Concurrent Users

Resource Usage

Stress Readiness

---

## 8. Operational Readiness

Define validation for:

Monitoring

Logging

Alerts

Dashboards

Support Documentation

Runbooks

Operational Contacts

Incident Response

Maintenance Procedures

Escalation

Business Support

---

## 9. Backup & Recovery Validation

Generate standards covering:

Backup Verification

Recovery Validation

Restore Testing

Disaster Recovery

Recovery Objectives

Recovery Documentation

Recovery Contacts

Recovery Approval

---

## 10. Deployment Validation

Describe:

Pre-deployment Validation

Deployment Sequencing

Dependency Validation

Smoke Testing

Health Validation

Business Validation

Post-deployment Verification

Rollback Readiness

Final Approval

---

## 11. Go-live Checklist

Generate a comprehensive checklist including:

Business Readiness

Technical Readiness

Infrastructure

Security

Database

Application

Monitoring

Logging

Backup

Recovery

Performance

Documentation

Support

Communication

Compliance

Approval

Sign-off

Generate enterprise checklist tables suitable for release governance.

---

## 12. Post-production Validation

Define standards for:

Smoke Tests

Business Validation

User Acceptance

Monitoring

Performance Observation

Security Validation

Error Monitoring

Operational KPIs

Business KPIs

Stabilization Period

Lessons Learned

---

## 13. AI Coding Agent Guidance

Provide implementation guidance covering:

Deployment sequencing

Validation order

Rollback preparation

Configuration validation

Operational readiness

Monitoring

Security

Database compatibility

Business validation

Future release automation

---

## 14. Release Lifecycle

Define standards for:

Planning

Development Complete

QA Complete

UAT Complete

Release Candidate

Go-live Approval

Production Deployment

Validation

Stabilization

Maintenance

Retirement

Continuous Improvement

---

## 15. Architecture Decision Summary

Generate a summary table including:

Area

Decision

Reason

Business Benefit

Operational Benefit

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Production Readiness & Go-live Specification.

Avoid implementation details.

Avoid deployment scripts.

Avoid cloud-provider-specific guidance.

Avoid CI/CD implementation.

Focus entirely on production governance, operational readiness, deployment validation, security, observability, recoverability, compliance, maintainability, and enterprise release management.

This document should become the definitive production deployment standard governing every release of the Enterprise School Management System.
