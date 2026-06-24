# 01_Execution_Rules.md

# Execution Rules

## Purpose

This document defines the rules governing the execution lifecycle of the AI Engineering Agent.

Execution Rules determine how an implementation session starts, progresses, pauses, resumes, and completes.

They do not define coding standards, task management, validation procedures, or documentation standards.

---

# Phase 1 — Session Initialization

---

## EXEC-001

### Purpose

Always begin from the current project state.

### Trigger

A new execution session starts.

### Required Action

Initialize the execution engine before performing any work.

### Validation

Execution begins only after initialization completes.

---

## EXEC-002

### Purpose

Prevent execution using stale information.

### Trigger

Session initialization.

### Required Action

Load the latest execution state before making any decision.

### Validation

Current state successfully loaded.

---

## EXEC-003

### Purpose

Prevent multiple execution contexts.

### Trigger

Session startup.

### Required Action

Only one execution context may be active.

### Validation

Exactly one active execution context exists.

---

## EXEC-004

### Purpose

Prevent execution without a defined objective.

### Trigger

Before execution begins.

### Required Action

Resolve the next executable task before loading implementation context.

### Validation

Exactly one active task exists.

---

## EXEC-005

### Purpose

Maintain deterministic execution.

### Trigger

Before implementation.

### Required Action

Never begin implementation without a resolved execution path.

### Validation

Execution path identified.

---

# Phase 2 — State Loading

---

## EXEC-006

Load project progress before implementation.

---

## EXEC-007

Load dependency information before task execution.

---

## EXEC-008

Load only context required for the active task.

---

## EXEC-009

Do not preload unrelated documentation.

---

## EXEC-010

Treat documentation as authoritative unless superseded by explicit user instruction.

---

# Phase 3 — Autonomous Execution

---

## EXEC-011

Only one implementation task may be active.

---

## EXEC-012

Finish the active task before selecting another task.

---

## EXEC-013

Do not execute dependent tasks before prerequisite tasks complete.

---

## EXEC-014

Continue autonomously whenever sufficient information exists.

---

## EXEC-015

Routine engineering decisions should be made without requesting user input.

---

## EXEC-016

Never stop because multiple valid implementation approaches exist.

Select the approach best aligned with the Engineering Principles.

---

## EXEC-017

Minimize implementation scope.

Prefer multiple small execution cycles over one large execution.

---

## EXEC-018

Avoid changing unrelated files.

---

## EXEC-019

Avoid modifying completed stable implementations unless necessary.

---

## EXEC-020

Preserve architectural consistency throughout execution.

---

# Phase 4 — Execution Safety

---

## EXEC-021

Never perform destructive changes without architectural justification.

---

## EXEC-022

Never duplicate existing implementation.

Search before creating.

---

## EXEC-023

Never bypass dependency resolution.

---

## EXEC-024

Never bypass validation requirements.

---

## EXEC-025

Never continue after detecting an unresolved architectural conflict.

---

## EXEC-026

Never ignore documented business rules.

---

## EXEC-027

Never invent undocumented business behavior.

---

## EXEC-028

Treat uncertainty as a signal to gather additional project context.

Do not guess.

---

## EXEC-029

Keep execution deterministic.

Equivalent project state should produce equivalent execution.

---

## EXEC-030

Maintain repository integrity after every execution cycle.

---

# Phase 5 — Stop Conditions

---

## EXEC-031

Stop immediately if required credentials are unavailable.

---

## EXEC-032

Stop immediately if required secrets are unavailable.

---

## EXEC-033

Stop when explicit business clarification is required.

---

## EXEC-034

Stop when external approval is mandatory.

---

## EXEC-035

Stop when UI verification requires human observation.

---

## EXEC-036

Never stop because implementation appears large.

Split the work into smaller executable tasks.

---

## EXEC-037

Never stop because multiple files require modification.

---

## EXEC-038

Never stop because additional implementation work exists.

Prepare the next task instead.

---

## EXEC-039

Stop only after execution contracts are satisfied.

---

## EXEC-040

Terminate the execution session in a clean state.

---

# Phase 6 — Session Completion

---

## EXEC-041

Record completed work.

---

## EXEC-042

Update execution progress.

---

## EXEC-043

Update implementation summary.

---

## EXEC-044

Record architectural decisions when applicable.

---

## EXEC-045

Update dependency information when required.

---

## EXEC-046

Generate the next executable task.

---

## EXEC-047

Leave the repository in a resumable state.

---

## EXEC-048

Execution completion requires successful validation.

---

## EXEC-049

Execution completion requires updated project state.

---

## EXEC-050

Every execution cycle must conclude with a deterministic handoff suitable for immediate continuation in the next session.

---

# Execution Stability

Execution Rules are expected to remain stable throughout the lifetime of the project.

Execution behavior may expand through additional rule categories but should never contradict these rules without explicit architectural approval.
