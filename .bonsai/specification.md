# Bonsai Specification

Bonsai is a workspace-memory and execution-workflow system for AI-assisted software development.

It preserves the structured context an AI needs to design, build, inspect, map, and continue serious software work across fresh sessions without making chat history authoritative.

Bonsai currently supports two concrete resumable workspace types:

- projects;
- maps.

Projects preserve durable product and architecture truth plus implementation execution memory.

Maps preserve durable repository-local mapping execution memory while producing reusable generated source knowledge.

Bonsai is designed to support:

- simple repositories that need only local project memory;
- repositories containing multiple independent Bonsai projects;
- large repositories whose code mapping spans many fresh sessions;
- projects whose useful source universe spans multiple repositories;
- reusable code maps for independently maintained libraries or frameworks;
- reusable developer and agent context;
- frequent fresh implementation or mapping sessions with small startup prompts.

Bonsai does not attempt to be a general software-engineering methodology.

Coding style, testing philosophy, abstraction preferences, framework conventions, local tooling choices, and similar engineering guidance belong in developer context, repository guidance, source guidance, or other applicable skills unless they are genuinely part of approved project requirements or architecture.

This document defines the Bonsai operating model.

It is framework-authoring truth, not routine implementation-session context.

For the human-facing workflow and usage instructions, see `README.md`.

---

# Specification Authority

`specification.md` is the authoritative human-owned specification and final truth for Bonsai itself.

Bonsai standard prompts, skills, templates, bootstrap files, helper scripts, and workflow behavior implement this specification. They are not peer authorities.

Conceptually:

```text
specification.md
    Human-owned Bonsai final truth
        ↓
prompts/
    Standard entry workflows
        ↓
skills/
    Detailed triggered procedures
        ↓
templates/
    Structures consumed by workflows
```

The user-facing `README.md` explains how to use Bonsai. It should conform to this specification but is not a peer authority.

When another Bonsai standard artifact conflicts with this specification, this specification is authoritative unless the human explicitly revises it.

Changes to Bonsai behavior, boundaries, ownership, lifecycle, environment model, workspace model, mapping model, or interaction model should therefore be reflected here before or alongside changes to the standard files that implement them.

Detailed procedural mechanics may live in prompts and skills when repeating them here would make the specification unnecessarily large.

---

# Framework Artifact Discovery

`specification.md` is the normal starting point for understanding or designing changes to Bonsai.

The specification defines Bonsai's authoritative behavior and identifies the major framework artifact categories that implement it. Detailed workflow mechanics remain in the applicable prompts, skills, and templates rather than being duplicated here.

When additional implementation-facing context is needed, Bonsai supports progressive framework discovery:

```text
<bonsai-home>/specification.md
        ↓
category guide
        ↓
specific framework artifact
```

The standard category guides are:

```text
<bonsai-home>/skills/skills.md
<bonsai-home>/prompts/prompts.md
<bonsai-home>/templates/templates.md
```

Each category guide identifies the artifacts currently available in that category and gives enough responsibility information for a human or AI to determine which artifacts are relevant to the work being designed.

Category guides are routing aids. They are not peer authorities with `specification.md` and must not duplicate detailed behavioral rules from the artifacts they reference.

A category guide should normally change only when an artifact is:

- added;
- removed;
- renamed; or
- materially changed in responsibility.

Ordinary internal changes to an artifact do not require restating those changes in its category guide.

## Web UI design of Bonsai changes

When designing a change to Bonsai in a Web UI AI session, the human should normally begin by supplying the current:

```text
<bonsai-home>/specification.md
```

along with the proposed change, problem, or enhancement.

The design agent should use the specification to identify which framework artifact categories may contain relevant implementation detail.

When more context is required, the agent should request the applicable category guide and then request specific prompts, skills, templates, or other artifacts as needed.

The human should not need to know Bonsai's complete internal artifact set in advance, and a design session should not require loading the entire Bonsai standard merely to avoid missing a potentially relevant artifact.

Unless the human is intentionally comparing versions, category guides and individual standard artifacts supplied to the design session should come from the same resolved Bonsai Home as the supplied `specification.md`.

Code maps are not part of this category-guide mechanism. Relevant map or source context may be supplied separately when a design discussion needs it.

This progressive-discovery model preserves both sufficient design context and Bonsai's lazy-loading principle.

---

# Core Principles

## Durable truth is separate from working state

For projects, requirements and architecture describe the product and target system.

For both projects and maps, plans and state describe how approved or selected work is currently being carried out.

The implementation agent must not casually turn execution decisions into durable project truth or reusable source truth.

## Human-owned and agent-owned memory are visibly different

For Bonsai project, map-workspace, and context memory, human-owned artifacts normally use natural names and agent-owned execution artifacts use the `agent_` prefix.

Examples:

```text
requirements.md
architecture.md
developer_context.md
icebox.md
map_calibration.md

agent_plan.md
agent_state.md
agent_context.md
```

The `agent_` prefix means Bonsai is allowed to maintain or rewrite that memory artifact according to its lifecycle rules.

It does not mean the artifact is automatically loaded every session.

Generated code-map artifacts use the identities defined by the mapping model rather than the project-memory ownership naming convention.

## Human control should not require constant babysitting

Bonsai uses explicit gates at meaningful boundaries.

Project gates may include:

- Phase 1 detailed-plan approval;
- later phase planning approval when required;
- durable contract review;
- final-truth clarification or revision;
- material execution deviations.

Map work uses human gates when a real human decision is required, but mapping does not inherit project phase, contract, or final-truth gates merely because maps share the workspace lifecycle.

Ordinary maintenance of agent-owned execution memory does not require approval.

## Simple work should stay simple

A normal repository should not require a registry, dependency graph, generic workspace framework, or elaborate configuration system merely to use Bonsai.

Additional structure should appear only when the work actually needs it.

## AI sessions are the primary interaction model

The normal Bonsai coding-agent experience begins inside an AI session.

The canonical startup instruction is intentionally small:

```text
Read .bonsai/start.md and follow its instructions.
```

Optional shell helpers may make setup or startup more convenient, but they are not the conceptual center of Bonsai.

## Bootstrap should resolve identity, not load knowledge

Bootstrap establishes:

- Bonsai Home;
- repository home;
- active workspace identity.

It should not eagerly load every context file, map, skill, requirement area, architecture subsystem, or mapping artifact.

The implementation kernel decides what knowledge is needed after identity is established.

## Deterministic discovery should be cheap

Filesystem enumeration, environment-variable lookup, project listing, map-workspace listing, and similar deterministic tasks should use host tools rather than model reasoning when possible.

Bonsai should not spend model context rediscovering facts that can be resolved cheaply.

## Durable discovery should become agent memory

When an agent discovers an operational fact that is durable, actionable, sufficiently supported, and likely to matter again, it should preserve the current working rule in the appropriate `agent_context.md`.

The intended lifecycle is:

```text
discover
    ↓
qualify as durable and useful
    ↓
preserve current actionable rule
    ↓
reuse rather than rediscover
```

Agent context stores the useful conclusion, not troubleshooting history.

## Context should be loaded when useful

Adding a Bonsai artifact must not automatically add permanent context cost.

Bonsai distinguishes between:

- bootstrap context;
- workflow-triggered context;
- facet-triggered context.

Large or specialized artifacts should normally be loaded only when the current work needs them.

## Projects and maps are both workspaces

Projects and maps are the two concrete Bonsai workspace types.

Both use:

```text
workspace.md
agent_plan.md
agent_state.md
```

Both support:

- exact-next-step resumption;
- execution readiness;
- human gates when required;
- current-session continuation;
- fresh-session continuation;
- fresh-session one-step auto-execution;
- `Exit for now`;
- session-local active workspace identity.

The shared workspace seam exists to eliminate duplicated lifecycle behavior.

It is not a generic plugin system.

Do not generalize Bonsai to arbitrary workspace types until a concrete third use case proves that necessary.

## Mapping is part of Bonsai

Code mapping is an integrated Bonsai capability.

A mapping effort may itself be durable, planned, and resumable across fresh sessions.

The map workspace is distinct from the generated reusable map.

## Code maps are the primary user-facing mapping concept

A **code map** is the normal user-facing concept for source mapping.

A **map workspace** is the durable execution mechanism Bonsai uses to create, maintain, rebuild, and resume work on a code map.

Users should not normally need to understand or manually create a map workspace before asking Bonsai to map source.

The normal intent is:

```text
Create a code map for this source.
```

When persistent mapping work is required, Bonsai may create or reuse the corresponding map workspace automatically.

Explicit map-workspace management remains available when the human needs direct control over mapping execution memory, such as:

- preparing a mapping effort before generated output exists;
- mapping source unrelated to the active project;
- resuming or inspecting a long-running mapping effort;
- managing mapping scope or calibration independently from generated output.

The distinction between map workspace memory and reusable generated map output remains architecturally significant even when normal interaction hides that distinction.

## Maps describe source, not projects

A generated map represents a source universe or source snapshot.

The active Bonsai project may inform map generation, but the project does not become the generated map identity.

## Maps and source must agree

A generated code map represents a particular source snapshot.

Bonsai must not silently use a generated map for one source version while reasoning from another incompatible version.

---

# Bonsai Environment Model

Bonsai separates the shared standard, reusable developer assets, repository-local workspace memory, project truth, and reusable generated source maps.

## Bonsai Home

The **Bonsai Home** is the location of the Bonsai standard used by the current session.

In the normal Bonsai Home model, the environment variable:

```text
BONSAI_HOME
```

identifies that location.

A conceptual Bonsai Home may look like:

```text
$BONSAI_HOME/
├── specification.md
├── README.md
├── prompts/
│   ├── prompts.md
│   ├── implementation.md
│   ├── create_project.md
│   └── create_map.md
├── skills/
│   ├── skills.md
│   ├── artifact_index.md
│   ├── menu.md
│   ├── phase_execution.md
│   ├── dry_run.md
│   ├── handoff.md
│   ├── final_truth_update.md
│   ├── agent_context.md
│   └── code_maps.md
├── templates/
│   ├── templates.md
│   ├── plan_phase_template.md
│   └── icebox_template.md
├── developer_context.md                 # Optional reusable human-owned context
├── agent_context.md                     # Optional reusable agent-owned context
└── maps/
    ├── source-a/
    └── source-b/
```

The exact physical path is host and environment dependent.

Bonsai must not assume that Unix `~`, a Windows user profile, WSL home, and other host notions of a home directory refer to the same physical location.

A developer working across environments may point each environment at the same physical Bonsai Home when practical.

## Embedded Bonsai

A simple repository may carry the Bonsai standard directly in its own `.bonsai` directory.

When `BONSAI_HOME` is not available and the repository-local `.bonsai` contains a valid embedded Bonsai standard, that directory may serve as Bonsai Home.

This allows the simplest topology to collapse naturally:

```text
repo/.bonsai
    = Bonsai Home
    + repository Bonsai memory
```

Embedded mode must use the same workspace semantics as Bonsai Home mode.

When repository-local map workspace memory and the active generated map store physically overlap in Embedded Bonsai, their conceptual ownership remains distinct.

## Creating a Bonsai Home

A repository may begin in embedded mode and later create a reusable Bonsai Home.

**Create Bonsai Home** is a Bonsai workflow, normally available through **See more options** and also invokable as an explicit startup request.

For example:

```text
Read .bonsai/start.md and follow its instructions. Create a Bonsai Home.
```

The workflow requires:

```text
BONSAI_HOME
```

to already be defined.

`BONSAI_HOME` identifies the intended reusable home location. The target directory does not have to exist yet.

If `BONSAI_HOME` is not defined, the workflow must stop and tell the human to configure it before trying again.

Bonsai should not silently substitute a path supplied only for the current session and should not store the Bonsai Home location in `agent_context.md` as a discovery fallback.

The Bonsai Home location is environment identity, not learned project knowledge.

Creating a Bonsai Home must not automatically modify shell startup files, machine configuration, or other developer-owned environment configuration without explicit authorization.

When both a valid `BONSAI_HOME` and an embedded standard are available, the Bonsai Home is the preferred standard for the session.

## Repository home

The **repository home** is the source-repository root containing the local `.bonsai` anchor.

The repository-local `.bonsai/start.md` establishes the repository anchor for a normal AI session.

## Repository-local Bonsai memory

In Bonsai Home mode, repository-local `.bonsai` contains the material that belongs to that repository and its workspaces, plus the small startup bootstrap.

Conceptually:

```text
repo/
└── .bonsai/
    ├── start.md
    ├── developer_context.md              # Optional human-owned local context
    ├── agent_context.md                  # Optional agent-owned local context
    ├── projects/
    │   └── main/
    │       ├── workspace.md
    │       ├── requirements.md
    │       ├── architecture.md
    │       ├── agent_plan.md
    │       ├── agent_state.md
    │       ├── agent_context.md          # Optional project-specific operational context
    │       ├── icebox.md                 # Optional
    │       ├── plan/
    │       │   └── agent_plan_phase_1.md
    │       ├── requirements/
    │       │   └── requirements_<AREA>.md
    │       └── architecture/
    │           └── architecture_<SUBSYSTEM>.md
    └── maps/
        └── source-a/
            ├── workspace.md
            ├── agent_plan.md
            ├── agent_state.md
            ├── map_calibration.md        # Optional human-owned input
            └── plan/                     # Optional detailed mapping plans
```

Bonsai Home mode does not require copies of `specification.md`, standard prompts, skills, or templates inside every repository.

## Developer-level reusable material

A Bonsai Home may contain reusable context and generated maps that apply across repositories.

Examples include:

- stable developer preferences;
- host or toolchain context;
- reusable operational knowledge;
- source locations;
- reusable generated code maps.

Developer-level material must remain distinct in meaning from repository and workspace memory even when it physically lives under the same Bonsai Home.

---

# Workspaces

A Bonsai workspace is a repository-local durable unit of resumable agent work.

Bonsai currently defines exactly two concrete workspace types:

```text
project
map
```

Their directory locations remain concrete and user-facing:

```text
repo/.bonsai/projects/<project>/
repo/.bonsai/maps/<map>/
```

Do not introduce a generic repository-level `workspaces/` directory.

## `workspace.md`

Every workspace has:

```text
workspace.md
```

`workspace.md` is the stable declarative entry document for the workspace.

It identifies the workspace type and gives the implementation kernel enough routing information to determine which workspace-specific workflow and secondary artifacts apply.

It is not execution state.

Volatile progress, exact next steps, blockers, readiness, and active detailed-plan identity belong in `agent_state.md`.

Roadmap structure belongs in `agent_plan.md`.

A workspace entry document should remain small enough to load routinely after workspace identity has been resolved.

## Shared workspace execution memory

Every workspace uses:

```text
agent_plan.md
agent_state.md
```

`agent_plan.md` is the workspace-wide roadmap.

`agent_state.md` is the current resume state.

Workspace-specific sections may extend those common roles without changing their basic ownership.

---

# Startup Bootstrap

Every Bonsai-enabled repository has the canonical local entry point:

```text
.bonsai/start.md
```

The normal implementation-session prompt is:

```text
Read .bonsai/start.md and follow its instructions.
```

The human may append a natural-language startup request when useful.

Project example:

```text
Read .bonsai/start.md and follow its instructions. Active project: configuration-runtime.
```

Map example:

```text
Read .bonsai/start.md and follow its instructions. Active map: niagara4.
```

Other examples:

```text
Read .bonsai/start.md and follow its instructions. Create a Bonsai Home.
```

```text
Read .bonsai/start.md and follow its instructions. Manage Code Maps.
```

Bonsai should not require a formal startup-command language. Natural language is sufficient.

`start.md` is deliberately small.

Its job is to establish environment identity, resolve the active workspace when the request requires one, load that workspace's `workspace.md`, and hand control to the Bonsai Home or embedded implementation kernel.

## Bootstrap responsibilities

The bootstrap should:

1. establish repository home from the local `.bonsai` anchor;
2. resolve Bonsai Home;
3. resolve the active workspace type and name when operating in a workspace;
4. locate and read that workspace's `workspace.md`;
5. preserve Bonsai Home, repository home, active workspace identity, and the startup request as current-session context;
6. load `<bonsai-home>/prompts/implementation.md`;
7. continue under the standard implementation workflow.

The bootstrap should not routinely load requirements, architecture, generated maps, developer context, agent context, detailed plans, or specialized skills itself.

## Bonsai-home resolution

The preferred Bonsai Home mechanism is:

```text
BONSAI_HOME
```

Resolution should conceptually follow:

1. use `BONSAI_HOME` when it identifies a valid Bonsai standard;
2. otherwise use the repository-local `.bonsai` as Bonsai Home when it contains a valid embedded standard;
3. otherwise ask the human to identify or configure Bonsai Home.

Bonsai should not perform broad filesystem searches merely to guess where the standard may be installed.

## Workspace selection

Explicit workspace identity supplied by the human is authoritative for that session.

Project form:

```text
Active project: <project>.
```

Map form:

```text
Active map: <map>.
```

An ordinary unqualified startup continues to use project-oriented default resolution:

1. if `projects/main` exists, use it;
2. otherwise enumerate project directories;
3. if exactly one project exists, use it;
4. if several projects exist, present stable numbered human selection;
5. if no project exists, surface the applicable project creation/design or other requested workflow.

A map workspace is selected explicitly through `Active map: <map>` or through a map-management workflow.

Bonsai should not guess that an unqualified ordinary startup means a map merely because map workspaces exist.

Whenever Bonsai asks the human to choose one workspace from several workspaces of the same concrete type, present the available directories in stable lexical order as numbered choices and accept the corresponding number as the selection.

## Active workspace is session state

The active workspace belongs to the current AI session.

It must not be persisted as a mutable repository-wide pointer.

It also should not be stored in durable `agent_context.md` merely because the current session selected it.

This allows concurrent sessions in the same repository to operate on different projects or maps without interfering with one another.

---

# Projects

A repository may contain one Bonsai project or many.

Each project owns its own:

- `workspace.md`;
- requirements;
- architecture;
- execution roadmap;
- execution state;
- phase plans;
- optional icebox;
- layered project truth;
- optional project operational context;
- other project-specific durable artifacts.

## Conventional default project

The conventional project name for a normal single-project repository is:

```text
main
```

`projects/main` is a real project directory.

It is not an alias, symlink convention, or mutable pointer to another project.

For the common case:

```text
repo/.bonsai/projects/main/
```

the human normally starts with only:

```text
Read .bonsai/start.md and follow its instructions.
```

No project name is necessary.

## Named projects

Large repositories may contain several independent Bonsai projects:

```text
.bonsai/projects/
    project-a/
    project-b/
    project-c/
```

Project selection changes the active workspace for the current session only.

## Project management

Project-management actions are part of the normal Bonsai interaction model and normally live under **See more options**.

Useful actions include:

- List Projects;
- Switch Project;
- Create Project.

Creating a project establishes its workspace-memory location.

It does not invent requirements or architecture.

If durable project design has not yet been synthesized, the project's execution readiness is effectively `Design required`.

---

# Artifact Ownership

Ownership determines who controls the durable meaning of an artifact.

Ownership is separate from loading behavior.

## Human-owned artifacts

Human-owned project, map-workspace, and context artifacts use natural names.

Typical examples include:

```text
requirements.md
architecture.md
developer_context.md
icebox.md
map_calibration.md
```

Human ownership does not mean the human must manually edit every line.

An AI may draft or mechanically maintain a human-owned artifact when instructed, but changes to durable meaning require human authorization.

## Agent-owned artifacts

Agent-owned workspace and context artifacts use the `agent_` prefix.

Typical examples include:

```text
agent_plan.md
agent_state.md
agent_context.md
plan/agent_plan_phase_<N>.md
plan/agent_plan_<scope>.md
```

The agent actively maintains these when their current truth changes.

They should describe current useful state, not preserve a historical diary.

## Generated map artifacts

Generated reusable map artifacts are agent-produced source-navigation knowledge.

Examples include:

```text
code_map.md
subsystems/
namespace_router.tsv
manifest.tsv
symbol_index.tsv
```

They are outputs of the mapping workflow, not execution memory for the map workspace.

## Standard framework artifacts

Prompts, skills, templates, category guides, bootstrap files, and helper scripts are Bonsai standard implementation artifacts.

Their identities are defined by the framework rather than by the workspace-memory ownership prefix convention.

An implementation agent may create, modify, rename, or remove them only when an authorized Bonsai change requires it and the resulting standard remains consistent with `specification.md`.

## Avoid hybrid ownership

Bonsai should avoid artifacts whose ownership is genuinely ambiguous.

When an artifact contains human-authorized meaning but is mechanically maintained by the agent, ownership is determined by who controls its durable meaning.

`icebox.md` remains human-owned because an observation may only be preserved there when the human chooses to retain it.

`map_calibration.md` remains human-owned because it expresses mapping emphasis and guidance rather than agent execution state.

---

# Project Final Truth

## `requirements.md`

`requirements.md` is human-owned product truth.

It defines:

- what the system is for;
- who it serves;
- workflows;
- functional requirements;
- product constraints;
- accepted product decisions;
- scope boundaries;
- intentionally retained unresolved product questions.

It should not become an implementation log.

When one product area becomes too detailed for the top-level document, Bonsai may use:

```text
requirements/requirements_<AREA>.md
```

The top-level requirements should remain an orienting summary.

## `architecture.md`

`architecture.md` is human-owned target implementation truth.

It defines, when required by the approved design:

- target system structure;
- major subsystems;
- data ownership;
- durable contracts;
- dependency constraints;
- allowed flows;
- cross-cutting rules;
- architectural guardrails;
- explicitly rejected approaches.

Architecture describes the system intended to exist after successful implementation.

It should not manufacture interfaces, modules, adapters, abstraction layers, or other structure merely to make the document appear complete.

When one subsystem requires deeper architectural truth, Bonsai may use:

```text
architecture/architecture_<SUBSYSTEM>.md
```

## Final-truth impact

Requirements and architecture together form the normal project final truth.

Additional project-specific artifacts may also become final truth when the human explicitly designates them that way.

During project implementation, proposed or completed work is classified against final truth as:

- `None`;
- `Clarification`;
- `Revision`.

A revision requires explicit human approval before substantive implementation proceeds under the changed direction.

Map workspaces do not inherit project final-truth classification unless the map work is explicitly modifying project final truth.

---

# Agent Execution Memory

## `agent_plan.md`

`agent_plan.md` is the agent-maintained workspace-wide roadmap.

Common responsibilities include:

- major work units;
- status of roadmap work;
- the active roadmap area;
- roadmap-level deferrals;
- completed roadmap work;
- enough structure to determine whether work remains.

It should remain roadmap-level.

### Project `agent_plan.md`

A project plan additionally records project execution concepts such as:

- implementation phases;
- active phase;
- execution mode;
- phase-planning state;
- approved execution-basis type;
- phase-plan presence;
- phase-plan approval state when a detailed plan exists.

Detailed project execution sequencing belongs in a phase plan when one is needed.

### Map `agent_plan.md`

A map plan records the overall mapping roadmap.

Useful map work units may include:

- modules;
- packages;
- subsystems;
- source regions;
- cross-module relationship passes;
- validation or reconciliation passes;
- maintenance scopes.

A map roadmap must be able to decompose large mapping units without forcing the entire unit into one session.

## `agent_state.md`

`agent_state.md` is the current workspace resume state.

It records only information that could materially change what the next session does.

Common contents include:

- active workspace objective;
- execution mode when applicable;
- execution readiness;
- current objective;
- concise current snapshot;
- resume-critical files;
- active blockers or risks;
- active detailed plan when one exists;
- exact next step;
- success condition;
- compact active dry-run baseline when one exists.

Project state may additionally record:

- current phase;
- phase-planning state;
- approved execution-basis type;
- phase-plan approval state;
- current phase pass for two-pass contract-first execution.

Map state may additionally record:

- current mapping scope;
- active map plan;
- source/map identity concerns;
- current generated-map reconciliation concerns.

`agent_state.md` is not session history.

When updating it, the agent should remove:

- completed next steps;
- resolved blockers;
- obsolete active files;
- stale observations;
- superseded decisions;
- expired dry-run baselines;
- commentary that no longer affects resumption.

A useful rule is:

> If removing a fact would not materially change what the next workspace session does, it probably does not belong in `agent_state.md`.

## Project phase plans

Detailed active project phase plans are agent-owned:

```text
plan/agent_plan_phase_<N>.md
```

Phase 1 is intentionally special.

Every newly synthesized Bonsai project begins implementation by drafting and reviewing its Phase 1 detailed plan before substantive implementation begins.

Every later phase also passes through phase planning before substantive execution unless an already-approved detailed plan for that phase remains applicable.

Later phase planning may remain lightweight. Create a detailed phase plan only when the phase genuinely benefits from one.

Useful reasons for a detailed later phase plan include:

- ordered sequencing too detailed for `agent_plan.md`;
- contract-first two-pass execution;
- multiple meaningful review gates;
- explicit constraints that must stay visible through execution.

A phase plan should not exist merely because a phase touches several files.

## Map detailed plans

A map workspace may create detailed scoped plans under:

```text
plan/
```

when a mapping unit is too large for useful roadmap-level execution.

Examples:

```text
plan/agent_plan_baja.md
plan/agent_plan_baja_lang.md
plan/agent_plan_core.md
```

These are detailed mapping plans, not project phases.

The map-wide `agent_plan.md` remains the authoritative roadmap.

`agent_state.md` identifies the active detailed map plan and the exact next step.

Map planning may decompose recursively in concept:

```text
map roadmap
    ↓
mapping unit
    ↓
detailed plan when needed
    ↓
smaller mapping unit
    ↓
another detailed plan when needed
```

The filesystem representation should remain simple.

Use flat scoped plan filenames under `plan/` rather than introducing nested plan-directory trees until actual use demonstrates that nesting is needed.

Creating or refining an agent-owned detailed map plan does not by itself introduce a project-style human approval gate.

A human gate is required only when the mapping workflow reaches a decision that genuinely requires human authorization, changes the requested mapping scope, or is otherwise governed by an explicit review rule.

## Project phase completion and body-of-work completion

A project phase is one execution unit within the approved roadmap.

Completing a phase completes that phase only.

After a phase completes, Bonsai must reconcile the approved roadmap before deriving the next execution condition.

If unfinished project roadmap work remains, Bonsai continues the body of work by establishing the next applicable phase and its planning, review, blocker, or execution gate.

`Execution Readiness: Complete` is valid for a project only when the approved roadmap contains no unfinished implementation work in the current body of work.

## Map-scope completion

A map workspace is `Complete` when the current approved or selected mapping scope contains no unfinished mapping work and the generated map output has been reconciled sufficiently for that scope.

Map completion does not mean the source can never require mapping work again.

A later source change, maintenance request, expanded mapping scope, or newly discovered need may reactivate the existing map workspace.

---

# Developer Context

`developer_context.md` contains durable context intentionally owned by the developer or team.

Useful examples include:

- coding preferences;
- testing philosophy;
- abstraction preferences;
- local SDK locations;
- known build constraints;
- stable runtime constraints;
- AI working preferences;
- recurring environment conventions.

Developer context is not product truth.

It must not override approved requirements or architecture.

It also should not become the automatic destination for facts discovered by an agent.

Those facts belong in agent operational context when they qualify for preservation.

---

# Agent Context

`agent_context.md` is agent-owned operational memory.

Useful agent context may include:

- reliable build or tool invocation knowledge;
- discovered tooling limitations;
- reliable temporary-directory choices;
- runtime or filesystem constraints;
- source locations;
- map locations or map-selection rules;
- environment-specific working rules;
- stable operational facts discovered through actual repository work.

Agent context should preserve current actionable knowledge, not troubleshooting history.

Applicable agent context governs concrete operational choices within its authorized scope.

Using an existing correct agent-context rule is read-only consumption.

Do not rewrite, normalize, or restate `agent_context.md` merely because its guidance was applied.

Agent context must not contain secrets.

It also does not authorize the agent to:

- install software;
- modify machine configuration;
- change project dependencies;
- alter developer-owned context;
- expand implementation or mapping scope.

Current blockers belong in the active workspace's `agent_state.md`.

A durable lesson learned while resolving a blocker may also belong in `agent_context.md`.

## Agent-context scopes

Bonsai supports developer-level, repository-level, and project-level agent context.

Conceptually:

```text
$BONSAI_HOME/agent_context.md
        +
repo/.bonsai/agent_context.md
        +
repo/.bonsai/projects/<project>/agent_context.md
        =
effective project operational context
```

More specific statements win when they conflict with broader statements.

A discovered fact should be stored at the narrowest scope that still makes it reusable.

Examples:

- a source checkout location reused across several repositories may belong in developer-level agent context;
- a build rule shared by all workspaces in one repository belongs in repository-level agent context;
- the code maps used only by one Bonsai project belong naturally in that project's `agent_context.md`;
- the active project or active map for the current session belongs in none of them.

Map-workspace execution identity and progress remain in map workspace memory, not in agent context.

## Project-to-code-map associations

A project may explicitly select reusable generated code maps that are useful to it.

Store that selection in:

```text
repo/.bonsai/projects/<project>/agent_context.md
```

Canonical compact form:

```text
Useful code maps:
- barcache
- tickerview
```

Bonsai should support adding and removing project map selections through code-map management without searching the entire map store in every future session.

Adding or removing an association changes only project operational context.

It does not create, rebuild, move, rename, or delete the reusable generated map.

---

# Context Layering

Bonsai supports reusable developer-level context plus more specific repository and project context.

Conceptually:

```text
developer-level context
        +
repository-local context
        +
project-local context when applicable
        =
effective context
```

When several levels address the same subject, the more specific statement is authoritative.

Bonsai does not require a formal Markdown override language.

Normal human-readable specificity is preferred.

Additional layers should not be introduced unless real use demonstrates a need for them.

---

# Lazy Loading

Bonsai treats context loading as a first-class concern.

The number of Bonsai files is not itself a problem.

Loading all of them during every session is.

## Bootstrap context

Bootstrap context is small and necessary to establish identity and determine what should happen next.

The local `start.md` establishes Bonsai Home, repository home, and active workspace identity.

The selected `workspace.md` establishes the workspace type and routing seam.

The standard implementation prompt then loads only the minimum workspace state required to determine the current execution condition.

## Workflow-triggered context

Workflow files are loaded when the current state or requested action invokes that workflow.

Examples include:

- menu presentation;
- project phase planning;
- contract review;
- dry run;
- handoff;
- final-truth reconciliation;
- project management;
- code-map management;
- map generation or maintenance.

## Facet-triggered context

Specialized context is loaded only when the current work needs that facet.

Examples include:

- generated code maps;
- developer context;
- agent context;
- deep subsystem architecture;
- detailed requirement areas;
- detailed map plans;
- preserved icebox observations.

The implementation kernel defines the exact loading rules.

The general principle is:

> Adding an artifact must not automatically make every future session more expensive.

---

# Project Creation Workflow

Product and architecture design is a Bonsai capability, but it is not primarily a coding-CLI workflow.

Bonsai assumes that design often happens in a Web UI AI conversation because conversational design is easier to inspect and can be materially cheaper than coding-agent sessions.

The design should develop naturally.

Bonsai should not force a design conversation into templates prematurely.

When the design is mature enough to preserve, the human uses:

```text
<bonsai-home>/prompts/create_project.md
```

The workflow synthesizes the discussion into durable Bonsai project memory.

For initial synthesis, it packages a repository-root extractable zip that normally contains:

```text
.bonsai/
    start.md
    projects/
        <project>/
            workspace.md
            requirements.md
            architecture.md
            agent_plan.md
            agent_state.md
```

It may also contain project-local:

```text
agent_context.md
requirements/
architecture/
```

when the design genuinely warrants them.

Before initial synthesis, the workflow resolves the project name.

If the human already supplied one, use it after validation.

Otherwise ask what the Bonsai project should be called and suggest `main` as the conventional default.

The generated `.bonsai/start.md` is the canonical repository-local bootstrap for the Bonsai version that owns the workflow.

For an existing-project design update, the workflow preserves the existing project identity when unambiguous and packages only materially affected project files.

If the human has identified external source or code maps during design, the workflow may seed project-level `agent_context.md` with that approved operational information.

The project creation workflow does not generate the initial detailed Phase 1 plan.

Phase 1 planning remains the first implementation gate.

---

# Map Creation Workflow

Bonsai supports both direct code-map creation from a coding-agent session and explicit map-workspace creation from a Web UI design or calibration conversation.

## Direct code-map creation

The normal coding-agent mapping intent is:

```text
Create a code map.
```

When invoked from a repository with an active Bonsai project, Bonsai should use already-established context rather than require the human to restate information it can determine reliably.

Where unambiguous, Bonsai should derive sensible defaults for:

- source location from the current repository;
- source identity from the current checkout;
- map name from the repository or active project context;
- initial mapping scope from the selected source;
- project association when the new map is clearly being created for the active project.

The human may override these defaults.

If persistent mapping work is required and no suitable map workspace exists, Bonsai creates the corresponding repository-local map workspace automatically.

If a suitable map workspace already exists, Bonsai should reuse or resume it rather than create duplicate execution memory.

Direct code-map creation may therefore conceptually perform:

```text
source selection
    ↓
map identity resolution
    ↓
create or reuse map workspace
    ↓
mapping workflow
    ↓
generated reusable code map
```

Creating the workspace is part of implementing the user's mapping intent rather than a prerequisite the user must normally perform separately.

## Explicit map-workspace creation

A mapping effort may also begin in a Web UI design or calibration conversation.

The human may use:

```text
<bonsai-home>/prompts/create_map.md
```

to explicitly establish a repository-local map workspace before mapping begins.

This workflow is useful when:

- mapping scope requires deliberate calibration;
- the source is external to the project currently being discussed;
- mapping will be substantial enough to benefit from preparation;
- the human wants to prepare durable mapping memory before entering a coding-agent session.

Initial output normally contains:

```text
.bonsai/
    start.md
    maps/
        <map>/
            workspace.md
            agent_plan.md
            agent_state.md
            map_calibration.md
```

`map_calibration.md` is optional human-owned mapping guidance and should be synthesized when useful.

The workflow may also create the empty `plan/` directory or allow it to appear later when detailed map planning is needed.

The explicit map-workspace creation workflow must not generate reusable map outputs such as:

```text
code_map.md
subsystems/
namespace_router.tsv
manifest.tsv
symbol_index.tsv
```

Those remain outputs of the coding-agent mapping workflow.

The actual source remains authoritative.

Creating a map workspace does not require creating a Bonsai project for that source.

---

# Implementation Workflow

After `.bonsai/start.md` resolves session identity and loads the selected `workspace.md`, implementation continues through:

```text
<bonsai-home>/prompts/implementation.md
```

The implementation kernel:

1. receives Bonsai Home, repository home, active workspace type/name/home, and the retained startup request;
2. loads the minimum active workspace state;
3. determines the exact next step and execution readiness;
4. routes through the workspace-specific workflow defined by `workspace.md`;
5. loads additional project truth, map output, plans, context, or skills only when required;
6. identifies blockers or inconsistencies;
7. applies project final-truth classification when project final truth is implicated;
8. stops at a structured startup gate unless an explicit startup request authorizes the one exact next action to proceed without stopping at that gate after canonical state reconstruction;
9. executes only that human-authorized exact next action and does not carry startup authorization into a subsequent action;
10. reconciles completed work;
11. maintains current workspace execution memory;
12. preserves qualifying operational discoveries;
13. reconciles affected framework category guides when authorized standard artifacts are added, removed, renamed, or materially change responsibility;
14. stops at the next natural gate.

The implementation prompt is a stable router and invariant set.

Project-specific phase execution belongs in project workflow and skills.

Mapping-specific source inspection, generated-map maintenance, and source/map identity handling belong in the mapping workflow and `skills/code_maps.md`.

Detailed workflow belongs in triggered skills rather than one permanently loaded monolithic prompt.

---

# Execution Readiness

Bonsai makes the difference between planned, blocked, review-bound, executable, and complete work explicit.

Common execution-readiness values include:

| Value | Meaning |
| --- | --- |
| `Design required` | A required human-owned design or scope decision must be resolved first. |
| `Awaiting human review` | A required plan, contract, revision, or other artifact is waiting for approval. |
| `Ready to execute` | The exact next step has an authorized basis and no required gate remains. |
| `Blocked` | A concrete blocker prevents safe execution. |
| `Complete` | The active workspace's current roadmap or selected scope contains no unfinished work. |

Projects additionally use:

| Value | Meaning |
| --- | --- |
| `Phase planning required` | The current project phase does not yet have an approved execution basis, including the required planning decision about whether a detailed phase plan is warranted. |

The existence of a plan does not imply implementation authorization.

For maps, creating or refining an agent-owned detailed plan is ordinary execution-memory maintenance unless a real human decision or explicit review rule makes a gate necessary.

---

# Human Gates and Menus

Bonsai uses explicit human gates at material boundaries.

Menus are part of the workflow contract, not incidental presentation.

The detailed reusable interaction rules live in:

```text
<bonsai-home>/skills/menu.md
```

Individual workflows determine which decisions must be offered.

The menu skill determines how those decisions are presented and how secondary actions behave.

## Primary menus

Primary menus stay focused on the decision immediately required by the current workflow.

They should not accumulate every optional Bonsai capability merely because those capabilities exist.

Actions should use concrete wording that identifies the real next step.

## See more options

Less-frequent actions normally live under:

**See more options**

**See more options** is a navigation action.

Selecting it opens a contextual secondary menu.

Depending on context, this may include:

- Manage Projects;
- Manage Code Maps;
- Create Bonsai Home, when running embedded and no reusable home exists;
- Dry Run;
- diagnostics;
- maintenance actions;
- other secondary workflows relevant to the current state.

The submenu is contextual.

It must not become a fixed junk drawer containing every possible Bonsai action.

A normally secondary action may be promoted into the primary menu when the current context makes it directly relevant.

## Subordinate workflows

A menu action may invoke a smaller workflow such as:

- project management;
- code-map management;
- observation review;
- clarification;
- dry run;
- correction;
- triage.

After the subordinate workflow completes, Bonsai should return to the invoking gate with refreshed choices unless the subordinate action created a new required gate or materially changed execution state.

A subordinate action should not accidentally make its parent gate disappear.

## Startup gate

Before substantive work begins, the implementation agent summarizes the current execution condition and normally stops.

The normal gate offers actions equivalent to:

1. Proceed with the identified next step.
2. Correct or discuss the identified next step.
3. Exit for now.

Secondary actions remain accessible through **See more options** when applicable.

A natural-language startup request may explicitly authorize the one exact next action to proceed without stopping at the startup gate.

The implementation agent must still reconstruct canonical durable state first and execute only the exact next action that state establishes.

This exception bypasses only the startup presentation gate.

It does not bypass an independent design, approval, review, final-truth, contract, blocker, or other mandatory human gate.

---

# Handoff

`skills/handoff.md` owns the shared workspace handoff lifecycle.

Handoff is not project-only behavior.

At a natural boundary, handoff reconciles the active workspace before presenting continuation choices.

## Shared reconciliation

For both projects and maps, handoff reconciles:

- completed work;
- relevant checks or validation;
- `agent_plan.md`;
- `agent_state.md`;
- active detailed plan when one exists;
- exact next step;
- success condition;
- execution readiness;
- blockers or inconsistencies;
- whether the current workspace scope is complete.

## Project-specific reconciliation

When the active workspace is a project, handoff additionally reconciles applicable:

- project final-truth impact;
- phase completion;
- roadmap continuation;
- phase-plan state;
- contract state;
- icebox observations;
- other project-specific gates.

## Map-specific reconciliation

When the active workspace is a map, handoff additionally reconciles applicable:

- current mapping scope;
- active detailed map plan;
- generated map output touched by the completed work;
- source/map identity concerns;
- whether generated output is sufficiently reconciled for the completed mapping scope.

Map handoff must not invent project final-truth, phase, or contract semantics merely to fit the shared lifecycle.

---

# Code Maps

Generated code maps are reusable navigation knowledge for source.

They help an agent:

- orient quickly;
- identify the right owning subsystem;
- find the right source to inspect;
- avoid repeatedly rediscovering important architectural structure;
- preserve non-obvious calling and extension mechanics when they are likely to matter again.

Generated maps do not replace source inspection.

They help future agents read the right source first.

## Code-map interaction model

Humans normally interact with **code maps** rather than with the execution machinery used to build them.

A request to create, update, inspect, rebuild, remove, or associate a code map should therefore be expressed primarily in code-map terms.

Map workspaces remain visible when their lifecycle matters, but normal code-map operations may create, reuse, resume, or update map workspace memory as necessary.

Bonsai should avoid requiring the human to choose between "create a map workspace" and "create a code map" when the human's actual intent is simply to map the current source.

## Map workspace memory and generated map output are separate

For a repository checkout being mapped, durable mapping execution memory belongs with that source repository:

```text
<source-repository>/.bonsai/maps/<map>/
    workspace.md
    agent_plan.md
    agent_state.md
    map_calibration.md        # optional human-owned input
    plan/                     # optional detailed mapping plans
```

The reusable generated map belongs in the active map store.

With a reusable Bonsai Home:

```text
$BONSAI_HOME/maps/<map>/
    code_map.md
    subsystems/
    namespace_router.tsv
    manifest.tsv
    symbol_index.tsv
    ...
```

Conceptually:

```text
repo/.bonsai/      = workspace memory
$BONSAI_HOME/maps/ = reusable generated source knowledge
```

In Embedded Bonsai these locations may physically overlap.

Their conceptual roles remain distinct.

Do not place mapping `agent_plan.md` or `agent_state.md` into the reusable generated map merely to support continuation.

## `map_state.md` is retired

The mapping model does not use:

```text
map_state.md
```

Mapping continuation belongs in repository-local:

```text
agent_plan.md
agent_state.md
```

The standard must not create, require, maintain, or template `map_state.md`.

## Map identity

A generated map describes a particular source snapshot.

Bonsai must be able to determine what source the map represents.

Relevant identity may include:

- logical source name;
- version;
- Git revision;
- artifact coordinates;
- source type;
- exact source location.

The exact metadata format should remain as small as possible.

For released dependencies, a matching source artifact may be more appropriate than an unrelated development checkout.

For active cross-repository development, an exact matching repository revision may be preferable.

## Map entry document

A generated map set uses:

```text
code_map.md
```

as its normal entry document.

The entry document identifies the map and routes the agent into more detailed generated map data when needed.

## Mapping inputs

Every map is grounded in actual source.

Additional mapping context may come from:

- relevant source-local Bonsai project memory;
- `map_calibration.md`;
- source structure;
- previous generated map output;
- durable agent context.

Project memory and `map_calibration.md` may both be used when both are available.

Neither replaces actual source inspection.

## `map_calibration.md`

`map_calibration.md` is optional human-owned source-specific mapping guidance.

It may describe:

- important concepts;
- representative entry points;
- areas that deserve deeper mapping;
- misleading or low-value areas;
- extension points;
- patterns worth recognizing;
- source areas that can be treated lightly.

It is not:

- product truth;
- architecture truth;
- source evidence;
- generated map output;
- execution state;
- map identity.

## Mapping context and map storage are separate

The source context used to create a map, repository-local workspace memory, and the location where the reusable generated map is stored are different concerns.

When mapping an external source, Bonsai should operate against the actual selected source and use that source's relevant project memory and map workspace when available.

If a Bonsai Home is active, the resulting reusable generated map still belongs under:

```text
$BONSAI_HOME/maps/<map>/
```

This produces the rule:

> Map creation and maintenance use source-local workspace context. Generated reusable map storage uses the active Bonsai map store.

## External source without project memory

Bonsai must support mapping source that has no Bonsai project.

The workflow is:

```text
actual source
    +
repo-local map workspace
    ↓
mapping workflow
    ↓
named reusable generated map
```

A map workspace is sufficient durable memory for a large standalone mapping effort.

---

# Integrated Mapping Workflow

Code mapping is part of the main Bonsai workflow rather than a parallel standalone subsystem.

The Bonsai standard routes active mapping through the same startup, workspace, menu, context-layering, execution-memory, handoff, and fresh-session model used by projects where those concepts genuinely apply.

A mapping workflow executes through a map workspace, whether that workspace was explicitly selected by the human or created or reused automatically while fulfilling a code-map operation.

A mapping workflow should:

- resolve, create, or reuse the applicable map workspace;
- make that workspace active for the mapping execution session;
- use the active Bonsai generated-map store;
- identify the source being mapped independently from any active project;
- use relevant project memory when available;
- use source-local `map_calibration.md` when available;
- use actual source as authoritative;
- decompose large mapping units through optional detailed map plans when useful;
- preserve stable source locations or mapping rules in appropriate agent context;
- maintain map `agent_plan.md` and `agent_state.md`;
- support exact-next-step fresh-session continuation;
- reconcile generated output and map/source identity before declaring the current mapping scope complete.

Existing generated map index and source-navigation structures should be retained where they remain useful.

Integration does not require rewriting generated map data solely for architectural neatness.

---

# Manage Code Maps

Bonsai exposes code-map lifecycle actions through:

**Manage Code Maps**

During normal project implementation, it generally appears under **See more options**.

The menu should present **code maps** as the primary managed object.

Useful primary operations include:

- Create Code Map;
- Inspect Code Map;
- Update or Rebuild Code Map;
- Remove Code Map;
- Add a Code Map to the Active Project;
- Remove a Code Map from the Active Project;
- Manage Map Workspaces.

Map-workspace operations are secondary lifecycle operations rather than peers of normal code-map creation.

**Manage Map Workspaces** may provide actions such as:

- Create Map Workspace;
- List or Inspect Map Workspaces;
- Resume Map Workspace;
- Inspect Map Workspace State.

## Context-aware code-map creation

When **Create Code Map** is invoked from an active repository or project, Bonsai should prefer known session context over asking the human to restate it.

When reliably derivable, Bonsai should present or use defaults for:

- the current repository as the source;
- the current checkout as source identity;
- a map name derived from the repository or active context;
- the active project as a likely consumer of the map.

The human must be able to change those choices before they become durable when the defaults are not appropriate.

Creating a code map may automatically create the repository-local map workspace required to perform and resume the mapping effort.

The existence of that workspace is not itself a reason to interrupt the user with a separate workspace-creation decision.

If a suitable workspace already exists, Bonsai should reuse it.

## Discovery and inspection

Map-workspace discovery uses:

```text
repo/.bonsai/maps/
```

Reusable generated-map discovery uses the active Bonsai map store.

These are related but distinct collections.

Bonsai should use cheap deterministic discovery to determine available map names and workspace names.

It should not perform expensive source inspection, full map validation, or source-identity reconciliation merely to display the management menu unless the current workflow actually requires those checks.

An **Inspect Code Map** or source-identity operation may perform deeper inspection when selected.

If the management screen already displays the discovered generated maps, a separate operation need not exist merely to list the same names again.

## Project associations

Project map associations are stored in project `agent_context.md`.

Managing an association does not create, rebuild, move, or delete the generated map.

Creating a code map for the current project may offer or establish that association when the intent is unambiguous, but map identity remains independent from project identity.

## First-use behavior

When Bonsai encounters a substantial existing codebase without a useful generated map, it may surface **Create Code Map** once as a primary contextual action.

If the human declines, mapping remains available through **See more options** rather than repeatedly interrupting implementation.

For a greenfield repository with little useful source, mapping should normally be deferred.

---

# Multi-Repository Source Universes

A Bonsai project may depend on source outside its repository.

Example:

```text
application
    → library-a
    → library-b
```

Each source repository may have its own Bonsai projects, map workspaces, both, or neither.

Reusable generated maps may live under:

```text
$BONSAI_HOME/maps/
    application/
    library-a/
    library-b/
```

A consuming project may explicitly select useful maps through project `agent_context.md`.

Bonsai may also use dependency information, source locations, map identity, and source inspection to locate appropriate source and matching generated maps.

Once Bonsai discovers stable cross-repository source locations or working rules, it should preserve them in the appropriate agent context so subsequent sessions do not repeatedly rediscover them.

Bonsai should not require the consuming project's requirements or architecture to duplicate machine-specific source paths.

---

# Archaeological Work

Existing software often needs to be understood before new design or implementation begins.

Archaeological work may inspect:

- source structure;
- runtime behavior;
- durable contracts;
- existing tests;
- extension points;
- architectural relationships;
- previous implementation decisions.

Archaeological output is supporting analysis.

It does not automatically become human-owned product or architecture truth.

Useful archaeological knowledge may later inform:

- requirements;
- architecture;
- project plans;
- map plans;
- generated code maps;
- agent context.

The destination depends on the kind of truth discovered.

---

# Framework Prompts

Standard entry workflows live under:

```text
<bonsai-home>/prompts/
```

The category guide is:

```text
<bonsai-home>/prompts/prompts.md
```

The exact prompt set should remain small.

## `prompts/implementation.md`

Stable workspace-aware implementation kernel and router.

It receives Bonsai Home, repository home, active workspace identity, and the retained startup request from `../../../distech/eclypse-framework/.bonsai/start.md`, then determines the minimum additional context required for the current execution condition.

## `prompts/create_project.md`

Web UI project creation and repository-bootstrap packaging workflow.

It turns a mature design conversation into durable Bonsai project workspace memory and, for initial synthesis, a repository-root zip containing the canonical local `../../../distech/eclypse-framework/.bonsai/start.md` anchor plus the selected project under:

```text
.bonsai/projects/<project>/
```

## `prompts/create_map.md`

Web UI map-workspace creation and repository-bootstrap packaging workflow.

It turns mapping discussion or source calibration into a resumable repository-local map workspace under:

```text
.bonsai/maps/<map>/
```

It may synthesize `map_calibration.md`.

It does not generate reusable map outputs.

---

# Framework Skills

Detailed workflow behavior lives in triggered skills rather than being permanently loaded.

The category guide is:

```text
<bonsai-home>/skills/skills.md
```

Typical skills include:

- artifact index;
- menu;
- phase execution;
- dry run;
- handoff;
- final-truth update;
- agent context;
- code maps.

Skills are Bonsai standard files.

They are not workspace memory.

## `skills/artifact_index.md`

`skills/artifact_index.md` owns framework category-guide maintenance.

It maintains:

```text
<bonsai-home>/skills/skills.md
<bonsai-home>/prompts/prompts.md
<bonsai-home>/templates/templates.md
```

when the corresponding framework artifact set changes.

## `skills/phase_execution.md`

Project-specific phase execution behavior.

It must not be applied to map workspaces merely because maps share `agent_plan.md`, `agent_state.md`, handoff, or fresh-session continuation.

## `skills/final_truth_update.md`

Project final-truth reconciliation behavior.

It applies when human-owned project final truth is being clarified or revised.

It is not a required map-workspace lifecycle step unless map work itself implicates project final truth.

## `skills/handoff.md`

Shared workspace handoff behavior.

It handles both project and map workspaces and invokes workspace-specific reconciliation only where applicable.

## `skills/agent_context.md`

Operational-context qualification, layering, maintenance, and project code-map association behavior.

## `skills/code_maps.md`

Map-workspace execution, source inspection, generated-map production and maintenance, map/source identity, mapping validation, and map-specific completion behavior.

---

# Session Boundaries

Bonsai preserves continuity across fresh sessions, but it does not control the host application.

Bonsai cannot:

- terminate a chat;
- clear a session;
- reset a session;
- create a new session.

Those are human actions.

At a natural handoff, Bonsai records the exact next step and execution readiness in the active workspace before presenting continuation choices.

When one concrete agent-performable exact next action is established and no independent human-decision gate is active, the human may normally choose to continue:

- with that action in the current session;
- in a fresh session that automatically executes that one exact next action after startup reconstructs canonical durable state;
- after reviewing or changing the next step;
- or not at all right now, presented as **Exit for now**.

This continuation model applies to both project and map workspaces.

It is not limited to `Ready to execute` project implementation.

It may also apply to project planning work or map planning/mapping work when the exact next agent-performable action is durable and no independent human-decision gate is active.

Planning output still stops at any required approval gate.

`Complete`, blockers, design requirements, approvals, reviews, final-truth decisions, contracts, and other mandatory human gates are not bypassed by fresh-session continuation.

Neither current-session nor fresh-session continuation is inherently preferred when both are contextually useful.

A session that has just been entered through fresh-session continuation should not immediately offer another fresh-session continuation choice before substantive work has occurred.

This is session-local interaction context, not durable workspace memory.

## Ordinary fresh-session resume

For a project, the ordinary startup pointer is:

```text
Read .bonsai/start.md and follow its instructions.
```

Use the project-qualified form when startup without it would not deterministically resolve the same project:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

For a map, ordinary resume uses explicit map identity:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

## Exit for now

When the human chooses **Exit for now** at any Bonsai gate, preserve the current durable execution condition and present the applicable ordinary startup pointer introduced by wording equivalent to:

```text
You can resume later with:
```

**Exit for now** carries no auto-execution authorization and does not approve, discard, execute, or otherwise resolve the action or gate being left.

Choosing it must not alter durable state merely to record that the human exited.

## Fresh-session auto-execute

When the human chooses fresh-session continuation with automatic execution of the exact next action, use:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate.
```

For a project, append explicit identity only when needed:

```text
Active project: <project>.
```

For a map, append:

```text
Active map: <map>.
```

Example:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate. Active map: niagara4.
```

The auto-execute request carries no rendered phase, mapping unit, pass, readiness, approval state, or next-step text.

The new session reconstructs canonical durable workspace state and executes the one exact next action it establishes.

That startup authorization does not persist in workspace memory and does not authorize a subsequent action.

If reconstruction finds a mandatory human gate, inconsistent state, or no safe exact next action, Bonsai stops there instead.

Volatile continuation detail belongs in `agent_state.md`, not in the fresh-session prompt.

---

# Optional Helper Scripts

Bonsai may provide small shell or host-specific helper scripts for convenience.

They are not required for the conceptual workflow.

A helper may:

- create the initial `../../../distech/eclypse-framework/.bonsai/start.md` bootstrap;
- create the conventional `projects/main` directory;
- list workspace directories without invoking an AI;
- launch a configured coding CLI with an initial Bonsai prompt.

The same underlying capabilities should remain understandable from the AI workflow.

Routine implementation, workspace switching, project management, map management, and map resumption must not depend on a helper script once a Bonsai session is running.

---

# Enabling Bonsai in a New Repository

A repository becomes Bonsai-enabled when it has the local anchor:

```text
.bonsai/start.md
```

A project or map creation workflow may package that anchor for extraction at repository root.

For a simple project repository, the conventional structure is:

```text
.bonsai/
    start.md
    projects/
        main/
            workspace.md
            ...
```

For a repository being mapped without project memory:

```text
.bonsai/
    start.md
    maps/
        <map>/
            workspace.md
            agent_plan.md
            agent_state.md
            ...
```

Enabling the repository does not itself perform product design or generate a reusable code map.

---

# File Maintenance Discipline

## Bonsai specification

`specification.md` is human-owned Bonsai final truth.

Prompts, skills, templates, bootstrap files, README guidance, helper scripts, and category guides must conform to it.

## Framework category guides

When an authorized Bonsai change adds, removes, renames, or materially changes the responsibility of a standard prompt, skill, or template, the implementation agent must reconcile the corresponding category guide before the change is complete.

Category guides are maintained through `skills/artifact_index.md`.

They should remain concise routing artifacts and should not accumulate duplicated procedural truth.

## Human-owned project final truth

The implementation agent must not silently redefine:

```text
requirements.md
architecture.md
```

or applicable layered final-truth documents.

Clarifications and revisions require human authorization.

## Human-owned map calibration

The mapping agent must not silently reinterpret or rewrite durable mapping emphasis in:

```text
map_calibration.md
```

as though it were agent execution memory.

Human-authorized calibration may be drafted or revised when requested.

## Agent execution memory

The agent actively maintains workspace execution memory when current truth changes.

Common files:

```text
agent_plan.md
agent_state.md
```

Project detailed plans:

```text
plan/agent_plan_phase_<N>.md
```

Map detailed plans:

```text
plan/agent_plan_<scope>.md
```

The agent should replace stale state rather than append history.

## Agent context

`agent_context.md` is maintained only when a learned operational fact is:

- durable;
- actionable;
- sufficiently supported;
- likely to matter again.

Transient failures and troubleshooting noise should not be preserved.

## Icebox

The agent updates `icebox.md` only after the human chooses to preserve an observation.

Human authorization to preserve an item is not authorization to implement it.

## Generated maps

Generated maps should be updated when structural changes materially affect what the map is supposed to represent.

Routine local source edits do not necessarily require map maintenance.

Map/source identity must remain trustworthy enough that Bonsai does not knowingly apply a stale or mismatched generated map as though it represented current source.

## Retired mapping state

The standard must not reintroduce:

```text
map_state.md
templates/map_state_template.md
```

Mapping continuation is workspace execution memory.

---

# Clean Rebuild Objective

Bonsai memory should describe durable truth and current execution reality, not every historical detour.

A mature project workspace should support a clean rebuild from useful durable project memory.

A mature map workspace should support resuming or rebuilding mapping work from durable roadmap/state plus authoritative source.

Preserve:

- final project requirements when applicable;
- final project architecture when applicable;
- useful workspace roadmap structure;
- current workspace execution state;
- durable operational knowledge;
- useful map calibration;
- useful generated maps.

Discard or replace:

- obsolete pivots;
- stale session history;
- resolved blockers;
- superseded execution state;
- troubleshooting history;
- temporary scaffolding;
- obsolete mapping-state files;
- accidental implementation or mapping scars that no longer describe current truth.

---

# Typical Working Rhythm

## Project work

A normal new Bonsai project may look like this:

1. Explore product and architecture design in a Web UI AI.
2. Use `prompts/create_project.md` when the design is mature enough to preserve.
3. Select the Bonsai project name, normally accepting the suggested `main` default for a simple repository.
4. Extract the resulting zip at repository root, creating `../../../distech/eclypse-framework/.bonsai/start.md` and the selected project workspace.
5. Start with `Read .bonsai/start.md and follow its instructions.`
6. Let bootstrap resolve Bonsai Home, repository home, and active project workspace.
7. Draft and review the initial Phase 1 plan.
8. Execute one authorized bounded step.
9. Load generated maps, deep truth, developer context, agent context, and specialized skills only when needed.
10. Preserve durable operational discoveries in agent context rather than rediscovering them.
11. Reconcile project execution memory after completed work.
12. When a phase completes and roadmap work remains, activate the next phase and enter its applicable planning or review gate.
13. Record the exact next step and execution readiness.
14. Continue the exact next action in the current session or a fresh session when both are contextually useful.
15. Keep durable truth, working state, operational context, and maps compact as the project evolves.

## Map work

A normal mapping effort may look like this:

1. From the repository to be mapped, choose **Create Code Map**.
2. Let Bonsai derive the current source location, source identity, and sensible map identity when they are unambiguous.
3. Review or override those defaults when needed.
4. Let Bonsai create or reuse the repository-local map workspace required for durable mapping execution.
5. Make the map workspace active for mapping execution.
6. Use `agent_plan.md` as the map-wide roadmap.
7. Map bounded units of source.
8. Create scoped plans under `plan/` only when a mapping unit is too large for useful roadmap-level execution.
9. Reconcile generated map output, source identity, `agent_plan.md`, and `agent_state.md` at natural boundaries.
10. Record the exact next mapping step and readiness.
11. Continue in the current session or choose a fresh session that automatically executes that one exact next action.
12. Mark the map workspace complete only when the current mapping scope is exhausted and its generated output is reconciled.
13. Reactivate the same map workspace later when source changes or the requested mapping scope expands.

For mapping efforts that require deliberate preparation or calibration before coding-agent execution, the human may instead use `prompts/create_map.md` to create the map workspace explicitly.

---

# Validation Cases

The Bonsai standard should validate at least the following workspace-refactor behaviors.

## Workspace startup

1. An ordinary project repository with `projects/main` still starts with:

```text
Read .bonsai/start.md and follow its instructions.
```

2. An explicit named project resolves that project workspace.

3. An explicit `Active map: <map>` resolves the map workspace and loads its `workspace.md`.

4. Active workspace identity remains session-local and is not written into `agent_context.md`.

5. Startup does not eagerly load full project truth, full generated maps, or detailed map plans.

## Shared handoff

6. A project with an executable exact next step offers current-session and fresh-session one-step continuation.

7. A map with an executable exact next step offers the same continuation semantics.

8. Project auto-execute reconstruction does not bypass project gates.

9. Map auto-execute reconstruction does not bypass real human gates or blockers.

10. `Exit for now` changes no durable state merely because the human exits.

11. Map resume prompts include explicit `Active map: <map>`.

## Map planning

12. A small map may execute entirely from `agent_plan.md` without detailed plans.

13. A large module may create `plan/agent_plan_<scope>.md`.

14. A still-larger sub-scope may create another flat scoped detailed plan without introducing nested plan directories.

15. `agent_state.md` identifies the active detailed plan and exact next step.

16. Detailed map plans do not become project phases and do not automatically create phase-review gates.

## Map storage and ownership

17. Map workspace execution memory remains repository-local.

18. Generated reusable map output remains in the active map store.

19. Embedded Bonsai may physically overlap those locations without confusing their roles.

20. `map_state.md` and `map_state_template.md` are absent from the active model.

21. `map_calibration.md` remains human-owned input and is not treated as execution state.

## Project-map associations

22. A project can add or remove useful map selections in project `agent_context.md`.

23. Association changes do not rebuild, move, or delete generated maps.

24. Future project sessions can use those selected maps without rediscovering the entire map store.

## Creation workflows

25. `create_project.md` creates `workspace.md` plus project memory and the repository bootstrap for initial synthesis.

26. `create_map.md` creates `workspace.md`, `agent_plan.md`, `agent_state.md`, optional `map_calibration.md`, and the repository bootstrap.

27. `create_map.md` does not generate `code_map.md`, subsystem maps, or lookup tables.


## Code-map creation interaction

28. From an active project repository with no existing map workspace, **Create Code Map** can derive the current repository as the default source and create the required map workspace without requiring a separate **Create Map Workspace** action.

29. When the repository or project name provides an unambiguous map-name default, Bonsai may propose or use that default while allowing the human to override it.

30. If a suitable map workspace already exists, **Create Code Map** reuses or resumes it rather than creating duplicate workspace memory.

31. A source unrelated to the active project can still be mapped by explicitly selecting another source or by explicitly creating a map workspace.

32. The main **Manage Code Maps** menu presents code-map operations before map-workspace lifecycle operations.

33. Discovering names for display in **Manage Code Maps** does not require full inspection or validation of every generated map.

34. If available generated maps are already displayed in code-map status, Bonsai does not require a redundant list operation merely to expose those same map names.

35. Explicit map-workspace creation remains available without becoming a prerequisite for ordinary code-map creation.

---

# Intentionally Open Design Boundaries

Bonsai avoids over-specifying mechanisms before real use demonstrates that additional structure is necessary.

## Map manifest detail

The exact metadata stored in `code_map.md` or an adjacent manifest should remain minimal until real versioned map use proves what is required.

## Automatic dependency-to-map resolution

Bonsai may use dependency information, source locations, map identity, explicit project map selections, and agent context to connect consuming projects with useful generated maps.

The exact automatic discovery mechanics should remain as small as practical and should not be replaced by a large registry without demonstrated need.

## Detailed map-plan hierarchy

Maps may recursively decompose work by creating additional scoped detailed plans under `plan/`.

Do not introduce nested plan directories, a formal plan tree, or a generalized recursive planning framework until real use proves flat scoped plans insufficient.

## Generic workspace types

Projects and maps prove the shared workspace seam.

Do not add:

- a generic `workspaces/` directory;
- arbitrary third workspace types;
- a generic workspace plugin/type registry;
- generic empty-workspace creation.

Wait for a concrete third use case.

## Faber direction

Bonsai may gradually move toward Faber-like navigable truth where concepts naturally align:

- directories represent meaningful things;
- each thing has an entry document;
- agents start small and navigate to more context;
- relationships and secondary documents can become richer over time.

Do not make Bonsai depend on Faber yet.

Do not redesign project requirements or architecture as Faber spaces yet.

`workspace.md` should leave that evolution possible without encoding Faber semantics prematurely.

## Bonsai Home layering

Do not introduce personal/work Bonsai Home layering or a generalized Bonsai Home hierarchy without a concrete use case.

## Helper-script packaging

Helper scripts are useful convenience, but their exact shell and host packaging is not fundamental Bonsai truth.

The AI-session workflow must remain usable without making the helper script the conceptual entry point.

## Migration

Migration from earlier Bonsai versions is not part of the operating model defined here.

Do not preserve compatibility aliases for renamed prompts or retired mapping-state artifacts unless a concrete compatibility requirement is adopted.

---

# Summary

Bonsai has one human-owned specification:

```text
<bonsai-home>/specification.md
```

The remaining standard files implement it.

The normal coding-agent entry point is repository-local:

```text
.bonsai/start.md
```

The standard implementation kernel lives under Bonsai Home:

```text
<bonsai-home>/prompts/implementation.md
```

Bonsai now has two concrete resumable workspace types:

```text
projects
maps
```

Every workspace has:

```text
workspace.md
agent_plan.md
agent_state.md
```

Projects add durable product and architecture truth plus project-specific phase, contract, and final-truth workflow.

Maps add source-specific calibration, mapping plans when useful, source/map reconciliation, and reusable generated map production.

Although maps are resumable Bonsai workspaces internally, **code maps are the primary user-facing mapping concept**.

A normal user may ask Bonsai to create a code map for the current repository without first creating or selecting a map workspace manually.

Bonsai creates or reuses the required map workspace as part of fulfilling that intent.

Direct map-workspace management remains available for advanced, external-source, calibration, and resume scenarios.

Mapping workspace memory stays with the source repository.

Reusable generated map knowledge stays in the active Bonsai map store.

Fresh-session handoff, exact-next-step resumption, one-step auto-execution, and `Exit for now` are shared workspace lifecycle behavior.

Map work may be decomposed through optional flat detailed plans under `plan/` without turning maps into phase-based projects.

Project-to-map associations live in project operational context.

The active project or map belongs to the current session and is never persisted as a mutable global pointer.

This separation allows Bonsai to support simple projects, large monorepositories, long-running mapping efforts, multi-repository source universes, reusable developer environments, progressive framework design context, and frequent fresh AI sessions without turning routine work into constant process management.
