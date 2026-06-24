# Documentation Generation Rules

## Purpose

These rules govern every documentation generation cycle.

The agent must follow every rule unless explicitly overridden by the user.

---

# Generation Rules

## RULE-001

Generate exactly one document per execution cycle.

---

## RULE-002

Never generate multiple documents in a single execution.

---

## RULE-003

Always follow the order defined in `04_ROADMAP.yaml`.

---

## RULE-004

Never skip a pending task unless blocked by dependencies.

---

## RULE-005

Read only the files listed in `05_DEPENDENCY_MAP.yaml` for the active task.

Never scan the entire repository.

---

## RULE-006

Never regenerate completed documents unless:

* The user explicitly requests it.
* A dependency change requires updating it.

---

## RULE-007

Maintain consistency with all dependency documents.

Do not contradict previously approved documentation.

---

## RULE-008

If a required prerequisite is missing:

* Insert it into the roadmap.
* Update the dependency map.
* Generate the prerequisite first.
* Resume the original task afterward.

---

## RULE-009

Do not invent project structure, architecture, or workflows already defined in existing documentation.

---

## RULE-010

Avoid duplicate content.

Reference existing documentation instead of repeating it.

---

## RULE-011

Each document must have a single clear purpose.

---

## RULE-012

Keep documents modular.

Avoid combining unrelated topics.

---

## RULE-013

Always validate the generated document before completion.

---

## RULE-014

After successful generation update:

* `03_STATE.md`
* `04_ROADMAP.yaml`
* `06_SUMMARY.md`

---

## RULE-015

Never continue automatically after completing one document.

Stop and wait for explicit user approval.

---

## RULE-016

Never ask the user what document should be generated next.

Determine it from the roadmap.

---

## RULE-017

If multiple documents become eligible, generate only the first executable pending document.

---

## RULE-018

If execution fails, resume using the current state instead of restarting.

---

## RULE-019

Never modify unrelated documentation.

---

## RULE-020

Every completed execution cycle must leave the repository in a resumable state.
