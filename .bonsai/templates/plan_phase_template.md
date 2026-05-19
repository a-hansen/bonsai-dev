## `plan_phase_template.md`

```md
# AI Plan - Phase <N>: <Phase Name>

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**
**Project:** <Project name> | **Parent:** `plan.md`
**Status:** <Not started | Active | Awaiting Review | Blocked | Complete>
**Mode:** <Single-pass | Two-pass contract-first>

## Objective & Scope

**Objective:** <Concrete outcome this phase must produce>
**Inputs:** [Requirements Section] | [Architecture Section] | [Prior Phase Output]
**In Scope:** [List items]
**Out of Scope / Do Not Do Yet:** [List items]
**Expected Deliverables:** [List deliverables]

## Ordered Work

*(Note: If Single-Pass, delete Pass A and use only Pass B/Implementation steps)*

### Pass A: Contract (Review Gate)

* **Step A1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step A2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
  *(Stop here for Human Review of API/Tests before Pass B)*

### Pass B: Implementation (Or Single-Pass)

* **Step B1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step B2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

## Validation & Done Criteria

* **Validation Strategy:** [List specific tests, manual checks, and verifications]
* **Definition of Done:** [List completion conditions. For two-pass, include "Faithful to approved contract"]

## Context & Wrap-up

* **Dependencies:** [List known dependencies]
* **Risks:** [List known risks]
* **Open Questions:** [Active execution questions, max 5]
* **Completion Summary:** *(Fill when done)* **Outcome:** [Results] | 
  **Unlocked:** [Next capability]
```
