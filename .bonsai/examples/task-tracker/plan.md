# AI Plan

**Project:** Task Tracker
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** First establish the core task behavior contract and behavior-focused tests through a two-pass contract-first phase. This prevents later CLI and persistence work from hardening an unreviewed API shape. After that contract is approved and implemented, add the command-line interaction layer, then complete local persistence and executable packaging validation.

## Roadmap

### Phase Summaries

1. **Task Behavior Contract:** <Define the task model, task operations, reviewable API/structure, and behavior-focused tests before implementation> | **Mode:** Two-pass contract-first |
   **Status:** Active |
   **Plan:** `plan_phase_1.md`
2. **CLI Interaction Layer:** <Implement the Java CLI workflow for invoking task operations and presenting results> | **Mode:** Single-pass |
   **Status:** Pending |
   **Plan:** None
3. **Persistence & Executable Packaging Completion:** <Retain tasks between runs, finalize executable JAR behavior, and complete end-to-end validation> | **Mode:** Single-pass |
   **Status:** Pending |
   **Plan:** None

## Active Phase Detail

See active phase plan file.

## Deferred & Completed

* **Deferred:** [Exact CLI command syntax, Local persistence format, Task identifier format, End-to-end executable JAR validation until the packaging phase]
* **Completed:** [None]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, and recommended AI level belong in `state.md`.
* Add a separate `plan_phase_<N>.md` when a phase requires deep sequencing, two-pass execution,
  or enough detail that it would bloat this file.
* Compress completed phase detail aggressively once it no longer helps execution.