# Agent Plan - Phase <N>: <Phase Name>

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**  
**Project:** <Project name> | **Parent:** `../agent_plan.md`  
**Phase Status:** <Not started | Active | Awaiting Review | Blocked | Complete>  
**Plan Status:** <Draft | Ready for Review | Approved | Superseded>  
**Mode:** <Single-pass | Two-pass contract-first>

## Objective & Scope

**Objective:** <Concrete outcome this phase must produce>  
**Inputs:** <Approved final truth, roadmap items, contracts, and prior outputs>  
**In Scope:** <Bounded implementation areas and deliverables>  
**Out of Scope / Do Not Do Yet:** <Explicit exclusions>  
**Expected Deliverables:** <Files, behaviors, or other outcomes>

## Execution Constraints

- **Implementation Scope:** <Approved areas this phase may create or modify, or `Not prescribed`>
- **Approved Boundaries:** <Relevant approved boundaries, or `None`>
- **Durable Contracts:** <APIs, schemas, protocols, formats, extension points, or integrations established or
  changed by this phase, or `None`>
- **Human Review Focus:** <What must be reviewed at the next gate, or `None`>

Do not invent seams, interfaces, abstraction layers, dependency rules, module boundaries, or validation work to
populate this section.

## Ordered Work

<!--
TEMPLATE INSTRUCTION: Retain exactly one mode structure below. Delete the unused structure and every template
instruction or placeholder when instantiating this plan. A single-pass plan must not contain Pass A or Pass B
labels. A two-pass plan must retain the contract-review stop between Pass A and Pass B.
-->

<!-- SINGLE-PASS STRUCTURE: delete this marker and the entire two-pass structure when selected. -->

### Implementation

- **Step 1 — <Name>:** <Goal> | **Files:** <Paths> | **Done:** <Observable condition>
- **Step 2 — <Name>:** <Goal> | **Files:** <Paths> | **Done:** <Observable condition>

<!-- TWO-PASS STRUCTURE: delete this marker and the entire single-pass structure when selected. -->

### Pass A: Contract

- **Step A1 — <Name>:** <Review-surface goal> | **Files:** <Paths> | **Done:** <Observable condition>
- **Step A2 — <Name>:** <Review-surface goal> | **Files:** <Paths> | **Done:** <Observable condition>

Pass A produces the smallest useful native contract surface, relevant approved constraints, and only the tests,
examples, schemas, or other artifacts that materially improve review. For code contracts, source and contract-test
source must compile before review. Behavior may remain intentionally unimplemented; behavior-focused tests may
fail or remain disabled when this plan says so. Concrete types are valid contract surfaces. Do not require prose,
interfaces, builders, adapters, dependency injection, or other abstraction merely to formalize the gate.

**Contract Review Stop:** Reconcile actual final-truth impact and execution memory, then stop for human approval
before Pass B.

### Pass B: Implementation

- **Step B1 — <Name>:** <Goal> | **Files:** <Paths> | **Done:** <Observable condition>
- **Step B2 — <Name>:** <Goal> | **Files:** <Paths> | **Done:** <Observable condition>

Pass B may change test fixtures, helpers, imports, construction, and other plumbing without renewed review when
approved scenarios, inputs, observable outcomes, and failure expectations remain materially unchanged. Before
completion, enable every approved expectation and make all approved contract tests pass. Return to contract review
before weakening, removing, contradicting, or materially changing an approved expectation.

## Validation & Done Criteria

- **Validation Strategy:** <Tests, builds, static checks, scenarios, or manual verification>
- **Architecture / Contract Validation:** <Checks for approved boundaries or contracts, or `None`>
- **Definition of Done:** <Concrete completion conditions; for two-pass, include faithful implementation of the
  approved contract>

## Context & Wrap-up

- **Dependencies:** <Known dependencies, or `None`>
- **Risks:** <Material execution risks, or `None`>
- **Open Questions:** <Prioritized active questions, or `None`>
- **Completion Summary:** *(Fill when done; replace stale execution detail)* **Outcome:** <Result> |
  **Unlocked:** <Next capability>

## Maintenance Rules

- Treat this file as agent-owned active execution memory, not product or architecture truth.
- Keep `agent_plan.md` roadmap-level; do not duplicate this plan's detailed sequencing there.
- Keep `agent_state.md`, `agent_plan.md`, and this plan aligned for phase, mode, plan status, pass, review state,
  readiness, blockers, and exact next step.
- Preserve approved project final truth, contracts, and boundaries during execution.
- Do not introduce interfaces, adapters, builders, abstraction layers, dependency constraints, or other structure
  merely to satisfy Bonsai workflow.
- Follow project conventions and relevant source, developer-context, and agent-context guidance for implementation
  and testing style.
- If required behavior conflicts with approved final truth or a durable contract, stop for phase-plan correction,
  final-truth reconciliation, or renewed contract review as applicable.
- Set `Plan Status: Ready for Review` only when drafting is complete and approval is required. Set `Approved` only
  after explicit human approval.
- Reconcile execution memory whenever a gate or current execution fact changes. Correct a stale or inconsistent
  plan before substantive execution continues.
- Compress completed detail when it no longer helps resumption; preserve only enough summary to explain the
  outcome and next capability.
