# AI Plan - Phase <N>: <Phase Name>

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** <Project name> | **Parent:** `../plan.md`  
**Status:** <Not started | Active | Awaiting Review | Blocked | Complete>  
**Mode:** <Single-pass | Two-pass contract-first>

## Objective & Scope

**Objective:** <Concrete outcome this phase must produce>  
**Inputs:** [Requirements Section] | [Architecture Section] | [Prior Phase Output]  
**In Scope:** [List items]  
**Out of Scope / Do Not Do Yet:** [List items]  
**Expected Deliverables:** [List deliverables]

## Module Scope & Boundaries

* **Modules In Scope:** [Modules/subsystems/packages/layers this phase may create or modify]
* **Modules Out of Scope:** [Modules/subsystems/packages/layers this phase must not modify]
* **Boundary Rules:** [Dependency direction, ownership rules, adapter/domain/runtime/protocol separation rules, or `None`]
* **Public Seams / Contracts:** [Interfaces, schemas, entry points, extension points, tests, examples, or review artifacts that should make the boundary human-reviewable]
* **Human Review Focus:** [What the reviewer should inspect to confirm the implementation shape remains understandable]

## Ordered Work

*(Note: If Single-Pass, delete Pass A and use only Pass B / Implementation steps.)*

### Pass A: Contract (Review Gate)

* **Step A1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step A2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

Pass A should normally produce:

* the reviewable API, structural contract, or design surface being established,
* the module seams, subsystem boundaries, or dependency rules this phase will rely on, when relevant, and
* behavior-focused tests, usage examples, or equivalent review artifacts that make the intended
  behavior concrete before full implementation.

**Stop here for Human Review of the contract, module boundaries, and review artifacts before Pass B.**

### Pass B: Implementation (Or Single-Pass)

* **Step B1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step B2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

## Validation & Done Criteria

* **Validation Strategy:** [List specific tests, manual checks, and verifications]
* **Module Boundary Validation:** [How to confirm responsibilities, dependency direction, public seams, and human-digestible structure were preserved]
* **Definition of Done:** [List completion conditions. For two-pass, include "Faithful to approved contract and module boundaries"]

## Context & Wrap-up

* **Dependencies:** [List known dependencies]
* **Risks:** [List known risks]
* **Open Questions:** [Active execution questions, prioritized by importance]
* **Completion Summary:** *(Fill when done)* **Outcome:** [Results] |
  **Unlocked:** [Next capability]

## Maintenance Rules

* Treat this file as the authoritative detailed execution plan for this phase.
* Keep `plan.md` at roadmap level. Do not duplicate phase-level sequencing there.
* Keep `state.md` aligned with this file for:
    * current pass,
    * exact next step,
    * review-gate status,
    * blockers,
    * phase completion state.
* Preserve the approved module scope and boundary rules during execution.
* Do not collapse responsibilities into convenience classes, add cross-module shortcuts, or introduce new dependencies outside the approved boundary shape without human approval.
* If required behavior does not fit the approved module structure, stop and require phase-plan correction, architecture clarification, architecture revision, or icebox capture before continuing.
* When a pass boundary, review gate, blocker state, or phase status changes, verify whether
  `state.md` and `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project
  direction, correct it before substantive phase execution continues.
* Compress completed phase detail when it no longer helps execution, while preserving enough
  summary to explain the outcome and what it unlocked.