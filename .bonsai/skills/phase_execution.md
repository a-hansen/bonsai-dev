# Phase Execution Skill

## Purpose

Handle phase activation, execution-mode selection, detailed phase planning, contract-first gates, approved
module-boundary constraints, and review gates during an implementation session.

This skill is subordinate to `implementation_prompt.md`. Apply its execution rules, final-truth
reconciliation rules, invoking-gate return rule, and maintenance discipline throughout.

Bonsai manages project memory and execution workflow. It does not create implementation structure merely
because a phase is being planned or reviewed.

## Required Inputs

Before executing this skill, inspect the project memory needed for the current step:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`
* Active `plan/plan_phase_<N>.md`, when one exists
* The approved contract, approved dry-run baseline, or recorded exact next step, when applicable
* Any relevant maps or developer context needed to understand execution constraints

Do not treat missing optional files as permission to guess. Surface missing or inconsistent project memory
before substantive execution.

## Execution-State Terminology

Use pass labels only when they describe the actual workflow.

* For single-pass execution, use `Current Phase Pass: Single-pass Implementation`.
* Reserve `Pass A (Contract)`, `Contract Review`, and `Pass B (Implementation)` for actual two-pass
  contract-first phases.
* Never represent a single-pass phase as Pass B.

## Phase Execution Mode Assessment

When activating a new phase, or when the current active phase has not yet had its execution mode resolved,
determine whether it should use:

* **Single-pass execution**, as the normal mode when the phase can be implemented and reviewed without first
  approving a separate durable contract.

* **Two-pass contract-first execution**, only when the phase establishes or materially changes a durable
  contract or design surface that independently merits human approval before implementation continues.

Examples that can justify two-pass contract-first execution include:

* an externally consumed API,
* a schema or persistent format,
* a protocol or message contract,
* an extension or plugin contract,
* an integration surface, or
* another durable project-specific contract that downstream code or external consumers will rely on and
  that independently merits a human review gate.

Do not select two-pass contract-first execution merely because the phase:

* is large or complex,
* touches multiple modules or packages,
* creates new classes,
* introduces internal helpers or abstractions,
* creates or changes internal module organization,
* changes implementation dependency structure that is not itself an approved durable contract,
* needs tests,
* has multiple implementation concerns,
* would benefit from ordinary code review, or
* contains a high-leverage implementation decision that does not independently require contract approval.

Existing approved contracts do not require a redundant Bonsai contract gate. If the contract that governs the
phase has already been explicitly approved outside the current Bonsai pass, the phase may use single-pass
execution unless it is establishing or materially changing another review-worthy durable contract.

A Bonsai contract gate must not force Java interfaces, builders, adapters, dependency-injection layers,
abstract base types, module seams, or other implementation indirection. Those structures exist only when
approved project truth or the implementation itself genuinely requires them.

## Visible Mode Recommendation

If the phase execution mode is unresolved at startup, state the recommended mode and one-sentence rationale
in the Startup Gate summary.

Do not resolve the mode, update files, or proceed into planning until the human explicitly asks you to continue.

## Approved Boundary Assessment

When activating a phase, creating or correcting a phase plan, or entering Pass A, identify only the module or
dependency boundaries that are already part of approved project truth or are necessary to interpret an
approved durable contract.

Assess, when relevant:

* **Implementation areas in scope:** modules, subsystems, packages, layers, or areas the phase may create or modify.
* **Implementation areas out of scope:** areas the approved phase must not modify.
* **Durable seams:** approved APIs, schemas, protocols, extension points, integration surfaces, or other contracts.
* **Dependency constraints:** dependency direction explicitly prescribed by approved architecture.
* **Forbidden coupling:** coupling explicitly rejected by approved architecture.

Do not invent internal seams, module boundaries, layering rules, or dependency restrictions merely to make a
phase plan more complete.

If an approved architectural boundary required for the next step is genuinely unclear, classify the issue as
one of:

1. Phase plan correction
2. Architecture clarification
3. Architecture revision
4. Out-of-scope observation

Use final-truth reconciliation when the issue changes or clarifies human-owned final truth.

## Phase Plan Creation

When activating a new phase, determine whether that phase needs a detailed `plan/plan_phase_<N>.md`.

Create one before substantive phase execution when preserving detailed execution-level information outside
`plan.md` materially improves the workflow, such as when the phase:

* uses two-pass contract-first execution and therefore needs an explicit contract review gate,
* requires detailed ordered sequencing that would bloat `plan.md`,
* has multiple meaningful review or validation gates,
* has approved scope or architectural constraints that need to remain visible across several bounded steps, or
* otherwise contains enough execution detail that a dedicated active phase plan materially improves resumption.

Do not create a phase plan merely because a phase is complex in the abstract, touches several files or modules,
creates internal abstractions, or needs ordinary implementation decomposition.

Update `plan.md` and `state.md` to reflect the resolved execution mode and the phase plan path when one is created.
For single-pass phases, set `Current Phase Pass: Single-pass Implementation` when implementation becomes the
active pass state.

## Missing or Incomplete Phase Plans

* **Missing Phase Plan:** If the current active phase genuinely requires a detailed `plan/plan_phase_<N>.md`
  but none exists, treat drafting that phase plan as the exact next step before substantive phase execution.
  After drafting it, use the Phase Plan Approval Gate.

* **Incomplete Existing Phase Plan:** If `plan/plan_phase_<N>.md` already exists but is incomplete, stale, or
  inconsistent with current approved project direction, treat completing or correcting that phase plan as the
  exact next step before substantive phase execution. Do not duplicate partial phase detail in `plan.md`.
  After updating it, use the Phase Plan Approval Gate.

* **Unresolved Phase Mode:** If the current active phase has not yet had its execution mode resolved, treat
  determining the mode, updating roadmap/state, and drafting any genuinely required phase plan as the exact
  next step before substantive phase execution. After that planning update, use the Phase Plan Approval Gate
  when a phase plan was created or materially changed; otherwise complete the planning step normally.

## Phase Plan Content Requirements

When drafting or materially correcting a phase plan, preserve only execution detail that is actually relevant
to the phase.

A phase plan should identify, when applicable:

* implementation scope,
* approved architecture boundaries,
* durable contracts established or changed by the phase,
* ordered work,
* validation strategy,
* meaningful review gates,
* human review focus, and
* active execution questions.

Do not invent internal seams, interfaces, abstraction layers, module boundaries, dependency rules, or validation
work merely to fill a template. Use `None` or `Not prescribed` where the approved project does not prescribe them.

If a required approved boundary or durable contract is unresolved, preserve the question in the phase plan and
route it through the appropriate gate before implementation.

## Phase Plan Approval Gate

After creating or materially correcting a phase plan, STOP before substantive implementation.

State:

* Final-truth impact: `None`, `Clarification`, or `Revision`.
* Affected final-truth documents, when impact is not `None`.
* Any final-truth update required before the next planned work.
* Approved-boundary impact, when relevant.
* Human review focus.

For an unresolved `Revision`, use the Final-Truth Reconciliation choices from `implementation_prompt.md`
instead of authorizing the next planned work.

Otherwise present the phase-plan review choices:

1. Approve the phase plan.
2. Request revisions to the phase plan.
3. Discuss concerns before deciding.
4. Return to roadmap-level planning.

When the human approves the plan:

* mark the plan approved,
* reconcile `plan.md` and `state.md`,
* record the exact next step and execution readiness,
* stop before beginning the newly approved implementation or contract pass unless the human explicitly asks
  to continue in the current session.

After the completed phase-plan gate, present the canonical fresh-session guidance after the current-session
choices as a separate human action. Do not place it inside the numbered gate menu. Bonsai does not terminate,
reset, or create the session.

## Two-Pass Contract Gate

Use this gate only when Pass A is active for an actual two-pass contract-first phase.

Pass A should:

1. Produce the reviewable durable contract or design surface being established or changed.
2. Preserve approved architecture constraints needed to interpret that contract.
3. Produce tests, usage examples, signatures, schemas, message examples, or other review artifacts only when
   they materially clarify the intended contract and fit the project.
4. Classify final-truth impact and identify affected final-truth documents, when any.
5. STOP before Pass B.

Pass A does not require implementation interfaces, builders, adapters, module seams, abstraction layers, or
other indirection unless approved project truth or the contract itself requires them.

Do not begin Pass B until the contract is approved and any required final-truth update is approved and applied.

For an unresolved `Revision`, use the Final-Truth Reconciliation choices from `implementation_prompt.md`
instead of authorizing Pass B.

Otherwise present:

1. Approve the contract.
2. Request revisions to the contract.
3. Discuss concerns before deciding.
4. Return to the phase plan.

After contract approval:

* record the approval,
* set `Current Phase Pass: Pass B (Implementation)`,
* recompute the exact next step and execution readiness,
* stop before Pass B begins unless the human explicitly asks to continue in the current session.

A dry run remains available on request. Do not insert it into the contract menu by default.

After the completed contract gate, present the canonical fresh-session guidance after the current-session
choices as a separate human action. Do not place it inside the numbered gate menu.

## Implementation Discipline

During Pass B or single-pass implementation:

* Preserve approved human-owned project truth.
* Preserve approved contracts.
* Respect module or dependency constraints only when they are part of approved project truth or the approved
  execution basis.
* Execute only the exact next step and approved scope.
* Follow project conventions, developer context, source guidance, and applicable external skills for coding
  and testing style.

Do not use Bonsai itself as justification for adding interfaces, builders, adapters, dependency-injection
layers, abstraction boundaries, module seams, convenience restrictions, or test structure.

If required behavior conflicts with approved project truth or an approved contract, STOP before changing that
truth or contract and route the issue through the appropriate clarification, revision, or planning gate.

## Boundary Validation

At review gates and step completion, report boundary impact only when it materially affects approved
architecture, a durable contract, dependency direction, rebuildability, or future phase work.

When relevant, report:

* approved modules or subsystems materially created or modified,
* durable public seams created or modified,
* approved dependency direction preserved or changed,
* approved boundary violations avoided or discovered, and
* any architecture clarification or revision required.

Do not over-report ordinary file organization or private implementation detail.

## Fresh Session Startup Prompt

After every completed planning or contract gate, the response must provide fresh-session guidance as a separate
human action after the current-session choices. The copyable prompt itself must contain only the canonical
fresh-session prompt:

You can also start a fresh session yourself using:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Do not make this conditional on whether the agent believes a clean session would be useful, and do not place
the fresh-session action inside the numbered gate menu.

Before providing that prompt, record all next-step, approval, phase, pass, dry-run, required-skill, boundary,
and stop-condition details in `state.md` and any required planning documents.

Do not embed those details in the fresh-session prompt. Starting the fresh session is a human action.

## Stop Conditions

STOP and ask for human direction when:

* phase execution mode is unresolved and the human has not authorized planning,
* a genuinely required phase plan is missing, stale, or inconsistent,
* a phase plan has been created or materially corrected and requires approval,
* an approved architectural boundary or durable contract required for the next step is unclear,
* Pass A has produced a contract package,
* actual work requires a `Revision` to final-truth documents,
* actual work requires an unapproved change to a durable contract or approved architecture boundary, or
* the requested next step exceeds the approved phase plan, contract, dry-run baseline, or recorded exact next step.
