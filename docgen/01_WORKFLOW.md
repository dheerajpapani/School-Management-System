# Documentation Generation Workflow

## Purpose

This document defines the exact execution workflow for generating project documentation.

Every execution cycle must follow this workflow without deviation.

---

# Workflow

## Step 1 — Initialize

* Read `00_MANIFEST.md`
* Confirm documentation generation mode.

---

## Step 2 — Load State

Read:

* `03_STATE.md`

Determine:

* Current phase
* Current progress
* Current status

---

## Step 3 — Load Roadmap

Read:

* `04_ROADMAP.yaml`

Locate the first executable task with status `pending`.

---

## Step 4 — Resolve Dependencies

Read:

* `05_DEPENDENCY_MAP.yaml`

Determine only the files required for the current document.

Do not scan the repository.

---

## Step 5 — Load Context

Read only:

* Dependency documents
* Required templates (if applicable)

Ignore unrelated documentation.

---

## Step 6 — Generate

Generate exactly one markdown document.

The generated document must:

* Follow project conventions
* Respect dependencies
* Avoid duplication
* Remain consistent with existing documentation

---

## Step 7 — Validate

Verify the generated document against the project checklist.

If validation fails, fix the document before continuing.

---

## Step 8 — Update Project State

Update:

* `03_STATE.md`
* `04_ROADMAP.yaml`
* `06_SUMMARY.md`

---

## Step 9 — Stop

Terminate execution.

Do not generate another document.

Wait for explicit user approval before continuing.

---

# Missing Dependency Handling

If a required document does not exist:

1. Insert it into `04_ROADMAP.yaml`.
2. Update `05_DEPENDENCY_MAP.yaml`.
3. Generate the missing prerequisite first.
4. Resume the original task after approval.

---

# Failure Recovery

If execution stops unexpectedly:

1. Read the Manifest.
2. Read the State.
3. Read the Roadmap.
4. Continue from the first pending task.

Never regenerate completed documents unless explicitly instructed.

---

# Completion Criteria

An execution cycle is complete only when:

* One document has been generated.
* Validation has passed.
* State has been updated.
* Roadmap has been updated.
* Summary has been updated.
* Execution has stopped awaiting user approval.
