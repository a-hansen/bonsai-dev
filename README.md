# Bonsai

**Structured project memory and execution workflow for AI-assisted software development.**

Version: **v2.0.0**

Bonsai helps AI stay useful across the life of a real software project, not just for one chat session.

It keeps durable project truth, execution state, operational knowledge, and source-navigation memory in plain Markdown close to the code. A new AI session can reconstruct what matters without depending on chat history or requiring another hand-written recap.

Bonsai helps you:

- preserve product and architecture truth outside chat history;
- start fresh AI sessions without re-explaining the project;
- separate human-owned design truth from agent-maintained execution state;
- carry one exact next action safely across session boundaries;
- preserve useful environment and tooling discoveries;
- navigate large and multi-repository source trees with reusable code maps;
- keep meaningful human approval gates without approving every file edit.

Bonsai is plain Markdown plus a small set of prompts, skills, and templates.

**No server. No database. No external memory service. No agent framework lock-in.**

For the complete operating guide, see [`.bonsai/README.md`](.bonsai/README.md). For the authoritative Bonsai operating model, see [`.bonsai/specification.md`](.bonsai/specification.md).

---

## What's New in 2.0

Bonsai 2.0 is a redesign of the 1.x workflow. The main changes are:

* **Reusable Bonsai Home** through `BONSAI_HOME`, allowing one cloned Bonsai installation to serve many repositories and provide shared resources such as code maps.
* **Fresh-session continuation** that reconstructs project state and automatically continues the next authorized step when no human decision is required.
* **Persistent environment knowledge** through `agent_context.md`, allowing Bonsai to retain useful repository and development-environment lessons instead of rediscovering them in later sessions.
* **Integrated reusable code maps** that give agents durable knowledge of unfamiliar codebases, with resumable mapping and create, extend, refresh, and rebuild workflows.
* **Lower context overhead** through lazy loading, so Bonsai loads detailed workflows and supporting material only when they are actually needed.
* **Standardized project memory** through `projects/main` for normal repositories, with named projects available when multiple independent bodies of work are needed.
* **Stronger human control across sessions**, preserving approval gates, final-truth ownership, and explicitly authorized work even when execution continues in a fresh session.

Bonsai 2.0 is also self-hosting: continued Bonsai development uses Bonsai's own persistent project memory, code maps, operational context, and workflow.

---

## Install

The preferred installation is to clone this repository and use its `.bonsai` directory as your **Bonsai Home**.

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

### 2. Extract the project memory

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

Bonsai reconstructs the current workspace state, determines the applicable gate or exact next action, and loads deeper context only when the work needs it.

The startup prompt stays small because the durable memory does the remembering.

---

## The Core Model

A Bonsai project deliberately separates different kinds of truth and state.

| File | Purpose | Ownership |
| --- | --- | --- |
| `requirements.md` | Product behavior, constraints, workflows, scope | Human-owned |
| `architecture.md` | Intended system structure and durable architectural decisions | Human-owned |
| `agent_plan.md` | Implementation roadmap and phase progression | Agent-owned |
| `agent_state.md` | Current resume state and exact next action | Agent-owned |
| `agent_context.md` | Durable project-specific operational knowledge, when useful | Agent-owned |

Requirements are not a progress log. Architecture does not silently mutate to match whatever code was written. Execution state is not chat history. Operational context is not a troubleshooting diary.

Additional requirements, architecture, detailed plans, context, and an icebox are created only when useful. Bonsai is intended to grow structure as the project needs it rather than front-loading a documentation system.

---

## Fresh Sessions Are Normal

Long AI sessions accumulate stale decisions, abandoned approaches, debugging history, duplicated context, and assumptions that no longer matter.

Bonsai is designed around a different model:

> **Keep durable memory in the project. Start clean sessions whenever it is useful.**

`agent_state.md` carries the current execution condition and exact next action. At a natural boundary, Bonsai can either continue in the current session or provide a fresh-session prompt that reconstructs canonical state and executes the already-established next action.

A fresh session does not need a hand-written summary of the previous chat.

Approval, review, blocker, contract, and design gates are not bypassed merely because execution moves to a new session.

---

## Human Control Without Constant Babysitting

Bonsai is designed for meaningful human control, not approval of every internal implementation step.

The coding agent maintains execution memory and routine operational knowledge. The human retains authority over product and architecture truth.

During implementation, proposed changes to project final truth are classified as:

- **None**: the current requirements and architecture already support the work;
- **Clarification**: the intended design is unchanged, but final truth should be stated more precisely;
- **Revision**: product behavior, architecture, constraints, or system boundaries need to change.

A revision stops for human approval before it becomes the new direction.

For durable contracts such as public APIs, schemas, protocols, persistent formats, or extension surfaces, Bonsai can also use contract-first execution: review the smallest useful contract surface first, then implement beneath the approved contract.

The goal is simple:

> **Let the agent manage execution. Keep the developer in control of what is being built and why.**

---

## Code Maps

Project memory answers questions such as:

- What are we building?
- What architecture are we aiming for?
- What work is active?
- What happens next?

Large codebases add another recurring problem:

- Where is the relevant code?
- Which subsystem owns this behavior?
- What callers or extension points matter?
- What should the agent inspect before changing it?

Bonsai code maps preserve selective structural knowledge for source navigation.

Maps belong to the **source they describe**, not to whichever project first created them. That makes one map reusable across projects and especially useful when a project's source universe spans several repositories.

Actual source remains authoritative. Maps help the agent reach the right source faster rather than replacing source inspection.

Normal map operations include **Create**, **Extend**, **Refresh**, and **Rebuild**. Substantial mapping work uses repository-local resumable map memory while reusable generated map output lives in the active Bonsai map store.

To begin code mapping from a Bonsai session, use **Manage Code Maps** or ask Bonsai to create a code map for the current source. For deliberate Web UI calibration before mapping, use:

```text
<bonsai-home>/prompts/create_map.md
```

See [`.bonsai/README.md`](.bonsai/README.md) for the full mapping workflow.

---

## Operational Memory

Not every durable discovery belongs in requirements or architecture.

During real work an agent may establish facts such as:

- the correct build command in the current environment;
- a stable external source location;
- which reusable code maps matter to a project;
- a filesystem or tooling limitation;
- another environment-specific working rule.

When a discovery is durable, actionable, sufficiently supported, and likely to matter again, Bonsai can preserve the useful rule in `agent_context.md` at the appropriate developer, repository, or project scope.

That turns repeated rediscovery into reusable operational knowledge without polluting product truth.

---

## Try Bonsai

This repository includes two examples with different purposes.

### Bonsai Testbed

`bonsai-testbed-project.zip` is a deliberately small fixture for observing the Bonsai workflow itself: startup, Phase 1 planning, gates, execution state, fresh-session continuation, operational context, and later-phase progression.

After configuring `BONSAI_HOME`, extract the ZIP into a throwaway repository root and start with:

```text
Read .bonsai/start.md and follow its instructions.
```

### Task Tracker

The included Task Tracker is a fuller example of Bonsai project memory around a small application. It shows requirements, architecture, planning, and execution state for a concrete application that has not yet been implemented.

See [Task Tracker Example](.bonsai/projects/task-tracker/README.md).

Start it with:

```text
Read .bonsai/start.md and follow its instructions. Active project: task-tracker.
```

---

## Bonsai Is Not an Agent Framework

Bonsai does not replace your coding agent, IDE, `AGENTS.md`, repository instructions, coding standards, or development methodology.

It focuses on a narrower problem: **durable structured memory and controlled execution continuity across AI sessions**.

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

## Documentation

- [Practical user guide](.bonsai/README.md)
- [Authoritative specification](.bonsai/specification.md)
- [Task Tracker example](.bonsai/projects/task-tracker/README.md)

---

## Name

A bonsai is not wild growth.

It is growth shaped deliberately over time.

AI can generate enormous amounts of motion. Bonsai is about turning that motion into deliberate, maintainable software.
