# 05_Indexing_Strategy.md

## Objective

You are acting as a Principal Database Performance Architect responsible for defining the complete Indexing Strategy for an Enterprise School Management System (SMS).

This document is the authoritative specification governing how database indexes are designed, categorized, maintained, optimized, monitored, and evolved across the School Management System.

The objective is to provide a scalable indexing architecture capable of supporting enterprise workloads while maintaining fast query performance, efficient writes, predictable execution plans, and long-term maintainability.

This document defines indexing philosophy and architectural decisions only.

It is NOT a SQL implementation document.

It is NOT a CREATE INDEX document.

It is NOT a database engine tuning guide.

Assume all previously generated documentation already exists.

Do not duplicate previous documents.

---

# Scope

Define the indexing architecture for the complete School Management System.

Cover every module and every major access pattern.

Focus on why indexes exist and how they should be governed.

Avoid implementation.

---

# Document Structure

## 1. Purpose

Explain:

Why indexing is necessary.

Relationship between:

Normalization

Indexes

Query Performance

Write Performance

Storage Cost

Reporting

Analytics

Scalability

---

## 2. Indexing Philosophy

Describe principles including:

Business-driven Indexing

Read Optimization

Balanced Write Performance

Minimal Redundant Indexes

Selective Indexing

Covering Index Readiness

Composite Index Readiness

Historical Query Optimization

Predictable Query Plans

Maintainability

Future Growth

Explain each principle.

---

## 3. Index Categories

Describe:

Primary Indexes

Unique Indexes

Lookup Indexes

Composite Indexes

Reporting Indexes

Search Indexes

Historical Indexes

Foreign Key Supporting Indexes

Audit Indexes

Background Processing Indexes

Analytics Indexes

Dashboard Indexes

Import Indexes

Export Indexes

Future Full-Text Readiness

Future Spatial Readiness

Explain each category.

---

## 4. Access Pattern Analysis

Describe expected access patterns.

Examples:

Student Lookup

Admission Processing

Attendance Entry

Attendance Reports

Result Generation

Fee Collection

Invoice Search

Payment History

Timetable Generation

Library Search

Employee Search

Inventory Search

Transport Assignment

Hostel Allocation

Notifications

Audit Review

Historical Queries

Global Search

Generate all additional access patterns.

---

## 5. Module-wise Index Strategy

For every module define expected indexing requirements.

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

For every module explain:

High-frequency Reads

High-frequency Writes

Lookup Columns

Filtering Columns

Sorting Columns

Reporting Columns

Historical Queries

Future Scaling

---

## 6. Composite Index Strategy

Describe conceptual design for:

Student + Academic Year

Student + Section

Attendance + Date

Attendance + Subject

Invoice + Status

Invoice + Due Date

Payment + Date

Exam + Subject

Teacher + Timetable

Library + Status

Hostel + Room

Transport + Route

Employee + Department

Generate all additional composite index opportunities.

Do NOT write SQL.

---

## 7. Reporting Optimization

Describe indexing considerations for:

Attendance Reports

Fee Reports

Result Reports

Promotion Reports

Financial Reports

Analytics

Dashboards

Executive Reports

Historical Reports

Scheduled Reports

Bulk Exports

---

## 8. Search Optimization

Describe indexing strategy for:

Student Search

Employee Search

Book Search

Asset Search

Global Search

Reference Data

Autocomplete

Filters

Lookups

Configuration

Future Full-text Search

---

## 9. Background Processing Optimization

Describe indexing considerations for:

Scheduled Jobs

Queue Processing

Import

Export

Notifications

Analytics

Cleanup

Archival

Synchronization

Monitoring

---

## 10. Performance Strategy

Discuss:

Read-heavy Tables

Write-heavy Tables

Large Transaction Tables

Historical Tables

Configuration Tables

Reference Tables

Bulk Operations

Peak Admission Season

Exam Period

Fee Collection Peaks

Long-term Scalability

---

## 11. Index Maintenance Strategy

Describe:

Index Review

Unused Index Detection

Duplicate Index Prevention

Fragmentation Awareness

Historical Index Review

Growth Planning

Monitoring

Documentation

Governance

---

## 12. Monitoring & Observability

Describe monitoring for:

Slow Queries

Index Usage

Unused Indexes

Duplicate Indexes

Query Plans

Read Performance

Write Performance

Historical Trends

Growth

Capacity

---

## 13. Future Extensibility

Support future:

Full-text Search

External Search Engines

Distributed Databases

Read Replicas

Data Warehouse

Analytics Platforms

Machine Learning

AI Search

Regional Scaling

Multi-Tenant Deployments

---

## 14. Architecture Decision Summary

Create a summary table.

Columns:

Area

Index Category

Business Purpose

Read Benefit

Write Impact

Future Extension

---

# Writing Style

Maintain the tone of a professional Enterprise Database Performance Architecture Specification.

Do not include:

- SQL
- CREATE INDEX statements
- Database engine configuration
- Query optimizer hints
- EXPLAIN plans
- ORM mappings

Focus entirely on indexing philosophy, access patterns, performance optimization, governance, scalability, reporting, and maintainability.

This document should enable database architects and AI coding agents to design an optimized indexing strategy before physical SQL schema generation.
