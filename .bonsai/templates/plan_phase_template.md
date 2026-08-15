# AI Plan - Phase <N>: <Phase Name>

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** <Project name> | **Parent:** `../plan.md`  
**Phase Status:** <Not started | Active | Awaiting Review | Blocked | Complete>  
**Plan Status:** <Draft | Ready for Review | Approved | Superseded>  
**Mode:** <Single-pass | Two-pass contract-first>

## Objective & Scope

**Objective:** <Concrete outcome this phase must produce>  
**Inputs:** [Requirements Section] | [Architecture Section] | [Prior Phase Output]  
**In Scope:** [List items]  
**Out of Scope / Do Not Do Yet:** [List items]  
**Expected Deliverables:** [List deliverables]

## Execution Constraints

* **Implementation Scope:** [Known modules/subsystems/packages/layers this phase may create or modify, or `Not prescribed`]
* **Approved Boundaries:** [Relevant architecture boundaries or `None`]
* **Public Contracts:** [APIs, schemas, protocols, persistent formats, extension points, or other durable contracts this phase establishes or changes, or `None`]
* **Human Review Focus:** [What the reviewer must inspect before the next gate, or `None`]

Do not invent internal seams, interfaces, abstraction layers, dependency rules, or module boundaries merely
to populate this section.

## Ordered Work

*(If Single-Pass, delete Pass A and rename the implementation section to `### Implementation`. Do not use a Pass B label for single-pass work.)*

### Pass A: Contract (Review Gate)

Use Pass A only when this phase establishes or materially changes a contract that independently merits
human approval before implementation.

* **Step A1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step A2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

Pass A should produce:

* the reviewable contract, API shape, schema, protocol surface, extension contract, persistent format,
  or other durable design surface being established in its native developer-facing form when practical,
* relevant approved architecture constraints needed to interpret that contract, and
* tests, examples, signatures, schemas, or other review artifacts only when they materially clarify
  intended behavior and fit project conventions.

For a code contract, prefer minimal source-level API or structural skeletons plus behavior-focused tests or
usage examples. Concrete classes with intentionally unimplemented methods are valid contract artifacts. Pass A
may establish names, types, signatures, visibility, and structural relationships but should leave substantive
behavior for Pass B. The Pass A contract package, including contract-test source, must compile successfully before
the contract review gate. Behavior-focused contract tests do not need to pass in Pass A and may be temporarily
disabled when appropriate; the phase plan should require Pass B to enable any temporarily disabled contract tests
and make all approved behavioral expectations pass. Do not default to a standalone prose contract document when
the native source and review artifacts already express the contract clearly.

A Bonsai contract gate does not itself require Java interfaces, builders, adapters, dependency
injection, abstraction layers, or similar indirection.

**Stop here for Human Review before Pass B.**

### Pass B: Implementation

* **Step 1 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>
* **Step 2 <Name>:** <Goal> | **Files:** [Paths] | **Done:** <Condition>

## Validation & Done Criteria

* **Validation Strategy:** [Project-appropriate tests, builds, manual checks, examples, or other verification]
* **Architecture Validation:** [Checks required to confirm approved architecture or contracts were preserved, or `None`]
* **Definition of Done:** [List completion conditions. For two-pass, include faithful implementation of the approved contract]

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
    * phase-plan approval state,
    * current pass,
    * exact next step,
    * review-gate status,
    * blockers,
    * phase completion state.
* Preserve approved project architecture and contracts during execution.
* Do not introduce interfaces, abstraction layers, adapters, builders, dependency constraints, or other
  structures merely to satisfy Bonsai workflow.
* Implementation style and test style follow project conventions, approved project memory,
  developer context, and applicable external skills.
* For an approved two-pass code contract, Pass A behavior tests preserve behavioral expectations rather than
  immutable test source. During Pass B, fixtures, fakes, helpers, imports, construction, and other test plumbing
  may change without another contract review when approved scenarios, inputs, observable outcomes, and failure
  expectations remain materially unchanged. Require contract review before weakening, removing, contradicting,
  or materially changing an approved behavioral expectation.
* If required behavior conflicts with approved architecture or an approved contract, stop and require
  phase-plan correction, final-truth clarification, or final-truth revision before continuing.
* When a pass boundary, review gate, blocker state, phase status, or plan approval state changes,
  verify whether `state.md` and `plan.md` require corresponding updates.
* If this phase plan becomes incomplete, stale, or inconsistent with current approved project direction,
  correct it before substantive phase execution continues.
* Set `Plan Status: Ready for Review` when drafting is complete and human approval is required.
* Set `Plan Status: Approved` only after explicit human approval.
* Compress completed phase detail when it no longer helps execution, while preserving enough summary
  to explain the outcome and what it unlocked.