# 01_Server_Architecture.md

## Objective

You are acting as a Principal Enterprise Infrastructure Architect responsible for designing the Server Architecture Specification for an Enterprise School Management System (SMS).

This document defines the logical and physical server architecture required to host, operate, scale, secure, monitor, and maintain the complete School Management System.

This document is architecture-focused.

It defines deployment topology and infrastructure responsibilities without depending on any specific hosting provider or operating system.

Assume all application architecture, database architecture, APIs, security architecture, workflows, modules, design system, and deployment strategy documents already exist.

Reference previous documentation instead of duplicating it.

Remain implementation-independent.

Do NOT generate:

* Shell scripts

* Docker Compose files

* Kubernetes manifests

* Terraform

* Ansible

* CloudFormation

* Server commands

* OS-specific configuration

---

# Scope

Generate the complete enterprise server architecture covering:

Application Layer

Database Layer

Storage Layer

Caching Layer

Background Processing

Messaging

Monitoring

Logging

Authentication

Search

File Storage

Backup

Analytics

Reporting

Future AI Services

Future Integrations

Future Multi-campus Deployment

Future SaaS Deployment

---

# Enterprise Deployment Principles

High Availability

Scalability

Fault Tolerance

Security by Design

Horizontal Scaling

Vertical Scaling

Isolation

Maintainability

Observability

Disaster Recovery

Future Cloud Readiness

---

# Document Structure

## 1. Architecture Overview

Describe:

Purpose

Objectives

Deployment Philosophy

Logical Architecture

Physical Architecture

Responsibilities

Infrastructure Boundaries

Growth Strategy

Future Evolution

---

## 2. Infrastructure Layers

Define architecture for:

Load Balancer

Reverse Proxy

Web Layer

Application Layer

Business Services

API Layer

Background Workers

Message Queue

Scheduler

Database

Cache

File Storage

Search Engine

Reporting

Monitoring

Logging

Backup

Analytics

Identity Services

Future AI Layer

---

## 3. Server Roles

Define server responsibilities for:

Web Server

Application Server

Database Server

Cache Server

Queue Server

Scheduler Server

Storage Server

Monitoring Server

Logging Server

Backup Server

Search Server

Reporting Server

Authentication Server

Future AI Server

Development Environment

Testing Environment

Staging Environment

Production Environment

---

## 4. Logical Communication

Describe communication between:

Client

Reverse Proxy

Application

API

Database

Cache

Storage

Queue

Scheduler

Search

Monitoring

Backup

Analytics

Notification Services

Future Services

---

## 5. Scalability Strategy

Define:

Horizontal Scaling

Vertical Scaling

Read Scaling

Write Scaling

Session Management

Background Processing

Caching

Static Assets

Large File Handling

Reporting

Analytics

Future Growth

---

## 6. High Availability

Describe:

Redundancy

Load Balancing

Health Checks

Failover

Database Availability

Queue Availability

Cache Availability

Storage Availability

Recovery

Maintenance Windows

---

## 7. Security Architecture

Cover:

Network Segmentation

Server Isolation

TLS Boundaries

Firewall Layers

Internal Communication

Secrets Isolation

Administrative Access

Monitoring

Audit

Compliance

---

## 8. Performance Strategy

Define:

Connection Management

Caching Layers

Database Connections

Worker Pools

Static Asset Delivery

Compression

Request Optimization

Background Processing

Reporting Optimization

Large Imports

Large Exports

---

## 9. Monitoring Architecture

Describe monitoring for:

Infrastructure

Servers

Applications

Databases

Queues

Storage

Cache

Search

Background Jobs

Reports

Security

Business KPIs

---

## 10. Disaster Recovery Readiness

Cover:

Recovery Objectives

Backups

Redundancy

Replication Readiness

Recovery Validation

Business Continuity

Infrastructure Restoration

Future Geo-redundancy

---

## 11. AI Coding Agent Guidance

Provide implementation guidance covering:

Infrastructure separation

Server responsibilities

Deployment sequencing

Dependency order

Scaling readiness

Monitoring

Logging

Security boundaries

Future cloud migration

Future containerization

---

## 12. Architecture Decision Summary

Generate a summary table including:

Area

Decision

Reason

Business Benefit

Operational Benefit

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Server Architecture Specification.

Avoid vendor-specific recommendations.

Avoid operating-system-specific instructions.

Avoid implementation scripts.

Focus entirely on logical infrastructure architecture, scalability, security, maintainability, observability, reliability, and future evolution.

This document should become the definitive infrastructure blueprint for deploying the Enterprise School Management System in any enterprise environment.
