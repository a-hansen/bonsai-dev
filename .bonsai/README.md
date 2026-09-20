# Bonsai

Bonsai keeps the project knowledge an AI needs outside the chat session so software projects and code-mapping work can continue cleanly across fresh sessions.

This README is the practical user guide. For the authoritative Bonsai operating model, see [`specification.md`](specification.md).

---

# Install Bonsai

The preferred installation is a Git checkout of the Bonsai repository used as your **Bonsai Home**.

A Bonsai Home is one shared Bonsai installation that can serve multiple source repositories.

```text
git clone https://github.com/a-hansen/bonsai-dev.git
```

Configure `BONSAI_HOME` to point at the checkout's `.bonsai` directory:

```text
BONSAI_HOME=<path-to-bonsai-dev>/.bonsai
```

Use your normal shell or operating-system mechanism to make that environment variable available to coding-agent sessions.

Prompts, skills, templates, reusable context, and generated code maps live under the Bonsai Home rather than being copied into every source repository.

## Updating Bonsai

When Bonsai Home is a Git checkout, update it normally:

```text
cd <path-to-bonsai-dev>
git pull
```

Repository-local project and map workspace memory remains with the repositories that own it.

## Embedded Bonsai

A repository may instead contain a complete Bonsai standard inside its local `.bonsai` directory.

If `BONSAI_HOME` is unavailable and the embedded standard is valid, Bonsai can use it.

Embedded mode is useful for a self-contained repository, but a shared Git-backed Bonsai Home is the normal installation for working across repositories.

---

# Enable a Repository

A Bonsai-enabled repository needs:

```text
repo/
└── .bonsai/
    └── start.md
```

Project and map workspaces are added beneath `.bonsai` as needed.

If you create project memory with:

```text
<bonsai-home>/prompts/create_project.md
```

the generated package includes the appropriate `.bonsai/start.md`.

For a repository that does not yet need project memory, place the Bonsai distribution's canonical `start.md` at:

```text
repo/.bonsai/start.md
```

In Bonsai Home mode, the repository-local `.bonsai` directory holds repository and workspace memory while the shared Bonsai standard remains in Bonsai Home.

In Embedded mode, the local `.bonsai` directory holds both.

---

# The Prompt You Will Use Most

Open a coding-agent session in a Bonsai-enabled repository and start with:

```text
Read .bonsai/start.md and follow its instructions.
```

That is the normal Bonsai entry point.

For a named project:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

For a map workspace, always identify it explicitly:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

You can also append an ordinary request:

```text
Read .bonsai/start.md and follow its instructions. Manage Code Maps.
```

The startup prompt should stay small. You should not need to summarize the previous chat, tell the agent which Bonsai skills to load, or reconstruct where the work stopped.

Bonsai's saved workspace state carries that information.

---

# Day-to-Day Project Workflow

A normal project rhythm is:

1. Design or revise product behavior and architecture in a Web UI AI conversation when useful.
2. Preserve mature design with `<bonsai-home>/prompts/create_project.md`, or update the existing project requirements and architecture.
3. Start the coding agent with `Read .bonsai/start.md and follow its instructions.`
4. Review any planning, contract, design, or approval step that needs your input.
5. Let the agent perform the authorized implementation work.
6. Let Bonsai load deeper requirements, architecture, code maps, context, or skills only when they become relevant.
7. Let Bonsai preserve useful environment and tooling discoveries when they are likely to matter again.
8. Stop before implementation changes approved product behavior or architecture without your approval.
9. Preserve unrelated issues only when you choose to keep them.
10. At a natural boundary, let Bonsai record where the work stopped and what should happen next.
11. Continue in the current session or resume later from the saved project state.

Mapping work follows the same general pattern, but around selected areas of source rather than project implementation phases.

---

# The Basic Model

Bonsai separates shared framework material from repository-local work:

```text
Bonsai Home
    shared standard
    reusable developer/agent context
    reusable generated code maps

Source repository
    .bonsai/start.md
    repository context
    project workspaces
    map workspaces
```

Bonsai has two resumable workspace types:

| Workspace | Location                      | Purpose                                                                |
| --------- | ----------------------------- | ---------------------------------------------------------------------- |
| Project   | `.bonsai/projects/<project>/` | Product and architecture truth plus implementation state               |
| Map       | `.bonsai/maps/<map>/`         | Repository-local state for creating and maintaining reusable code maps |

The directory structure defines the workspace type. Projects and maps do not need a separate manifest declaring what they are.

Every established workspace has:

```text
agent_plan.md
agent_state.md
```

`agent_plan.md` is the durable roadmap.

`agent_state.md` records where the work stopped, whether it is ready to continue, any current blocker, and what should happen next.

---

# Projects

For a normal single-project repository, use:

```text
.bonsai/projects/main/
```

`main` is the conventional default project name.

A repository may also contain multiple named projects:

```text
.bonsai/projects/
├── project-a/
├── project-b/
└── project-c/
```

If several projects could apply, identify the desired project explicitly when starting the session.

Bonsai does not rely on a persistent repository-wide "current project" setting. Active project selection belongs to the session.

## Creating Project Memory

Product and architecture design is usually best handled conversationally in a Web UI AI session.

Work through the design normally. When it is mature enough to preserve, use:

```text
<bonsai-home>/prompts/create_project.md
```

Paste that prompt into the design conversation.

The workflow produces an extractable repository-root package containing `.bonsai/start.md` and the selected project memory.

A normal project begins with:

```text
.bonsai/projects/<project>/
├── requirements.md
├── architecture.md
├── agent_plan.md
└── agent_state.md
```

Additional requirements, architecture, project-specific context, detailed plans, or an icebox are added only when useful.

After extracting the package into the repository, start implementation with the normal `start.md` prompt.

## Project Files

| File                                       | Role                                                             | Ownership   |
| ------------------------------------------ | ---------------------------------------------------------------- | ----------- |
| `requirements.md`                          | Product behavior, constraints, scope, accepted product decisions | Human-owned |
| `architecture.md`                          | Target implementation structure and architectural constraints    | Human-owned |
| `agent_plan.md`                            | Project roadmap and phase progression                            | Agent-owned |
| `agent_state.md`                           | Where work stopped and what should happen next                   | Agent-owned |
| `agent_context.md`                         | Project-specific reusable operational knowledge                  | Agent-owned |
| `plan/agent_plan_phase_<N>.md`             | Detailed phase plan when warranted                               | Agent-owned |
| `requirements/requirements_<AREA>.md`      | Deeper product truth when warranted                              | Human-owned |
| `architecture/architecture_<SUBSYSTEM>.md` | Deeper subsystem architecture when warranted                     | Human-owned |
| `icebox.md`                                | Human-selected deferred observations                             | Human-owned |

These files deliberately have different jobs.

Requirements are not implementation notes. Architecture is not a task list. State is not session history. Agent context is not a troubleshooting diary.

---

# What Happens at Startup

`start.md` identifies the active Bonsai installation, repository, and workspace, then reconstructs enough saved state to decide what should happen next.

Bonsai does not automatically load every requirement, architecture file, code map, context file, plan, or skill.

By default, Bonsai reconstructs where the work left off and stops before beginning new implementation if your input or approval is required.

If work was already authorized, you can explicitly tell a fresh session to continue it immediately.

This keeps startup small while avoiding accidental continuation through a decision that still needs human review.

---

# Planning and Execution

## Phase 1

A newly created project begins implementation by drafting and reviewing its Phase 1 plan before substantive implementation starts.

The design conversation does not create that detailed implementation plan.

Planning happens in the implementation environment because the coding agent can inspect the actual repository and current development environment.

## Later Phase Plans

Later detailed phase plans are created only when they add real value.

Examples include:

* sequencing that is too detailed for the project roadmap;
* an important API or other contract that deserves a separate review;
* several approval points that need to remain visible during execution.

A phase touching several files is not by itself a reason to create a detailed phase plan.

## Execution Readiness

`agent_state.md` records the actual current condition of the work.

Common states include:

```text
Design required
Phase planning required
Awaiting human review
Blocked
Ready to execute
Complete
```

A plan existing does not mean implementation is authorized.

`Ready to execute` means the next task is established and no separate human decision still blocks it.

## Contract Reviews

Some work establishes an API, schema, protocol, persistent format, extension surface, or other contract that is worth reviewing before the implementation beneath it is written.

When that review would be useful, Bonsai can split the work into:

1. contract definition;
2. human review;
3. implementation.

Tests may be used to demonstrate intended contract usage before the rest of the implementation exists.

This is not required merely because work can be divided into two steps. The contract itself should be worth reviewing.

---

# Fresh Sessions and Handoffs

Fresh sessions are normal Bonsai usage.

At a natural stopping point, Bonsai updates the active workspace so the saved state reflects where the work actually stopped and what should happen next.

You can then:

* continue in the current session;
* start a fresh session;
* change or review the next step;
* stop for now.

Ordinary project resume:

```text
Read .bonsai/start.md and follow its instructions.
```

Ordinary map resume:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

If Bonsai has already established work that is ready to execute and you deliberately want a fresh session to perform it immediately:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate.
```

Append the project identity when needed for unambiguous selection. Always append the map identity for map work.

The new session reloads the saved project or map state before executing.

It does not rely on copied phase text or a hand-written summary from the previous chat, and it still stops if it discovers a new blocker or a decision that requires human input.

Do not paste a previous chat summary into every fresh session. Bonsai memory should carry what matters.

---

# Changing Requirements or Architecture

Bonsai treats project requirements and architecture as **human-owned final truth**.

During implementation, a proposed change to that final truth is classified as:

```text
None
Clarification
Revision
```

**None** means the existing requirements and architecture already support the work.

**Clarification** means the intended design is unchanged, but the documentation should state it more precisely.

**Revision** means approved behavior, constraints, architecture, or system boundaries would change.

A revision stops for human approval before implementation continues in the new direction.

For a meaningful design change, update the affected requirements or architecture, review the new direction, then resume implementation from the saved project state.

Chat history is not the authoritative record of the change.

---

# Developer Context and Agent Context

Bonsai keeps guidance you intentionally provide separate from useful operational facts discovered while working.

## Developer Context

`developer_context.md` is human-owned guidance.

It can contain things such as:

* coding preferences;
* testing philosophy;
* repository conventions;
* required tools or SDKs;
* runtime constraints;
* AI working preferences.

Bonsai Home mode may use both:

```text
$BONSAI_HOME/developer_context.md
repo/.bonsai/developer_context.md
```

Bonsai Home context applies broadly. Repository context is more specific when the two overlap.

Developer context does not override approved project requirements or architecture.

## Agent Context

`agent_context.md` is reusable operational knowledge discovered while working.

Examples include:

* a repository requires `python3` rather than `python`;
* the reliable build or test command;
* the location of an external source checkout;
* an environment-specific tooling limitation;
* which reusable code maps are useful to a project.

Instead of rediscovering those facts in later sessions, Bonsai can preserve the useful conclusion and reuse it when relevant.

Agent context may exist at Bonsai Home, repository, or project scope:

```text
$BONSAI_HOME/agent_context.md
repo/.bonsai/agent_context.md
repo/.bonsai/projects/<project>/agent_context.md
```

Users normally do not need to create, organize, or edit these files.

Agent context should contain concise reusable conclusions, not troubleshooting history or session transcripts.

Active project or map identity does not belong there, and secrets must never be stored there.

---

# Out-of-Scope Discoveries

Implementation often exposes adjacent issues.

Bonsai does not automatically turn those observations into authorized work.

The normal behavior is:

1. notice the issue;
2. continue the authorized work when safe;
3. surface the observation at a natural boundary;
4. preserve it in `icebox.md` only if you choose to keep it.

The icebox is not an approved backlog.

Preserving an observation does not authorize implementation.

---

# Code Maps

Code maps are reusable structural knowledge for navigating source.

They help Bonsai avoid rediscovering the same architecture, extension points, public surfaces, and relationships each time it works in a large or unfamiliar codebase.

Code maps are navigation aids, not project truth and not substitutes for inspecting actual source.

The source remains authoritative.

## Map Workspace vs. Generated Code Map

These are related but have different jobs:

```text
repo/.bonsai/maps/<map>/
    repository-local mapping state

$BONSAI_HOME/maps/<map>/
    reusable generated source knowledge
```

A map workspace contains `agent_plan.md`, `agent_state.md`, optional human calibration, and optional detailed mapping plans.

It allows substantial mapping work to resume across sessions.

The generated map is the reusable result.

`code_map.md` is its normal entry document, with deeper subsystem or API maps added when source discovery justifies them.

In Embedded mode, workspace and generated-map storage can physically overlap while keeping those roles distinct.

## Creating a Code Map

From a coding-agent session, the normal request is simply:

```text
Create a code map.
```

Or use **Manage Code Maps**.

When enough context is already known, Bonsai derives sensible defaults rather than asking you to repeat the current source, map identity, workspace, or initial focus.

For deliberate Web UI preparation or calibration before mapping, use:

```text
<bonsai-home>/prompts/create_map.md
```

That workflow prepares the repository-local map workspace and optional `map_calibration.md`.

It does not generate the reusable code map itself. Mapping happens later against the actual source.

## Map Lifecycle

Bonsai supports four main map operations:

* **Create**: establish a map where no suitable reusable map exists.
* **Extend**: add useful coverage, such as another subsystem or cross-cutting concern.
* **Refresh**: reconcile mapped knowledge after source changes while preserving the map's intended coverage where possible.
* **Rebuild**: replace a substantial part of the generated representation when refresh or extension is not enough.

Mapping is normally done in selected areas of the source rather than attempting to map an entire repository at once.

Once you approve an area to map, Bonsai normally completes that mapping work, updates the reusable map, validates the result, and records where the mapping work stands.

## Project Associations

A project can record which reusable code maps are useful to it.

The association is stored in project `agent_context.md`:

```text
Useful code maps:
- library-a
- library-b
```

Use **Manage Code Maps** to add or remove an association.

Bonsai maintains the agent-context entry. The association does not modify the generated map.

## Source Alignment

A generated code map represents a particular version of its source.

Bonsai should not knowingly use a map against an incompatible source version.

Map identity retains enough source information to distinguish meaningful versions or revisions when necessary.

---

# Multi-Repository Work

A project can use source and code maps from several repositories without copying those repositories' project memory into the consuming project.

Reusable generated maps live under the active Bonsai map store.

Stable source locations and other operational facts can be preserved in agent context.

Project requirements and architecture remain focused on the product rather than machine-specific source paths.

This allows Bonsai to reuse knowledge of libraries, frameworks, and neighboring repositories while keeping each project's own requirements and architecture separate.

---

# In One Picture

```text
                    coding-agent session
                           │
                           ▼
                  repo/.bonsai/start.md
                           │
                           ▼
                 reconstruct saved state
                           │
                 ┌─────────┴─────────┐
                 │                   │
                 ▼                   ▼
          needs your input     work is authorized
                 │                   │
                 ▼                   ▼
             stop and ask          execute
                                     │
                                     ▼
                              update saved state
                                     │
                                     ▼
                         continue now or resume later
```

The startup stays small.

Bonsai loads the project, context, and source knowledge it needs as the work requires them, records useful state before stopping, and lets a later session continue from there.
