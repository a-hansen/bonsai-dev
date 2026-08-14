# AI Plan

**Project:** Task Tracker
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** First establish the core task behavior contract and behavior-focused tests through a two-pass contract-first phase. The human-owned requirements and architecture already settle the example's identifier semantics, list ordering, CLI vocabulary, and persistence model, so implementation planning should apply those decisions rather than reopen them. After the core contract is approved and implemented, add the command-line interaction layer, then implement the settled local JSON persistence and complete executable packaging validation.

## Roadmap

### Phase Summaries

1. **Task Behavior Contract:** <Define the task model, task operations, reviewable API/structure, and behavior-focused tests before implementation> | **Mode:** Two-pass contract-first |
   **Status:** Active |
   **Plan:** None
2. **CLI Interaction Layer:** <Implement the settled command-line vocabulary for invoking task operations and presenting results> | **Mode:** Single-pass |
   **Status:** Pending |
   **Plan:** None
3. **Persistence & Executable Packaging Completion:** <Implement the settled local JSON persistence model, retain next-identifier state between runs, finalize executable JAR behavior, and complete end-to-end validation> | **Mode:** Single-pass |
   **Status:** Pending |
   **Plan:** None

## Active Phase Detail

No detailed active phase plan has been created yet.

## Deferred & Completed

* **Deferred:** [CLI implementation until Phase 2, Concrete JSON storage implementation and end-to-end executable JAR validation until Phase 3]
* **Completed:** [Project requirements and architecture decisions, including identifier semantics, list ordering, CLI vocabulary, and persistence model]

## Maintenance Rules

* Keep this file focused on the durable execution roadmap, not current-session handoff details.
* Current session status, exact next action, and recommended AI level belong in `state.md`.
* Add a separate `plan_phase_<N>.md` when a phase requires deep sequencing, two-pass execution, or enough detail that it would bloat this file.
* Compress completed phase detail aggressively once it no longer helps execution.
* Treat settled human-owned requirements and architecture as constraints during planning. Do not convert settled design choices back into implementation-time open questions.
