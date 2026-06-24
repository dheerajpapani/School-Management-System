# AGENTS.md

# Repository Entry Point

Welcome to the Enterprise School Management System repository.

This repository is designed to be executed by autonomous AI coding agents.

Do not begin implementation immediately.

Always follow the execution flow defined in this repository.

---

# Primary Objective

Your objective is to complete the repository incrementally while preserving architectural consistency, traceability, maintainability, and deterministic execution.

Never attempt large implementations.

Complete one small task per execution cycle.

---

# Operating Modes

The repository has two execution modes.

## 1. Documentation Generation

Use this mode while project documentation is incomplete.

Entry Point:

```text
docgen/07_PROMPT.md
```

Generate exactly one document.

Update all required state files.

Stop.

Wait for explicit user approval.

---

## 2. Project Implementation

Use this mode only after documentation generation has been completed and approved.

Entry Point:

```text
agent/00_AGENT.md
```

Follow the complete Agent Operating System.

Implement exactly one executable task.

Validate.

Update project state.

Stop.

Wait for user approval.

---

# Mandatory Startup Sequence

Before every execution cycle:

1. Determine the current execution mode.
2. Read the appropriate entry point.
3. Read project state.
4. Read project roadmap.
5. Determine the next executable task.
6. Load only required dependencies.
7. Execute one task.
8. Validate.
9. Update repository state.
10. Stop.

---

# Repository Rules

Always:

* Execute exactly one task.
* Keep tasks as small as possible.
* Update progress after every task.
* Update summaries after every task.
* Update the roadmap after every task.
* Preserve architectural consistency.
* Preserve documentation consistency.
* Leave the repository in a resumable state.

Never:

* Skip roadmap order.
* Execute multiple tasks.
* Scan the entire repository.
* Modify unrelated files.
* Ask the user what to do next.
* Continue automatically after completing one task.

---

# Dynamic Task Management

If execution reveals missing prerequisite work:

1. Insert the prerequisite into the roadmap.
2. Update dependency mappings.
3. Complete the prerequisite first.
4. Resume the original task after approval.

Do not silently ignore missing dependencies.

---

# User Interaction

The user should only be interrupted when:

* Business clarification is required.
* Credentials or secrets are required.
* Human verification is required.
* A blocking issue prevents execution.

Otherwise continue autonomously.

At the end of every execution cycle provide:

* Completed Task
* Files Read
* Files Created
* Files Updated
* Validation Result
* Current Progress
* Next Task

Then stop and wait for:

**OK**

before continuing.

---

# Long-Term Goal

Continue this execution model until:

* Documentation is complete.
* Implementation is complete.
* Testing is complete.
* Deployment is complete.
* The repository reaches production readiness.

Every execution cycle should improve the repository while minimizing context usage and maximizing deterministic behavior.
