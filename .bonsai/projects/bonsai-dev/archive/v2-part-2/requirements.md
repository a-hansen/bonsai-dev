# Requirements

**Project:** `bonsai-dev`  
**[Meta: Human-owned | Current Product Truth | Bounded Scope | No Implementation Detail]**

## Product Goal and Problem

**Goal:** Keep `bonsai-dev` as the persistent self-development project used to evolve Bonsai while ensuring its live project memory describes the current Bonsai work rather than completed historical work.

**Problem:** Bonsai's standard is intentionally split across a specification, prompts, skills, and templates. A Web UI design session should be able to start from the authoritative `specification.md` and discover only the additional standard artifacts relevant to the change being designed. Today there is no concise standard routing surface for discovering those artifacts, and the existing `bonsai-dev` requirements still describe the completed v1.4-to-v2 bootstrap instead of current self-development work.

**Primary Users:** Bonsai contributors using a Web UI AI to design Bonsai changes and a coding-agent CLI to implement them.

## Outcomes and Workflows

**Core Outcomes:**

- A contributor can begin a Bonsai design session with the current `specification.md` and the proposed change without preloading the whole Bonsai standard.
- The Web UI AI can request concise category guides to discover relevant skills, prompts, or templates, then request only the specific artifacts needed.
- The coding-agent implementation workflow keeps those category guides synchronized when the standard artifact set changes.
- `bonsai-dev` remains a persistent project whose requirements, architecture, roadmap, and state describe the current body of work.

- **Design a Bonsai change:** Human supplies the current `specification.md` and proposed change -> AI identifies relevant artifact categories -> human supplies the requested category guide -> AI requests specific standard artifacts as needed -> design proceeds with bounded context. | **Failures:** The design must not assume an unprovided artifact's detailed behavior or silently mix artifacts from different Bonsai Homes.
- **Maintain framework discovery:** Authorized implementation adds, removes, renames, or materially changes the responsibility of a standard skill, prompt, or template -> coding agent reconciles the corresponding category guide -> validation confirms routing completeness and reference integrity. | **Failures:** A lifecycle change is incomplete if the applicable guide is materially inaccurate.
- **Continue Bonsai self-development:** A bounded Bonsai work package becomes active -> `bonsai-dev` live project memory is reconciled to that work -> implementation proceeds through normal Bonsai planning and execution gates. | **Failures:** Completed-work history must not remain live in a way that misrepresents the current project.

## Functional Requirements

- **FR-1 — Specification-first framework design:** `specification.md` must be the normal starting artifact for designing a Bonsai framework change in a Web UI. | **Acceptance:** A design session can determine which standard artifact categories may matter without receiving all prompts, skills, and templates up front. | **Details:** `None`
- **FR-2 — Category guides:** The Bonsai standard must provide `<bonsai-home>/skills/skills.md`, `<bonsai-home>/prompts/prompts.md`, and `<bonsai-home>/templates/templates.md`. | **Acceptance:** Each guide identifies the artifacts currently available in its category and gives concise responsibility-oriented routing information sufficient to decide what to load next. | **Details:** `None`
- **FR-3 — Progressive discovery:** Category guides must route to individual artifacts rather than duplicate their detailed behavioral rules. | **Acceptance:** A human or AI can move from `specification.md` to a category guide to specific artifacts while keeping unrelated standard context unloaded. | **Details:** `None`
- **FR-4 — Same-home consistency:** Framework artifacts used together for a Bonsai design should normally come from the same resolved Bonsai Home unless the human deliberately supplies another version for comparison. | **Acceptance:** Guide identities and requested standard artifacts resolve relative to the active Bonsai Home in both reusable-home and Embedded Bonsai modes. | **Details:** `None`
- **FR-5 — Automatic guide maintenance:** Bonsai must provide a standard skill that reconciles category guides when skills, prompts, or templates are added, removed, renamed, or materially changed in responsibility. | **Acceptance:** Authorized artifact lifecycle changes leave the corresponding guide accurate without requiring the human to maintain the guide manually. | **Details:** `None`
- **FR-6 — Bounded maintenance:** Ordinary internal edits that do not materially change an artifact's responsibility must not require category-guide churn. | **Acceptance:** Guide maintenance is tied to discoverability changes, not every implementation edit. | **Details:** `None`
- **FR-7 — Reference integrity:** Category-guide maintenance must validate that listed artifacts exist and that relevant standard artifacts are not omitted from their category guide. | **Acceptance:** Broken references and missing discoverable entries are detected before the framework-artifact change is considered complete. | **Details:** `None`
- **FR-8 — Maps remain outside this router feature:** Runtime code maps are not part of the new category-guide/indexing mechanism. | **Acceptance:** No `maps/maps.md` router is introduced by this work; relevant map or source context may still be supplied separately during Web UI design when needed. | **Details:** `None`
- **FR-9 — Current persistent project memory:** `bonsai-dev` live core project memory must describe current Bonsai self-development rather than the completed v2 bootstrap/promotion work. | **Acceptance:** `requirements.md`, `architecture.md`, `agent_plan.md`, and `agent_state.md` agree that Artifact Discovery is the active body of work and that the v2 self-hosting transition is historical rather than current. | **Details:** `None`

## Rules and Constraints

- **Core Concepts:** `specification.md` is Bonsai framework final truth; category guides are concise routing aids; individual prompts, skills, and templates implement detailed behavior; `bonsai-dev` is a persistent project while plans/phases represent bounded work packages.
- **Behavioral Rules:** Start broad with authoritative specification truth, request category guides only when relevant, request individual standard artifacts only as needed, and reconcile the applicable guide whenever its discoverable artifact surface changes.
- **System Constraints:** Guide identities resolve under `<bonsai-home>` rather than assuming the current repository owns the standard; Embedded Bonsai works by making `repo/.bonsai` the Bonsai Home. Category guides must not become peer authorities with the specification.
- **Quality Requirements:** Discovery must remain compact, understandable when files are uploaded outside their directory context, and resistant to drift through explicit reference/completeness validation.

## Scope and Decisions

- **Out of Scope / Non-Goals:** A global router for runtime code maps; Portable Design Context; Archive workflow semantics; semantic review artifacts; fresh-session continuation changes; contextual Dry Run promotion; numbered project-selection changes; redesign of unrelated standard artifacts.
- **Accepted Decisions:** Use `skills/skills.md`, `prompts/prompts.md`, and `templates/templates.md` rather than generic `README.md` or `index.md`; add `skills/artifact_index.md` as the reusable maintenance skill; keep maps outside this feature; resolve all standard guide identities relative to the active Bonsai Home; category guides are routing aids and do not duplicate detailed rules; the CLI agent is responsible for keeping the guides current during authorized framework-artifact lifecycle changes.
- **Foundational Open Questions:** `None`
- **Open Questions:** `None`

## Definition of Done

This work package is complete when the approved specification revision is reflected in the active Bonsai standard; `skills/artifact_index.md`, `skills/skills.md`, `prompts/prompts.md`, and `templates/templates.md` exist at their canonical Bonsai Home-relative identities; the three category guides accurately route the current standard artifact set without duplicating detailed behavior; validation proves reference integrity and expected completeness; maps remain outside the router feature; and `bonsai-dev` execution memory is reconciled to the completed result and next work boundary.
