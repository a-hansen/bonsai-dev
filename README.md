# Bonsai

**Structured project memory and execution workflow for serious AI-assisted software development.**

AI coding tools are remarkably capable inside a session. The harder problem is keeping them useful across the life of a real software project.

Bonsai keeps the project knowledge that matters in structured Markdown close to the code, so a fresh AI session can reconstruct what it needs without relying on chat history or another hand-written recap.

*Already using Bonsai? See [What's New in 2.0](#whats-new-in-20).*

Bonsai helps you:

* keep AI context small, structured, and high-signal;
* start fresh AI sessions without having to explain the project again;
* move cleanly from Web AI design to IDE or CLI implementation;
* preserve the final intended system instead of letting implementation drift become the design;
* keep important product and architecture decisions under human control;
* review major contracts before implementation, with tests that demonstrate intended usage at important API, protocol, schema, and extension surfaces;
* automatically preserve useful environment and tooling discoveries across sessions;
* guide coding agents through large and multi-repository source trees with reusable code maps.

Bonsai is plain Markdown plus a small set of prompts, skills, and templates.

**No server. No database. No external memory service. No agent framework lock-in.**

It is a workflow built by a developer for developers who want AI to remain useful as a project grows, changes, and spans many sessions, not just for one good chat.

For the practical operating guide, see [`.bonsai/README.md`](.bonsai/README.md). For the authoritative Bonsai operating model, see [`.bonsai/specification.md`](.bonsai/specification.md).

---

## Install

The preferred installation is to clone this repository and use its `.bonsai` directory as your **Bonsai Home**.

A Bonsai Home is one shared Bonsai installation that can serve multiple source repositories.

```text
git clone https://github.com/a-hansen/bonsai-dev.git
```

Configure `BONSAI_HOME` to point to the clone's `.bonsai` directory:

```text
BONSAI_HOME=<path-to-bonsai-dev>/.bonsai
```

Make the variable available to the AI coding environments where you use Bonsai. The exact environment-variable setup is host-specific.

A single Bonsai Home can serve many repositories. Each source repository keeps its local bootstrap plus repository and project/map memory, while the shared Bonsai standard, reusable context, and generated code maps live in the cloned Bonsai repository.

To update Bonsai later:

```text
cd <path-to-bonsai-dev>
git pull
```

Embedded Bonsai is also supported when a repository needs to carry a complete standard locally. The shared Bonsai Home model is the normal installation path.

---

## Quick Start

### 1. Design the project

Product and architecture design often works best in a normal Web UI AI conversation. Discuss the project naturally before forcing it into documents.

When the design is mature enough to preserve, use:

```text
<bonsai-home>/prompts/create_project.md
```

Paste that prompt into the design conversation. Bonsai produces a repository-ready package containing `.bonsai/start.md` and durable project memory.

### 2. Add the project memory to the repository

For a typical project:

```text
repo/
└── .bonsai/
    ├── start.md
    └── projects/
        └── main/
            ├── requirements.md
            ├── architecture.md
            ├── agent_plan.md
            └── agent_state.md
```

`main` is the conventional default project name. A repository can also contain multiple named projects.

### 3. Start the coding agent

Open the repository in your coding agent and say:

```text
Read .bonsai/start.md and follow its instructions.
```

That is the normal Bonsai entry point.

For a named project:

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

Bonsai reconstructs where the project left off, determines whether it needs your input or can continue working, and loads deeper context only when the work needs it.

The startup prompt stays small because the durable memory does the remembering.

---

## The Core Model

A Bonsai project deliberately separates different kinds of truth and state.

| File               | Purpose                                                       | Ownership   |
| ------------------ | ------------------------------------------------------------- | ----------- |
| `requirements.md`  | Product behavior, constraints, workflows, scope               | Human-owned |
| `architecture.md`  | Intended system structure and durable architectural decisions | Human-owned |
| `agent_plan.md`    | Implementation roadmap and phase progression                  | Agent-owned |
| `agent_state.md`   | Where work stopped and what should happen next                | Agent-owned |
| `agent_context.md` | Durable project-specific operational knowledge, when useful   | Agent-owned |

Requirements are not a progress log. Architecture does not silently mutate to match whatever code was written. Execution state is not chat history. Operational context is not a troubleshooting diary.

Additional requirements, architecture, detailed plans, context, and an icebox are created only when useful. Bonsai grows structure as the project needs it rather than front-loading a documentation system.

---

## Fresh Sessions Are Normal

Long AI sessions accumulate stale decisions, abandoned approaches, debugging history, duplicated context, and assumptions that no longer matter.

Bonsai is designed around a different model:

> **Keep durable memory in the project. Start clean sessions whenever it is useful.**

`agent_state.md` records where work stopped and what should happen next. At a natural boundary, Bonsai can either continue in the current session or provide a fresh-session prompt that reconstructs the project state and continues work that has already been authorized.

A fresh session does not need a hand-written summary of the previous chat.

Moving to a new session does not bypass a decision, review, blocker, or design issue that still needs human input.

---

## Human Control Without Constant Babysitting

Bonsai is designed for meaningful human control, not approval of every internal implementation step.

The coding agent maintains implementation plans, execution state, and routine operational knowledge. The human retains authority over product and architecture decisions.

When implementation suggests that the agreed requirements or architecture need to change, Bonsai classifies the proposed change as:

* **None**: the current requirements and architecture already support the work;
* **Clarification**: the intended design is unchanged, but it should be stated more precisely;
* **Revision**: product behavior, architecture, constraints, or system boundaries need to change.

A revision stops for human approval before it becomes the new direction.

For durable contracts such as public APIs, schemas, protocols, persistent formats, or extension surfaces, Bonsai can also stop for review of the smallest useful contract before implementation proceeds beneath it. Tests can demonstrate the intended use of that contract before the rest of the implementation exists.

The goal is simple:

> **Let the agent manage execution. Keep the developer in control of what is being built and why.**

---

## Code Maps

Bonsai code maps help coding agents navigate large or unfamiliar codebases without rediscovering the same structure every session.

Project memory tells the agent what you are building, what architecture you are aiming for, and what work is active.

Code maps answer a different set of questions:

* Where does this behavior live?
* Which subsystem owns it?
* What callers or extension points matter?
* What source should be inspected before changing it?

Maps belong to the **source they describe**, not to whichever project first created them. That makes one map reusable across projects and especially useful when a project's source spans several repositories.

Actual source remains authoritative. Maps help the agent reach the right source faster rather than replacing source inspection.

Normal map operations include **Create**, **Extend**, **Refresh**, and **Rebuild**. Substantial mapping work can resume across sessions, while reusable generated map output lives in the active Bonsai map store.

To begin code mapping from a Bonsai session, use **Manage Code Maps** or ask Bonsai to create a code map for the current source.

For deliberate Web UI calibration before mapping, use:

```text
<bonsai-home>/prompts/create_map.md
```

See [`.bonsai/README.md`](.bonsai/README.md) for the full mapping workflow.

---

## Operational Memory

During real work, an agent often discovers useful facts that do not belong in requirements or architecture: the correct build command, a tooling limitation, a stable external source location, which code maps apply to a project, or some other environment-specific working rule.

When a discovery is durable and likely to matter again, Bonsai can preserve the useful part in `agent_context.md` at the appropriate scope.

Later sessions can reuse that knowledge instead of rediscovering it.

---

## Try Bonsai

### Bonsai develops Bonsai

Bonsai 2.0 is developed using Bonsai itself. Its project memory, implementation work, code maps, operational context, fresh-session continuation, and human review points use the same workflow described here.

### Bonsai Testbed

`bonsai-testbed-project.zip` is a deliberately small fixture for seeing the Bonsai workflow end to end: planning, human review, implementation, session boundaries, fresh-session continuation, operational discoveries, and later work.

After configuring `BONSAI_HOME`, extract the ZIP into a throwaway repository root and start with:

```text
Read .bonsai/start.md and follow its instructions.
```

### Task Tracker

The included Task Tracker is a fuller example of Bonsai project memory around a small application. It shows requirements, architecture, planning, and execution state together in a concrete project.

See [Task Tracker Example](.bonsai/projects/task-tracker/README.md).

Start it with:

```text
Read .bonsai/start.md and follow its instructions. Active project: task-tracker.
```

---

## Bonsai Is Not an Agent Framework

Bonsai does not replace your coding agent, IDE, `AGENTS.md`, repository instructions, coding standards, or development methodology.

It focuses on a narrower problem: **preserving the right project knowledge and carrying work cleanly across AI sessions.**

Use it with one assistant, an IDE coding agent, a CLI agent, or a larger agent system. The memory remains plain Markdown in the repository or Bonsai Home.

---

## Why Bonsai Exists

Bonsai grew out of the friction of using AI on real software projects.

The problem was not that the models could not write code. The problem was continuity.

One session contained important design decisions. Another discovered a better architecture. A coding agent made progress, but the next session needed a careful recap. Large repositories were rediscovered repeatedly. Old conversation context became more expensive and less useful at the same time.

The obvious answer seemed to be more context.

The better answer was **better-structured context**.

Bonsai keeps that structure in Markdown because Markdown is easy to inspect, diff, edit, version, copy, and hand to almost any AI tool.

The technology is deliberately boring.

**The workflow is the product.**

---

## What's New in 2.0

Bonsai 2.0 is a redesign of the 1.x workflow. The main changes are:

* **Reusable Bonsai Home** through `BONSAI_HOME`, allowing one cloned Bonsai installation to serve many repositories and provide shared resources such as code maps.
* **Fresh-session continuation** that reconstructs project state and automatically continues already-authorized work when no human decision is required.
* **Persistent environment knowledge** through `agent_context.md`, allowing Bonsai to retain useful repository and development-environment lessons instead of rediscovering them in later sessions.
* **Integrated reusable code maps** that give agents durable knowledge of unfamiliar codebases, with resumable mapping and create, extend, refresh, and rebuild workflows.
* **Standardized project memory** through `projects/main` for normal repositories, with named projects available when multiple independent bodies of work are needed.

Bonsai 2.0 is also self-hosting: continued Bonsai development uses Bonsai's own persistent project memory, code maps, operational context, and workflow.

For the complete change list and release notes, see the [GitHub release notes](https://github.com/a-hansen/bonsai-dev/releases/tag/v2.0.0).

---

## Documentation

* [Practical user guide](.bonsai/README.md)
* [Authoritative specification](.bonsai/specification.md)
* [Task Tracker example](.bonsai/projects/task-tracker/README.md)

---

## Name

A bonsai is not wild growth.

It is growth shaped deliberately over time.

AI can generate enormous amounts of motion. Bonsai is about turning that motion into deliberate, maintainable software.
