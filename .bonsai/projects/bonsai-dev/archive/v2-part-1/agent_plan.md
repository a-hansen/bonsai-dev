# Agent Plan

**Project:** Bonsai Dev
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** Completed. `.bonsai/` is the sole shipped/self-hosting Bonsai v2 runtime; the verified rollback archive remains retained locally.

## Roadmap

### Phase Summaries

1. **Archaeology and Artifact Contracts:** Extract and approve durable artifact contracts from the prior runtime. | **Mode:** Single-pass | **Status:** Completed | **Plan:** `None` | **Plan Status:** `None`
2. **Bootstrap and Core Execution Model:** Implement the v2 startup and implementation spine. | **Mode:** Single-pass | **Status:** Completed | **Plan:** `None` | **Plan Status:** `None`
3. **Context and Project Workflows:** Implement context, project, phase, final-truth, dry-run, handoff, and template workflows. | **Mode:** Single-pass | **Status:** Completed | **Plan:** `None` | **Plan Status:** `None`
4. **Integrated Code Maps:** Integrate source identity, reusable map storage, project-aware selection, and map lifecycle behavior. | **Mode:** Single-pass | **Status:** Completed | **Plan:** `None` | **Plan Status:** `None`
5. **Validation, Promotion, and Self-Hosting Proof:** Prove the promoted runtime in a fresh session and collapse to the final single-tree repository. | **Mode:** Single-pass | **Status:** Completed | **Plan:** `None` | **Plan Status:** `None`

## Completion

- **Promotion Status:** Complete
- **Execution Readiness:** Complete
- **Outcome:** Fresh-session self-hosting proof passed, the separately authorized cleanup removed `bonsai/`, `.bonsai/` is the sole shipped/self-hosting standard and source, and the verified rollback archive remains unchanged.
- **Recovery Asset:** `.bonsai-backups/bonsai-20260830-143353.zip`

## Deferred and Completed

- **Deferred:** None.
- **Completed:** Artifact contracts, staged v2 implementation, workflow/topology validation, Task Tracker v2 preparation, candidate validation, rollback verification, live candidate promotion, fresh-session self-hosting proof, staging cleanup, and final single-tree validation.

## Maintenance Rules

- Keep this file roadmap-level and consistent with terminal project state in `agent_state.md`.
- Preserve human-owned final truth and approved promotion/self-hosting contracts.
- Keep only current v2 execution truth; do not restore prior-runtime execution identities or compatibility aliases.
- Retain the verified rollback archive unless the human separately authorizes its removal.
