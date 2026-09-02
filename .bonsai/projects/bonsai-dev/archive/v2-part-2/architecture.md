# Architecture

**Project:** `bonsai-dev`  
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Goal and Overview

**Architectural Goal:** Keep Bonsai self-hosting and progressively discoverable: framework final truth remains centralized in `specification.md`, detailed behavior remains in lazy-loaded standard artifacts, and Web UI design can discover those artifacts through small category-specific routing guides.

**System Overview:** `bonsai-dev` is the persistent Bonsai project stored under the repository-local project-memory area. Bonsai standard artifacts resolve from the active Bonsai Home, which may be the repository's embedded `.bonsai` tree or an external reusable home. The active standard contains the authoritative specification, framework prompts, skills, templates, and their category guides. `bonsai-dev` project memory tracks the current Bonsai work package without becoming authority for framework behavior that belongs in `specification.md`.

**Approved Principles:**

- `specification.md` is the authoritative human-owned Bonsai framework truth.
- Standard prompts, skills, templates, and bootstrap files implement the specification.
- Framework context is progressively discovered and lazily loaded.
- Category guides route to standard artifacts but do not restate their detailed behavior.
- Standard-artifact identities are resolved relative to the active Bonsai Home.
- `bonsai-dev` persists across work packages while its live execution memory tracks the current work.
- Completed v2 bootstrap/promotion artifacts are history, not current architecture.

## Major Subsystems

- **Framework Authority:** `<bonsai-home>/specification.md` | **Owns:** Authoritative Bonsai behavior, boundaries, ownership, lifecycle, environment model, and interaction model. | **Must Not Own:** Detailed procedure that belongs only in a triggered standard artifact when duplicating it would bloat final truth. | **Dependencies:** `None` | **Details:** `None`
- **Artifact Discovery:** `<bonsai-home>/skills/skills.md`, `<bonsai-home>/prompts/prompts.md`, and `<bonsai-home>/templates/templates.md` | **Owns:** Concise category-level discovery and routing to current standard artifacts. | **Must Not Own:** Detailed workflow behavior or duplicated specification truth. | **Dependencies:** Corresponding standard artifact directories and framework authority. | **Details:** `None`
- **Artifact Index Maintenance:** `<bonsai-home>/skills/artifact_index.md` | **Owns:** Reconciliation and validation of the three category guides when the discoverable standard artifact surface changes. | **Must Not Own:** Authorization to invent Bonsai behavior or runtime map lifecycle. | **Dependencies:** `specification.md`, the three category guides, and the corresponding standard artifact directories. | **Details:** `None`
- **Framework Implementation Artifacts:** `<bonsai-home>/skills/`, `<bonsai-home>/prompts/`, and `<bonsai-home>/templates/` | **Owns:** Detailed triggered procedures, entry workflows, and reusable structures that implement the specification. | **Must Not Own:** Peer authority over `specification.md`. | **Dependencies:** Framework authority and applicable standard routing. | **Details:** `None`
- **Persistent Self-Development Project:** `repo/.bonsai/projects/bonsai-dev/` | **Owns:** Current Bonsai-development requirements, architecture, roadmap, resume state, and other project-specific memory. | **Must Not Own:** Bonsai framework behavior that belongs in `specification.md`, or completed-work history as if it were current execution truth. | **Dependencies:** Repository-local Bonsai project-memory conventions and the active Bonsai standard. | **Details:** `None`

## Module Boundaries and Dependency Shape

- **Human-Digestible Modules:** Framework Authority; Artifact Discovery; Artifact Index Maintenance; Framework Implementation Artifacts; Persistent Self-Development Project.
- **Public Seams:** Canonical standard identities `<bonsai-home>/skills/skills.md`, `<bonsai-home>/prompts/prompts.md`, `<bonsai-home>/templates/templates.md`, and `<bonsai-home>/skills/artifact_index.md`.
- **Dependency Direction:** `specification.md` -> category guides and detailed standard artifacts; category guides -> referenced artifacts for discovery; `artifact_index.md` -> category guides for maintenance; `bonsai-dev` project memory -> specification/standard artifacts as implementation inputs, never the reverse as authority.
- **Forbidden Coupling:** Category guides must not duplicate detailed behavior from individual artifacts; guide resolution must not assume the standard is physically stored in the current repository; artifact-index maintenance must not absorb runtime code-map indexing; project execution memory must not redefine Bonsai framework truth.
- **Review Anchors:** `specification.md`; `skills/artifact_index.md`; `skills/skills.md`; `prompts/prompts.md`; `templates/templates.md`.

## Domain, State, and Flows

- **Bonsai Home:** The resolved standard root for the current session. It may be an external reusable home or the repository's embedded `.bonsai`.
- **Category Guide:** A concise standard artifact that identifies the artifacts in one framework category and explains their routing-level responsibilities.
- **Discoverable Artifact Surface:** The set of standard skills, prompts, or templates that should be represented in the corresponding category guide.
- **Persistent Project:** A Bonsai project such as `bonsai-dev` that represents an ongoing product/system while individual plans and phases represent bounded bodies of work.
- **State / Persistence:** Framework authority and category guides persist in the active Bonsai standard. `bonsai-dev` requirements/architecture persist as current project final truth. `agent_plan.md` and `agent_state.md` persist only current execution truth and are reconciled as work packages change.
- **Web UI Design Flow:** Human supplies current `specification.md` plus proposed Bonsai change -> design agent identifies relevant standard categories -> human supplies requested category guide(s) from the same Bonsai Home -> design agent requests specific artifacts -> design proceeds using only needed context. | **Failure Handling:** If required detailed behavior is not present, request the specific artifact rather than guessing; if supplied framework artifacts appear to come from conflicting Bonsai Homes, surface the mismatch.
- **Framework Artifact Lifecycle Flow:** Authorized change adds/removes/renames/materially repurposes a skill, prompt, or template -> implementation loads `skills/artifact_index.md` -> corresponding category guide is reconciled -> references and completeness are validated -> change may complete. | **Failure Handling:** Broken or missing routing entries block completion of the lifecycle change.
- **Persistent Project Update Flow:** New bounded Bonsai work becomes active -> Web UI project-memory synthesis reconciles `bonsai-dev` final truth and execution memory -> CLI starts at Phase 1 planning -> implementation proceeds under the current specification. | **Failure Handling:** Stale project memory is corrected before it is relied upon as current project truth.

## Cross-Cutting Constraints

- **Runtime / Build Assumptions:** Standard artifact locations are expressed relative to `<bonsai-home>`. Embedded mode resolves `<bonsai-home>` to `repo/.bonsai`; reusable-home mode may resolve outside the current repository.
- **Error / Recovery:** Missing guide references, omitted discoverable artifacts, ambiguous Bonsai Home identity, or authority conflicts must be surfaced rather than guessed around.
- **Concurrency:** `Not prescribed`
- **Security / Integrity:** Category guides cannot grant new behavioral authority. The specification remains authoritative when a guide or implementation artifact conflicts with it.
- **Observability:** Validation should make guide reference integrity and expected completeness directly inspectable.
- **Extension / Configuration:** New category guides should not be added merely for symmetry. Runtime maps remain outside this router feature unless later use demonstrates a need.

## Guardrails and Questions

- **Implementation Guardrails:** Preserve the natural filenames `skills.md`, `prompts.md`, and `templates.md`; do not rename them to generic `README.md`/`index.md` or `agent_` forms; do not add `maps/maps.md` in this work; do not make the guides exhaustive behavioral summaries.
- **Architecture Guardrails:** Framework standard and project memory remain distinct even when Embedded Bonsai places both beneath `repo/.bonsai`; the same canonical `<bonsai-home>` identities must work in embedded and reusable-home modes; the artifact-index skill owns standard category-guide maintenance only.
- **Explicitly Rejected:** One giant global artifact catalog; three generic `README.md` routing files; generic `index.md` names that lose category identity when uploaded to a Web UI; eager loading of all standard artifacts; a maps router in this work package.
- **Foundational Open Questions:** `None`
- **Open Questions:** `None`
