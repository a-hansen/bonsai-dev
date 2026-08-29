# AI Plan

**Project:** Bonsai Dev  
**[Meta: Agent-maintained | Active Execution Roadmap | Bonsai 1.4 Bootstrap Truth | Prune Aggressively]**

## Bootstrap Note

This project is using Bonsai 1.4 to build Bonsai 2.0.

While Bonsai 1.4 is the active runtime, this `plan.md` is the authoritative execution roadmap expected by v1.4.

Do not create a parallel `agent_plan.md` during the bootstrap period.

The target Bonsai 2.0 execution-memory artifact is `agent_plan.md`. Conversion to the v2 names occurs during validated self-hosting promotion.

## Strategy

**Build Strategy:** Preserve Bonsai's learned behavior before rewriting its standard artifacts. First extract and review durable artifact contracts from the existing Bonsai 1.4 implementation. Then build Bonsai 2.0 in the isolated `bonsai/` staging tree, validate it using durable tests whose generated output remains outside the staged distribution, integrate the mature mapping subsystem, and finally archive the running v1.4 installation and promote the validated v2 into `.bonsai`. Complete the transition only after a fresh session successfully resumes `bonsai-dev` using v2.

## Roadmap

### Phase Summaries

1. **Archaeology and Artifact Contracts:** Inventory the Bonsai 1.4 standard, extract learned behavior and edge cases, classify Keep / Adapt / Drop / Missing, and produce reviewed contracts before implementation |
   **Mode:** Single-pass |
   **Status:** Active |
   **Plan:** None |
   **Plan Status:** None
2. **Bootstrap and Core Execution Model:** Implement the staged v2 startup/bootstrap, implementation router, identity resolution, and core menu/gate behavior under `bonsai/` |
   **Mode:** To determine at activation |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None
3. **Context and Project Workflows:** Implement developer/agent context layering, project management, Bonsai Home creation, project-memory synthesis, phase execution, final-truth handling, dry runs, handoff, and templates |
   **Mode:** To determine at activation |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None
4. **Integrated Code Maps:** Preserve useful mature mapping internals while integrating source identity, Bonsai Home map storage, project-aware mapping, map selection, and normal Bonsai routing |
   **Mode:** To determine at activation |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None
5. **Validation, Promotion, and Self-Hosting Proof:** Validate staged v2 and artifact-producing workflows, build/validate a complete replacement candidate, archive current `.bonsai`, promote v2, convert the self-hosting project to v2 execution-memory names, prove fresh-session self-hosting, and remove staging |
   **Mode:** To determine at activation |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None

## Active Phase Detail

* **Goal:** Produce a reviewable durable contract layer that captures the behavior Bonsai 2.0 must preserve, adapt, deliberately drop, or newly implement before standard artifacts are rewritten.
* **Execution Readiness:** Phase planning required
* **Scope:** [Inventory existing standard artifacts, extract core execution behavior, extract project/context workflow behavior, extract mapping behavior in bounded batches, identify missing v2 seams, reconcile contracts against `bonsai/specification.md`, define validation obligations without implementing staged v2 artifacts]
* **Approved Constraints:** [Bonsai 1.4 remains the running runtime, `bonsai/` is temporary staged v2 distribution, do not put generated test output under `bonsai/`, do not create duplicate v1/v2 execution-memory truth, do not materially rewrite standard artifacts before relevant contract coverage is understood, specification wins over archaeological evidence]
* **Ordered Steps:**
    1. Draft `plan/plan_phase_1.md` from `.bonsai/templates/plan_phase_template.md` and stop for Phase Plan Approval.
    2. After approval, execute bounded archaeology beginning with the core execution cluster.
    3. Review contract coverage before moving from archaeology into staged implementation.
* **Validation:** [All existing standard artifacts inventoried, each target artifact or unresolved seam has explicit contract coverage, high-value learned behavior is classified, v2-required missing behavior is assigned or explicitly unresolved, no substantive staged v2 implementation occurs during Phase 1]
* **Done When:** Phase 1 contracts are sufficient and reviewed so Phase 2 can implement the staged v2 core without relying on chat history or blindly copying v1.4 artifacts.

## Deferred & Completed

* **Deferred:** [All staged v2 implementation until Phase 2+, test harness/output creation until needed by implementation/validation, promotion/self-overwrite until Phase 5]
* **Completed:** [Bonsai v2 operating specification, current v2 user-facing README, self-hosting repository/staging model, artifact-contract approach, temporary staging/promotion architecture, test-output separation decision]

## Maintenance Rules

* Keep this file focused on roadmap-level execution truth.
* Current resume state, blockers, exact next step, and current gate belong in `state.md`.
* While Bonsai 1.4 is active, `plan.md`, `state.md`, and `plan/plan_phase_<N>.md` are the only authoritative execution-memory filenames.
* Do not create duplicate `agent_plan.md` / `agent_state.md` files during bootstrap.
* Keep phase status, execution mode, plan references, and approval state consistent with `state.md`.
* Add a separate `plan/plan_phase_<N>.md` only when required by the active Bonsai 1.4 workflow or genuinely useful for later phases.
* Do not implement staged v2 artifacts during Phase 1 merely because their target paths are known.
* Compress completed phase detail aggressively when it no longer helps execution.
