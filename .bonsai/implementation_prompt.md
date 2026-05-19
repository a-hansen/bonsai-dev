# AI Prompt

## Purpose

Run implementation sessions inside an existing project workspace (`.bonsai/projects/<project>/`).

## Communication & Style

* **User-facing:** Telegraphic. No filler, exact paths, concise.
* **Reasoning:** Structured. Numbered steps, explicit blockers, concrete tradeoffs.
* **Code:** Adhere strictly to the optional `.bonsai/style_guide.md` when creating or modifying code or tests, when this file is available.

## Startup Sequence

1. Read `.bonsai/maps/code_map.md`.
2. Read project core:

    * `requirements.md`
    * `architecture.md`
    * `plan.md`
    * `state.md`
3. **Conditionally Read:**

    * Active phase plan, if named in `state.md`.
    * If `state.md` does not identify a phase plan, use `plan.md` to determine whether one
      exists.
    * Subsystem architecture files only when relevant to the exact next step.
    * `icebox.md`, only when present and only if its contents are relevant to the exact next step
      or recent project context.
4. **Respond:** Output a telegraphic summary:

    * Active project
    * Current phase
    * Current phase pass
    * Exact next step
    * Blockers
    * Recommended AI level

## Startup Gate

After completing the Startup Sequence and outputting the startup summary, STOP.
Do not modify files, update Bonsai documents, inspect implementation targets
beyond the required startup reads, or execute the next step until the user
explicitly asks you to proceed.

## Execution Rules

* **Authority:** Never modify Human-owned files (`requirements.md`, `architecture.md`) without
  explicit instruction.
* **Agent-Owned Maintenance:** Actively maintain:

    * `plan.md`
    * `state.md`
    * The active `plan/plan_phase_<N>.md`, when one exists
    * `icebox.md`, when out-of-scope observations need to be preserved
* **Focus:** Execute only the exact next step in `state.md`. Do not broaden scope casually.
* **Out-of-Scope Discoveries:** If you notice adjacent bugs, technical debt, missing tests,
  refactor opportunities, documentation gaps, or other useful work outside the exact next step:

    * Do not fix them unless the user explicitly expands scope.
    * Record them concisely in `icebox.md`.
    * Continue the assigned work.
    * Treat `icebox.md` as agent-maintained, non-authoritative observation storage, not an approved
      backlog or execution plan.
* **Framework:** Zero trust. Do not invent framework behavior. Consult deeper `.bonsai/maps/` files
  and relevant source guidance before relying on non-obvious APIs, lifecycle assumptions, or
  platform conventions.
* **Framework Evidence:** State which maps or source guidance were checked when framework-specific
  behavior materially affects the implementation.

## Phase Activation & Planning

* **Phase Execution Mode Assessment:** When activating a new phase, or when the current active phase
  has not yet had its execution mode resolved, determine whether it should use:

    * **Single-pass execution**, for bounded work whose implementation direction is already clear, or
    * **Two-pass contract-first execution**, when the phase introduces or materially reshapes a
      public API, important abstraction, subsystem boundary, extension contract, rebuild-relevant
      structure, or other high-leverage design surface that merits human review before full
      implementation.

* **Phase Plan Creation:** When activating a new phase, determine whether that phase needs a detailed
  `plan/plan_phase_<N>.md`. Create one before substantive phase execution when the phase:

    * is complex enough to need ordered sequencing,
    * uses two-pass contract-first execution,
    * has multiple review or validation gates, or
    * would otherwise bloat `plan.md`.

  Update `plan.md` and `state.md` to reflect the resolved execution mode and the phase plan path when
  one is created.

* **Missing Phase Plan:** If the current active phase appears to require a detailed
  `plan/plan_phase_<N>.md` but none exists, treat drafting that phase plan as the exact next step before
  substantive phase execution. After drafting it, STOP for human review before proceeding with
  implementation work.

* **Unresolved Phase Mode:** If the current active phase has not yet had its execution mode resolved,
  treat determining the mode, updating roadmap/state, and drafting any required phase plan as the
  exact next step before substantive phase execution. After that planning update, STOP for human
  review before proceeding with implementation work.

* **Two-Pass Gates:** If Pass A is active, build the API shape and behavioral tests or usage examples,
  then STOP for human review. Do not begin Pass B until the contract is approved.

## Maintenance Discipline

* **Plan Discipline:** Update `plan.md` only when roadmap-level truth changes: phase status,
  ordering, deferrals, completion, resolved execution mode, or the need for a separate phase plan.
* **State Discipline:** Update `state.md` whenever the exact next step, current objective,
  blockers, recommended AI level, pass state, active phase plan, or execution mode changes.
* **Icebox Discipline:** Update `icebox.md` only for observations that are useful to preserve but
  not approved for immediate execution. Keep entries compact, specific, and easy for a human to
  triage later.
* **Map Updates:** After code changes, update shared maps only if public structure, extension
  points, lifecycles, or rebuild-relevant behavior changed.

## Rebuild Objective

Optimize for clean target-state rebuildability. Preserve current truth; discard history, old pivots,
and temporary scaffolding.