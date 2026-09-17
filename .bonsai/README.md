# Bonsai

Bonsai is a workspace-memory and execution workflow for AI-assisted software development. It keeps the durable context an AI needs outside the chat session so projects and source-mapping work can continue across fresh sessions without repeatedly reconstructing history.

This README is the practical user guide. For the authoritative Bonsai operating model, see `specification.md`.

---

# Install Bonsai

The preferred installation is a Git checkout of the Bonsai repository used directly as your **Bonsai Home**.

```text
git clone https://github.com/a-hansen/bonsai-dev.git
```

Configure `BONSAI_HOME` to point at the checkout's `.bonsai` directory:

```text
BONSAI_HOME=<path-to-bonsai-dev>/.bonsai
```

Use your normal shell or operating-system mechanism to make that environment variable available to coding-agent sessions.

This gives you one reusable Bonsai standard for all repositories. Prompts, skills, templates, reusable context, and generated code maps live under that Bonsai Home rather than being copied into every source repository.

To update Bonsai later, update the checkout normally:

```text
cd <path-to-bonsai-dev>
git pull
```

## Embedded Bonsai

A repository may instead contain a complete Bonsai standard inside its local `.bonsai` directory. If `BONSAI_HOME` is unavailable and that embedded standard is valid, Bonsai can use it.

Embedded mode is useful for a self-contained repository, but a shared Git-backed Bonsai Home is the normal installation for working across repositories.

---

# Enable a Repository

A Bonsai-enabled repository has:

```text
repo/
└── .bonsai/
    └── start.md
```

Project and map workspaces are added beneath that local `.bonsai` directory as needed.

If you create project memory with `prompts/create_project.md`, the generated package includes the appropriate `.bonsai/start.md`. For a repository that does not yet need project memory, place the Bonsai distribution's canonical `start.md` at `.bonsai/start.md`.

The repository-local `.bonsai` directory holds repository and workspace memory. The shared Bonsai standard remains in `BONSAI_HOME`.

---

# The Prompt You Will Use Most

Open a coding-agent session in a Bonsai-enabled repository and start with:

```text
Read .bonsai/start.md and follow its instructions.
```

That is the normal implementation entry point.

For a named project:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

For a map workspace, always identify it explicitly:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

You can also append ordinary natural-language requests such as:

```text
Read .bonsai/start.md and follow its instructions. Manage Code Maps.
```

The startup prompt should stay small. You should not need to summarize the previous chat, identify which skills to load, or reconstruct the exact next step. Bonsai's durable workspace memory carries that information.

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

| Workspace | Location | Purpose |
| --- | --- | --- |
| Project | `.bonsai/projects/<project>/` | Product/architecture truth plus implementation execution memory |
| Map | `.bonsai/maps/<map>/` | Repository-local execution memory for creating and maintaining reusable source maps |

The directory structure defines the workspace type. Projects and maps do not need a separate manifest declaring what they are.

Every established workspace has:

```text
agent_plan.md
agent_state.md
```

`agent_plan.md` is the durable roadmap. `agent_state.md` holds the current resume state, readiness, blocker when present, and exact next action.

---

# Projects

For a normal single-project repository, use:

```text
.bonsai/projects/main/
```

`main` is the conventional default project name. Repositories may also contain multiple named projects:

```text
.bonsai/projects/
├── project-a/
├── project-b/
└── project-c/
```

If several plausible projects exist, identify the desired project explicitly at startup rather than relying on a persistent repository-wide "current project" setting. Active workspace selection belongs to the session.

## Creating Project Memory

Product and architecture design is usually best handled conversationally in a Web UI AI session.

Work through the design normally. When it is mature enough to preserve, use:

```text
$BONSAI_HOME/prompts/create_project.md
```

Paste that prompt into the design conversation. The workflow produces an extractable repository-root package containing `.bonsai/start.md` and the selected project memory.

A normal project begins with:

```text
.bonsai/projects/<project>/
├── requirements.md
├── architecture.md
├── agent_plan.md
└── agent_state.md
```

Additional requirements, architecture, project-level agent context, detailed plans, or an icebox are added only when useful.

After extracting the package into the repository, start implementation with the normal `start.md` prompt.

## Project Files

| File | Role | Ownership |
| --- | --- | --- |
| `requirements.md` | Product behavior, constraints, scope, accepted product decisions | Human-owned |
| `architecture.md` | Target implementation structure and architectural constraints | Human-owned |
| `agent_plan.md` | Project roadmap and phase progression | Agent-owned |
| `agent_state.md` | Current resume state and exact next action | Agent-owned |
| `agent_context.md` | Project-specific durable operational knowledge | Agent-owned |
| `plan/agent_plan_phase_<N>.md` | Detailed phase plan when warranted | Agent-owned |
| `requirements/requirements_<AREA>.md` | Deeper product truth when warranted | Human-owned |
| `architecture/architecture_<SUBSYSTEM>.md` | Deeper subsystem architecture when warranted | Human-owned |
| `icebox.md` | Human-selected deferred observations | Human-owned |

These files deliberately have different jobs. Requirements are not implementation notes, architecture is not a task list, state is not session history, and agent context is not a troubleshooting diary.

---

# What Happens at Startup

`start.md` resolves the active Bonsai Home, repository, and workspace, then hands control to the shared implementation workflow.

Bonsai loads only enough state to determine what should happen next. It does not automatically load every requirement, architecture file, code map, context file, plan, or skill.

A normal project startup identifies the current execution state, exact next step, readiness, and any active blocker or required human decision. Bonsai then stops at a human gate before substantive work unless the startup request explicitly authorizes the reconstructed exact next action.

This keeps routine startup cheap while preserving deliberate control over meaningful decisions.

---

# Planning and Execution

## Phase 1

A newly synthesized project begins implementation by drafting and reviewing its Phase 1 plan before substantive implementation starts.

The design session does not generate that detailed plan. Planning is the first implementation gate because the implementation agent has the source repository and current execution environment available to it.

## Later phase plans

Later detailed phase plans are created only when they add real value, for example when sequencing is too detailed for the roadmap, a durable contract deserves a separate review pass, or several meaningful gates must remain visible during execution.

A phase touching several files is not by itself a reason to create a detailed phase plan.

## Execution readiness

`agent_state.md` records the actual current execution condition. Common states include design required, planning required, awaiting review, blocked, ready to execute, and complete.

A plan existing does not mean implementation is authorized. `Ready to execute` means one safe exact action is established and no independent human-decision gate remains.

## Contract-first work

Some phases establish a durable API, schema, protocol, persistent format, or other integration surface that is worth reviewing before implementation underneath it.

When warranted, Bonsai can split the work into a contract pass, human review, and implementation pass. This is used only when the contract itself provides a useful review surface, not merely because work can be divided into two steps.

---

# Final Truth and Design Changes

Project requirements and architecture are human-owned final truth.

During implementation, Bonsai distinguishes between:

```text
None
Clarification
Revision
```

A revision changes approved behavior, constraints, architecture, or system boundaries. Bonsai stops before silently implementing that change.

For a meaningful design change, update the affected final-truth documents, review the new direction, then resume implementation from durable state. Chat history is not the authoritative record of the change.

---

# Developer Context and Agent Context

Bonsai separates intentionally supplied developer guidance from operational knowledge learned during work.

## Developer context

`developer_context.md` is human-owned reusable guidance such as coding preferences, testing philosophy, local conventions, SDK locations, runtime constraints, or AI working preferences.

Bonsai Home mode may use both:

```text
$BONSAI_HOME/developer_context.md
repo/.bonsai/developer_context.md
```

Repository-specific guidance is more specific when the two overlap. Developer context does not override approved project requirements or architecture.

## Agent context

`agent_context.md` is agent-owned durable operational memory. Examples include a reliable build command, a source checkout location, an environment-specific working rule, or which reusable code maps matter to a project.

Possible scopes are:

```text
$BONSAI_HOME/agent_context.md
repo/.bonsai/agent_context.md
repo/.bonsai/projects/<project>/agent_context.md
```

Use the narrowest scope that remains reusable.

Agent context stores the useful conclusion, not troubleshooting history. Active project or map identity does not belong there, and secrets must never be stored there.

---

# Out-of-Scope Discoveries

Implementation often exposes adjacent issues. Bonsai does not automatically turn those observations into authorized work.

The normal behavior is to notice the issue, continue the authorized work when safe, surface the observation at a natural boundary, and preserve it in `icebox.md` only when the human chooses to keep it.

The icebox is not an approved backlog. Preserving an observation does not authorize implementation.

---

# Code Maps

Code maps are reusable structural memory for source navigation. They help Bonsai avoid repeatedly rediscovering the same architecture, extension points, public surfaces, and cross-boundary relationships.

They are navigation aids, not project truth and not substitutes for source inspection. Actual source remains authoritative.

## Map workspace vs. generated code map

These are related but distinct:

```text
repo/.bonsai/maps/<map>/
    repository-local mapping execution memory

$BONSAI_HOME/maps/<map>/
    reusable generated source knowledge
```

A map workspace contains `agent_plan.md`, `agent_state.md`, optional human calibration, and optional detailed mapping plans. It makes substantial mapping work resumable.

The generated map is the reusable source-knowledge product. `code_map.md` is its normal entry document, with deeper subsystem or API maps created when justified by source discovery.

In Embedded mode, workspace and generated-map storage can physically overlap while retaining these distinct roles.

## Creating a code map

From a coding-agent session, the normal user intent is simply:

```text
Create a code map.
```

Or use **Manage Code Maps**.

When enough context is already known, Bonsai derives sensible defaults for the current source, map identity, local map workspace, and initial focus rather than asking you to restate information it already has.

For deliberate Web UI preparation or calibration before mapping, use:

```text
$BONSAI_HOME/prompts/create_map.md
```

That workflow prepares the repository-local map workspace and optional `map_calibration.md`. It does not generate the reusable code map itself. Mapping happens later against actual source.

## Map lifecycle

Bonsai supports four main lifecycle operations:

- **Create** establishes a map for source that has no suitable reusable map.
- **Extend** deliberately broadens useful coverage, such as another subsystem or cross-cutting concern.
- **Refresh** reconciles mapped knowledge after material source change while preserving the map's intended identity and coverage where possible.
- **Rebuild** intentionally replaces substantial generated representation and is used when refresh or extension is insufficient.

Mapping is executed as bounded, human-selected focuses. Once a focus is authorized, source discovery, ownership resolution, standard generated-map updates, validation, and state reconciliation normally form one complete mapping unit.

## Project associations

A project can record the reusable maps that are useful to it in project `agent_context.md`:

```text
Useful code maps:
- library-a
- library-b
```

Manage Code Maps can add or remove these associations. The association changes only project operational context; it does not modify the generated map.

## Source alignment

A generated map represents a particular source universe and snapshot. Bonsai should not knowingly reason from a map that represents an incompatible source version.

Map identity keeps enough source information to distinguish meaningful versions or revisions when necessary, without requiring every possible metadata field for every map.

---

# Multi-Repository Work

A project can use source and code maps from several repositories without copying those repositories' project memory into the consuming project.

Reusable generated maps live under the active Bonsai map store. Stable source locations and other operational facts can be preserved in appropriate agent context. Project requirements and architecture remain focused on the product rather than machine-specific source paths.

This allows Bonsai to accumulate reusable understanding of libraries, frameworks, and neighboring repositories while keeping each project's durable truth separate.

---

# Fresh Sessions and Handoffs

Fresh sessions are normal Bonsai usage.

At a natural boundary, Bonsai reconciles the active workspace so `agent_state.md` contains the exact next action and actual readiness. You can then continue in the current session, start a fresh session, review/change the next step, or exit for now.

Ordinary project resume:

```text
Read .bonsai/start.md and follow its instructions.
```

Ordinary map resume:

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

When Bonsai has already established one executable exact next action and you deliberately want a fresh session to perform it immediately, use:

```text
Read .bonsai/start.md, follow its instructions and execute the exact next step without stopping at the startup gate.
```

Append the project identity when needed for deterministic selection, and always append the map identity for map work.

The new session reconstructs canonical durable state before executing. The prompt does not carry forward rendered phase text, readiness, or next-step details from the old chat, and it never bypasses a newly discovered blocker or mandatory human gate.

Do not paste a previous chat summary into every fresh session. Durable Bonsai memory should carry what matters.

---

# Day-to-Day Project Workflow

A normal project rhythm is:

1. Design or revise product/architecture in a Web UI AI conversation when needed.
2. Preserve mature design with `prompts/create_project.md` or update the existing human-owned final truth.
3. Start the coding agent with `Read .bonsai/start.md and follow its instructions.`
4. Review the current state and any required planning or approval gate.
5. Execute one authorized bounded action.
6. Let Bonsai load deeper project truth, maps, context, or skills only when they become relevant.
7. Preserve reusable operational discoveries in agent context.
8. Stop before material final-truth revisions.
9. Preserve out-of-scope observations only when you choose to keep them.
10. Let Bonsai reconcile roadmap and resume state at natural boundaries.
11. Continue in the current session or resume later from durable state.

For mapping work, the same lifecycle applies at bounded mapping-unit boundaries rather than project phases.

---

# In One Picture

```text
                         coding-agent session
                                │
                                │
           Read .bonsai/start.md and follow its instructions.
                                │
                                ▼
                       repo/.bonsai/start.md
                                │
               ┌────────────────┼────────────────┐
               │                │                │
          Bonsai Home      repository home   active workspace
               │                │                │
               └────────────────┼────────────────┘
                                │
                                ▼
              $BONSAI_HOME/prompts/implementation.md
                                │
                                ▼
                       Bonsai workflow
                                │
          ┌─────────────────────┼─────────────────────┐
          │                     │                     │
    workspace memory       context as needed     maps as needed
          │                     │                     │
          └─────────────────────┼─────────────────────┘
                                │
                                ▼
                      authorized bounded work
```

The startup stays small. Durable memory does the remembering. Shared framework material stays in Bonsai Home, repository-specific memory stays with the repository, and reusable maps follow the source they describe.
