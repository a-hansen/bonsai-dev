# Create Bonsai Project Memory

## Purpose

Turn a mature Web UI design conversation into durable, independently usable Bonsai project memory and, for an
initial synthesis, a repository-root Bonsai bootstrap package. Preserve the human's approved product and
architecture decisions, honest unresolved questions, and a minimal implementation roadmap without turning the
conversation into a transcript or beginning implementation.

Keep design conversational until synthesis is requested. Do not force the human to fill templates during
exploration.

## Invocation and Inputs

Use this workflow when the human says the current design is mature enough to preserve. Synthesize from:

- the complete current design conversation;
- explicitly supplied source, design, or existing project-memory artifacts; and
- the Bonsai project name resolved below.

This is primarily a Web UI artifact-producing workflow. It does not invoke the coding-agent implementation
workflow or modify a repository directly.

## Choose the Project Root Safely

For initial synthesis, resolve the project name before generating artifacts:

- If the human already supplied a project name, use it after validation.
- Otherwise ask what the Bonsai project should be called and suggest `main` as the conventional default.
- Treat acceptance of the suggested default as selection of `main`; do not require the human to invent another
  name merely because named projects are supported.

For an existing-project design update, preserve the supplied existing project identity when it is unambiguous; do
not ask the human to rename or reselect it merely because the workflow is being rerun.

The selected project name must be one non-empty directory segment: not `.` or `..`, not absolute, and containing
no `/`, `\`, drive prefix, traversal, or control characters. Ask for a corrected name when unsafe; do not
sanitize it silently. Do not create `main` as an alias when another safe name was selected.

The selected project root is:

```text
.bonsai/projects/<project>/
```

## Initial Synthesis and Existing-Project Updates

### Initial synthesis

Produce one repository-root archive containing the canonical local Bonsai bootstrap plus the four instantiated core
project files:

```text
.bonsai/
    start.md
    projects/
        <project>/
            requirements.md
            architecture.md
            agent_plan.md
            agent_state.md
```

Add only genuinely warranted optional project files under `.bonsai/projects/<project>/`:

```text
agent_context.md
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
```

Simple projects should contain only `start.md` and the four core project files. The archive enables the
repository-local Bonsai entry point; it does not make the repository an Embedded Bonsai installation unless the
repository separately contains a complete valid Bonsai standard.

### Existing-project design update

When the human supplies existing Bonsai project memory and requests a design update:

1. Treat supplied human-owned final truth as the approved baseline.
2. Change only files materially affected by the approved design discussion unless full regeneration is explicitly
   requested.
3. Preserve unaffected content; do not normalize or rewrite it for style.
4. Include `agent_plan.md` or `agent_state.md` only when the design change requires roadmap, phase, blocker,
   readiness, or next-step reconciliation.
5. Do not perform implementation work.

Package update files at their existing project-root-relative paths. If the approved change requires deleting or
renaming an existing file, state that action explicitly for human review; omission from an update archive does not
silently authorize deletion. Do not include `.bonsai/start.md` in an existing-project design update.

## Canonical Initial Bootstrap

For initial synthesis, create `.bonsai/start.md` exactly from the canonical bootstrap below. Do not specialize it
for the selected project, inline Bonsai Home, or otherwise adapt it to the current design conversation.

````markdown
# Bonsai Startup

This file is the repository-local Bonsai bootstrap. Keep startup read-only and small.

It is not a Bonsai Home entry point. Normal startup must begin from the target repository's local `.bonsai/start.md` anchor.

## Session Inputs

Retain the human's complete startup request as natural language. An explicit active-project request is session
identity; any remaining request is passed through unchanged after identity resolution. Do not require or invent a
startup command syntax.

## Bootstrap Location Guard

Before deriving repository home, verify that the startup request is using this file as the target repository's local
`.bonsai/start.md` bootstrap. `BONSAI_HOME` supplies the Bonsai standard after repository identity is established; it
must not be used as a substitute repository anchor.

If the human explicitly directed startup through `$BONSAI_HOME/start.md`, or through an equivalent resolved path to
the reusable Bonsai Home copy of `start.md`, stop before deriving repository home. Do not ask for confirmation and do
not treat the parent of `BONSAI_HOME` as a repository. Explain that Bonsai startup must begin from the target
repository and provide the canonical instruction:

```text
Read .bonsai/start.md and follow its instructions.
```

An embedded Bonsai installation remains valid because its `start.md` is the repository-local `.bonsai/start.md`
anchor. The guard rejects using a reusable Bonsai Home as the repository anchor; it does not reject a repository-local
embedded standard merely because that same `.bonsai` directory also serves as Bonsai Home.

## Resolve Identity

Resolve deterministic facts with host tools when available.

1. **Repository home:** Treat the parent of the `.bonsai` directory containing this file as repository home. Do
   not infer repository home from the process working directory when the two differ.
2. **Bonsai Home:** A directory is a valid Bonsai standard for bootstrap when it contains readable
   `specification.md` and `prompts/implementation.md` files.
   - If `BONSAI_HOME` is defined and identifies a valid standard, use it.
   - Otherwise, if the repository-local `.bonsai` directory is a valid embedded standard, use it.
   - Otherwise stop and ask the human to configure or identify Bonsai Home. Report a defined but invalid
     `BONSAI_HOME`; do not search broadly for another installation, substitute a one-session path for the missing
     environment configuration, or persist a guessed location.
3. **Active project:** Resolve only immediate child directories of `<repository-home>/.bonsai/projects/`.
   - If the human explicitly named a project, use it only when that project directory exists. Otherwise stop and
     ask the human to correct the project or choose an available one. When multiple existing projects are offered
     as alternatives, present them in stable lexical order as numbered choices and accept the corresponding number
     as the selection.
   - Otherwise, use `main` when `projects/main/` exists.
   - Otherwise, if exactly one project directory exists, use it.
   - Otherwise, if several project directories exist, enumerate them in stable lexical order, present them as
     numbered choices, and ask the human to choose by number. Accept the corresponding number as the project
     selection; do not require the human to retype the project name.
   - Otherwise stop and surface project creation or project design as the required next action. Do not create
     project memory or invent durable design during bootstrap.

Keep repository home, Bonsai Home, active project, and the retained startup request as current-session context
only. Do not write a current-project pointer or store session identity in developer context, agent context, or
project memory.

## Hand Off

After all identity values are resolved:

1. read `<bonsai-home>/prompts/implementation.md`;
2. provide it the resolved Bonsai Home, repository home, active project, and retained natural-language startup
   request;
3. follow it as the implementation kernel.

Do not load requirements, architecture, maps, developer context, agent context, or specialized skills in this
bootstrap. Do not execute requested project, Bonsai Home, code-map, or implementation workflows here; preserve
the request for the implementation kernel, which must report any unavailable delegated workflow without claiming
success.
````

The bootstrap is standard framework content, not project final truth. If the canonical bootstrap changes in the
Bonsai standard, this workflow must be updated to keep the generated repository anchor identical.

## Blocking Clarifications Before Synthesis

Ask concise questions only when synthesizing durable memory would otherwise guess a consequential foundation.
Examples include:

- product goal, users, core behavior, or scope boundaries;
- primary language/runtime, build system, execution environment, or persistence choice when it materially shapes
  target architecture or the first phase;
- required repository/module layout;
- a durable API, schema, protocol, extension, or integration boundary;
- dependency direction or forbidden coupling that is intended architecture; or
- another decision that materially changes roadmap, phase mode, or the first implementation action.

Do not block on ordinary coding style, test philosophy, naming taste, abstraction preference, local SDK paths, or
other developer-specific guidance unless it truly changes approved product or target architecture. Do not hide a
missing foundation behind phrases such as "standard tooling", "normal layout", or "clean architecture".

If the human explicitly chooses to synthesize with a foundational uncertainty unresolved:

- do not choose an answer;
- preserve it under `Foundational Open Questions` in the affected human-owned document;
- reflect its roadmap and readiness consequences; and
- set `Execution Readiness: Design required` when it prevents safe Phase 1 planning.

Non-blocking uncertainty belongs under ordinary `Open Questions` and does not prevent synthesis.

## Synthesis Rules

- Base every durable statement on the conversation or explicitly supplied artifacts.
- Preserve settled decisions plainly; do not weaken them into assumptions.
- Preserve accepted exclusions and rejected approaches when they remain rebuild-relevant.
- Write current target truth, not chat chronology, implementation history, or rationale that no longer matters.
- Keep requirements about product behavior and constraints; keep architecture about intended system structure and
  rebuild-relevant implementation boundaries.
- Do not invent features, constraints, modules, interfaces, adapters, layers, builders, dependency rules, testing
  conventions, or framework patterns.
- Record module boundaries only when they materially belong to the approved target architecture. Capture approved
  modules, public seams, dependency direction, and forbidden coupling; use `Not prescribed` or `None` otherwise.
- Keep top-level truth orienting. Add a deeper area/subsystem file only when its isolated complexity would
  materially bloat the top-level document.
- If a top-level file links an optional layered file, include that exact file in the archive. Do not leave broken
  references.
- Instantiate every schema field. Leave no `<placeholder>`, `[List]`, template instruction, or fabricated filler.
  Put genuine uncertainty in the appropriate question section.
- Do not generate implementation source, tests, generated test output, a phase-plan file, or a transcript summary.

## Ownership Boundaries

- `requirements.md`, `architecture.md`, and their warranted layered documents are human-owned final truth.
- `agent_plan.md` and `agent_state.md` are agent-owned execution memory initialized by this workflow and maintained
  by implementation afterward.
- Optional project `agent_context.md` is agent-owned operational memory. Seed it only from human-approved facts
  that are useful specifically to this project, such as external source locations or selected code maps.
- Operational source/map facts do not belong in requirements or architecture.
- Never store active-project selection, secrets, credentials, transient troubleshooting, roadmap state, or product
  truth in `agent_context.md`.
- Never generate `developer_context.md` at any path. Developer context is a separate human-owned home/repository
  workflow, not project-memory output.
- Generated human-owned truth is a review artifact until the human accepts it. Generation alone does not approve
  or silently replace durable design.

## Initialize the Roadmap and State Honestly

Define an initial phase-level roadmap in `agent_plan.md`; do not create
`plan/agent_plan_phase_1.md`.

Choose the first phase mode as follows:

- `Single-pass` is normal when no separately reviewed durable contract is being established or changed.
- `Two-pass contract-first` is justified only for an independently review-worthy durable API, schema, persistent
  format, protocol, extension contract, integration surface, or comparable contract.
- Do not select two-pass because the phase is large, spans files, creates classes, needs tests, or is internally
  complex.
- Use `To determine at activation` when the conversation cannot support a responsible choice.

When design is sufficient for implementation planning, initialize:

```text
Active Phase Plan File: None
Phase Plan Status: None
Current Phase Pass: Phase Planning
Execution Readiness: Phase planning required
Exact Next Step: Draft plan/agent_plan_phase_1.md for human review before Phase 1 implementation.
```

When accepted foundational uncertainty still prevents safe planning, initialize:

```text
Active Phase Plan File: None
Phase Plan Status: None
Current Phase Pass: Not applicable
Execution Readiness: Design required
Exact Next Step: Resolve the named foundational design questions.
```

Never initialize a new project directly into `Single-pass Implementation`, `Pass A (Contract)`, or `Ready to
execute`. The implementation workflow drafts and reviews the detailed Phase 1 plan as its first planning gate.

## Archive Protocol

Create one zip archive suitable for extraction at repository root.

- Every archive entry starts under `.bonsai/`; do not add a wrapper directory above it.
- For initial synthesis, include `.bonsai/start.md`, all four required core files under
  `.bonsai/projects/<project>/`, and every referenced optional project file.
- For an existing-project update, include only materially affected project files unless full regeneration was
  requested. Do not include `.bonsai/start.md`.
- Include no `developer_context.md`, implementation source, detailed phase plan, logs, or generated test output.
- Use ordinary UTF-8 Markdown files with stable relative links.
- Inspect the archive manifest before presenting it. For initial synthesis, verify that `.bonsai/start.md` is
  present and exactly matches the canonical bootstrap in this workflow. For all archives, verify safe paths,
  required project files, ownership metadata, cross-document links, roadmap/state agreement, and absence of
  placeholders.

The initial-synthesis archive intentionally maps onto repository-local `.bonsai` paths. If the human has indicated
that the target repository already contains `.bonsai/start.md` or the selected project path, surface the potential
overwrite before presenting the archive. Do not silently rename the project, alter the bootstrap, or claim that
extraction is non-destructive.

If the host cannot create and attach a real zip, report that limitation. Do not claim an archive exists and do not
substitute a long manual-copy protocol unless the human explicitly requests a fallback.

Present the archive with a compact manifest, the selected project root, unresolved foundational questions if any,
execution readiness, and a clear instruction to extract the archive at repository root. Remind the human to review
the generated final truth before adoption. Do not add conversational filler or begin implementation.

## Inline Output Schemas

Instantiate these schemas; do not emit the blank forms.

### `requirements.md`

```markdown
# Requirements

**Project:** <Project name>
**[Meta: Human-owned | Current Product Truth | Bounded Scope | No Implementation Detail]**

## Product Goal and Problem

**Goal:** <What the product must accomplish>
**Problem:** <Problem, affected users, and why it matters>
**Primary Users:** <Users or user classes>

## Outcomes and Workflows

**Core Outcomes:** <Observable product outcomes>

- **<Workflow>:** <Trigger> -> <steps> -> <success> | **Failures:** <Meaningful failure conditions>

## Functional Requirements

- **FR-1 — <Name>:** <Required behavior> | **Acceptance:** <Observable conditions> | **Details:** <Layered file or `None`>

## Rules and Constraints

- **Core Concepts:** <Definitions and domain rules>
- **Behavioral Rules:** <Strict product behavior>
- **System Constraints:** <Approved product constraints>
- **Quality Requirements:** <Only approved usability, reliability, performance, integrity, or similar outcomes>

## Scope and Decisions

- **Out of Scope / Non-Goals:** <Explicit exclusions>
- **Accepted Decisions:** <Settled product decisions>
- **Foundational Open Questions:** <Blocking product questions or `None`>
- **Open Questions:** <Prioritized non-blocking product questions or `None`>

## Definition of Done

<Observable product-level completion conditions>
```

### Optional `requirements/requirements_<AREA>.md`

```markdown
# Requirements — <Area>

**Project:** <Project name> | **Parent:** `../requirements.md`
**[Meta: Human-owned | Durable Product-Area Truth | Bounded Scope | No Implementation Detail]**

## Goal and Scope

**Area Goal:** <Product intent>
**Owns:** <Behaviors and decisions>
**Does Not Own:** <Adjacent concerns>

## Outcomes, Workflows, and Requirements

- **Outcome:** <User-visible outcome>
- **<Workflow>:** <Trigger> -> <steps> -> <success> | **Failures:** <Conditions>
- **FR-<AREA>-1 — <Name>:** <Required behavior> | **Acceptance:** <Observable conditions>

## Rules, Relationships, and Decisions

- **Rules / Constraints:** <Approved area rules>
- **Depends On:** <Product relationships or `None`>
- **Must Stay Separate From:** <Approved boundary or `None`>
- **Out of Scope / Non-Goals:** <Exclusions>
- **Accepted Decisions:** <Settled decisions>
- **Open Questions:** <Prioritized questions or `None`>

## Definition of Done

<Observable area-level completion conditions>
```

### `architecture.md`

```markdown
# Architecture

**Project:** <Project name>
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Goal and Overview

**Architectural Goal:** <Primary target optimization>
**System Overview:** <Major moving parts and responsibilities>
**Approved Principles:** <Only design principles established in the conversation>

## Major Subsystems

- **<Subsystem>:** <Purpose> | **Owns:** <Responsibilities> | **Must Not Own:** <Boundary or `None`> |
  **Dependencies:** <Approved dependencies or `Not prescribed`> | **Details:** <Layered file or `None`>

## Module Boundaries and Dependency Shape

- **Human-Digestible Modules:** <Approved modules or `Not prescribed`>
- **Public Seams:** <Durable externally consumed contracts or `None`>
- **Dependency Direction:** <Approved directions or `Not prescribed`>
- **Forbidden Coupling:** <Explicitly rejected coupling or `None`>
- **Review Anchors:** <Native artifacts that expose important contracts or `None`>

## Domain, State, and Flows

- **<Concept>:** <Purpose, owner, properties, lifecycle>
- **State / Persistence:** <Categories, location, ownership, and lifecycle>
- **<Key Flow>:** <Trigger> -> <path> -> <output> | **Failure Handling:** <Rules>

## Cross-Cutting Constraints

- **Runtime / Build Assumptions:** <Approved assumptions or `Not prescribed`>
- **Error / Recovery:** <Approved failure boundaries>
- **Concurrency:** <Approved model or `Not prescribed`>
- **Security / Integrity:** <Trust and validation boundaries or `Not prescribed`>
- **Observability:** <Approved expectations or `Not prescribed`>
- **Extension / Configuration:** <Approved model or `None`>

## Guardrails and Questions

- **Implementation Guardrails:** <Strict approved technical constraints or `None`>
- **Architecture Guardrails:** <Rules preserving approved target structure or `None`>
- **Explicitly Rejected:** <Rejected approaches and reasons or `None`>
- **Foundational Open Questions:** <Blocking architecture questions or `None`>
- **Open Questions:** <Prioritized non-blocking architecture questions or `None`>
```

### Optional `architecture/architecture_<SUBSYSTEM>.md`

```markdown
# Architecture — <Subsystem>

**Project:** <Project name> | **Parent:** `../architecture.md`
**[Meta: Human-owned | Durable Subsystem Truth | Rebuild-Grade]**

## Role and Boundaries

**Role:** <Subsystem purpose and architectural intent>
**Owns:** <Responsibilities>
**Must Not Own:** <Explicit exclusions or `None`>

## Contracts, Domain, and Flow

- **Public Contract:** <Durable contract and consumers or `None`>
- **Domain:** <Owned concepts and lifecycle>
- **State / Persistence:** <Ownership and persistence rules>
- **Key Flow:** <Trigger> -> <steps> -> <output> | **Failure:** <Rule>

## Dependencies and Cross-Cutting Rules

- **Allowed Dependencies:** <Approved dependencies or `Not prescribed`>
- **Forbidden Dependencies:** <Explicit prohibitions or `None`>
- **Lifecycle / Concurrency:** <Approved rules or `Not prescribed`>
- **Error / Recovery:** <Rules>
- **Extension / Configuration:** <Approved model or `None`>
- **Security / Integrity / Observability:** <Approved rules or `Not prescribed`>

## Guardrails and Questions

- **Guardrails:** <Approved subsystem constraints or `None`>
- **Rejected Approaches:** <Approaches and reasons or `None`>
- **Open Questions:** <Prioritized questions or `None`>
- **Fitness Criteria:** <Observable architecture conditions>
```

### `agent_plan.md`

```markdown
# Agent Plan

**Project:** <Project name>
**[Meta: Agent-maintained | Active Execution Roadmap | Phase-Level Truth | Prune Aggressively]**

## Strategy

**Build Strategy:** <Concise sequencing and risk-reduction approach>

## Roadmap

### Phase Summaries

1. **<Phase 1>:** <Objective> | **Mode:** <To determine at activation | Single-pass | Two-pass contract-first> |
   **Status:** <Active | Blocked> | **Plan:** `None` | **Plan Status:** `None`
2. **<Later phase>:** <Objective> | **Mode:** <To determine at activation | Single-pass | Two-pass contract-first> |
   **Status:** `Pending` | **Plan:** `None` | **Plan Status:** `None`

## Active Phase Detail

- **Goal:** <Phase 1 outcome>
- **Execution Readiness:** <Design required | Phase planning required>
- **Scope:** <Known approved areas or `Not prescribed`>
- **Approved Constraints:** <Relevant approved constraints or `None`>
- **Planning Boundary:** Draft and review `plan/agent_plan_phase_1.md` before substantive implementation.
- **Validation:** <Phase-level checks known from approved design>
- **Done When:** <Phase completion conditions>

## Deferred and Completed

- **Deferred:** <Later roadmap work or `None`>
- **Completed:** `None`

## Maintenance Rules

- Keep this file roadmap-level; detailed sequencing belongs in a warranted phase plan.
- Keep phase, mode, plan identity/status, and readiness consistent with `agent_state.md`.
- Phase 1 always receives a reviewed `plan/agent_plan_phase_1.md` before implementation.
- Later phase plans are conditional, not automatic.
- Preserve current execution truth and compress completed detail.
```

### `agent_state.md`

```markdown
# Agent State

**Project:** <Project name>
**[Meta: Agent-maintained | Current Resume State | Keep Minimal]**

## Current Execution State

**Current Phase:** <Phase 1 name>
**Active Phase Plan File:** `None`
**Phase Plan Status:** `None`
**Current Phase Pass:** <Phase Planning | Not applicable>
**Phase Execution Mode:** <To determine at activation | Single-pass | Two-pass contract-first>
**Execution Readiness:** <Phase planning required | Design required>
**Current Objective:** <Draft the initial phase plan, or resolve named foundational design>

- **Current Snapshot:** <Only current design/readiness truth needed to resume>
- **Active Files:** <Immediate truth/memory files needed next>
- **Blockers / Risks:** <Foundational blockers or `None`>

**Exact Next Step:** <Concrete planning or design action>
**Success Condition:** <Observable result and next required human gate>

### Approved Dry-Run Baseline

`None`

## Maintenance Rules

- Keep current resume truth, not session history.
- Remove resolved blockers, completed steps, obsolete files, stale observations, and expired baselines.
- Keep roadmap, phase-plan, pass, readiness, and exact-next-step truth consistent.
- Do not use state as product or architecture authority.
```

### Optional `agent_context.md`

Use concise concern-based headings and only approved project-specific operational facts. Omit the file entirely
when none qualify.

```markdown
# Agent Context

**[Meta: Agent-owned | Project Scope | Current Operational Truth]**

## Code Maps

- Useful maps: <Exact approved map identities>

## Source Locations

- <Stable project-specific source identity or location and how it should be used>
```

Omit unused sections. Never include secrets, active project selection, developer preferences, requirements,
architecture, roadmap, transient blockers, or discovery history.
