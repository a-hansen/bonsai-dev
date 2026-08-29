# Bonsai Specification

Bonsai is a project-memory and execution-workflow system for AI-assisted software development.

It preserves the structured context an AI needs to design, build, inspect, and continue serious software work across fresh sessions without making chat history authoritative.

Bonsai is designed to support:

- simple repositories that need only local project memory;
- repositories containing multiple independent Bonsai projects;
- projects whose useful source universe spans multiple repositories;
- reusable code maps for independently maintained libraries or frameworks;
- reusable developer and agent context;
- frequent fresh implementation sessions with small startup prompts.

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

Changes to Bonsai behavior, boundaries, ownership, lifecycle, environment model, mapping model, or interaction model should therefore be reflected here before or alongside changes to the standard files that implement them.

Detailed procedural mechanics may live in prompts and skills when repeating them here would make the specification unnecessarily large.

---

# Core Principles

## Durable truth is separate from working state

Requirements and architecture describe the product and target system.

Plans and state describe how approved work is currently being executed.

The implementation agent must not casually turn execution decisions into durable product or architectural truth.

## Human-owned and agent-owned artifacts are visibly different

Human-owned artifacts use natural names.

Agent-owned artifacts use the `agent_` prefix.

Examples:

```text
requirements.md
architecture.md
developer_context.md
icebox.md

agent_plan.md
agent_state.md
agent_context.md
```

The prefix means Bonsai is allowed to maintain or rewrite the artifact according to its lifecycle rules.

It does not mean the artifact is automatically loaded every session.

## Human control should not require constant babysitting

Bonsai uses explicit gates at meaningful boundaries:

- Phase 1 plan approval;
- later phase-plan approval when a detailed plan is warranted;
- durable contract review;
- final-truth clarification or revision;
- material execution deviations.

It does not require approval for ordinary maintenance of agent-owned execution memory.

## Simple projects should stay simple

A normal repository should not require a registry, dependency graph, or elaborate configuration system merely to use Bonsai.

Additional structure should appear only when the work actually needs it.

## AI sessions are the primary interaction model

The normal Bonsai implementation experience begins inside a coding-agent session.

The canonical startup instruction is intentionally small:

```text
Read .bonsai/start.md and follow its instructions.
```

Optional shell helpers may make setup or startup more convenient, but they are not the conceptual center of Bonsai.

## Bootstrap should resolve identity, not load knowledge

Bootstrap establishes:

- Bonsai Home;
- repository home;
- active project.

It should not eagerly load every context file, map, skill, requirement area, or architecture subsystem.

The implementation kernel decides what knowledge is needed after identity is established.

## Deterministic discovery should be cheap

Filesystem enumeration, environment-variable lookup, project listing, and similar deterministic tasks should use host tools rather than model reasoning when possible.

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

## Mapping is part of Bonsai

Code mapping is an integrated Bonsai capability.

Bonsai can create, inspect, update, remove, and use maps as part of normal implementation work.

A repository does not need to become a full Bonsai project before its source can be mapped.

## Maps describe source, not projects

A map represents a source universe or source snapshot.

The active Bonsai project may inform map generation, but the project does not become the map identity.

## Maps and source must agree

A code map represents a particular source snapshot.

Bonsai must not silently use a map for one source version while reasoning from another incompatible version.

---

# Bonsai Environment Model

Bonsai separates the shared standard, reusable developer assets, repository-local memory, project memory, and source maps.

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
│   ├── implementation.md
│   ├── create_project_memory.md
│   └── create_map_repo.md
├── skills/
│   ├── menu.md
│   ├── phase_execution.md
│   ├── dry_run.md
│   ├── handoff.md
│   ├── final_truth_update.md
│   ├── agent_context.md
│   └── code_maps.md
├── templates/
│   ├── plan_phase_template.md
│   └── icebox_template.md
├── developer_context.md                 # Optional reusable human-owned context
├── agent_context.md                     # Optional reusable agent-owned context
└── maps/
    ├── barcache/
    ├── tickerview/
    └── investment-app/
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

Embedded mode must use the same project-memory semantics as Bonsai Home mode.

A user should not need to set `BONSAI_HOME` merely to point Bonsai at standard files already present in the repository.

## Creating a Bonsai Home

A repository may begin in embedded mode and later create a reusable Bonsai Home.

**Create Bonsai Home** is a Bonsai workflow, normally available through **See more options** and also invokable as an explicit startup request.

For example:

```text
Read .bonsai/start.md and follow its instructions. Create a Bonsai Home.
```

The workflow requires the environment variable:

```text
BONSAI_HOME
```

to already be defined.

`BONSAI_HOME` identifies the intended reusable home location. The target directory does not have to exist yet.

If `BONSAI_HOME` is not defined, the workflow must stop and tell the human to configure it before trying again.

Bonsai should not silently substitute a path supplied only for the current session and should not store the Bonsai Home location in `agent_context.md` as a discovery fallback.

The Bonsai Home location is environment identity, not learned project knowledge.

Once `BONSAI_HOME` is configured, Create Bonsai Home may:

- create the target directory when necessary;
- copy the Bonsai standard there;
- create reusable context and map locations when required;
- preserve repository project memory;
- explain any follow-up environment configuration still required.

Creating a Bonsai Home must not automatically modify shell startup files, machine configuration, or other developer-owned environment configuration without explicit authorization.

When both a valid `BONSAI_HOME` and an embedded standard are available, the Bonsai Home is the preferred standard for the session.

## Repository home

The **repository home** is the source-repository root containing the local `.bonsai` anchor.

Bonsai does not require a separate `PROJECT_HOME` environment variable.

The repository-local `.bonsai/start.md` establishes the repository anchor for a normal AI session.

## Repository-local Bonsai memory

In Bonsai Home mode, repository-local `.bonsai` contains only the material that belongs to that repository or its projects, plus the small startup bootstrap.

Conceptually:

```text
repo/
└── .bonsai/
    ├── start.md
    ├── developer_context.md              # Optional human-owned local context
    ├── agent_context.md                  # Optional agent-owned local context
    └── projects/
        └── main/
            ├── requirements.md
            ├── architecture.md
            ├── agent_plan.md
            ├── agent_state.md
            ├── agent_context.md          # Optional project-specific operational context
            ├── icebox.md                 # Optional
            ├── plan/
            │   └── agent_plan_phase_1.md
            ├── requirements/
            │   └── requirements_<AREA>.md
            └── architecture/
                └── architecture_<SUBSYSTEM>.md
```

Bonsai Home mode does not require copies of `specification.md`, standard prompts, skills, or templates inside every repository.

## Developer-level reusable material

An Bonsai Home may contain reusable context and maps that apply across repositories.

Examples include:

- stable developer preferences;
- host or toolchain context;
- reusable operational knowledge;
- source locations;
- shared code maps.

Developer-level material must remain distinct in meaning from repository and project memory even when it physically lives under the same Bonsai Home.

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

Examples:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

```text
Read .bonsai/start.md and follow its instructions. Create a Bonsai Home.
```

```text
Read .bonsai/start.md and follow its instructions. Manage Code Maps.
```

Bonsai should not require a formal startup-command language. Natural language is sufficient.

`start.md` is deliberately small.

Its job is to establish environment identity and hand control to the Bonsai Home or embedded implementation kernel.

## Bootstrap responsibilities

The bootstrap should:

1. establish repository home from the local `.bonsai` anchor;
2. resolve Bonsai Home;
3. resolve the active project;
4. preserve those resolved values as current-session context;
5. load `<bonsai-home>/prompts/implementation.md`;
6. continue under the standard implementation workflow.

The bootstrap should not routinely load requirements, architecture, maps, developer context, agent context, or specialized skills itself.

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

## Active project is session state

The active project belongs to the current AI session.

It must not be persisted as a mutable repository-wide pointer.

It also should not be stored as durable `agent_context.md` merely because the current session selected it.

This allows two sessions in the same repository to operate on different named projects without interfering with one another.

---

# Projects

A repository may contain one Bonsai project or many.

Each project owns its own:

- requirements;
- architecture;
- execution roadmap;
- execution state;
- phase plans;
- optional icebox;
- layered project truth;
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

An explicit project supplied by the human is authoritative for that session.

If no project is explicit, project selection should be resolved cheaply:

1. if `projects/main` exists, use it;
2. otherwise enumerate project directories;
3. if exactly one project exists, use it;
4. if several projects exist, present a human selection;
5. if no project exists, surface project creation or design as the next required action.

Project selection must not overwrite another concurrent session's project selection.

## Project management

Project-management actions are part of the normal Bonsai interaction model and normally live under **See more options**.

Useful actions include:

- List Projects;
- Switch Project;
- Create Project.

Switching changes the active project for the current session only.

Creating a project establishes its project-memory location. It does not invent requirements or architecture.

If durable project design has not yet been synthesized, the new project's execution readiness is effectively `Design required`.

---

# Artifact Ownership

Ownership determines who controls the durable meaning of an artifact.

Ownership is separate from loading behavior.

## Human-owned artifacts

Human-owned artifacts use natural names.

Typical examples include:

```text
requirements.md
architecture.md
developer_context.md
icebox.md
```

Human ownership does not mean the human must manually edit every line.

An AI may draft or mechanically maintain a human-owned artifact when instructed, but changes to durable meaning require human authorization.

## Agent-owned artifacts

Agent-owned artifacts use the `agent_` prefix.

Typical examples include:

```text
agent_plan.md
agent_state.md
agent_context.md
plan/agent_plan_phase_<N>.md
```

The agent actively maintains these when their current truth changes.

They should describe current useful state, not preserve a historical diary.

## Avoid hybrid ownership

Bonsai should avoid artifacts whose ownership is genuinely ambiguous.

When an artifact contains human-authorized meaning but is mechanically maintained by the agent, ownership is determined by who controls its durable meaning.

`icebox.md` remains human-owned because an observation may only be preserved there when the human chooses to retain it.

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

During implementation, proposed or completed work is classified against final truth as:

- `None`;
- `Clarification`;
- `Revision`.

A revision requires explicit human approval before substantive implementation proceeds under the changed direction.

---

# Agent Execution Memory

## `agent_plan.md`

`agent_plan.md` is the agent-maintained roadmap.

It records:

- implementation phases;
- phase status;
- active phase;
- execution mode;
- phase-plan presence;
- phase-plan approval state;
- roadmap-level deferrals;
- completed roadmap work.

It should remain roadmap-level.

Detailed execution sequencing belongs in a phase plan when one is needed.

## `agent_state.md`

`agent_state.md` is the current resume state.

It records only information that could materially change what the next implementation session does.

Typical contents include:

- current phase;
- active phase plan;
- phase-plan approval state;
- current phase pass;
- execution mode;
- execution readiness;
- current objective;
- concise current snapshot;
- resume-critical files;
- active blockers or risks;
- exact next step;
- success condition;
- compact active dry-run baseline, when one exists.

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

> If removing a fact would not materially change what the next implementation session does, it probably does not belong in `agent_state.md`.

## Phase plans

Detailed active phase plans are agent-owned:

```text
plan/agent_plan_phase_<N>.md
```

Phase 1 is intentionally special.

Every newly synthesized Bonsai project begins implementation by drafting and reviewing its Phase 1 plan before substantive implementation begins.

Later phase plans are created only when the phase genuinely benefits from them.

Useful reasons include:

- ordered sequencing too detailed for `agent_plan.md`;
- contract-first two-pass execution;
- multiple meaningful review gates;
- explicit constraints that must stay visible through execution.

A phase plan should not exist merely because a phase touches several files.

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

It replaces the narrower Bonsai 1.x concept of tooling-only memory.

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

Prefer:

```text
Use the repository Gradle wrapper for this build.
```

over a history of failed commands that led to that conclusion.

Agent context must not contain secrets.

It also does not authorize the agent to:

- install software;
- modify machine configuration;
- change project dependencies;
- alter developer-owned context;
- expand implementation scope.

Current blockers belong in `agent_state.md`.

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
effective operational context
```

More specific statements win when they conflict with broader statements.

A discovered fact should be stored at the narrowest scope that still makes it reusable.

Examples:

- a source checkout location reused across several repositories may belong in developer-level agent context;
- a build rule shared by all projects in one repository belongs in repository-level agent context;
- the code maps used only by one Bonsai project belong naturally in that project's `agent_context.md`;
- the active project for the current session belongs in none of them.

Project-level agent context is especially useful in repositories with several Bonsai projects or in projects whose source universe spans several repositories.

For example:

```text
Useful code maps:
- barcache
- tickerview
```

The project-memory creation workflow may seed project-level `agent_context.md` from human-approved design information such as known external source or code-map usage. The implementation agent then maintains that file as current operational truth.

Agent ownership does not prevent the design workflow from creating the initial file. It means the implementation agent may maintain it when the operational truth changes.

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

The local `start.md` establishes Bonsai Home, repository home, and active project.

The standard implementation prompt then loads only the minimum project state required to determine execution condition.

## Workflow-triggered context

Workflow files are loaded when the current state or requested action invokes that workflow.

Examples include:

- menu presentation;
- phase planning;
- contract review;
- dry run;
- handoff;
- final-truth reconciliation;
- project management;
- code-map management.

## Facet-triggered context

Specialized context is loaded only when the current work needs that facet.

Examples include:

- code maps;
- developer context;
- agent context;
- deep subsystem architecture;
- detailed requirement areas;
- preserved icebox observations.

The implementation kernel defines the exact loading rules.

The general principle is:

> Adding an artifact must not automatically make every future session more expensive.

---

# Project-Memory Creation Workflow

Product and architecture design is a Bonsai capability, but it is not primarily a coding-CLI workflow.

Bonsai assumes that design often happens in a Web UI AI conversation because conversational design is easier to inspect and can be materially cheaper than coding-agent sessions.

The human should be able to explore:

- goals;
- users;
- workflows;
- scope;
- constraints;
- architecture;
- alternatives;
- risks;
- sequencing.

The design should develop naturally.

Bonsai should not force a design conversation into templates prematurely.

When the design is mature enough to preserve, the human uses:

```text
$BONSAI_HOME/prompts/create_project_memory.md
```

or the equivalent embedded path.

The workflow synthesizes the discussion into durable Bonsai project memory.

For a normal single-project repository, the default output is a zip whose project memory is rooted at:

```text
.bonsai/projects/main/
```

The zip normally contains:

```text
.bonsai/projects/main/
    requirements.md
    architecture.md
    agent_plan.md
    agent_state.md
```

It may also contain:

```text
agent_context.md
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
```

when the design genuinely warrants them.

If the human has identified external source or code maps during design, the workflow may seed project-level `agent_context.md` with that approved operational information.

For example:

```text
Useful code maps:
- barcache
- tickerview
```

For a repository intentionally using named Bonsai projects, the human may explicitly request a named project instead of `main`.

The project-memory workflow does not generate the initial detailed Phase 1 plan.

Phase 1 planning remains the first implementation gate.

---

# Implementation Workflow

After `.bonsai/start.md` resolves session identity, implementation continues through:

```text
<bonsai-home>/prompts/implementation.md
```

The implementation agent:

1. loads the minimum project bootstrap state;
2. determines the exact next step and execution readiness;
3. loads additional project truth, plans, maps, context, or skills only when required;
4. identifies blockers or inconsistencies;
5. classifies anticipated final-truth impact;
6. stops at a structured startup gate;
7. executes only the human-authorized next step;
8. reconciles completed work;
9. maintains current execution memory;
10. preserves qualifying operational discoveries;
11. stops at the next natural gate.

The implementation prompt is a stable router and invariant set.

Detailed workflow belongs in triggered skills rather than one permanently loaded monolithic prompt.

---

# Execution Readiness

Bonsai makes the difference between planned and ready to execute explicit.

Typical execution-readiness values include:

| Value | Meaning |
| --- | --- |
| `Design required` | Product or architecture decisions must be resolved first. |
| `Phase planning required` | Durable design exists, but execution planning is incomplete. |
| `Awaiting human review` | A required plan, contract, or other artifact is waiting for approval. |
| `Ready to execute` | The exact next step has an approved basis and no required gate remains. |
| `Blocked` | A concrete blocker prevents safe execution. |
| `Complete` | No further implementation work is currently required. |

The existence of a plan does not imply implementation authorization.

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

## Host-provided free-form choices

Bonsai should not manufacture a generic `Other` menu entry when the host already provides a free-form choice such as:

```text
Other (type your answer)
```

## Startup gate

Before substantive work begins, the implementation agent summarizes current execution condition and stops.

The normal gate offers actions equivalent to:

1. Proceed with the identified next step.
2. Correct or discuss the identified next step.
3. Stop here.

Secondary actions remain accessible through **See more options** when applicable.

## Phase-plan gate

Every new project reviews the initial Phase 1 plan before Phase 1 implementation begins.

Later phase-plan gates exist only when a detailed phase plan is warranted.

## Contract gate

Contract-first two-pass execution is used when a phase establishes or materially changes a durable contract that independently deserves human review.

Examples may include:

- externally consumed APIs;
- schemas;
- persistent formats;
- protocols;
- extension contracts;
- durable integration surfaces.

Contract-first execution is not automatically required because a phase is large or internally complicated.

## Final-truth gate

If implementation requires a material change to human-owned requirements or architecture, the agent stops before silently adopting the change.

The impact is classified as:

| Impact | Meaning |
| --- | --- |
| `None` | Existing approved truth already covers the work. |
| `Clarification` | Intent is unchanged, but final truth should be stated more precisely. |
| `Revision` | Product behavior, constraints, architecture, or system boundaries change. |

A revision requires explicit human approval.

---

# Contract-First Two-Pass Execution

When a durable contract genuinely merits separate review, Bonsai may use two passes.

## Pass A: Contract

The agent produces the smallest useful native review surface.

Depending on the project, that may be:

- source-level API skeletons;
- concrete class shapes;
- schemas;
- protocol definitions;
- message examples;
- behavior-focused tests;
- usage examples;
- another durable contract artifact.

Bonsai should prefer the artifact developers will actually consume rather than manufacturing a separate prose contract merely for process.

Pass A must not invent unnecessary abstractions.

## Contract review

The human reviews the contract that matters.

After approval and any required final-truth reconciliation, Bonsai records the implementation next step.

## Pass B: Implementation

Only after contract approval does implementation proceed beneath the approved contract.

Single-pass work must not be labeled Pass B.

---

# Dry Runs

Dry runs are optional, read-only previews.

They may be useful when execution carries unusual risk or ambiguity.

A dry run may identify:

- approved basis;
- expected touch points;
- intended result;
- planned checks;
- likely scope concerns;
- anticipated final-truth impact.

Dry runs are deliberately secondary.

They should not appear as a routine mandatory step in ordinary Bonsai work.

During normal work, Dry Run is generally available through **See more options** rather than consuming space in the primary gate.

---

# Out-of-Scope Observations and `icebox.md`

Implementation frequently exposes adjacent work.

Examples include:

- unrelated bugs;
- technical debt;
- refactoring opportunities;
- missing documentation;
- missing tests;
- future enhancements.

Bonsai prevents these discoveries from silently expanding the authorized task.

The default behavior is:

1. notice the issue;
2. do not fix it;
3. continue the authorized work when safe;
4. do not automatically preserve it;
5. surface meaningful observations at the next natural gate.

The human decides whether an observation is worth keeping.

Only human-authorized observations belong in:

```text
icebox.md
```

The icebox is not:

- an approved backlog;
- a requirement source;
- an architecture source;
- a roadmap;
- an execution plan;
- an automatic dumping ground for agent observations.

Human authorization to preserve an item is not authorization to implement it.

---

# Code Maps

Code maps provide selective structural memory for source navigation.

They are navigation aids, not substitutes for source inspection and not project truth.

## Map store and source names

Every map has a meaningful source identity.

When an Bonsai Home is active, the map store is:

```text
$BONSAI_HOME/maps/
```

When Bonsai is embedded and no Bonsai Home is active, the repository's embedded store is:

```text
repo/.bonsai/maps/
```

The storage model is otherwise the same.

Examples:

```text
maps/
    barcache/
    tickerview/
    investment-app/
```

When version identity matters, the map identity may include a version or other distinguishing information:

```text
maps/
    barcache-1.0.0/
    tickerview-1.2.0/
```

The folder name does not need to carry every source-identity detail forever. The map entry document may preserve richer identity.

## Map identity follows source identity

A map is named for the source universe it represents, not for the Bonsai project that created it.

For a simple repository:

```text
repository: investment-app
project: main
map: investment-app
```

For a large repository containing several Bonsai projects, several projects may consume one map of the same repository source.

Bonsai should not generate duplicate maps merely because multiple project-memory directories exist.

## Mapping inputs

Every map is grounded in actual source.

Additional calibration can come from two complementary places.

### Existing Bonsai project memory

When the source being mapped belongs to an existing Bonsai project, mapping should use relevant durable project memory when available.

Useful inputs may include:

- requirements;
- architecture;
- archaeological analysis;
- implementation knowledge;
- source structure already captured in project memory.

Project memory helps Bonsai understand what concepts and boundaries matter.

It does not replace source inspection.

### Web UI mapping calibration

A repository or external source does not need existing Bonsai project memory in order to be mapped.

The human may use the Bonsai Web UI mapping-session prompt to describe:

- important concepts;
- representative entry points;
- areas that deserve deeper mapping;
- misleading or low-value areas;
- extension points;
- patterns worth recognizing;
- source areas that can be treated lightly.

That calibration produces an optional human-owned mapping artifact conventionally named:

```text
map_repo.md
```

A map store may therefore look like:

```text
$BONSAI_HOME/maps/barcache/
    map_repo.md               # Optional human-approved mapping calibration
    code_map.md
    ...
```

`map_repo.md` is mapping guidance. It is not product truth or architecture truth.

Project memory and `map_repo.md` may both be used when both are available.

## Mapping context and map storage are separate

The source context used to create a map and the location where the resulting map is stored are different concerns.

When mapping `barcache`, Bonsai should operate against the actual `barcache` source and use `barcache` project memory when available.

If an Bonsai Home is active, the resulting reusable map still belongs under:

```text
$BONSAI_HOME/maps/barcache/
```

This produces the rule:

> Map creation uses the context of the source being mapped. Map storage uses the active Bonsai map store.

## External source without Bonsai project memory

Bonsai must support mapping source that has no `.bonsai` project memory.

The workflow is:

```text
actual source
    +
optional Web UI map_repo.md
    ↓
mapping workflow
    ↓
named source map
```

This preserves the original Bonsai mapping use case while allowing project-aware maps when richer memory exists.

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

For released dependencies, a matching source artifact may be more appropriate than an unrelated development checkout.

For active cross-repository development, an exact matching repository revision may be preferable.

## Map entry document

A map set uses `code_map.md` as its normal entry document.

The entry document identifies the map and routes the agent into more detailed map data when needed.

The exact indexing and manifest format may evolve through real multi-repository use, but the source-identity boundary is required.

---

# Integrated Mapping Workflow

Code mapping is part of the main Bonsai workflow rather than a parallel Bonsai subsystem.

The v2 standard should therefore route mapping through the same startup, menu, context-layering, agent-context, and source-identity model used by implementation.

Legacy mapping prompts or procedures that assume a standalone `.bonsai/maps` workflow should be refactored accordingly.

The integrated mapping workflow should:

- be entered through **Manage Code Maps** or an explicit startup request;
- use the active Bonsai map store;
- identify the source being mapped independently from the active Bonsai project;
- use relevant project memory when available;
- use optional `map_repo.md` calibration when available;
- use actual source as authoritative;
- preserve stable source locations or mapping rules in appropriate agent context;
- return to the invoking Bonsai gate when the subordinate mapping workflow completes.

Existing map index and source-navigation structures should be retained where they remain useful. Integration does not require rewriting map data solely for architectural neatness.

---

# Manage Code Maps

Bonsai exposes code-map lifecycle actions through:

**Manage Code Maps**

During normal implementation, it generally appears under **See more options**.

Useful operations include:

- Create Code Map;
- Inspect Code Maps;
- Update or Rebuild Code Map;
- Remove Code Map;
- Inspect Map/Source Identity.

Map discovery should prefer the active Bonsai map store.

The human should not need to manually attach a map to every consuming project when Bonsai can identify the matching source and map safely.

## First-use behavior

When Bonsai encounters a substantial existing codebase without a useful map, it may surface map creation once as a primary contextual action.

If the human declines, mapping remains available through **See more options** rather than repeatedly interrupting implementation.

For a greenfield repository with little useful source, mapping should normally be deferred.

---

# Multi-Repository Source Universes

A Bonsai project may depend on source outside its repository.

Example:

```text
investment-app
    → barcache
    → tickerview
```

Each repository may have its own Bonsai project memory.

Maps for each source are reusable developer assets:

```text
$BONSAI_HOME/maps/
    investment-app/
    tickerview/
    barcache/
```

When a consuming project needs external source, Bonsai may use durable agent context, dependency information, map identity, and source inspection to locate the appropriate source and matching map.

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

The exact set should remain small.

## `prompts/implementation.md`

Stable implementation kernel and router.

It receives Bonsai Home, repository home, and active project from `start.md`, then determines the minimum additional context required for the current execution condition.

## `prompts/create_project_memory.md`

Web UI project-memory creation workflow.

It turns a mature design conversation into a zip containing durable Bonsai project memory, normally rooted at `.bonsai/projects/main/`.

It may also seed project-level `agent_context.md` with human-approved operational context such as known external code maps.

## `prompts/create_map_repo.md`

Web UI code-map calibration workflow.

It allows the human to provide source-specific mapping priorities when project memory is absent or when additional mapping emphasis is useful.

Its output is optional human-owned mapping guidance named `map_repo.md`.

---

# Framework Skills

Detailed workflow behavior lives in triggered skills rather than being permanently loaded.

Typical skills include:

- menu;
- phase execution;
- dry run;
- handoff;
- final-truth update;
- agent context;
- code maps.

Skills are Bonsai standard files.

They are not project memory.

---

# Framework Templates

Reusable artifact templates live under:

```text
<bonsai-home>/templates/
```

Templates should exist only when Bonsai has an explicit workflow that consumes them.

A template should not exist merely because a document type could theoretically be templated.

---

# Session Boundaries

Bonsai preserves continuity across fresh sessions, but it does not control the host application.

Bonsai cannot:

- terminate a chat;
- clear a session;
- reset a session;
- create a new session.

Those are human actions.

At a natural handoff, Bonsai records the exact next step and execution readiness before presenting continuation choices.

When execution is ready, the human may choose to continue:

- in the current session;
- in a fresh session;
- after reviewing or changing the next step;
- not at all right now.

Neither current-session nor fresh-session continuation is inherently preferred.

A fresh session does not bypass a blocker, review gate, or design requirement.

The canonical fresh-session prompt is:

```text
Read .bonsai/start.md and follow its instructions.
```

When project selection should be explicit:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

Phase, pass, approval state, next step, dry-run state, and other volatile information belong in project memory rather than the fresh-session prompt.

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

Routine implementation, project switching, project listing, project creation, and map management must not depend on the helper script once a Bonsai session is running.

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

A helper script may create this structure.

It may also be created manually from the Bonsai distribution.

Enabling the repository does not perform product design.

Durable requirements, architecture, roadmap, and state are synthesized through the Web UI design workflow.

---

# File Maintenance Discipline

## Bonsai specification

`specification.md` is human-owned Bonsai final truth.

Prompts, skills, templates, bootstrap files, README guidance, and helper scripts must conform to it.

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
```

when their current truth changes.

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

Maps should be updated when structural changes materially affect what the map is supposed to represent.

Routine local source edits do not necessarily require map maintenance.

Map/source identity must remain trustworthy enough that Bonsai does not knowingly apply a stale or mismatched map as though it represented current source.

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

A normal Bonsai project may look like this:

1. Enable Bonsai in the repository with `.bonsai/start.md`.
2. Explore product and architecture design in a Web UI AI.
3. Use `prompts/create_project_memory.md` to synthesize durable project memory.
4. Save the resulting memory under `.bonsai/projects/main/` or a named project.
5. Start implementation with `Read .bonsai/start.md and follow its instructions.`
6. Let bootstrap resolve Bonsai Home, repository home, and active project.
7. Draft and review the initial Phase 1 plan.
8. Execute one authorized bounded step.
9. Use contract-first execution only when a durable contract actually merits separate review.
10. Load maps, deep truth, developer context, agent context, and specialized skills only when needed.
11. Preserve durable operational discoveries in agent context rather than rediscovering them.
12. Keep primary menus focused and use **See more options** for project management, map management, and Dry Run.
13. Stop before material final-truth revisions or unauthorized scope expansion.
14. Let the human decide which out-of-scope observations deserve preservation.
15. Reconcile execution memory after completed work.
16. Record the exact next step and execution readiness.
17. Continue in the current session or a fresh one at the human's discretion.
18. Create named reusable maps for external repositories when they become part of the useful source universe.
19. Keep durable truth, working state, operational context, and maps compact as the project evolves.

---

# Bonsai 2.0 Validation Cases

Bonsai 2.0 should be validated against several concrete source topologies.

## Standalone repository

One repository, one `projects/main`, no relevant external source.

This case must remain extremely simple.

## Reusable multi-repository project

```text
investment-app
    → barcache
    → tickerview
```

This validates:

- Bonsai Home;
- reusable global and local context;
- project-aware map creation;
- maps for multiple repositories;
- dependency source discovery;
- durable source-location memory;
- map/source identity;
- reuse of maps across projects.

## Large monorepository

One repository contains many independent Bonsai projects and a large shared source universe.

This validates:

- named projects;
- session-local project selection;
- one source map serving several projects;
- avoidance of duplicate per-project maps;
- cheap project listing and switching.

## External source without Bonsai memory

A repository or released source tree has no Bonsai project memory.

This validates:

- Web UI mapping calibration;
- mapping from actual source without project memory;
- reusable named maps;
- source identity independent of project memory.

## Greenfield repository

Little useful source exists yet.

This validates that Bonsai does not pressure the human to create a code map when mapping would provide little value.

---

# Design Boundaries Still Being Validated

Bonsai 2.0 intentionally avoids over-specifying mechanisms that should be tested through real multi-repository use.

## Map manifest detail

The exact metadata stored in `code_map.md` or an adjacent manifest should remain minimal until real versioned map use proves what is required.

## Automatic dependency-to-map resolution

Bonsai should use dependency information, source locations, map identity, and agent context to connect consuming projects with useful maps.

The exact automatic discovery mechanics should be validated with `barcache`, `tickerview`, and `investment-app` rather than replaced by a large registry in advance.

## Helper-script packaging

Helper scripts are useful convenience, but their exact shell and host packaging is not fundamental Bonsai truth.

The AI-session workflow must remain usable without making the helper script the conceptual entry point.

## Migration

Migration from Bonsai 1.x is not part of the Bonsai 2.0 operating model defined here.

Migration behavior should not distort the clean 2.0 design unless a separate migration requirement is explicitly adopted.

---

# Summary

Bonsai has one human-owned specification:

```text
specification.md
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

Bonsai keeps several kinds of memory deliberately separate:

1. what the product should do;
2. what target architecture the human has approved;
3. what the agent should do next;
4. what deferred observations the human chose to preserve;
5. what durable working context the developer intentionally supplied;
6. what operational knowledge the agent learned;
7. what source structure code maps make cheaply navigable.

The active project belongs to the current session.

`projects/main` is the simple real-project convention, not a mutable project pointer.

Developer and agent context may exist globally and locally.

Durable discovery should become agent context when it is worth reusing.

Code maps are named for the source they represent.

When `BONSAI_HOME` is active, reusable maps live in its map store. Embedded mode uses the repository-local map store with the same semantics.

Map creation may use existing Bonsai project memory, optional Web UI mapping calibration, or both, but actual source remains authoritative.

This separation allows Bonsai to support simple repositories, monorepositories, multi-repository projects, reusable developer environments, and frequent fresh AI sessions without turning routine implementation into constant process management.
