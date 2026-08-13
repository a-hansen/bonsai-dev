# Bonsai

Repo-local project memory for AI-assisted software development.

Current release: **v1.4.0**

Bonsai is a set of Markdown files and prompts that keeps project context outside the AI session.

The basic idea is simple:

* keep requirements, architecture, planning, and current execution state separate
* let coding agents maintain the operational parts
* keep product and architecture decisions human-owned
* use fresh AI sessions without having to explain the project again
* load detailed context only when it is needed

There is no server, database, or external memory service. Bonsai lives in the repository under:

```text
.bonsai/
```

For the full workflow, see [.bonsai/README.md](.bonsai/README.md).

---

## Repository Layout

```text
bonsai-dev/
├── README.md
└── .bonsai/
    ├── README.md
    ├── design_session.md
    ├── implementation_prompt.md
    ├── developer_context.example.md
    ├── skills/
    │   ├── phase_execution.md
    │   ├── dry_run.md
    │   ├── handoff.md
    │   └── final_truth_update.md
    ├── maps/
    │   └── ...
    └── projects/
        └── task-tracker/
            └── ...
```

The `.bonsai/` directory is intended to be copied into a software repository.

---

# How It Works

A Bonsai project normally starts with four files:

```text
.bonsai/projects/<project>/
├── requirements.md
├── architecture.md
├── plan.md
└── state.md
```

They have different jobs.

| File | Purpose | Ownership |
| --- | --- | --- |
| `requirements.md` | Product behavior and constraints | Human-owned |
| `architecture.md` | Intended system architecture | Human-owned |
| `plan.md` | Implementation roadmap | Agent-maintained |
| `state.md` | Current execution state and exact next step | Agent-maintained |

Larger projects can add more detailed files when needed:

```text
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
plan/plan_phase_<N>.md
```

There is also an optional `icebox.md` for out-of-scope observations the human explicitly decides are worth preserving.

The goal is to keep each file focused. `state.md`, in particular, is current state rather than a running history.

---

# Design Workflow

Bonsai assumes that early design work often happens in a Web AI conversation.

Discuss the project normally:

* requirements
* workflows
* constraints
* architecture
* tradeoffs
* implementation phases

When the design is mature enough to preserve, paste:

```text
.bonsai/design_session.md
```

into that conversation.

The AI synthesizes the discussion into the Bonsai project-memory files.

A small project will usually produce only:

```text
requirements.md
architecture.md
plan.md
state.md
```

More detailed documents are created only when there is enough complexity to justify them.

---

# Implementation Workflow

Start an IDE or CLI coding-agent session with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

The agent reads the project memory, determines the current execution state, identifies the exact next step, and stops before making changes.

A normal startup tells you:

* current phase
* current pass
* execution mode
* whether planning is actually complete
* exact next step
* blockers
* whether the proposed work affects approved requirements or architecture

The human then decides whether to proceed.

Bonsai deliberately separates **planning complete** from **ready to implement**. A phase plan can be fully drafted but still require human review before execution.

---

# Human-Owned Truth

`requirements.md` and `architecture.md` describe the intended system.

Coding agents do not silently rewrite them to match whatever happened during implementation.

When implementation reveals a mismatch, Bonsai classifies it as:

* **None**: current requirements and architecture already cover the work
* **Clarification**: the intended design is unchanged, but the documentation should be more precise
* **Revision**: product behavior, architecture, constraints, or system boundaries need to change

Revisions require human approval before implementation continues.

`plan.md` and `state.md` are different. They are execution memory and are expected to change as the work progresses.

---

# State Is a Baton Pass, Not a Log

`state.md` is intentionally small.

It records things such as:

* current phase
* active phase plan
* current pass
* execution readiness
* current objective
* blockers
* exact next step
* resume-critical files

Stale information should be removed rather than accumulated.

A useful rule is:

> If removing something from `state.md` would not change what the next coding session does, it probably does not belong there.

This makes new sessions cheap to orient and reduces the amount of old implementation noise carried forward.

For a normal single-pass phase, `state.md` uses:

```text
Current Phase Pass: Single-pass Implementation
```

`Pass A (Contract)`, `Contract Review`, and `Pass B (Implementation)` are reserved for actual two-pass
contract-first phases.

---

# Phase Plans and Contract-First Work

Most implementation can use a normal single-pass workflow.

Bonsai also supports two-pass contract-first work when a phase establishes or materially changes a durable contract that independently merits human approval before implementation, for example:

* an external API
* a protocol
* a schema
* a persistent format
* an extension or plugin contract
* another durable integration surface

An already approved contract does not require a redundant Bonsai contract gate merely because a phase implements it.
Large phases, multiple modules, internal abstractions, tests, or implementation dependency changes are not by
themselves reasons to create Pass A and Pass B.

Pass A produces the reviewable contract.

The human approves it.

Pass B implements it.

Contract-first does **not** mean Bonsai expects interfaces, builders, dependency-injection layers, or other abstractions. Those are implementation choices governed by the project's architecture, conventions, developer context, and other skills.

The point of the gate is to review an important contract before a large amount of code depends on it.

---

# Dry Runs

Dry runs are available when a read-only implementation preview would be useful.

They can show:

* expected touch points
* intended result
* planned checks
* likely scope concerns

They are optional and are not part of every normal execution gate.

See:

```text
.bonsai/skills/dry_run.md
```

---

# Out-of-Scope Discoveries

Coding agents regularly notice things unrelated to the current task:

* bugs
* technical debt
* refactoring opportunities
* missing tests
* documentation gaps
* future improvements

Bonsai prevents those from silently expanding the current scope.

The agent can tell the human that out-of-scope observations are available for review.

Only observations the human decides are worth retaining are written to:

```text
icebox.md
```

The icebox is not an approved backlog. If observation review or an immediate correction is invoked from a
handoff, Bonsai returns to that handoff afterward unless the action creates a new required gate.

At handoff, the actual next step and execution readiness are shown as standalone fields so they are not buried
inside completion prose. Menu choices name the concrete next action.

---

# Fresh Sessions

Bonsai is designed to work well with frequent clean AI sessions.

The project memory lives in the repository, so the conversation itself does not need to carry the full history.

When a clean session makes sense, start one yourself with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

That prompt intentionally contains no handoff summary.

The new agent reads `state.md` and the other Bonsai files to determine what happens next.

Bonsai does not attempt to terminate, clear, or create AI sessions. Session control remains with the human.

---

# Developer Context

Optional developer-specific guidance can live in:

```text
.bonsai/developer_context.md
```

Start from:

```text
.bonsai/developer_context.example.md
```

This is a good place for things such as:

* coding preferences
* testing preferences
* local SDK paths
* build commands
* machine-specific setup
* recurring AI instructions

These are deliberately separate from Bonsai project truth.

Bonsai is meant to work with different developers, coding styles, and external skills rather than defining one preferred engineering style itself.

---

# Code Maps

Bonsai includes a repository mapping system for larger or unfamiliar codebases.

The top-level map is:

```text
.bonsai/maps/code_map.md
```

More detailed maps can provide navigation into specific subsystems.

The goal is not to replace source inspection. It is to help the coding agent find the right source faster and avoid repeatedly rediscovering important repository structure.

See [.bonsai/maps/README.md](.bonsai/maps/README.md) for the mapping workflow.

---

# Try the Example

The repository includes:

```text
.bonsai/projects/task-tracker/
```

The Task Tracker example can be used either to walk through a design session or to inspect an already-generated Bonsai project.

See [.bonsai/projects/task-tracker/README.md](.bonsai/projects/task-tracker/README.md).

To start an implementation session against the included project:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker
```

---

# Using Bonsai in Your Own Repository

Copy:

```text
.bonsai/
```

into the repository.

Create:

```text
.bonsai/projects/<project>/
```

Design the project, use `design_session.md` to generate the initial memory, save those files under the project directory, and start implementation with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

See [.bonsai/README.md](.bonsai/README.md) for the detailed workflow.

---

# Status

Bonsai is a workflow I use and continue to refine through real AI-assisted development.

The pieces are plain Markdown on purpose. The useful part is the separation of responsibilities and the discipline around keeping project memory current, small, and reviewable.
