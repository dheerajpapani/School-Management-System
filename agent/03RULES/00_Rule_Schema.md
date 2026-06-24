# 00_Rule_Schema.md

# Rule Definition Standard

## Purpose

This document defines the standard format for every operational rule within the Agent Operating System (AgentOS).

Every rule must follow this structure to ensure consistency, machine readability, traceability, maintainability, and future extensibility.

No rule should deviate from this schema.

---

# Rule Identifier

Every rule must have a permanent unique identifier.

Format:

```
<CATEGORY>-<NUMBER>
```

Examples:

```
EXEC-001
EXEC-002

CTX-001

TASK-001

CODE-001

VAL-001

COMP-001
```

Identifiers are immutable.

Deleted rules are never reused.

---

# Rule Categories

Every rule belongs to exactly one category.

Supported categories include:

* EXEC (Execution)
* CTX (Context)
* TASK (Task Management)
* CODE (Coding)
* DOC (Documentation)
* VAL (Validation)
* ARCH (Architecture)
* COMM (Communication)
* UI (UI Verification)
* REC (Recovery)
* GIT (Repository)
* DEBUG (Debugging)
* REFACTOR (Refactoring)
* PERF (Performance)
* SEC (Security)
* TEST (Testing)
* COMP (Completion)

---

# Rule Priority

Every rule shall define one priority.

Allowed values:

* Critical
* High
* Medium
* Low

Critical rules cannot be bypassed.

---

# Rule Structure

Every rule contains the following sections.

## Purpose

Why the rule exists.

---

## Trigger

When the rule becomes active.

---

## Condition

Requirements for execution.

---

## Required Action

The exact behavior expected from the agent.

---

## Exceptions

Situations where the rule may be skipped.

If none exist, explicitly state:

```
No exceptions.
```

---

## Dependencies

Other rules that should already be satisfied before this rule executes.

---

## Validation

How compliance with the rule is verified.

---

## Related Rules

Cross references to logically related rules.

---

# Rule Lifecycle

Rules may exist in one of the following states:

* Draft
* Active
* Deprecated
* Replaced
* Archived

Only Active rules participate in execution.

---

# Rule Modification

Existing rules should not be edited unless:

* Architecture changes
* Better engineering practices are adopted
* Existing behavior becomes invalid
* User explicitly approves

Major behavior changes require creation of a new rule when practical.

---

# Rule Ordering

Rules are ordered numerically within each category.

Numbers are never reused.

If a new rule belongs logically between existing rules, assign the next available identifier rather than renumbering previous rules.

---

# Rule Loading

Execution engines should load only rule categories required for the current task.

Example:

Implementing a repository:

Load:

* EXEC
* CODE
* VAL

Skip:

* UI
* PERF
* GIT

unless required.

---

# Rule Validation

Every rule should be:

* Unambiguous
* Deterministic
* Independently understandable
* Independently executable
* Independently verifiable

Rules should never depend on hidden assumptions.

---

# Rule Relationships

Rules may reference other rules.

Relationships should remain directional.

Circular rule dependencies should be avoided.

---

# Rule Stability

The schema defined in this document should remain stable throughout the lifetime of the project.

New categories may be introduced without changing the schema itself.
