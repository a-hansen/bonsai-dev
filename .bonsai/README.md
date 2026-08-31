# Bonsai Project Workflow

This is the practical guide to using Bonsai 2.0.

For the authoritative Bonsai operating model, see:

```text
specification.md
```

Bonsai keeps durable project memory outside the chat session so that design and implementation can continue across fresh AI sessions without repeatedly reconstructing the project.

The day-to-day idea is simple:

1. design in a Web UI AI when design work is needed;
2. save durable project memory under the repository's `.bonsai/projects/`;
3. start coding-agent sessions with one small prompt;
4. let Bonsai load only the context needed for the current step;
5. preserve durable operational discoveries so the agent does not keep rediscovering them;
6. use reusable code maps when the useful source universe spans large or multiple repositories.

---

# The Prompt You Will Use Most

From a coding-agent session opened in a Bonsai-enabled repository, start with:

```text
Read .bonsai/start.md and follow its instructions.
```

That is the normal Bonsai implementation entry point.

For a named project, you may be explicit:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

You may also append another natural-language startup request:

```text
Read .bonsai/start.md and follow its instructions. Create a Bonsai Home.
```

```text
Read .bonsai/start.md and follow its instructions. Manage Code Maps.
```

The startup prompt should stay boring.

You do not need to summarize the previous session, remember the active phase, identify which skills to load, or reconstruct the next step.

Bonsai project memory carries that information.

---

# Getting Started

Bonsai begins with the Bonsai repository itself.

Clone the Bonsai repository so you have a complete copy of the standard files.

From there you can use Bonsai in either of two ways:

- **Embedded Bonsai** for a self-contained repository;
- **Bonsai Home** for a reusable developer-level Bonsai environment shared across repositories.

## Embedded Bonsai

Embedded Bonsai is the simplest starting point.

Copy the Bonsai `.bonsai` directory into the repository you want to use.

Conceptually:

```text
repo/
└── .bonsai/
    ├── start.md
    ├── specification.md
    ├── README.md
    ├── prompts/
    ├── skills/
    ├── templates/
    ├── developer_context.md      # Optional
    ├── agent_context.md          # Optional
    ├── maps/
    └── projects/
        └── main/
```

No `BONSAI_HOME` setting is required.

Open a coding-agent session in the repository and start with:

```text
Read .bonsai/start.md and follow its instructions.
```

Embedded Bonsai is sufficient for a standalone repository and remains a valid way to use Bonsai permanently.

## Bonsai Home

If you use Bonsai across multiple repositories, a reusable Bonsai Home avoids copying and maintaining the full Bonsai standard separately in each repository.

A Bonsai Home may contain:

```text
$BONSAI_HOME/
├── specification.md
├── README.md
├── prompts/
├── skills/
├── templates/
├── developer_context.md          # Optional
├── agent_context.md              # Optional
└── maps/
    ├── barcache/
    ├── tickerview/
    └── investment-app/
```

Repositories then keep only their local bootstrap and local memory:

```text
repo/
└── .bonsai/
    ├── start.md
    ├── developer_context.md      # Optional
    ├── agent_context.md          # Optional
    └── projects/
        └── main/
```

## Creating a Bonsai Home

Start from an embedded Bonsai repository.

First configure the environment variable:

```text
BONSAI_HOME=<path-you-want-to-use>
```

The path may identify a directory that does not exist yet.

Then start Bonsai normally and choose:

```text
See more options
    → Create Bonsai Home
```

or start directly with:

```text
Read .bonsai/start.md and follow its instructions. Create a Bonsai Home.
```

If `BONSAI_HOME` is not defined, Bonsai stops the Create Bonsai Home workflow and tells you to configure it first.

Bonsai does not treat a one-session path as a substitute and does not store the Bonsai Home location in agent context.

Once created, the Bonsai Home becomes the preferred standard whenever `BONSAI_HOME` is available.

The repository's local project memory remains in the repository.

You do not need to remove the embedded standard immediately. It can remain as a fallback while the reusable home is being validated.

---

# What `.bonsai/start.md` Does

`start.md` is a small bootstrap.

It does not contain the full Bonsai implementation workflow.

It establishes three things:

```text
Bonsai Home
Repository home
Active project
```

Then it loads:

```text
<bonsai-home>/prompts/implementation.md
```

The implementation prompt takes over from there.

The bootstrap intentionally does not load every requirement, architecture file, map, skill, developer context file, or agent context file.

Bonsai loads those only when the current work needs them.

---

# Projects

## Simple repository

A normal single-project repository uses:

```text
.bonsai/projects/main/
```

`main` is the conventional default Bonsai project name for this repository.

It is not a pointer.

With that layout, startup is simply:

```text
Read .bonsai/start.md and follow its instructions.
```

## Multiple projects in one repository

A larger repository may contain:

```text
.bonsai/projects/
    project-a/
    project-b/
    project-c/
```

You can start explicitly:

```text
Read .bonsai/start.md and follow its instructions. Active project: project-b.
```

If you do not specify a project:

1. `projects/main` wins when it exists;
2. otherwise Bonsai can cheaply list project directories;
3. if exactly one exists, it can use it;
4. if several exist, Bonsai asks you to choose.

Project selection belongs to the current session.

Switching projects does not rewrite a repository-wide current-project pointer.

## Managing projects from a session

Project management normally lives under:

```text
See more options
    → Manage Projects
```

Useful actions include:

```text
List Projects
Switch Project
Create Project
```

Switching changes only the current session.

Creating a project creates a place for project memory. It does not invent requirements or architecture.

If the project still needs design, Bonsai should tell you that design is required.

---

# Creating Project Memory

Bonsai design work is intended primarily for a Web UI AI conversation.

That keeps design conversational and avoids making the coding CLI the center of every Bonsai activity.

## 1. Discuss the design normally

Work through whatever matters:

- goals;
- users;
- workflows;
- constraints;
- architecture;
- tradeoffs;
- scope;
- implementation strategy.

Do not fill templates prematurely.

## 2. Create project memory when the design is mature

Use:

```text
$BONSAI_HOME/prompts/create_project_memory.md
```

or the equivalent path in embedded mode.

Paste its contents into the same Web UI conversation.

For a normal single-project repository, the workflow produces a zip rooted at:

```text
.bonsai/projects/main/
```

The normal contents are:

```text
.bonsai/projects/main/
├── requirements.md
├── architecture.md
├── agent_plan.md
└── agent_state.md
```

The zip may also include deeper requirements, deeper architecture, or a project-level `agent_context.md` when useful.

If you told the design AI that the project will use the `barcache` and `tickerview` code maps, that operational fact can be seeded into:

```text
.bonsai/projects/main/agent_context.md
```

For example:

```text
Useful code maps:
- barcache
- tickerview
```

That keeps code-map selection with project-specific operational memory instead of putting it into product requirements or architecture.

The implementation agent owns and maintains that file after project memory is created.

For a repository intentionally using named Bonsai projects, request that project name explicitly instead of `main`.

The project-memory workflow does not generate the detailed Phase 1 plan.

Phase 1 planning remains the first implementation gate.

## 3. Extract the zip into the repository

Extract the generated zip at the repository root.

For the normal case, you should now have:

```text
repo/.bonsai/projects/main/
```

## 4. Start implementation

Open the repository in your coding agent and use:

```text
Read .bonsai/start.md and follow its instructions.
```

---

# What the Project Files Mean

| File | Purpose | Ownership |
| --- | --- | --- |
| `requirements.md` | Product behavior, constraints, workflows, scope | Human-owned |
| `architecture.md` | Target implementation structure and durable architectural truth | Human-owned |
| `agent_plan.md` | Execution roadmap and phase status | Agent-owned |
| `agent_state.md` | Current resume state and exact next step | Agent-owned |
| `agent_context.md` | Project-specific operational context such as external source or code maps | Agent-owned |
| `plan/agent_plan_phase_<N>.md` | Detailed active phase plan when warranted | Agent-owned |
| `requirements/requirements_<AREA>.md` | Deep product-area truth when warranted | Human-owned |
| `architecture/architecture_<SUBSYSTEM>.md` | Deep subsystem architecture when warranted | Human-owned |
| `icebox.md` | Human-selected deferred observations | Human-owned |
| `.bonsai/developer_context.md` | Repository-specific durable developer guidance | Human-owned |
| `.bonsai/agent_context.md` | Repository-specific durable operational knowledge | Agent-owned |

The files have deliberately different jobs.

Requirements should not become implementation notes.

Architecture should not become a task list.

Agent state should not become session history.

Agent context should not become a troubleshooting diary.

---

# Developer Context

Developer context contains durable guidance intentionally supplied by the developer or team.

Examples include:

- coding preferences;
- testing philosophy;
- abstraction preferences;
- SDK locations;
- stable build constraints;
- runtime constraints;
- AI working preferences.

Bonsai Home mode may have both:

```text
$BONSAI_HOME/developer_context.md
repo/.bonsai/developer_context.md
```

The repository-specific context is more specific when the two overlap.

Developer context does not override approved project requirements or architecture.

---

# Agent Context

Agent context is durable operational memory learned or established for implementation.

Examples:

```text
Use the repository Gradle wrapper for this build.
```

```text
The matching tickerview source checkout is at <path>.
```

```text
Useful code maps:
- barcache
- tickerview
```

The purpose is to avoid repeated rediscovery.

Bonsai Home mode may use three scopes:

```text
$BONSAI_HOME/agent_context.md
repo/.bonsai/agent_context.md
repo/.bonsai/projects/<project>/agent_context.md
```

Use the narrowest scope that remains reusable.

Developer-level context is appropriate for operational facts shared across repositories.

Repository-level context is appropriate for facts shared by all Bonsai projects in one repository.

Project-level context is appropriate for facts that apply only to one Bonsai project, including which external code maps form part of that project's useful source universe.

The `create_project_memory.md` workflow may create the initial project-level `agent_context.md` from information you explicitly established during design. The implementation agent owns and maintains it afterward.

Do not store the active project there. Active project is current-session state.

Do not store secrets.

---

# What Happens at Implementation Startup

After `start.md` resolves Bonsai Home, repository home, and active project, the implementation workflow reads enough project state to determine what should happen next.

A normal startup should tell you:

- current phase;
- current execution mode;
- execution readiness;
- exact next step;
- active blocker when one exists;
- anticipated final-truth impact.

Then Bonsai stops at a human gate before substantive execution.

The normal choices are equivalent to:

1. proceed with the identified next step;
2. correct or discuss the next step;
3. stop here.

Secondary workflows remain under:

```text
See more options
```

Depending on context, that submenu may include **Manage Projects**, **Manage Code Maps**, **Create Bonsai Home**, and **Dry Run**.

---

# Phase 1 and Later Phase Plans

Phase 1 is intentionally special.

Every newly synthesized Bonsai project begins implementation by drafting and reviewing its Phase 1 plan before substantive implementation starts.

The initial design session does not generate that detailed plan.

Later phase plans are created only when they are genuinely useful.

Good reasons include:

- sequencing too detailed for `agent_plan.md`;
- contract-first two-pass execution;
- several meaningful review gates;
- constraints that need to stay visible during execution.

A phase plan should not exist merely because a phase touches several files.

---

# Execution Readiness

`agent_state.md` makes readiness explicit.

| Value | Meaning |
| --- | --- |
| `Design required` | Product or architecture decisions still need to be resolved. |
| `Phase planning required` | Durable design exists, but execution planning is incomplete. |
| `Awaiting human review` | A required plan, contract, or other artifact is waiting for approval. |
| `Ready to execute` | The exact next step has an approved basis and no required gate remains. |
| `Blocked` | A concrete blocker prevents safe execution. |
| `Complete` | No further implementation work is currently required. |

A plan existing does not mean implementation is authorized.

---

# Final Truth and Design Changes

Requirements and architecture are normal human-owned final truth.

During implementation, Bonsai classifies proposed or discovered changes as:

```text
None
Clarification
Revision
```

A revision changes product behavior, constraints, architecture, or system boundaries.

Bonsai must stop before silently implementing a revision.

For significant design changes, return to a Web UI design conversation when that is the more natural place to reason about the change.

Update the affected final-truth documents, review them, then resume implementation normally.

Do not rely on chat history as the durable record of the new direction.

---

# Contract-First Two-Pass Work

Some phases establish a durable contract that deserves review before implementation underneath it.

Examples include:

- public APIs;
- schemas;
- persistent formats;
- protocols;
- extension contracts;
- durable integration surfaces.

When warranted, Bonsai uses:

```text
Pass A: Contract
    ↓
Human review
    ↓
Pass B: Implementation
```

Pass A should produce the smallest useful native review surface.

That may be source-level skeletons, schemas, examples, or behavior-focused tests.

Do not manufacture abstractions merely to create a contract gate.

Single-pass work is not called Pass B.

---

# Dry Runs

Dry runs are optional read-only execution previews.

They are useful when a step carries unusual risk or ambiguity.

Dry Run normally lives under:

```text
See more options
```

It is not a routine mandatory step.

---

# Out-of-Scope Discoveries

Implementation often exposes adjacent issues.

Bonsai's default behavior is:

1. notice the issue;
2. do not fix it automatically;
3. continue the authorized work when safe;
4. surface meaningful observations at the next natural gate;
5. preserve an observation in `icebox.md` only if the human chooses to keep it.

The icebox is not an approved backlog.

Approval to preserve an item is not approval to implement it.

---

# Code Maps

Code maps help Bonsai navigate source without repeatedly rediscovering the entire structure.

They do not replace source inspection.

They are not project truth.

Maps are named for the source they represent.

Bonsai Home mode:

```text
$BONSAI_HOME/maps/
    barcache/
    tickerview/
    investment-app/
```

Embedded mode:

```text
repo/.bonsai/maps/
    investment-app/
```


## One source, one reusable map

A code map describes source, not a Bonsai project.

If several Bonsai projects live in one large repository and all reason over the same source universe, they can use the same repository map.

Do not create duplicate maps merely because project-memory directories differ.

---

# Creating a Map When Project Memory Exists

Suppose `barcache` already has Bonsai project memory.

Open a coding-agent session in the `barcache` repository:

```text
Read .bonsai/start.md and follow its instructions.
```

Then:

```text
See more options
    → Manage Code Maps
        → Create Code Map
```

Bonsai should use:

```text
actual barcache source
+
relevant barcache requirements
+
relevant barcache architecture
+
other useful barcache project knowledge
```

to create a map that emphasizes concepts and boundaries Bonsai already understands.

The source remains authoritative.

With an Bonsai Home, the resulting map goes to:

```text
$BONSAI_HOME/maps/barcache/
```

The fact that the mapping session ran inside the `barcache` repository does not make the map repository-local.

---

# Creating a Map Without Bonsai Project Memory

You can still map an external repository that has never used Bonsai.

This preserves the original Bonsai mapping workflow.

## Optional Web UI calibration

Use:

```text
$BONSAI_HOME/prompts/create_map_repo.md
```

in a Web UI AI conversation.

Describe what matters in the repository:

- important concepts;
- representative source;
- entry points;
- extension points;
- areas that deserve deeper mapping;
- misleading or low-value areas;
- things the mapper can treat lightly.

The mapping session produces an optional:

```text
map_repo.md
```

Save it with the map configuration, for example:

```text
$BONSAI_HOME/maps/<source-name>/map_repo.md
```

Then create the map from a coding-agent session operating against that source.

Bonsai uses:

```text
actual source
+
optional map_repo.md
```

No Bonsai project memory is required.

---

# Project Memory and `map_repo.md` Can Work Together

They solve different problems.

Project memory says what the software is intended to be and which concepts matter to the project.

`map_repo.md` says how you want this particular source mapped.

If both exist, Bonsai may use both.

For example, `tickerview` may have strong project memory, while you still use a Web UI mapping session to tell Bonsai to emphasize its public chart API and treat example code lightly.

---

# Multi-Repository Example

Consider an `investment-app` that uses both external repositories:

```text
investment-app
    → barcache
    → tickerview
```

You have three repositories.

`barcache` and `tickerview` already exist.

`investment-app` is the consuming project.

With an Bonsai Home:

```text
$BONSAI_HOME/maps/
    barcache/
    tickerview/
    investment-app/
```

When creating `investment-app` project memory, you can tell the Web UI design conversation that the project uses the `barcache` and `tickerview` code maps. `create_project_memory.md` can preserve that in:

```text
.bonsai/projects/main/agent_context.md
```

so implementation sessions do not need to choose from the entire map store.

## 1. Map `barcache`

Open Bonsai from the `barcache` repository.

Create the code map through **Manage Code Maps**.

If `barcache` has project memory, Bonsai uses it.

The map is stored at:

```text
$BONSAI_HOME/maps/barcache/
```

## 2. Map `tickerview`

Open Bonsai from the `tickerview` repository.

Create its map.

If the `barcache` map or source is relevant while understanding `tickerview`, Bonsai may use that relationship.

The result is:

```text
$BONSAI_HOME/maps/tickerview/
```

## 3. Work on `investment-app`

Create or synthesize its Bonsai project memory.

Start implementation normally:

```text
Read .bonsai/start.md and follow its instructions.
```

When deeper understanding of dependencies is needed, Bonsai can use the reusable `tickerview` and `barcache` maps.

If it discovers stable source locations or other cross-repository working facts, it should preserve those facts in the appropriate agent context rather than rediscovering them next session.

---

# Map and Source Version Alignment

A map represents a particular source snapshot.

Bonsai should not silently use a map built for one incompatible source version while reasoning from another.

Map identity may eventually include:

- source name;
- version;
- Git revision;
- artifact coordinates;
- source type;
- source location.

The exact metadata format should stay small until real usage proves what is necessary.

For released dependencies, matching source artifacts may be safer than an unrelated current development checkout.

For active cross-repository work, a matching repository revision may be more useful.

---

# Starting Fresh Sessions

Fresh sessions are normal Bonsai usage.

At a natural handoff, Bonsai records the exact next step and execution readiness in project memory.

Then a fresh session starts with the same small instruction:

```text
Read .bonsai/start.md and follow its instructions.
```

Do not paste the previous chat summary into the new session unless there is a specific reason to do so.

The durable memory should carry what matters.

---

# Optional Helper Scripts

Shell scripts may exist for convenience, but they are optional.

Examples might include:

```text
bonsai.sh init
bonsai.sh --list
bonsai.sh <project>
```

A helper can make it easy to:

- copy or create `.bonsai/start.md` in a new repository;
- create `.bonsai/projects/main/`;
- list project directories;
- launch a coding CLI with an initial Bonsai prompt.

Once a Bonsai AI session is running, routine capabilities such as project listing, switching, project creation, and map management should remain available through the Bonsai menu system.

The scripts are helpers, not the workflow.

---

# Enabling Bonsai in a New Repository

A repository becomes Bonsai-enabled when it has:

```text
.bonsai/start.md
```

For a simple new project, a convenient initial structure is:

```text
.bonsai/
    start.md
    projects/
        main/
```

You can create this manually from the Bonsai distribution or use an optional helper.

Then design the project in the Web UI and place the generated project memory under `projects/main/`.

After that, normal implementation startup is always:

```text
Read .bonsai/start.md and follow its instructions.
```

---

# Typical Day-to-Day Workflow

A normal working rhythm is:

1. Start a coding-agent session in the repository.
2. Say `Read .bonsai/start.md and follow its instructions.`
3. Review Bonsai's current-state summary and startup gate.
4. Proceed with one authorized bounded step.
5. Let Bonsai load deep project truth, maps, context, or skills only when they become relevant.
6. Let the agent preserve durable operational discoveries in agent context.
7. Review contract gates when a durable contract deserves separate review.
8. Stop before material final-truth revisions.
9. Decide which out-of-scope observations, if any, belong in the icebox.
10. Let Bonsai reconcile `agent_plan.md` and `agent_state.md`.
11. Continue in the current session or open a fresh one.
12. Start the next session with the exact same `start.md` instruction.

For multi-repository work, reusable maps and global agent context allow Bonsai to accumulate source knowledge without copying unrelated project memory between repositories.

---

# The Model in One Picture

```text
                           AI coding session
                                  │
                                  │
             Read .bonsai/start.md and follow its instructions.
                                  │
                                  ▼
                         repo/.bonsai/start.md
                                  │
                 ┌────────────────┼────────────────┐
                 │                │                │
            Bonsai Home      repository home   active project
                 │                │                │
                 └────────────────┼────────────────┘
                                  │
                                  ▼
                 <bonsai-home>/prompts/implementation.md
                                  │
                                  ▼
                        normal Bonsai workflow
                                  │
          ┌───────────────────────┼────────────────────────┐
          │                       │                        │
     project memory          context as needed        maps as needed
          │                       │                        │
          └───────────────────────┼────────────────────────┘
                                  │
                                  ▼
                      authorized implementation
```

That is the intended Bonsai 2.0 user experience.

The startup stays small.

The durable memory does the remembering.

The standard lives in one place when you want reuse.

Local context stays local.

Maps follow the source they represent.

And multi-repository work becomes an extension of the same workflow rather than a separate Bonsai mode.
