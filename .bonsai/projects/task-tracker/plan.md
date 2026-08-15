# AI Plan

**Project:** Task Tracker  
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** First establish the core task behavior contract and behavior-focused tests through a two-pass contract-first phase. The human-owned requirements and architecture already settle the example's identifier semantics, list ordering, CLI vocabulary, and persistence model, so implementation planning should apply those decisions rather than reopen them. After the core contract is approved and implemented, add the command-line interaction layer, then implement the settled local JSON persistence and complete executable packaging validation.

## Roadmap

### Phase Summaries

1. **Task Behavior Contract:** Define the task model, task operations, reviewable API/structure, and behavior-focused tests before implementation |
   **Mode:** Two-pass contract-first |
   **Status:** Active |
   **Plan:** None |
   **Plan Status:** None
2. **CLI Interaction Layer:** Implement the settled command-line vocabulary for invoking task operations and presenting results |
   **Mode:** Single-pass |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None
3. **Persistence & Executable Packaging Completion:** Implement the settled local JSON persistence model, retain next-identifier state between runs, finalize executable JAR behavior, and complete end-to-end validation |
   **Mode:** Single-pass |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None

## Active Phase Detail

* **Goal:** Establish and implement the approved core task behavior contract while preserving the settled Task Tracker requirements and architecture.
* **Execution Readiness:** Phase planning required
* **Scope:** [Core task model and operations, reviewable source-level contract structure, behavior-focused contract tests or usage examples appropriate to the project, minimal build/test scaffolding needed to compile the Pass A contract package]
* **Approved Constraints:** [Java 17, Gradle Wrapper, JUnit 5, standard single-module Gradle Java layout, settled identifier semantics and ordering, settled CLI vocabulary and persistence model, Pass A contract package including contract-test source must compile before contract review, substantive behavior remains for Pass B]
* **Ordered Steps:**
    1. Draft `plan/plan_phase_1.md` from `.bonsai/templates/plan_phase_template.md` and stop for Phase Plan Approval.
    2. After phase-plan approval, execute Pass A through its contract review gate.
    3. After contract approval, execute Pass B and validate the approved behavioral expectations.
* **Validation:** [Phase plan reviewed and approved before Pass A, Pass A source and contract-test source compile before contract review, approved behavioral expectations are enabled and passing before Phase 1 completes]
* **Done When:** The approved Task Behavior Contract is implemented faithfully, all approved Phase 1 behavioral expectations pass, and the phase is complete with execution memory reconciled for Phase 2.

## Deferred & Completed

* **Deferred:** [CLI implementation until Phase 2, Concrete JSON storage implementation and end-to-end executable JAR validation until Phase 3]
* **Completed:** [Project requirements and architecture decisions, including identifier semantics, list ordering, CLI vocabulary, and persistence model]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, blockers, current pass state, and active dry-run baseline belong in `state.md`.
* Keep phase status, execution mode, phase-plan references, and phase-plan approval state consistent with `state.md`.
* When `state.md` records a phase-level or pass-level transition, verify whether this roadmap also requires a corresponding update.
* Add a separate `plan/plan_phase_<N>.md` when a phase requires detailed sequencing, a durable contract review gate,
  multiple meaningful review or validation gates, or enough execution detail that it would bloat this file.
* Do not create a phase plan merely to document ordinary implementation decomposition.
* When a `plan/plan_phase_<N>.md` file exists, treat it as the authoritative detailed execution plan for that phase.
  Do not partially duplicate phase-level sequencing here.
* If an active phase plan file exists but is incomplete, stale, or inconsistent with current approved
  project direction, update that phase plan rather than expanding `Active Phase Detail`.
* Use `Mode: To determine at activation` when execution mode should be resolved closer to implementation
  rather than guessed prematurely.
* A phase plan marked `Draft` or `Ready for Review` is not implementation authorization.
* A phase plan marked `Approved` has completed its planning gate. If no other blocker or contract gate remains,
  `state.md` should make the next executable step explicit and mark execution readiness accordingly.
* Compress completed phase detail aggressively once it no longer helps execution.
