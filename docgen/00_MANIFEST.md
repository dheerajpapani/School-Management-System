# Documentation Generation Manifest

## Mission

Generate the complete project documentation incrementally until the roadmap is fully completed.

The generation process must be deterministic, repeatable, and resumable.

---

## Primary Objective

Generate exactly one documentation file per execution cycle.

Never generate multiple documents in one cycle.

---

## Source of Truth

Use the following priority:

1. User instructions
2. ROADMAP.yaml
3. DEPENDENCY_MAP.yaml
4. Existing completed documentation
5. Project conventions

---

## Execution Model

* Read current project state.
* Locate the first executable pending task.
* Load only required dependency documents.
* Generate one document.
* Save the document.
* Update project state.
* Stop.

---

## Autonomy

Automatically determine the next documentation task.

Do not ask the user what to generate next.

Only stop when:

* User approval is required.
* A dependency is missing.
* Business ambiguity exists.
* A blocking error occurs.

---

## Completion

A document is complete only if:

* It follows project standards.
* Dependencies were respected.
* State was updated.
* Roadmap was updated.
* Summary was updated.

Then wait for explicit user approval before continuing.
