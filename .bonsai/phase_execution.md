# Phase Execution Procedure

## Purpose

Handle phase activation, execution-mode selection, detailed phase planning, and contract-first gates during an implementation session.

## When to Read

Read this file when:

* Activating a new phase.
* The active phase execution mode is unresolved.
* A detailed `plan/plan_phase_<N>.md` may need to be created or materially corrected.
* Pass A of a two-pass contract-first phase is active.
* The exact next step requires a phase-plan or contract approval gate.

This procedure is subordinate to `implementation_prompt.md`. Apply its execution rules, final-truth reconciliation rules, and maintenance discipline throughout.

## Phase Execution Mode Assessment

When activating a new phase, or when the current active phase has not yet had its execution mode resolved, determine whether it should use:

* **Single-pass execution**, when the phase:

    * implements already-approved behavior,
    * is bounded and localized,
    * has a clear implementation direction,
    * does not materially shape downstream design, and
    * can be safely reviewed after code and tests are produced.

* **Two-pass contract-first execution**, when the phase:

    * introduces or materially reshapes a public API,
    * defines or changes a schema, persistent format, protocol, extension contract, or integration surface,
    * establishes an important abstraction or subsystem boundary,
    * changes rebuild-relevant structure that later phases will rely on,
    * creates a high-leverage design surface where human review before full implementation is valuable, or
    * is otherwise likely to become costly to reverse after implementation begins.

## Visible Mode Recommendation

If the phase execution mode is unresolved at startup, state the recommended mode and one-sentence rationale in the Startup Gate summary.

Do not resolve the mode, update files, or proceed into planning until the user explicitly asks you to continue.

## Phase Plan Creation

When activating a new phase, determine whether that phase needs a detailed `plan/plan_phase_<N>.md`. Create one before substantive phase execution when the phase:

* is complex enough to need ordered sequencing,
* uses two-pass contract-first execution,
* has multiple review or validation gates, or
* would otherwise bloat `plan.md`.

Update `plan.md` and `state.md` to reflect the resolved execution mode and the phase plan path when one is created.

## Missing or Incomplete Phase Plans

* **Missing Phase Plan:** If the current active phase appears to require a detailed `plan/plan_phase_<N>.md` but none exists, treat drafting that phase plan as the exact next step before substantive phase execution. After drafting it, use the Phase Plan Approval Gate.

* **Incomplete Existing Phase Plan:** If `plan/plan_phase_<N>.md` already exists but is incomplete, stale, or inconsistent with the current approved project direction, treat completing or correcting that phase plan as the exact next step before substantive phase execution. Do not duplicate partial phase detail in `plan.md`. After updating it, use the Phase Plan Approval Gate.

* **Unresolved Phase Mode:** If the current active phase has not yet had its execution mode resolved, treat determining the mode, updating roadmap/state, and drafting any required phase plan as the exact next step before substantive phase execution. After that planning update, use the Phase Plan Approval Gate when a phase plan was created or materially changed; otherwise complete the step normally.

## Phase Plan Approval Gate

After creating or materially correcting a phase plan, STOP.

State:

* Final-truth impact: `None`, `Clarification`, or `Revision`.
* Affected final-truth documents, when impact is not `None`.
* Any final-truth update required before the next planned pass.

For an unresolved `Revision`, use the Final-Truth Reconciliation choices from `implementation_prompt.md` instead of authorizing the next planned pass.

Otherwise present:

1. Approve the phase plan. Record approval and the exact next step for the next planned pass, provide the startup instruction for a fresh session, then terminate this session.
2. Request revisions to the phase plan in this session.
3. Discuss concerns before deciding.
4. Return to roadmap-level planning.

After phase-plan approval, do not begin the next planned pass in this session unless the human explicitly requests continuation here.

## Two-Pass Contract Gate

If Pass A is active:

1. Build the API shape and behavioral tests or usage examples.
2. Classify final-truth impact and identify affected final-truth documents, when any.
3. STOP before Pass B.

Do not begin Pass B until the contract is approved and any `Revision` is reflected in approved final truth.

For an unresolved `Revision`, use the Final-Truth Reconciliation choices from `implementation_prompt.md` instead of authorizing Pass B.

Otherwise present:

1. Approve the contract. Record approval and the exact next step for Pass B implementation, provide the startup instruction for a fresh session, then terminate this session.
2. Approve the contract and require an implementation dry run first. Record the approved dry-run next step, provide the startup instruction for a fresh session, then terminate this session.
3. Request revisions to the contract in this session.
4. Return to the phase plan.

After contract approval, do not begin Pass B or its dry run in this session unless the human explicitly requests continuation here.
