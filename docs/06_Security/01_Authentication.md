# 01_Authentication.md

## Objective

You are acting as a Principal Security Architect responsible for defining the complete Authentication Architecture for an Enterprise School Management System (SMS).

This document is the authoritative specification governing how identities are established, authenticated, verified, recovered, and managed throughout the School Management System.

The objective is to establish a secure, scalable, user-friendly, auditable, extensible, and standards-compliant authentication framework for every user type.

This document defines authentication architecture only.

It does NOT define:

- Authorization
- RBAC
- SQL schema
- PHP implementation
- APIs
- UI implementation

Assume all previously generated documentation already exists.

Do not duplicate previous documents.

For every authentication contract define:

- Owner
- Consumers
- Allowed Dependencies
- Forbidden Dependencies
- Lifecycle
- Security Requirements
- Related Contracts

---

# Scope

Define authentication architecture for:

Students

Parents

Teachers

Employees

Librarians

Accountants

Transport Staff

Hostel Staff

HR

Department Heads

Principal

Vice Principal

Administrators

Alumni

External Users (future)

Generate every authentication scenario required.

---

# Document Structure

## 1. Purpose

Explain:

Why authentication exists.

Difference between:

Authentication

Authorization

Identity

Credential

Session

Token

Verification

Identity Provider

Explain why authentication must remain independent of business permissions.

---

## 2. Authentication Principles

Describe principles including:

Identity First

Least Privilege Foundation

Credential Confidentiality

Session Integrity

Strong Passwords

Password Hashing

Multi-factor Readiness

Single Sign-on Readiness

Auditability

Recoverability

Usability

Extensibility

Explain each principle.

---

## 3. Identity Model

Define supported identities.

Examples:

Student

Parent

Teacher

Employee

Administrator

Alumni

System Account

Service Account (future)

External Identity (future)

Describe identity ownership and lifecycle.

---

## 4. Authentication Lifecycle

Define lifecycle.

Examples:

Registration

Identity Verification

Credential Creation

First Login

Normal Login

Password Change

Password Reset

Account Lock

Unlock

Credential Rotation

Account Deactivation

Account Reactivation

Account Closure

---

## 5. Authentication Methods

Describe conceptual support for:

Username & Password

Email & Password

Mobile Number & Password

Institution ID

OTP (future)

Authenticator Apps (future)

Passkeys (future)

Single Sign-On (future)

Government Identity Integration (future)

Explain appropriate use cases.

---

## 6. Credential Policies

Describe:

Password Length

Complexity

Reuse Restrictions

Expiration Strategy

Rotation Policy

Temporary Passwords

Initial Passwords

Password History

Account Recovery

Credential Verification

---

## 7. Session Strategy

Describe:

Session Creation

Session Renewal

Idle Timeout

Absolute Timeout

Concurrent Sessions

Remember Me

Logout

Forced Logout

Session Invalidation

Future Token Readiness

---

## 8. Account Recovery

Describe:

Forgot Password

Password Reset

Account Recovery

Identity Verification

Recovery Expiration

Recovery Failure

Administrative Recovery

Emergency Recovery

---

## 9. Security Considerations

Describe:

Brute Force Protection

Credential Stuffing Protection

Account Lockout

Rate Limiting

Device Awareness

Location Awareness (future)

Audit Logging

Sensitive Accounts

Emergency Accounts

---

## 10. Monitoring & Auditing

Define monitoring for:

Successful Logins

Failed Logins

Password Changes

Password Resets

Locked Accounts

Unlocked Accounts

Concurrent Sessions

Recovery Requests

Authentication Trends

Security Incidents

---

## 11. Future Extensibility

Support future:

Single Sign-On

OAuth

OpenID Connect

SAML

Passkeys

Biometric Authentication

Government Identity Providers

Enterprise Identity Providers

Passwordless Authentication

Adaptive Authentication

Risk-based Authentication

---

## 12. Authentication Matrix

Create a matrix.

Columns:

Identity Type

Authentication Method

Recovery

Session

Security Level

Future Extension

---

## 13. Architecture Decision Summary

Create a summary table.

Columns:

Area

Decision

Reason

Security Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Authentication Architecture Specification.

Do not include:

- SQL
- PHP
- API implementation
- UI implementation
- Password hashing algorithms in code

Focus entirely on authentication governance, identity lifecycle, credential management, session strategy, monitoring, security, and extensibility.

This document should enable AI coding agents to implement a secure enterprise authentication framework across the entire School Management System.
