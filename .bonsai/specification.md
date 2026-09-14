# Bonsai Specification

Bonsai is a workspace-memory and execution-workflow system for AI-assisted software development.

It preserves the structured context an AI needs to design, build, inspect, map, and continue serious software work
across fresh sessions without making chat history authoritative.

Bonsai currently supports two concrete resumable workspace types:

- projects;
- maps.

Projects preserve durable product and architecture truth plus implementation execution memory.

Maps preserve durable repository-local mapping execution memory while producing reusable generated source
knowledge.

Bonsai is designed to support:

- simple repositories that need only local project memory;
- repositories containing multiple independent Bonsai projects;
- large repositories whose code mapping spans many fresh sessions;
- projects whose useful source universe spans multiple repositories;
- reusable code maps for independently maintained libraries or frameworks;
- reusable developer and agent context;
- frequent fresh implementation or mapping sessions with small startup prompts.

Bonsai does not attempt to be a general software-engineering methodology.

Coding style, testing philosophy, abstraction preferences, framework conventions, local tooling choices, and
similar engineering guidance belong in developer context, repository guidance, source guidance, or other
applicable skills unless they are genuinely part of approved project requirements or architecture.

This document defines the Bonsai operating model.

It is framework-authoring truth, not routine implementation-session context.

For the human-facing workflow and usage instructions, see `README.md`.

---

# Specification Authority

`specification.md` is the authoritative human-owned specification and final truth for Bonsai itself.

Bonsai standard prompts, skills, templates, bootstrap files, helper scripts, and workflow behavior implement this
specification. They are not peer authorities.

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

The user-facing `README.md` explains how to use Bonsai. It should conform to this specification but is not a peer
authority.

When another Bonsai standard artifact conflicts with this specification, this specification is authoritative unless
the human explicitly revises it.

Changes to Bonsai behavior, boundaries, ownership, lifecycle, environment model, workspace model, mapping model, or
interaction model should therefore be reflected here before or alongside changes to the standard files that
implement them.

Detailed procedural mechanics may live in prompts and skills when repeating them here would make the specification
unnecessarily large.

---

# Framework Artifact Discovery

`specification.md` is the normal starting point for understanding or designing changes to Bonsai.

The specification defines Bonsai's authoritative behavior and identifies the major framework artifact categories
that implement it. Detailed workflow mechanics remain in the applicable prompts, skills, and templates rather than
being duplicated here.

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

Each category guide identifies the artifacts currently available in that category and gives enough responsibility
information for a human or AI to determine which artifacts are relevant to the work being designed.

Category guides are routing aids. They are not peer authorities with `specification.md` and must not duplicate
detailed behavioral rules from the artifacts they reference.

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

The design agent should use the specification to identify which framework artifact categories may contain relevant
implementation detail.

When more context is required, the agent should request the applicable category guide and then request specific
prompts, skills, templates, or other artifacts as needed.

The human should not need to know Bonsai's complete internal artifact set in advance, and a design session should
not require loading the entire Bonsai standard merely to avoid missing a potentially relevant artifact.

Unless the human is intentionally comparing versions, category guides and individual standard artifacts supplied
to the design session should come from the same resolved Bonsai Home as the supplied `specification.md`.

Code maps are not part of this category-guide mechanism. Relevant map or source context may be supplied separately
when a design discussion needs it.

This progressive-discovery model preserves both sufficient design context and Bonsai's lazy-loading principle.

---

# Core Principles

## Durable truth is separate from working state

For projects, requirements and architecture describe the product and target system.

For both projects and maps, plans and state describe how approved or selected work is currently being carried out.

The implementation agent must not casually turn execution decisions into durable project truth or reusable source
truth.

## Human-owned and agent-owned memory are visibly different

For Bonsai project, map-workspace, and context memory, human-owned artifacts normally use natural names and
agent-owned execution artifacts use the `agent_` prefix.

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

The `agent_` prefix means Bonsai is allowed to maintain or rewrite that memory artifact according to its lifecycle
rules.

It does not mean the artifact is automatically loaded every session.

Generated code-map artifacts use the identities defined by the mapping model rather than the project-memory
ownership naming convention.

## Human control should not require constant babysitting

Bonsai uses explicit gates at meaningful boundaries.

Project gates may include:

- Phase 1 detailed-plan approval;
- later phase planning approval when required;
- durable contract review;
- final-truth clarification or revision;
- material execution deviations.

Map work uses human gates when a real human decision is required, but mapping does not inherit project phase,
contract, or final-truth gates merely because maps share the workspace lifecycle.

Ordinary maintenance of agent-owned execution memory does not require approval.

## Simple work should stay simple

A normal repository should not require a registry, dependency graph, generic workspace framework, or elaborate
configuration system merely to use Bonsai.

Additional structure should appear only when the work actually needs it.

## AI sessions are the primary interaction model

The normal Bonsai coding-agent experience begins inside an AI session.

The canonical startup instruction is intentionally small:

```text
Read .bonsai/start.md and follow its instructions.
```

Optional shell helpers may make setup or startup more convenient, but they are not the conceptual center of
Bonsai.

## Bootstrap should resolve identity, not load knowledge

Bootstrap establishes:

- Bonsai Home;
- repository home;
- active workspace identity.

It should not eagerly load every context file, map, skill, requirement area, architecture subsystem, or mapping
artifact.

The implementation kernel decides what knowledge is needed after identity is established.

## Deterministic discovery should be cheap

Filesystem enumeration, environment-variable lookup, project listing, map-workspace listing, and similar
deterministic tasks should use host tools rather than model reasoning when possible.

Bonsai should not spend model context rediscovering facts that can be resolved cheaply.

## Durable discovery should become agent memory

When an agent discovers an operational fact that is durable, actionable, sufficiently supported, and likely to
matter again, it should preserve the current working rule in the appropriate `agent_context.md`.

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

A **map workspace** is the durable execution mechanism Bonsai uses to create, extend, refresh, rebuild, and resume
work on a code map.

Users should not normally need to understand or manually create a map workspace before asking Bonsai to map source.

The normal intent is:

```text
Create a code map for this source.
```

When persistent mapping work is required, Bonsai may create or reuse the corresponding map workspace
automatically.

Explicit map-workspace management remains available when the human needs direct control over mapping execution
memory, such as:

- preparing a mapping effort before generated output exists;
- mapping source unrelated to the active project;
- resuming or inspecting a long-running mapping effort;
- managing mapping scope or calibration independently from generated output.

The distinction between map workspace memory and reusable generated map output remains architecturally significant
even when normal interaction hides that distinction.

## Maps describe source, not projects

A generated map represents a source universe or source snapshot.

The active Bonsai project may inform map generation, but the project does not become the generated map identity.

## Maps and source must agree

A generated code map represents a particular source snapshot.

Bonsai must not silently use a generated map for one source version while reasoning from another incompatible
version.

---

# Bonsai Environment Model

Bonsai separates the shared standard, reusable developer assets, repository-local workspace memory, project truth,
and reusable generated source maps.

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

Bonsai must not assume that Unix `~`, a Windows user profile, WSL home, and other host notions of a home directory
refer to the same physical location.

A developer working across environments may point each environment at the same physical Bonsai Home when
practical.

## Embedded Bonsai

A simple repository may carry the Bonsai standard directly in its own `.bonsai` directory.

When `BONSAI_HOME` is not available and the repository-local `.bonsai` contains a valid embedded Bonsai standard,
that directory may serve as Bonsai Home.

This allows the simplest topology to collapse naturally:

```text
repo/.bonsai
    = Bonsai Home
    + repository Bonsai memory
```

Embedded mode must use the same workspace semantics as Bonsai Home mode.

When repository-local map workspace memory and the active generated map store physically overlap in Embedded
Bonsai, their conceptual ownership remains distinct.

## Creating a Bonsai Home

A repository may begin in embedded mode and later create a reusable Bonsai Home.

**Create Bonsai Home** is a Bonsai workflow, normally available through **See more options** and also invokable as
an explicit startup request.

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

Bonsai should not silently substitute a path supplied only for the current session and should not store the Bonsai
Home location in `agent_context.md` as a discovery fallback.

The Bonsai Home location is environment identity, not learned project knowledge.

Creating a Bonsai Home must not automatically modify shell startup files, machine configuration, or other
developer-owned environment configuration without explicit authorization.

When both a valid `BONSAI_HOME` and an embedded standard are available, the Bonsai Home is the preferred standard
for the session.

## Repository home

The **repository home** is the source-repository root containing the local `.bonsai` anchor.

The repository-local `.bonsai/start.md` establishes the repository anchor for a normal AI session.

## Repository-local Bonsai memory

In Bonsai Home mode, repository-local `.bonsai` contains the material that belongs to that repository and its
workspaces, plus the small startup bootstrap.

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

Bonsai Home mode does not require copies of `specification.md`, standard prompts, skills, or templates inside every
repository.

## Developer-level reusable material

A Bonsai Home may contain reusable context and generated maps that apply across repositories.

Examples include:

- stable developer preferences;
- host or toolchain context;
- reusable operational knowledge;
- source locations;
- reusable generated code maps.

Developer-level material must remain distinct in meaning from repository and workspace memory even when it
physically lives under the same Bonsai Home.

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

It identifies the workspace type and gives the implementation kernel enough routing information to determine which
workspace-specific workflow and secondary artifacts apply.

It is not execution state.

Volatile progress, exact next steps, blockers, readiness, and active detailed-plan identity belong in
`agent_state.md`.

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

Its job is to establish environment identity, resolve the active workspace when the request requires one, load
that workspace's `workspace.md`, and hand control to the Bonsai Home or embedded implementation kernel.

## Bootstrap responsibilities

The bootstrap should:

1. establish repository home from the local `.bonsai` anchor;
2. resolve Bonsai Home;
3. resolve the active workspace type and name when operating in a workspace;
4. locate and read that workspace's `workspace.md`;
5. preserve Bonsai Home, repository home, active workspace identity, and the startup request as current-session
   context;
6. load `<bonsai-home>/prompts/implementation.md`;
7. continue under the standard implementation workflow.

The bootstrap should not routinely load requirements, architecture, generated maps, developer context, agent
context, detailed plans, or specialized skills itself.

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

Workspace selection is session-local. Bonsai must not persist an active-workspace pointer merely because one
session selected it.

When no workspace was explicitly selected, the implementation workflow may resolve a conventional project such as
`projects/main`, a sole valid project, or another deterministic repository-entry condition. It should not silently
choose among several plausible workspaces.

---

# Artifact Ownership

Ownership determines who controls the durable meaning of an artifact.

Ownership is separate from loading behavior.

The ownership naming rules in this section apply to Bonsai project and context memory. Standard framework artifacts
and code-map artifacts use their defined framework identities.

## Human-owned artifacts

Human-owned project and context artifacts use natural names.

Typical examples include:

```text
requirements.md
architecture.md
developer_context.md
icebox.md
map_calibration.md
```

Human ownership does not mean the human must manually edit every line.

An AI may draft or mechanically maintain a human-owned artifact when instructed, but changes to durable meaning
require human authorization.

## Agent-owned artifacts

Agent-owned project and context artifacts use the `agent_` prefix.

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

## Standard framework artifacts

Prompts, skills, templates, category guides, bootstrap files, and helper scripts are Bonsai standard
implementation artifacts.

Their identities are defined by the framework rather than by the project-memory ownership prefix convention.

An implementation agent may create, modify, rename, or remove them only when an authorized Bonsai change requires
it and the resulting standard remains consistent with `specification.md`.

## Avoid hybrid ownership

Bonsai should avoid artifacts whose ownership is genuinely ambiguous.

When an artifact contains human-authorized meaning but is mechanically maintained by the agent, ownership is
determined by who controls its durable meaning.

`icebox.md` remains human-owned because an observation may only be preserved there when the human chooses to retain
it.

## Derived workflow and historical artifacts

Some project-local artifacts are neither human-owned final truth nor agent-owned execution memory.

Semantic review artifacts under `review/` are derived workflow artifacts. Bonsai may generate and maintain them
according to the review lifecycle, but they do not use the `agent_` prefix because they are not agent execution
memory and their semantic filenames are part of the review interaction model.

Completed-work archives preserve artifact identities as historical evidence. Archival does not rename copied
human-owned, agent-owned, review, contract, or other project artifacts merely to normalize their names after
completion.

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

## `architecture.md`

`architecture.md` is human-owned architecture truth.

It defines the approved target architecture, important boundaries, major components, data and control relationships,
and architectural constraints.

Detailed architecture may be decomposed into:

```text
architecture/architecture_<SUBSYSTEM>.md
```

when that improves clarity and loading cost.

The implementation agent must not silently change durable project truth merely because implementation reveals a
conflict. It should surface the discrepancy through the final-truth workflow.

---

# Agent Execution Memory

Projects and maps both use agent-owned execution memory.

## `agent_plan.md`

`agent_plan.md` is the workspace-wide roadmap.

For a project, it tracks the project implementation roadmap and phase progression.

For a map, it tracks the map-wide mapping roadmap, current mapping scope, completed and pending mapping work, and
where scoped mapping plans exist.

It should remain roadmap-level rather than becoming a transcript of every step.

## `agent_state.md`

`agent_state.md` is the current resume state.

It should contain the minimum durable truth needed for a fresh session to determine the current execution
condition, including as applicable:

- current project phase or mapping scope;
- active detailed plan identity;
- execution readiness;
- blocker;
- exact next action;
- success condition;
- resume-critical artifact references.

It should replace stale state rather than append history.

## Detailed plans

Projects may use:

```text
plan/agent_plan_phase_<N>.md
```

Maps may use flat scoped plans such as:

```text
plan/agent_plan_<scope>.md
```

A map scoped plan is not a project phase. It refines one mapping unit or bounded portion of the map-wide roadmap
when the work is too large to execute reliably from roadmap-level detail.

Do not introduce nested mapping plan directories merely because a source area is large. Use additional flat peer
plans when another bounded mapping unit genuinely needs one.

---

# Developer Context

`developer_context.md` is human-owned reusable working guidance.

It may contain stable preferences, conventions, local tooling instructions, or other durable guidance that should
influence implementation behavior without becoming project requirements or architecture.

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

Bonsai should support adding and removing project map selections through code-map management without searching the
entire map store in every future session.

Adding or removing an association changes only project operational context.

It does not create, extend, refresh, rebuild, move, rename, or delete the reusable generated map.

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

The standard implementation prompt then loads only the minimum workspace state required to determine the current
execution condition.

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

Bonsai assumes that design often happens in a Web UI AI conversation because conversational design is easier to
inspect and can be materially cheaper than coding-agent sessions.

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

The generated `.bonsai/start.md` is the canonical repository-local bootstrap for the Bonsai version that owns the
workflow.

For an existing-project design update, the workflow preserves the existing project identity when unambiguous and
packages only materially affected project files.

If the human has identified external source or code maps during design, the workflow may seed project-level
`agent_context.md` with that approved operational information.

The project creation workflow does not generate the initial detailed Phase 1 plan.

Phase 1 planning remains the first implementation gate.

---

# Map Creation Workflow

Bonsai supports both direct code-map creation from a coding-agent session and explicit map-workspace creation from a
Web UI design or calibration conversation.

## Direct code-map creation

The normal coding-agent mapping intent is:

```text
Create a code map.
```

When invoked from a repository with an active Bonsai project, Bonsai should use already-established context rather
than require the human to restate information it can determine reliably.

Where unambiguous, Bonsai should derive sensible defaults for:

- source location from the current repository;
- source identity from the current checkout;
- map name from the repository or source identity;
- initial mapping scope from the selected source;
- project association when the new map is clearly being created for the active project.

The human may override these defaults.

If persistent mapping work is required and no suitable map workspace exists, Bonsai creates the corresponding
repository-local map workspace automatically.

If a suitable map workspace already exists, Bonsai should reuse or resume it rather than create duplicate execution
memory.

Direct code-map creation may therefore conceptually perform:

```text
source selection
    ↓
map identity resolution
    ↓
create or reuse map workspace
    ↓
select initial bounded mapping focus
    ↓
execute bounded mapping unit
    ↓
generated reusable code map
```

Creating the workspace is part of implementing the user's mapping intent rather than a prerequisite the user must
normally perform separately.

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

The workflow may also create the empty `plan/` directory or allow it to appear later when detailed map planning is
needed.

The map creation workflow must not generate reusable map outputs such as:

```text
code_map.md
subsystems/
namespace_router.tsv
manifest.tsv
symbol_index.tsv
```

Those are outputs of the later coding-agent mapping workflow.

The actual source remains authoritative.

Creating a map workspace does not require creating a Bonsai project for that source.

---

# Implementation Workflow

After `.bonsai/start.md` resolves session identity and loads the selected `workspace.md`, implementation continues
through:

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
8. stops at a structured startup gate unless an explicit startup request authorizes the one exact next action to
   proceed without stopping at that gate after canonical state reconstruction;
9. executes only that human-authorized exact next action and does not carry startup authorization into a subsequent
   action;
10. reconciles completed work;
11. maintains current workspace execution memory;
12. preserves qualifying operational discoveries;
13. when authorized project work materially changes source represented by a known relevant code map, identifies
    whether the existing map coverage now needs maintenance and surfaces one bounded maintenance action at a
    natural boundary;
14. when source inspection already required by authorized project work reveals reusable, non-obvious,
    architecturally significant source knowledge that is not adequately represented by a useful code map, may
    surface one bounded mapping recommendation without expanding source inspection merely to hunt for mapping
    opportunities;
15. reconciles affected framework category guides when authorized standard artifacts are added, removed, renamed,
    or materially change responsibility;
16. stops at the next natural gate.

For map work, one exact executable action may be a complete bounded mapping unit. Discovery, ownership resolution,
standard generated-map updates, validation, and reconciliation inside that unit are not separate authorization
steps merely because they occur sequentially.

The implementation prompt is a stable router and invariant set.

Project-specific phase execution belongs in project workflow and skills.

Mapping-specific source inspection, generated-map maintenance, and source/map identity handling belong in the
mapping workflow and `skills/code_maps.md`.

Project implementation may detect that mapping work would be valuable, but it does not silently acquire authority
to mutate reusable generated maps. A maintenance or mapping recommendation is a proposed next action. If the human
accepts it, Bonsai routes that work through the applicable map workspace and normal bounded mapping-unit
authorization.

For implementation-time maintenance detection, a **known relevant map** is one already selected for the project,
already loaded or used in the current work, or cheaply identifiable from the current source identity without loading
or surveying the entire map store. Bonsai does not need to enumerate and inspect every reusable map after every
source edit.

Implementation-driven mapping recommendations must arise from source knowledge the agent already had legitimate
reason to inspect for the current project action. Bonsai should not roam through unrelated source merely to find
additional things that might be worth mapping.

Detailed workflow belongs in triggered skills rather than one permanently loaded monolithic prompt.

---

# Execution Readiness

Bonsai makes the difference between planned, blocked, review-bound, executable, and complete work explicit.

Common execution-readiness values include:

- `Design required`;
- `Planning required` or a more specific planning state;
- `Awaiting review`;
- `Blocked`;
- `Ready to execute`;
- `Complete`.

The exact wording may vary by workspace-specific workflow, but readiness must describe the actual current gate.

`Ready to execute` means one safe exact agent-performable action is established and no independent human-decision
gate remains.

For a map, that exact action may be one bounded mapping unit established by a selected mapping focus.

`Complete` means the selected workspace scope has no unfinished required work and the relevant durable state is
reconciled. It must not be used merely because one intermediate step, such as mapping discovery, finished.

---

# Human Gates and Menus

Menus present choices. They do not own the workflow decisions they display.

The invoking workflow retains responsibility for:

- determining which choices are valid;
- validating the selected choice;
- applying mutations;
- reconciling resulting state.

A human gate is required when the human must approve, select, revise, or resolve something material.

A gate should not be inserted merely because an agent learned more detail while executing an already-authorized
bounded action.

For mapping specifically, discovery of the exact standard generated-map targets is normally internal execution
detail when those targets remain inside the selected focus and standard output envelope.

---

# Code Maps

Code maps provide selective structural memory for source navigation.

They are navigation aids, not substitutes for source inspection and not project truth.

## Code-map lifecycle intents

Bonsai distinguishes between creating, extending, refreshing, and rebuilding a code map.

**Create** establishes a reusable map for a source identity that does not yet have a suitable map.

**Extend** deliberately broadens the useful mapping scope of an existing map. Examples include adding coverage for
another architectural subsystem, mapping a cross-cutting concern, or mapping another reusable caller or extension
surface. Extending a map reuses and reactivates the existing map workspace rather than creating a duplicate map for
the same source identity.

**Refresh** reconciles existing mapped knowledge after the represented source changes materially. Refresh normally
preserves the existing map identity and intended coverage while updating the standard generated layers required to
keep that coverage trustworthy.

**Rebuild** intentionally replaces substantial generated representation and is distinct from ordinary extension or
refresh. Destructive removal, broad ownership restructuring, or replacement of existing generated output remains
separately gated.

These lifecycle intents all use the same source-backed mapping model. Once a concrete bounded mapping focus is
selected and authorized, `skills/code_maps.md` executes the applicable bounded mapping unit.

## Map store and source names

Every map has a meaningful source identity.

When a Bonsai Home is active, the map store is:

```text
$BONSAI_HOME/maps/
```

When Bonsai is embedded and no external Bonsai Home is active, the repository's embedded store is:

```text
repo/.bonsai/maps/
```

The storage model is otherwise the same.

Examples:

```text
maps/
    application/
    library-a/
    library-b/
```

When version identity matters, the map identity may include a version or other distinguishing information.

The folder name does not need to carry every source-identity detail forever. The map entry document may preserve
richer identity.

## Map identity follows source identity

A map is named for the source universe it represents, not for the Bonsai project that created it.

For a simple repository:

```text
repository: application
project: main
map: application
```

For a large repository containing several Bonsai projects, several projects may consume one map of the same
repository source.

Bonsai should not generate duplicate maps merely because multiple project-memory directories exist.

## Mapping inputs

Every map is grounded in actual source.

Additional calibration can come from two complementary places.

### Existing Bonsai project memory

When the source being mapped belongs to an existing Bonsai project, mapping should use relevant durable project
memory when available.

Useful inputs may include:

- requirements;
- architecture;
- archaeological analysis;
- implementation knowledge;
- source structure already captured in project memory.

Project memory helps Bonsai understand what concepts and boundaries matter.

It does not replace source inspection.

### `map_calibration.md`

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

Project memory and `map_calibration.md` may both be used when both are available.

## Mapping context and map storage are separate

The source context used to create a map, repository-local workspace memory, and the location where the reusable
generated map is stored are different concerns.

When mapping an external source, Bonsai should operate against the actual selected source and use that source's
relevant project memory and map workspace when available.

When the selected source is a repository checkout, source-local human calibration may live at:

```text
<source-repository>/.bonsai/maps/<source>/map_calibration.md
```

That calibration remains human-owned and must not be moved, copied, or rewritten merely because the generated map
is stored elsewhere.

If a Bonsai Home is active, the resulting reusable generated map still belongs under:

```text
$BONSAI_HOME/maps/<map>/
```

In Embedded Bonsai, repository-local workspace memory, calibration, and generated output may physically overlap.
Their conceptual ownership remains distinct.

This produces the rule:

> Map creation and maintenance use source-local workspace context. Generated reusable map storage uses the active
> Bonsai map store.

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

## Map and source identity

A map describes a particular source snapshot.

Bonsai must be able to determine what source the map represents.

Relevant identity may include:

- logical source name;
- version;
- Git revision;
- artifact coordinates;
- source type;
- exact source location.

The exact metadata format should remain as small as possible.

For released dependencies, a matching source artifact may be more appropriate than an unrelated development
checkout.

For active cross-repository development, an exact matching repository revision may be preferable.

## Map entry document

A map set uses `code_map.md` as its normal entry document.

The entry document identifies the map and routes the agent into more detailed map data when needed.

The exact indexing and manifest format may evolve through real use, but the source-identity boundary is required.

---

# Integrated Mapping Workflow

Code mapping is part of the main Bonsai workflow rather than a parallel standalone subsystem.

The Bonsai standard routes active mapping through the same startup, workspace, menu, context-layering,
execution-memory, handoff, and fresh-session model used by projects where those concepts genuinely apply.

A mapping workflow executes through a map workspace, whether that workspace was explicitly selected by the human
or created or reused automatically while fulfilling a code-map operation.

A mapping workflow should:

- resolve, create, or reuse the applicable map workspace;
- make that workspace active for the mapping execution session;
- use the active Bonsai generated-map store;
- identify the source being mapped independently from any active project;
- use relevant project memory when available;
- use source-local `map_calibration.md` when available;
- use actual source as authoritative;
- organize substantive mapping as human-selected bounded mapping focuses;
- decompose large mapping units through optional detailed map plans when useful;
- preserve stable source locations or mapping rules in appropriate agent context;
- maintain map `agent_plan.md` and `agent_state.md`;
- support exact-next-step fresh-session continuation;
- reconcile generated output and map/source identity before declaring the current mapping scope complete.

Existing generated map index and source-navigation structures should be retained where they remain useful.

Integration does not require rewriting generated map data solely for architectural neatness.

## Bounded mapping units

The normal executable unit of map work is a **bounded mapping unit** established by a human-selected bounded mapping
focus.

A mapping focus may be:

- one architectural subsystem;
- one public or extension API concern;
- a cross-cutting behavior;
- persistence;
- event handling;
- serialization;
- lifecycle;
- tracking; or
- another bounded source-backed concern.

A mapping focus is not required to correspond one-to-one with a generated subsystem.

Selecting the focus determines **what** the next mapping unit is.

After that selection has been reconciled into durable workspace state, the continuation choice determines **where**
the already-selected mapping unit executes:

```text
select bounded mapping focus
        ↓
persist exact next mapping unit
        ↓
choose current session / fresh session / review / exit
        ↓
execute complete mapping unit
```

When an executable mapping unit is authorized, that authorization normally covers:

```text
selected bounded mapping focus
        ↓
inspect authoritative source
        ↓
determine architectural ownership
        ↓
determine justified standard map layers
        ↓
create or update those layers
        ↓
validate against source
        ↓
reconcile agent_plan / agent_state
        ↓
stop at the next mapping-unit boundary
```

Discovery and generated-map production are not normally separate human-authorized actions.

Discovery is explicitly allowed to determine the exact standard generated-map targets needed to represent the
selected focus.

The normal generated-output authorization envelope for a non-destructive mapping unit includes:

```text
code_map.md
subsystems/<subsystem>/map.md
subsystems/<subsystem>/api_pub.md
subsystems/<subsystem>/api_ext.md
```

A mapping unit may justify changes to one subsystem, several existing subsystems, a newly justified subsystem, or
only some of those standard layers.

For example, a cross-cutting Event-handling focus may discover that durable event ownership belongs in an Element
map, a related mechanic belongs in a Control map, and no standalone Event-handling subsystem should exist. Those
standard updates remain part of the already-authorized Event-handling mapping unit.

Bonsai must not require another human gate merely because discovery:

- resolves different standard target files than could be known beforehand;
- places one cross-cutting concern in several existing subsystem maps;
- justifies `api_pub.md` or `api_ext.md`;
- justifies a new subsystem map inside the selected focus; or
- shows that no standalone subsystem corresponds to the selected focus.

The broader authorization remains bounded. Bonsai must stop for human direction when the work requires:

- material expansion of the selected mapping focus or source scope;
- a materially different source or map identity;
- resolution of source/map misalignment;
- destructive rebuild or removal;
- restructuring existing generated-map ownership rather than ordinary updates;
- a genuinely unrelated new mapping objective;
- a costly optional artifact;
- creation or material expansion of optional lookup/index artifacts;
- source evidence insufficient to map the selected focus safely; or
- another material decision that genuinely requires human judgment.

The selected focus establishes the authorization boundary. Discovery resolves the exact standard generated-map
targets inside that boundary.

## Map extension and maintenance

A completed map is complete only for its current mapping scope and represented source state. Completion does not
seal the map against later useful work.

An explicit request to broaden coverage should reactivate the existing compatible map workspace and establish a new
bounded mapping focus. The human may name an architectural subsystem directly, name a cross-cutting concern, or ask
Bonsai to review current coverage and suggest valuable additions. A requested subsystem is a mapping focus, not an
instruction to create a directory or generated subsystem blindly; source discovery still determines justified
architectural ownership and standard output.

A source change is a different lifecycle trigger. When Bonsai has changed source during authorized project work and
that change materially affects knowledge represented by a known relevant map, Bonsai should surface bounded map
maintenance at a natural project boundary. Material changes may include changes to:

- public or extension structure;
- lifecycle or ownership behavior;
- reusable caller or extension mechanics;
- architectural relationships;
- persistence, serialization, event, tracking, or similar mapped contracts;
- source identity or routing facts that make current map guidance misleading.

Routine local implementation edits, narrow bug fixes, private refactors, formatting, and other changes that do not
materially affect mapped knowledge should not trigger map maintenance.

Map maintenance is not an incidental side effect of project source mutation. The project agent identifies and
proposes the affected bounded maintenance work; accepted maintenance then runs through the normal mapping workflow
and map workspace. The agent should use what it already knows about the source change rather than rediscovering the
entire library merely to decide whether maintenance is warranted.

## Project-discovered mapping opportunities

Authorized project work may reveal reusable source knowledge that deserves mapping even when no source change made
the current map stale.

Bonsai may recommend creating or extending a code map when all of the following are true:

- the knowledge was discovered while inspecting source already required for the authorized project action;
- the knowledge is source-level and useful beyond the current project-specific implementation;
- the behavior or structure is non-obvious enough that preserving it would materially reduce future rediscovery;
- it is architecturally significant, cross-boundary, reusable, or otherwise valuable map content; and
- it is not already represented adequately by a useful current map.

The recommendation should identify the relevant source or existing map, the proposed bounded mapping focus, and
why the knowledge appears reusable enough to preserve. It should prefer extending an existing compatible map when
one already represents the source identity; otherwise the normal code-map creation path applies.

A mapping recommendation does not authorize source inspection beyond the current project need, does not mutate map
output, does not silently expand the active project's execution scope, and does not become durable map or project
state merely because the agent noticed it. If the human accepts the recommendation, Bonsai routes it through normal
map selection, mapping-unit authorization, and current-session or fresh-session continuation.

Bonsai should combine closely related observations and avoid repeatedly interrupting implementation with the same
mapping suggestion. The purpose is to preserve expensive reusable knowledge encountered naturally during real
work, not to turn every implementation session into a map-coverage survey.

## Map-specific reconciliation

When the active workspace is a map, handoff additionally reconciles applicable:

- current mapping scope;
- the completed or selected bounded mapping focus;
- active detailed map plan;
- generated map output touched by the completed mapping unit;
- source/map identity concerns;
- whether generated output is sufficiently reconciled for the completed mapping focus.

For executable map work, source discovery alone is not normally a natural handoff boundary. When the selected
mapping focus remains valid and discovery has established enough evidence to determine the justified standard map
layers, Bonsai should continue through generated-map production and validation before reconciling at the
mapping-unit boundary.

If the current mapping scope still contains useful work but no next bounded focus has been selected, handoff should
present concrete next-focus choices and stop for human direction. Selecting the next focus updates durable map
execution memory but does not begin substantive source inspection or generated-output mutation.

Map handoff must not invent project final-truth, phase, pass, or contract semantics merely to fit the shared
lifecycle.

---

# Manage Code Maps

Bonsai exposes code-map lifecycle actions through:

**Manage Code Maps**

During normal project implementation, it generally appears under **See more options** unless a mapping action has
become directly relevant to the current work.

The menu should present **code maps** as the primary managed object.

Useful primary operations include:

- Create Code Map;
- Inspect Code Map;
- Extend Code Map;
- Refresh Code Map;
- Rebuild Code Map;
- Remove Code Map;
- Add a Code Map to the Active Project;
- Remove a Code Map from the Active Project;
- Manage Map Workspaces.

**Extend Code Map** is the normal human-facing path for broadening the useful scope of an existing map. After a map
is selected, useful choices may include:

- map another subsystem;
- map a cross-cutting concern or reusable behavior;
- map another public or extension surface;
- review current coverage and suggest valuable additions.

These choices select or help derive a bounded mapping focus. They do not directly prescribe generated filesystem
structure. Source discovery determines where the resulting durable knowledge belongs.

**Refresh Code Map** is the normal non-destructive path for reconciling an existing map after source changes. It
should prefer the narrowest source-backed maintenance focus that restores trustworthy coverage.

**Rebuild Code Map** is reserved for cases where ordinary extension or refresh is not sufficient and substantial
replacement or ownership restructuring is intended. It retains the stronger human gates required for destructive
or broad restructuring work.

Map-workspace operations are secondary lifecycle operations rather than peers of normal code-map use.

**Manage Map Workspaces** may provide actions such as:

- Create Map Workspace;
- Inspect Map Workspace;
- Resume Map Workspace.

## Context-aware code-map creation and extension

When **Create Code Map** or **Extend Code Map** is invoked from an active repository or project, Bonsai should prefer
known session context over asking the human to restate it.

When reliably derivable, Bonsai should present or use defaults for:

- current repository source location;
- logical source identity;
- map identity;
- current source snapshot;
- corresponding repository-local map workspace;
- initial or expanded bounded mapping scope;
- initial bounded mapping focus;
- optional active-project association for new maps.

The human may override those defaults.

A code-map creation or extension proposal authorizes the selected mapping focus and standard generated-output
envelope, not a precomputed exact list of standard Markdown target files.

When the approved action requires creation or reactivation of the corresponding map workspace, that workspace
lifecycle step is part of the same approved action and should not trigger a redundant second workspace gate.

Extending a compatible map must reuse that map identity and preserve existing generated output unless the human
separately authorizes destructive replacement or restructuring.

## First-use behavior

When Bonsai encounters a substantial existing codebase without a useful generated map, it may surface map creation
once as a primary contextual action.

If the human declines, mapping remains available through **See more options** rather than repeatedly interrupting
implementation.

For a greenfield repository with little useful source, mapping should normally be deferred.

## Contextual map maintenance during project work

When authorized project implementation materially changes source represented by a known relevant map, Bonsai
should surface a concise maintenance recommendation at the next natural project boundary rather than silently
allowing the map to become knowingly misleading.

The recommendation should identify the affected map and the bounded area believed to need refresh. It may offer to
perform the maintenance in the current session, continue it in a fresh session through normal exact-next-action
semantics, review or change the proposed focus, or defer it.

The recommendation itself does not authorize map mutation. If accepted, map maintenance becomes normal map work
and is governed by `skills/code_maps.md`.

## Contextual mapping opportunities during project work

When authorized project work already required the agent to learn reusable, non-obvious source mechanics that are
not adequately mapped, Bonsai may surface a concise recommendation to create or extend the relevant code map.

The recommendation should explain:

- which source or existing map is implicated;
- the proposed bounded mapping focus;
- what reusable knowledge was expensive or non-obvious to establish; and
- why preserving it would help future work beyond the current project.

Bonsai must not perform unrelated source exploration merely to generate these recommendations. It should recommend
from evidence naturally encountered during the current authorized work.

If the human accepts, the recommendation enters the normal mapping workflow. If the human declines or defers, the
project continues without map mutation and Bonsai should not repeatedly surface the same suggestion during the same
work merely because it remains technically possible.

## Project map associations

Project map associations are stored in project `agent_context.md`.

Managing an association does not create, rebuild, move, rename, extend, refresh, or delete the generated map.

Map-workspace discovery should use the repository-local `.bonsai/maps/` workspace area.

Reusable generated-map discovery should use the active Bonsai map store.

These are related but distinct collections even when Embedded Bonsai makes them physically overlap.

---

# Multi-Repository Source Universes

A Bonsai project may depend on source outside its repository.

Example:

```text
application
    → library-a
    → library-b
```

Each repository may have its own Bonsai project memory.

Maps for each source are reusable developer assets:

```text
$BONSAI_HOME/maps/
    application/
    library-a/
    library-b/
```

When a consuming project needs external source, Bonsai may use durable agent context, dependency information, map
identity, and source inspection to locate the appropriate source and matching map.

Once Bonsai discovers stable cross-repository source locations or working rules, it should preserve them in the
appropriate agent context so subsequent sessions do not repeatedly rediscover them.

Bonsai should not require the consuming project's requirements or architecture to duplicate machine-specific
source paths.

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
- plans;
- code maps;
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

It identifies the available prompts and their responsibilities for discovery purposes. It does not duplicate their
detailed workflow rules.

The exact prompt set should remain small.

## `prompts/implementation.md`

Stable workspace-aware implementation kernel and router.

It receives Bonsai Home, repository home, active workspace identity, and the retained startup request from
`.bonsai/start.md`, then determines the minimum additional context required for the current execution condition.

During project execution it may also identify known code-map maintenance made necessary by the source changes it
just performed, or recommend a mapping opportunity revealed by source inspection already required for the project
action. It does not perform extra source exploration merely to search for mapping opportunities, and accepted map
work is routed to `skills/code_maps.md`.

## `prompts/create_project.md`

Web UI project creation and repository-bootstrap packaging workflow.

It turns a mature design conversation into durable Bonsai project workspace memory and, for initial synthesis, a
repository-root zip containing the canonical local `.bonsai/start.md` anchor plus the selected project under:

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

It should:

- add newly introduced artifacts;
- remove retired artifacts;
- reconcile renamed artifacts;
- update a routing description when an artifact's responsibility materially changes;
- validate that guide references resolve;
- detect relevant standard artifacts missing from their category guide;
- keep guide descriptions concise and responsibility-oriented.

It must not turn category guides into duplicate specifications or reproduce detailed procedural rules from
individual artifacts.

Category-guide reconciliation is part of completing an authorized framework-artifact lifecycle change.

The skill does not own code-map discovery or map lifecycle indexing.

## `skills/phase_execution.md`

Project-specific phase execution behavior.

It must not be applied to map workspaces merely because maps share `agent_plan.md`, `agent_state.md`, handoff, or
fresh-session continuation.

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

Map-workspace execution, source inspection, code-map creation, extension, refresh and rebuild behavior,
generated-map production and maintenance, map/source identity, mapping validation, and map-specific completion
behavior. It owns execution after a project implementation session's map-maintenance or mapping-opportunity
recommendation is accepted.

---

# Framework Templates

Reusable artifact templates live under:

```text
<bonsai-home>/templates/
```

The category guide is:

```text
<bonsai-home>/templates/templates.md
```

It identifies the available templates and their intended consumers for discovery purposes. It does not duplicate
the template contents or the workflow rules that consume them.

Templates should exist only when Bonsai has an explicit workflow that consumes them.

A template should not exist merely because a document type could theoretically be templated.

For generated code maps, template existence does not itself authorize output. Standard Markdown map artifacts may
be generated when justified inside an authorized mapping unit. Optional lookup/index artifacts remain separately
gated when their creation or material expansion is costly or unnecessary by default.

---

# Session Boundaries

Bonsai preserves continuity across fresh sessions, but it does not control the host application.

Bonsai cannot:

- terminate a chat;
- clear a session;
- reset a session;
- create a new session.

Those are human actions.

At a natural handoff, Bonsai records the exact next step and execution readiness in the active workspace before
presenting continuation choices.

When one concrete agent-performable exact next action is established and no independent human-decision gate is
active, the human may normally choose to continue:

- with that action in the current session;
- in a fresh session that automatically executes that one exact next action after startup reconstructs canonical
  durable state;
- after reviewing or changing the next step;
- or not at all right now, presented as **Exit for now**.

This continuation model applies to both project and map workspaces.

It is not limited to `Ready to execute` project implementation.

It may also apply to project planning work or map planning/mapping work when the exact next agent-performable action
is durable and no independent human-decision gate is active.

Planning output still stops at any required approval gate.

For an executable map workspace action, the exact next action may be one complete bounded mapping unit. In that
case, source discovery, architectural-ownership resolution, exact standard-map target resolution, generated-map
mutation, validation, and reconciliation are internal parts of that one action rather than separate continuation
actions.

Fresh-session boundaries for mapping should therefore normally occur **between bounded mapping units**, not between
discovery and generated-map production.

A mapping-unit continuation authorization ends when that mapping unit is reconciled, or earlier when a real blocker
or mandatory human gate is reached. It does not authorize selection or execution of the next mapping focus.

`Complete`, blockers, design requirements, approvals, reviews, final-truth decisions, contracts, and other
mandatory human gates are not bypassed by fresh-session continuation.

Neither current-session nor fresh-session continuation is inherently preferred when both are contextually useful.

A session that has just been entered through fresh-session continuation should not immediately offer another
fresh-session continuation choice before substantive work has occurred.

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

When the human chooses **Exit for now** at any Bonsai gate, preserve the current durable execution condition and
present the applicable ordinary startup pointer introduced by wording equivalent to:

```text
You can resume later with:
```

**Exit for now** carries no auto-execution authorization and does not approve, discard, execute, or otherwise
resolve the action or gate being left.

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

The auto-execute request carries no rendered phase, mapping unit, pass, readiness, approval state, or next-step
text.

The new session reconstructs canonical durable workspace state and executes the one exact next action it
establishes.

For map execution, if that reconstructed action is a ready bounded mapping unit, the startup authorization covers
the complete mapping unit, not merely its discovery stage.

That startup authorization does not persist in workspace memory and does not authorize a subsequent action.

If reconstruction finds a mandatory human gate or no safe exact next action, Bonsai stops there instead.

---

# Optional Helper Scripts

Bonsai may provide small shell or host-specific helper scripts for convenience.

They are not required for the conceptual workflow.

Useful conveniences may include:

```text
bonsai.sh init
bonsai.sh --list
bonsai.sh <project>
```

A helper may:

- create the initial `.bonsai/start.md` bootstrap;
- create the conventional `projects/main` directory;
- list project directories without invoking an AI;
- launch a configured coding CLI with an initial Bonsai prompt.

The same underlying capabilities should remain understandable from the AI workflow.

Routine implementation, project switching, project listing, project creation, and map management must not depend
on the helper script once a Bonsai session is running.

---

# Enabling Bonsai in a New Repository

A repository becomes Bonsai-enabled when it has the local anchor:

```text
.bonsai/start.md
```

and a project-memory area when project memory is needed.

For a simple repository, the conventional initial structure is:

```text
.bonsai/
    start.md
    projects/
        main/
```

The normal Web UI project synthesis workflow may create this repository-local structure and the initial project
memory together as one zip for extraction at repository root.

A helper script may also create the local bootstrap structure, and it may be created manually from the Bonsai
distribution. Creating only the repository-local anchor and project memory does not create an Embedded Bonsai
standard.

Enabling the repository does not itself approve or invent product design.

---

# File Maintenance Discipline

## Bonsai specification

`specification.md` is human-owned Bonsai final truth.

Prompts, skills, templates, bootstrap files, README guidance, helper scripts, and category guides must conform to
it.

## Framework category guides

When an authorized Bonsai change adds, removes, renames, or materially changes the responsibility of a standard
prompt, skill, or template, the implementation agent must reconcile the corresponding category guide before the
change is complete.

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

## Agent execution memory

The agent actively maintains:

```text
agent_plan.md
agent_state.md
plan/agent_plan_phase_<N>.md
plan/agent_plan_<scope>.md
```

when their current truth changes in the applicable workspace.

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

## Maps

Maps should be refreshed when structural changes materially affect knowledge the map already represents, and may
be extended when later work identifies valuable source concerns outside the current mapping scope.

Routine local source edits do not necessarily require map maintenance.

When Bonsai itself makes a material source change during project implementation and a known relevant map is
affected, it should surface bounded maintenance at a natural boundary rather than silently treating the existing map
as current. The source change does not itself authorize generated-map mutation; accepted maintenance runs through
the normal mapping workflow.

When project work naturally exposes reusable, non-obvious source knowledge that is not adequately mapped, Bonsai
may recommend map creation or extension. It must not broaden source inspection merely to search for such
opportunities.

Map/source identity must remain trustworthy enough that Bonsai does not knowingly apply a stale or mismatched map
as though it represented current source.

Generated standard map layers may be updated as part of an authorized bounded mapping unit when source discovery
shows they are the correct architectural destination for the selected focus. Exact standard file paths do not need
to be approved before discovery.

---

# Clean Rebuild Objective

Bonsai project memory should describe the target system and current execution reality, not every historical detour.

A mature Bonsai project should support a clean rebuild from useful durable memory.

Preserve:

- final requirements;
- final architecture;
- useful roadmap structure;
- current execution state;
- durable operational knowledge;
- useful maps.

Discard or replace:

- obsolete pivots;
- stale session history;
- resolved blockers;
- superseded execution state;
- troubleshooting history;
- temporary scaffolding;
- accidental implementation scars that no longer describe the target system.

---

# Typical Working Rhythm

## Project work

A normal Bonsai project may look like this:

1. Enable Bonsai in the repository with `.bonsai/start.md`.
2. Explore product and architecture design in a Web UI AI.
3. Use `prompts/create_project.md` to synthesize durable project memory.
4. Save the resulting memory under `.bonsai/projects/main/` or a named project.
5. Start implementation with `Read .bonsai/start.md and follow its instructions.`
6. Plan or review the current phase when required.
7. Execute the exact authorized next action.
8. Reconcile execution memory at natural boundaries.
9. When the just-completed work materially affected a known map, address the bounded maintenance recommendation;
   when already-required source inspection revealed valuable reusable unmapped knowledge, optionally act on the
   resulting mapping recommendation.
10. Continue in the current session, use fresh-session one-step continuation, review/change the next step, or exit.
11. Preserve durable operational discoveries in agent context when they qualify.
12. Complete the project when the approved scope is implemented and reconciled.

## Map work

A normal mapping effort may look like this:

1. From the repository to be mapped, choose **Create Code Map**, **Extend Code Map**, **Refresh Code Map**, or resume
   an existing map workspace.
2. Let Bonsai derive the current source location, source identity, and sensible map identity when they are
   unambiguous.
3. Review or override those defaults when needed.
4. Let Bonsai create, reuse, or reactivate the repository-local map workspace required for durable mapping
   execution.
5. Make the map workspace active for mapping execution.
6. Use `agent_plan.md` as the map-wide roadmap.
7. Select one bounded mapping focus appropriate to the lifecycle intent.
8. Reconcile that focus into the map roadmap/state as the exact next mapping unit without changing generated
   output.
9. Choose current-session continuation, fresh-session continuation, review/change, or **Exit for now**.
10. Execute the complete authorized mapping unit: inspect source, determine architectural ownership, resolve and
    update the justified standard map layers, validate them, and reconcile workspace state.
11. Create scoped plans under `plan/` only when a mapping unit is too large for useful roadmap-level execution.
12. At the next mapping-unit boundary, select another bounded focus rather than automatically continuing into
    unrelated mapping work.
13. Mark the map workspace complete only when the current mapping scope is exhausted and its generated output is
    reconciled.
14. Reactivate the same map workspace later for explicit extension, source-change maintenance, or an accepted
    project-discovered mapping recommendation.

For mapping efforts that require deliberate preparation or calibration before coding-agent execution, the human
may instead use `prompts/create_map.md` to create the map workspace explicitly.

---

# Validation Cases

The Bonsai standard should validate at least the following workspace and mapping behaviors.

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
13. A large mapping unit may create `plan/agent_plan_<scope>.md`.
14. A still-larger sub-scope may create another flat scoped detailed plan without introducing nested plan
    directories.
15. `agent_state.md` identifies the active detailed plan and exact next step.
16. Detailed map plans do not become project phases and do not automatically create phase-review gates.

## Map storage and ownership

17. Map workspace execution memory remains repository-local.
18. Generated reusable map output remains in the active map store.
19. Embedded Bonsai may physically overlap those locations without confusing their roles.
20. Legacy generated map state is absent from the active execution model; map `agent_plan.md` and `agent_state.md`
    own continuation.
21. `map_calibration.md` remains human-owned input and is not treated as execution state.

## Project-map associations

22. A project can add or remove useful map selections in project `agent_context.md`.
23. Association changes do not rebuild, move, or delete generated maps.
24. Future project sessions can use those selected maps without rediscovering the entire map store.

## Creation workflows

25. `create_project.md` creates `workspace.md` plus project memory and the repository bootstrap for initial
    synthesis.
26. `create_map.md` creates `workspace.md`, `agent_plan.md`, `agent_state.md`, optional `map_calibration.md`, and the
    repository bootstrap.
27. `create_map.md` does not generate `code_map.md`, subsystem maps, or lookup tables.

## Code-map creation interaction

28. **Create Code Map** may create or reuse the corresponding repository-local map workspace as part of the same
    approved code-map action.
29. Automatic workspace creation preserves existing generated output, calibration, supplied source, and unknown
    colocated files.
30. A partial or ownership-ambiguous same-name workspace blocks automatic repair or overwrite.
31. A newly usable generated map may be associated with the active project only when that association was part of
    the approved action or is separately selected later.

## Map completion and reactivation

32. Map completion requires exhausted current mapping scope plus reconciled generated output and source identity.
33. Completing a scoped map plan returns control to the map-wide roadmap rather than creating a project-style phase
    transition.
34. A completed map workspace may later reactivate for a real source change, explicit maintenance request, or
    expanded mapping scope without destroying prior generated output.
35. Handoff does not write project phases, passes, contracts, project final-truth state, icebox state, active
    workspace identity, or session history into map memory.

## Mapping-unit authorization

36. Selecting a bounded mapping focus updates durable map execution memory without beginning substantive source
    inspection or generated-output mutation.
37. Once that focus is one executable exact next action, current-session and fresh-session continuation authorize
    the complete mapping unit rather than discovery alone.
38. Source discovery may resolve the exact standard Markdown target set without another human gate.
39. A cross-cutting mapping focus may update standard layers in several existing subsystems without requiring a
    standalone subsystem of the same name.
40. Discovery may justify `api_pub.md`, `api_ext.md`, or a new subsystem map inside the selected focus without a
    second approval merely because those exact paths were not predictable beforehand.
41. Material source-scope expansion, materially different source/map identity, destructive work, generated-map
    ownership restructuring, unrelated new mapping work, and insufficient source evidence still stop at the
    applicable human gate.
42. Creating or materially expanding optional lookup/index artifacts remains separately gated and is not silently
    absorbed into the standard mapping-unit output envelope.
43. Mapping handoff normally occurs after generated-map production and validation, not immediately after discovery,
    unless discovery reaches a real blocker or mandatory human decision.

## Code-map extension, maintenance, and project recommendations

44. **Extend Code Map** reuses or reactivates the existing compatible map workspace and does not create a duplicate
    map merely because new coverage is requested.
45. A human request to map another subsystem becomes a bounded mapping focus; source discovery still determines the
    justified generated architectural ownership rather than blindly creating a same-named subsystem artifact.
46. A human may request a cross-cutting focus or ask Bonsai to review current map coverage and suggest valuable
    additions before selecting the next mapping unit.
47. When Bonsai materially changes source represented by a known relevant map during authorized project work, it
    surfaces bounded map maintenance at a natural project boundary when the existing mapped knowledge is affected.
48. Routine private implementation changes that do not materially alter mapped knowledge do not trigger map
    maintenance merely because files changed.
49. An implementation session that already had to establish reusable, non-obvious, architecturally significant
    source knowledge may recommend creating or extending a code map when that knowledge is not adequately mapped.
50. Project implementation does not inspect unrelated source merely to search for mapping opportunities.
51. A maintenance or mapping-opportunity recommendation does not mutate generated maps or silently expand project
    execution scope before human acceptance.
52. An accepted maintenance or mapping recommendation enters the normal map-workspace and bounded mapping-unit
    workflow and may use current-session or fresh-session continuation.
53. Closely related mapping observations are combined and a declined or deferred recommendation is not repeatedly
    resurfaced during the same work merely because the opportunity still exists.
54. Refresh preserves the intended map identity and coverage where possible, while rebuild remains the separately
    gated path for destructive replacement or broad generated-map ownership restructuring.

These cases are behavioral expectations, not a mandate for one particular test harness implementation.
