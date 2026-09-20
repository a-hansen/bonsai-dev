# Agent Plan

**Project:** Task Tracker
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** Establish the core task behavior contract and behavior-focused tests through a two-pass contract-first phase. Apply the settled identifier, ordering, CLI, and persistence decisions rather than reopening them. After the core contract is approved and implemented, add command-line interaction, then complete local JSON persistence and executable packaging.

## Roadmap

### Phase Summaries

1. **Task Behavior Contract:** Define the task model, operations, reviewable API or structure, and behavior-focused tests before implementation | **Mode:** Two-pass contract-first | **Status:** Active | **Plan:** `None` | **Plan Status:** `None`
2. **CLI Interaction Layer:** Implement the settled command vocabulary and user-facing results | **Mode:** Single-pass | **Status:** Pending | **Plan:** `None` | **Plan Status:** `None`
3. **Persistence and Executable Packaging:** Implement the settled local JSON persistence, retain next-identifier state, finalize executable JAR behavior, and complete end-to-end validation | **Mode:** Single-pass | **Status:** Pending | **Plan:** `None` | **Plan Status:** `None`

## Active Phase Detail

- **Goal:** Establish and implement the approved core task behavior contract.
- **Execution Readiness:** Phase planning required
- **Scope:** Core task model and operations, a reviewable source-level contract, behavior-focused contract tests or usage examples, and the minimal build scaffolding needed to compile the Pass A package.
- **Approved Constraints:** Java 17, Gradle Wrapper, JUnit 5, standard single-module Gradle layout, settled identifiers and ordering, settled CLI and persistence models, a compiling Pass A contract package, and substantive behavior reserved for Pass B.
- **Planning Boundary:** Draft and review `plan/agent_plan_phase_1.md` before substantive implementation.
- **Validation:** Review and approve the phase plan before Pass A; compile Pass A source and contract-test source before contract review; pass approved behavioral expectations before completing Phase 1.
- **Done When:** The approved Task Behavior Contract is implemented, its behavioral expectations pass, and execution memory advances coherently to Phase 2.

## Deferred and Completed

- **Deferred:** CLI implementation until Phase 2; concrete JSON persistence and end-to-end executable JAR validation until Phase 3.
- **Completed:** Project requirements and architecture decisions, including identifier semantics, ordering, CLI vocabulary, and persistence model.

## Maintenance Rules

- Keep this file roadmap-level; detailed sequencing belongs in a warranted phase plan.
- Keep phase, mode, plan identity/status, and readiness consistent with `agent_state.md`.
- Phase 1 always receives a reviewed `plan/agent_plan_phase_1.md` before implementation.
- Later phase plans are conditional, not automatic.
- Preserve current execution truth and compress completed detail.
