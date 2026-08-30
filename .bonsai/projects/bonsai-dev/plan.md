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
   **Status:** Completed |
   **Plan:** `plan/plan_phase_1.md` |
   **Plan Status:** Approved
2. **Bootstrap and Core Execution Model:** Implement the staged v2 startup/bootstrap, implementation router, identity resolution, and core menu/gate behavior under `bonsai/` |
   **Mode:** Single-pass |
   **Status:** Completed |
   **Plan:** `plan/plan_phase_2.md` |
   **Plan Status:** Approved
3. **Context and Project Workflows:** Implement developer/agent context layering, Bonsai Home creation, project-memory synthesis, phase execution, final-truth handling, dry runs, handoff, and templates; integrate and validate the inline Project Management already implemented by the Phase 2 router, correcting it only if Phase 3 exposes an approved-contract gap |
   **Mode:** Single-pass |
   **Status:** Completed |
   **Plan:** `plan/plan_phase_3.md` |
   **Plan Status:** Approved
4. **Integrated Code Maps:** Preserve useful mature mapping internals while integrating source identity, Bonsai Home map storage, project-aware mapping, map selection, and normal Bonsai routing |
   **Mode:** To determine at activation |
   **Status:** Active |
   **Plan:** None |
   **Plan Status:** None
5. **Validation, Promotion, and Self-Hosting Proof:** Validate staged v2 and artifact-producing workflows, build/validate a complete replacement candidate, archive current `.bonsai`, promote v2, convert the self-hosting project to v2 execution-memory names, prove fresh-session self-hosting, and remove staging |
   **Mode:** To determine at activation |
   **Status:** Pending |
   **Plan:** None |
   **Plan Status:** None

## Active Phase Detail

Phases 1–3 are complete. Phase 4 is active at its planning boundary: execution mode remains unresolved and no
detailed phase plan exists. The recommended mode is Single-pass because the durable mapping contracts were already
approved in Phase 1; a detailed Phase 4 plan is warranted for ordered integration and validation work.

## Deferred & Completed

* **Deferred:** [Phase 5 operating-model validation and promotion/self-overwrite]
* **Completed:** [Bonsai v2 operating specification, current v2 user-facing README, self-hosting repository/staging model, artifact-contract approach, temporary staging/promotion architecture, test-output separation decision, Phase 1 archaeology and approved complete artifact-contract layer, Phase 2 staged bootstrap and core execution model, Phase 3 context and project workflows]

## Maintenance Rules

* Keep this file focused on roadmap-level execution truth.
* Current resume state, blockers, exact next step, and current gate belong in `state.md`.
* While Bonsai 1.4 is active, `plan.md`, `state.md`, and `plan/plan_phase_<N>.md` are the only authoritative execution-memory filenames.
* Do not create duplicate `agent_plan.md` / `agent_state.md` files during bootstrap.
* Keep phase status, execution mode, plan references, and approval state consistent with `state.md`.
* Add a separate `plan/plan_phase_<N>.md` only when required by the active Bonsai 1.4 workflow or genuinely useful for later phases.
* Do not implement staged v2 artifacts until the active phase's planning and review gates authorize them.
* Compress completed phase detail aggressively when it no longer helps execution.
