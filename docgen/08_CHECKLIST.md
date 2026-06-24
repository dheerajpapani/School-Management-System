# Documentation Generation Validation Checklist

## Purpose

This checklist defines the mandatory validation criteria that every generated document must satisfy before the execution cycle can be considered complete.

The Documentation Generation Agent must verify every item before updating the project state.

---

# Phase 1 — Preparation

## Repository

* [ ] Manifest loaded
* [ ] Workflow loaded
* [ ] Rules loaded
* [ ] State loaded
* [ ] Roadmap loaded
* [ ] Dependency Map loaded

---

## Task Resolution

* [ ] First executable pending task identified
* [ ] Dependencies resolved
* [ ] Required documents loaded
* [ ] Unrelated documents ignored

---

# Phase 2 — Document Generation

## Structure

* [ ] Correct file path
* [ ] Correct filename
* [ ] Correct title
* [ ] Purpose included
* [ ] Required sections included
* [ ] Project conventions followed

---

## Quality

* [ ] No duplicate content
* [ ] No conflicting information
* [ ] Consistent terminology
* [ ] Production-ready
* [ ] Complete
* [ ] Readable
* [ ] Modular

---

## Dependency Validation

* [ ] Dependency documents respected
* [ ] References consistent
* [ ] No missing prerequisite
* [ ] No circular dependency introduced

---

# Phase 3 — Repository Update

## Files

* [ ] Document saved
* [ ] State updated
* [ ] Roadmap updated
* [ ] Summary updated

---

## Dynamic Updates

If required:

* [ ] New task inserted
* [ ] Dependency map updated
* [ ] Roadmap reordered

Otherwise:

* [ ] No dynamic update required

---

# Phase 4 — Validation

## Verification

* [ ] Structure verified
* [ ] Naming verified
* [ ] Dependency verification passed
* [ ] Internal consistency verified
* [ ] Validation successful

---

# Phase 5 — Completion

## Execution

* [ ] One document generated
* [ ] One task completed
* [ ] Next task identified
* [ ] Repository resumable
* [ ] Execution stopped

---

# User Approval

The execution cycle is complete only after presenting:

* Completed task
* Generated document
* Summary
* Current progress
* Next task

Then wait for:

OK

before continuing.

---

# Failure Handling

If any checklist item fails:

* Do not mark the task complete.
* Do not update the roadmap as completed.
* Correct the issue.
* Revalidate.
* Repeat until every checklist item passes.

---

# Success Criteria

A documentation generation cycle is successful only when:

* Every checklist item is satisfied.
* Repository state is synchronized.
* The next task is ready.
* The project can resume without additional context.
