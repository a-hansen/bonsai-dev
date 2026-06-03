# Phase Execution Skill

## Purpose

Handle phase activation, execution-mode selection, detailed phase planning, contract-first gates, module-boundary discipline, and review gates during an implementation session.

This skill is subordinate to `implementation_prompt.md`. Apply its execution rules, final-truth reconciliation rules, and maintenance discipline throughout.

## Required Inputs

Before executing this skill, inspect the project memory needed for the current step:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`
* Active `plan/plan_phase_<N>.md`, when one exists
* The approved contract, approved dry-run baseline, or recorded exact next step, when applicable
* Any relevant maps or developer context needed to understand execution constraints

Do not treat missing optional files as permission to guess. Surface missing or inconsistent project memory before substantive execution.

## Phase Execution Mode Assessment

When activating a new phase, or when the current active phase has not yet had its execution mode resolved, determine whether it should use:

* **Single-pass execution**, when the phase:

    * implements already-approved behavior,
    * is bounded and localized,
    * has a clear implementation direction,
    * does not materially shape downstream design,
    * does not establish or reshape important module boundaries, and
    * can be safely reviewed after code and tests are produced.

* **Two-pass contract-first execution**, when the phase:

    * introduces or materially reshapes a public API,
    * defines or changes a schema, persistent format, protocol, extension contract, or integration surface,
    * establishes an important abstraction or subsystem boundary,
    * establishes or changes human-digestible module boundaries,
    * changes dependency direction or cross-module seams,
    * changes rebuild-relevant structure that later phases will rely on,
    * creates a high-leverage design surface where human review before full implementation is valuable, or
    * is otherwise likely to become costly to reverse after implementation begins.

## Visible Mode Recommendation

If the phase execution mode is unresolved at startup, state the recommended mode and one-sentence rationale in the Startup Gate summary.

Do not resolve the mode, update files, or proceed into planning until the user explicitly asks you to continue.

## Module Boundary Assessment

When activating a phase, creating a phase plan, correcting a phase plan, or entering Pass A, identify whether the phase creates, modifies, or depends on important module boundaries.

Assess:

* **Modules in scope:** modules, subsystems, packages, layers, or implementation areas this phase may create or modify.
* **Modules out of scope:** modules, subsystems, packages, layers, or implementation areas this phase must not modify.
* **Public seams:** APIs, interfaces, schemas, contracts, message formats, entry points, extension points, or externally consumed behaviors.
* **Internal seams:** private implementation boundaries that should remain human-digestible even if they are not public API.
* **Dependency direction:** which modules may depend on which other modules.
* **Forbidden coupling:** dependencies, shortcuts, mixed responsibilities, or convenience access that would make the implementation harder to inspect or rebuild.

If the required module shape is unclear and materially affects architecture, phase planning, or the next implementation step, treat it as a blocker for substantive execution.

Classify the issue as one of:

1. Phase plan correction
2. Architecture clarification
3. Architecture revision
4. Icebox observation

Use final-truth reconciliation when the issue changes or clarifies `requirements.md`, `architecture.md`, or lower-layer final-truth documents.

## Phase Plan Creation

When activating a new phase, determine whether that phase needs a detailed `plan/plan_phase_<N>.md`.

Create one before substantive phase execution when the phase:

* is complex enough to need ordered sequencing,
* uses two-pass contract-first execution,
* has multiple review or validation gates,
* needs explicit module-scope control,
* creates or changes public seams,
* creates or changes important internal module boundaries,
* changes dependency direction or cross-module seams, or
* would otherwise bloat `plan.md`.

Update `plan.md` and `state.md` to reflect the resolved execution mode and the phase plan path when one is created.

## Missing or Incomplete Phase Plans

* **Missing Phase Plan:** If the current active phase appears to require a detailed `plan/plan_phase_<N>.md` but none exists, treat drafting that phase plan as the exact next step before substantive phase execution. After drafting it, use the Phase Plan Approval Gate.

* **Incomplete Existing Phase Plan:** If `plan/plan_phase_<N>.md` already exists but is incomplete, stale, or inconsistent with the current approved project direction, treat completing or correcting that phase plan as the exact next step before substantive phase execution. Do not duplicate partial phase detail in `plan.md`. After updating it, use the Phase Plan Approval Gate.

* **Unresolved Phase Mode:** If the current active phase has not yet had its execution mode resolved, treat determining the mode, updating roadmap/state, and drafting any required phase plan as the exact next step before substantive phase execution. After that planning update, use the Phase Plan Approval Gate when a phase plan was created or materially changed; otherwise complete the step normally.

## Phase Plan Content Requirements

When drafting or materially correcting a phase plan, include module-boundary detail whenever it is relevant to the phase.

A phase plan should identify:

* modules in scope,
* modules out of scope,
* boundary rules,
* public seams or contracts,
* internal seams that need to remain human-digestible,
* dependency direction,
* forbidden coupling,
* validation strategy,
* module-boundary validation, and
* human review focus.

Do not invent module boundaries merely to fill a template. If the phase does not require meaningful module-scope control, say `None` or keep the plan lightweight.

If module boundaries are required but unresolved, preserve the question in the phase plan and treat resolution as part of the next gate before implementation.

## Phase Plan Approval Gate

After creating or materially correcting a phase plan, STOP.

State:

* Final-truth impact: `None`, `Clarification`, or `Revision`.
* Affected final-truth documents, when impact is not `None`.
* Any final-truth update required before the next planned pass.
* Module-boundary impact: `None`, `Uses existing boundaries`, `Clarifies boundaries`, or `Changes boundaries`.
* Human review focus for module shape, when module-boundary impact is not `None`.

For an unresolved `Revision`, use the Final-Truth Reconciliation choices from `implementation_prompt.md` instead of authorizing the next planned pass.

Otherwise present:

1. Approve the phase plan. Record approval and the exact next step for the next planned pass in `state.md`, provide the canonical fresh-session prompt, then terminate this session.
2. Request revisions to the phase plan in this session.
3. Discuss concerns before deciding.
4. Return to roadmap-level planning.

After phase-plan approval, do not begin the next planned pass in this session unless the human explicitly requests continuation here.

## Two-Pass Contract Gate

If Pass A is active:

1. Build the reviewable API shape, structural contract, or design surface.
2. Build or identify the module seams, subsystem boundaries, dependency rules, or review anchors the phase relies on, when relevant.
3. Create behavioral tests, usage examples, or equivalent review artifacts that make intended behavior concrete.
4. Classify final-truth impact and identify affected final-truth documents, when any.
5. Classify module-boundary impact and identify the review focus, when any.
6. STOP before Pass B.

Do not begin Pass B until the contract is approved and any `Revision` is reflected in approved final truth.

For an unresolved `Revision`, use the Final-Truth Reconciliation choices from `implementation_prompt.md` instead of authorizing Pass B.

Otherwise present:

1. Approve the contract. Record approval and the exact next step for Pass B implementation in `state.md`, provide the canonical fresh-session prompt, then terminate this session.
2. Approve the contract and require an implementation dry run first. Record the approved dry-run next step in `state.md`, provide the canonical fresh-session prompt, then terminate this session.
3. Request revisions to the contract in this session.
4. Return to the phase plan.

After contract approval, do not begin Pass B or its dry run in this session unless the human explicitly requests continuation here.

## Modular Implementation Discipline

During Pass A, make important module seams reviewable before implementation begins.

During Pass B or single-pass execution:

* Preserve the approved module scope and boundary rules.
* Attach new behavior to the smallest appropriate module.
* Keep domain, protocol, runtime, persistence, adapter, UI, and infrastructure responsibilities separated according to approved architecture.
* Route cross-module behavior through approved public seams or explicit internal seams.
* Do not collapse responsibilities into convenience classes.
* Do not introduce new dependencies outside the approved dependency direction.
* Do not add shortcuts from lower-level modules to higher-level adapters, UI, framework objects, or environment-specific concerns unless approved architecture allows it.
* Do not move behavior across module boundaries merely because it is locally convenient.

If required behavior does not fit the approved module structure, STOP before changing the structure.

Classify the issue as one of:

1. Phase plan correction
2. Architecture clarification
3. Architecture revision
4. Icebox observation

Use final-truth reconciliation when the issue clarifies or changes approved final truth.

## Module Boundary Validation

At review gates and step completion, report whether module boundaries held.

Include:

* modules created or modified,
* public seams created or modified,
* internal seams created or modified when materially relevant,
* dependency direction preserved or changed,
* boundary violations avoided,
* any boundary issue moved to `icebox.md`, and
* any architecture clarification or revision required.

Do not over-report trivial file organization changes. Report module-boundary impact only when it affects human readability, public contracts, dependency direction, rebuildability, or future phase work.

## Fresh Session Startup Prompt

When a gate option terminates the session and continues in a clean session, the response must include the canonical fresh-session prompt only:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

Before providing that prompt, record all next-step, approval, phase, pass, dry-run, required-skill, module-boundary, and stop-condition details in `state.md` and any required planning documents.

Do not embed those details in the fresh-session prompt.

## Stop Conditions

STOP and ask for human direction when:

* phase execution mode is unresolved and the user has not authorized planning,
* a required phase plan is missing, stale, or inconsistent,
* a phase plan has been created or materially corrected,
* required module boundaries or dependency direction are unclear and materially affect the next step,
* Pass A has produced a contract package,
* actual work requires a `Revision` to final-truth documents,
* actual work requires unapproved module-boundary changes,
* the requested next step exceeds the approved phase plan, contract, dry-run baseline, or recorded exact next step,
* the user selects a terminate-session option.
