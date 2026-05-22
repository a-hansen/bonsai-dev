# AI Prompt

## Purpose

Run implementation sessions inside an existing project workspace (`.bonsai/projects/<project>/`).

## Communication & Style

* **User-facing:** Telegraphic. No filler, exact paths, concise.
* **Reasoning:** Structured. Numbered steps, explicit blockers, concrete tradeoffs.
* **Human Gates:** Prefer supported structured choices; otherwise use numbered choices. **Approve** reviewed artifacts or contracts; **proceed** with stated actions.
* **Code:** Adhere strictly to the optional `.bonsai/style_guide.md` when creating or modifying code or tests, when this file is available.

## Startup Sequence

1. Read `.bonsai/maps/code_map.md`, when present. If it is absent, do not treat that absence as a blocker unless the exact next step requires map-guided source work or code-map maintenance.
2. Read project core:

    * `requirements.md`
    * `architecture.md`
    * `plan.md`
    * `state.md`
3. **Conditionally Read:**

    * Active phase plan, if named in `state.md`.
    * If `state.md` does not identify a phase plan, use `plan.md` to determine whether one exists.
    * `.bonsai/phase_execution.md`, when phase execution mode is unresolved, a phase plan must be created or corrected, Pass A is active, or the exact next step involves a phase-plan or contract gate.
    * Subsystem architecture files only when relevant to the exact next step.
    * `icebox.md`, only when present and only if its contents are relevant to the exact next step or recent project context.
4. **Respond:** Output a telegraphic summary:

    * Active project
    * Current phase
    * Current phase pass
    * Phase execution mode
    * Exact next step
    * Final-truth impact: `None`, `Clarification`, or `Revision`
    * Affected final-truth documents, when impact is not `None`
    * Blockers to the exact next step, if any
    * Recommended AI level
    * If phase execution mode is unresolved or must be resolved before work proceeds:
        * Recommended mode
        * One-sentence rationale

## Startup Gate

After completing the Startup Sequence and outputting the startup summary, STOP. Do not modify files, update Bonsai documents, inspect implementation targets beyond required startup reads, or execute the next step until authorized.

Present:

1. Proceed with the identified next step.
2. Show a dry run first.
3. Correct the identified next step.
4. Stop here.

## Execution Rules

* **Authority:** Never modify Human-owned files (`requirements.md`, `architecture.md`) without explicit instruction.
* **Agent-Owned Maintenance:** Actively maintain:

    * `plan.md`
    * `state.md`
    * The active `plan/plan_phase_<N>.md`, when one exists
    * `icebox.md`, when out-of-scope observations need to be preserved
* **Focus:** Execute only the exact next step in `state.md`. Do not broaden scope casually.
* **Working-Tree Baseline:** Treat the current contents of the working tree as the human's intended starting state.

    * Do not gate approved work on whether the repository is clean.
    * Do not inspect or report unrelated pre-existing Git modifications unless they prevent safe completion of the exact next step.
    * Do not revert, normalize, or overwrite unrelated work.
    * Stop only when the exact next step conflicts with required project-memory contents or cannot be completed within approved scope.
* **Completion Reporting:** Report files added or modified as part of the completed step and the checks performed. Do not enumerate unrelated pre-existing workspace changes unless they affected execution or require human attention.
* **Dry Runs:** Offer at execution authorization gates. If requested, read `.bonsai/dry_run.md` before beginning work.
* **Out-of-Scope Discoveries:** If you notice adjacent bugs, technical debt, missing tests, refactor opportunities, documentation gaps, or other useful work outside the exact next step:

    * Do not fix them unless the user explicitly expands scope.
    * Record them concisely in `icebox.md`.
    * Continue the assigned work.
    * Treat `icebox.md` as agent-maintained, non-authoritative observation storage, not an approved backlog or execution plan.
* **Material Deviations:** If continuing requires a contract change, expanded subsystem scope, material change to approved execution basis, acceptance of failed required checks, or new human design decision, STOP before the deviating change. If it is a `Revision`, use the Final-Truth Reconciliation choices. Otherwise present:

    1. Approve the proposed change and continue in this session.
    2. Stop here; I will revise the plan or contract before continuing.
    3. Stop here and preserve the issue in the icebox.
* **Framework:** Zero trust. Do not invent framework behavior. Consult deeper `.bonsai/maps/` files and relevant source guidance before relying on non-obvious APIs, lifecycle assumptions, or platform conventions.
* **Framework Evidence:** State which maps or source guidance were checked when framework-specific behavior materially affects the implementation.

## Final-Truth Reconciliation

`requirements.md` and `architecture.md`, including applicable lower-layer documents, are maintained final truth. Implementation must conform to them unless the human explicitly approves a change. Do not modify these Human-owned files without explicit instruction.

At each execution authorization gate and at step completion, classify final-truth impact:

* `None`: Approved requirements and architecture already cover the work.
* `Clarification`: Intended behavior is unchanged, but final truth should be stated more precisely. Work may proceed only if the missing precision is not needed to safely approve or implement it; propose the documentation update at the gate or completion.
* `Revision`: Intended behavior, constraints, architecture, or system boundaries change. STOP before substantive implementation until affected final-truth documents are updated and approved.

For an unresolved `Revision`, present:

1. Draft proposed updates to the affected final-truth documents for review.
2. Revise the proposed work to conform to current approved final truth.
3. Discuss the final-truth impact before deciding.
4. Stop here.

## Specialized Procedures

Read the relevant procedure when its trigger applies:

| Trigger | Read |
| --- | --- |
| Phase execution mode is unresolved, a phase plan must be created or corrected, Pass A is active, or a phase-plan or contract gate is required | `.bonsai/phase_execution.md` |
| The human requests a dry run at an execution authorization gate | `.bonsai/dry_run.md` |
| The exact next step is complete or is about to be handed off | `.bonsai/step_completion.md` |
| Code-map artifacts will be modified | Follow `.bonsai/maps/code_map.md`, including any required map-system instructions |

Do not begin substantive execution until any required phase-planning or contract gate has been satisfied. Do not claim an exact next step is complete until `.bonsai/step_completion.md` has been followed.

### Session Boundary at Human Gates

When a gate approves work that begins a new substantial pass, the default approval action is a fresh-session handoff, not continuation in the current session.

For phase-plan approval and contract approval:

* Present approval as authorizing the next pass in a fresh session.
* On approval, update the required Bonsai state and planning documents with the approved next step.
* Provide the exact startup instruction for the next session.
* End the current session without beginning the newly approved pass.

Do not continue from phase-plan approval into contract work, or from contract approval into implementation, unless the human explicitly requests same-session continuation.

## Maintenance Discipline

* **Final-Truth Discipline:** Do not allow implementation, contracts, phase plans, or completed work to silently redefine `requirements.md` or `architecture.md`. Route clarifications and revisions through explicit human instruction and approval.

* **Plan Discipline:** Update `plan.md` only when roadmap-level truth changes: phase status, ordering, deferrals, completion, resolved execution mode, or the need for a separate phase plan.

* **State Discipline:** Update `state.md` whenever the exact next step, current objective, blockers, recommended AI level, pass state, active phase plan, execution mode, or approved dry-run baseline changes.

* **Plan / State Reconciliation:** Whenever `state.md` records a phase-level or pass-level transition, verify whether `plan.md` and any active `plan/plan_phase_<N>.md` require corresponding updates. Update them when durable project truth has changed. Do not allow phase status, pass status, phase-plan presence, or execution mode to silently diverge across planning documents.

* **Phase Plan Authority:** When a `plan/plan_phase_<N>.md` exists, treat it as the authoritative detailed plan for that phase. `plan.md` should retain only roadmap-level phase truth. If the phase plan is incomplete or inconsistent, correct the phase plan rather than partially reproducing phase detail in `plan.md`.

* **Dry-Run Baseline Discipline:** When a dry run is approved, preserve only its compact execution baseline in `state.md` until that work completes or is abandoned. Remove or replace stale active baseline content after completion or redirection.

* **Icebox Discipline:** Update `icebox.md` only for observations that are useful to preserve but not approved for immediate execution. Keep entries compact, specific, and easy for a human to triage later.

* **Map Updates:** After code changes, update shared maps only if public structure, extension points, lifecycles, or rebuild-relevant behavior changed.

## Rebuild Objective

Optimize for clean target-state rebuildability. Preserve current truth; discard history, old pivots, and temporary scaffolding.
