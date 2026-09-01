# Agent Plan - Phase 5: Validation, Promotion, and Self-Hosting Proof

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**
**Project:** Bonsai Dev | **Parent:** `../agent_plan.md`
**Phase Status:** Completed
**Plan Status:** Approved
**Mode:** Single-pass

## Objective & Scope

**Objective:** Prove the promoted Bonsai v2 runtime through a genuinely fresh self-hosting session, then remove the temporary staging tree through a separate authorized cleanup step.
**Inputs:** Approved project requirements, architecture, artifact contracts, validated promoted runtime, retained staging tree, verified rollback archive, and the canonical fresh-session pointer.
**In Scope:** Fresh Embedded startup, `bonsai-dev` v2-memory resume, one separately authorized bounded state-changing action, execution-memory reconciliation, proof recording, and post-proof staging cleanup.
**Out of Scope / Do Not Do Yet:** Staging removal before successful proof; rollback-archive deletion; prior-runtime fallback or compatibility identities; acceptance based only on file presence or startup prose.
**Expected Deliverables:** Fresh-session proof evidence, reconciled v2 execution memory, separately authorized staging removal, and final single-tree validation.

## Execution Constraints

- **Implementation Scope:** Use the promoted `.bonsai/` runtime and update only the bounded Bonsai-development artifact plus v2-owned execution memory authorized at the fresh-session gate.
- **Approved Boundaries:** Use only the canonical startup pointer; retain `bonsai/` and the rollback archive through proof; stop for a recovery decision on proof failure; remove staging only after separate continuation.
- **Durable Contracts:** Approved promotion and self-hosting contracts remain unchanged.
- **Human Review Focus:** Fresh-session identity, no prior-chat or prior-runtime fallback, an actual bounded state change, reconciled proof state, and the separate cleanup gate.

## Ordered Work

### Implementation

- **Step 1 — Promotion preparation and installation:** Artifact contracts, v2 implementation, topology validation, Task Tracker preparation, candidate conversion, rollback rehearsal/archive, preflight, and live candidate installation completed before this runtime became active. | **Status:** Completed | **Done:** Live `.bonsai/` is the verified candidate in `Promoted, Unproven` state; staging and rollback assets remain.
- **Step 2 — Prove fresh-session self-hosting:** Start with only `Read .bonsai/start.md and follow its instructions.`, resolve the promoted Embedded runtime and `bonsai-dev`, pass the normal gate, execute one separately authorized bounded state-changing action, and reconcile v2 execution memory. | **Status:** Completed | **Done:** The canonical pointer resolved the promoted Embedded runtime and `bonsai-dev`; the separately authorized step-identity correction changed and reconciled v2 execution memory without prior-chat or prior-runtime fallback; promotion status is `Proven, Cleanup Pending`.
- **Step 3 — Remove staging and close the transition:** After explicit post-proof continuation, remove only `bonsai/`, retain the rollback archive, validate the single-tree runtime, and close Phase 5. | **Status:** Completed | **Done:** The separately authorized cleanup removed only `bonsai/`; `.bonsai/` is the sole shipped/self-hosting standard and source; prior-runtime and duplicate execution identities are absent; the rollback archive remains unchanged.

## Validation & Done Criteria

- **Validation Strategy:** Fresh canonical-pointer startup, Embedded identity and memory checks, observable bounded state change, execution-memory reconciliation, then final whole-tree/reference and workflow validation after cleanup.
- **Architecture / Contract Validation:** Preserve the rollback/staging boundary through proof, require separate cleanup authorization, reject fallback/dual identities, and finish with one canonical `.bonsai/` tree.
- **Definition of Done:** The fresh-session proof and separately authorized cleanup both pass; project execution memory is concise, v2-native, and internally consistent.

## Context & Wrap-up

- **Dependencies:** None.
- **Risks:** None active; the verified rollback archive remains available as a local recovery asset.
- **Open Questions:** None.
- **Completion Summary:** **Outcome:** Fresh-session proof, separately authorized staging cleanup, and final single-tree validation passed. | **Unlocked:** Completed Bonsai v2 self-hosting runtime with `.bonsai/` as the sole standard and source.

## Maintenance Rules

- Treat this file as active v2 execution memory and keep it aligned with `agent_plan.md` and `agent_state.md`.
- Preserve approved final truth, promotion contracts, proof boundaries, and recovery assets.
- Stop for a concrete recovery decision if proof fails.
- Retain this file only as the approved Phase 5 completion record while it remains useful.
