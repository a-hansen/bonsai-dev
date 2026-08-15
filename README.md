# Bonsai

**Structured project memory for serious AI-assisted software development.**

Current release: **v1.4.0**

Bonsai is a repo-local memory system and workflow for developers who use AI to design, build, and evolve software across many sessions.

It helps you:

* keep AI context small, structured, and high-signal
* start fresh AI sessions without having to explain the project again
* keep requirements, architecture, planning, and current execution state separate
* keep product and architecture decisions human-owned while letting coding agents maintain execution state
* review major contracts before implementation, with tests that demonstrate intended usage at important API, protocol, schema, and extension surfaces
* move cleanly from Web AI design to IDE or CLI implementation
* preserve the final intended system instead of letting implementation drift become the design
* guide coding agents through large repositories with layered code maps

Bonsai is plain Markdown plus a small set of prompts.

No server.  
No database.  
No external memory service.  
No framework lock-in.

It is a workflow built by a developer for developers who want AI to be useful over the life of a real project, not just for one good chat.

For the complete Bonsai workflow and reference documentation, see [.bonsai/README.md](.bonsai/README.md).

---

# Try Bonsai First

The repository includes a small Task Tracker project so you can try the workflow before adapting it to your own codebase.

See:

[Task Tracker Example](.bonsai/projects/task-tracker/README.md)

You can use it in two ways:

* **Start from design:** use the supplied Task Tracker design prompt, choose your own language and tools, and let Bonsai turn the design session into project memory.
* **Jump directly into implementation:** use the included reference project memory and start a coding-agent session against it.

To start the included project:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker
```

That gives you the quickest look at what day-to-day Bonsai usage feels like.

---

# The Prompt You Will Use a Lot

For implementation work, this is the normal starting prompt:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

That prompt is intentionally simple.

You do not need to reconstruct the right instructions every time you open a coding session. You do not need to summarize the previous session. You do not need to remember which project files the agent should read first.

The prompt tells the coding agent to load Bonsai, inspect the active project memory, determine the current state and exact next step, and stop at the appropriate human gate before substantive execution.

In practice, this is one of the main conveniences of Bonsai: open the repository README in your IDE, copy the prompt, replace `<project>`, and start a clean session.

The project memory carries the context. The startup prompt stays boring.

---

# Repository Layout

Bonsai lives under:

```text
.bonsai/
```

This repository is laid out the same way Bonsai is intended to live inside a real software project:

```text
bonsai-dev/
├── README.md
└── .bonsai/
    ├── README.md
    ├── design_session.md
    ├── implementation_prompt.md
    ├── developer_context.example.md
    ├── skills/
    │   └── ...
    ├── maps/
    │   └── ...
    └── projects/
        └── task-tracker/
            └── ...
```

The repo-root `README.md` is the public project landing page.

`.bonsai/README.md` contains the detailed workflow.

The `.bonsai/` directory is the framework you copy into another repository.

---

# How Bonsai Works

A Bonsai project normally begins with four memory files:

```text
.bonsai/projects/<project>/
├── requirements.md
├── architecture.md
├── plan.md
└── state.md
```

They have deliberately different jobs.

| File | Purpose | Ownership |
| --- | --- | --- |
| `requirements.md` | Product behavior and constraints | Human-owned |
| `architecture.md` | Intended system architecture | Human-owned |
| `plan.md` | Implementation roadmap | Agent-maintained |
| `state.md` | Current execution state and exact next step | Agent-maintained |

That separation is the core of Bonsai.

Requirements should not turn into a progress log. Architecture should not quietly mutate to match whatever code happened to get written. State should not become a history of every completed task.

Each kind of memory has a place.

Larger projects can add deeper files only when they are useful:

```text
requirements/requirements_<AREA>.md
architecture/architecture_<SUBSYSTEM>.md
plan/plan_phase_<N>.md
```

The top-level files stay orienting. Detailed context is loaded only when the current work needs it.

---

# Design in One Session, Implement Across Many

Bonsai assumes that product and architecture work often begin in a Web AI conversation.

Discuss the project normally:

* what you are building
* requirements and workflows
* constraints
* architecture
* tradeoffs
* implementation strategy

When the design is mature enough to preserve, paste the contents of:

```text
.bonsai/design_session.md
```

into that same conversation.

The AI synthesizes the discussion into durable Bonsai project memory.

A small project usually starts with only:

```text
requirements.md
architecture.md
plan.md
state.md
```

The first implementation phase can also receive a detailed phase plan when one is warranted, giving you a concrete review gate before coding begins.

Save the generated files under:

```text
.bonsai/projects/<project>/
```

Then move to your coding tool and start with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

That is the bridge between design AI and implementation AI.

---

# Fresh Sessions Are a Feature

Long AI sessions tend to collect noise:

* stale decisions
* abandoned approaches
* old debugging branches
* duplicated context
* assumptions that were true three hours ago but are no longer true

Bonsai is designed around a different model:

> **Keep the durable memory in the repository. Start clean sessions whenever it is useful.**

`state.md` acts as the baton pass.

It records the current execution state, blockers, exact next step, and the small amount of resume-critical information the next coding session needs.

The new session reads the project memory rather than depending on a hand-written recap from the old conversation.

You can still continue in the same session when that is convenient. Bonsai simply makes a fresh one cheap.

---

# Keep Final Truth Separate from Execution

Software development is messy.

Requirements sharpen. APIs change. Early designs turn out to be wrong. Implementation exposes assumptions that were never written down.

That is normal.

What Bonsai tries to prevent is allowing those discoveries to silently redefine the project.

`requirements.md` and `architecture.md` describe the intended system. During implementation, the coding agent distinguishes between:

* **None:** the current truth already covers the work
* **Clarification:** the intended design is unchanged, but the truth should be stated more precisely
* **Revision:** product behavior, architecture, constraints, or system boundaries actually need to change

A revision requires human approval before it becomes the new direction.

This matters especially on projects that evolve through several pivots. The final project memory should describe the system you ultimately decided to build, not every detour taken to discover it.

That gives Bonsai another useful property:

> **A mature project can be rebuilt from its final intended form rather than from the scars of its prototype history.**

---

# Human Control Without Constant Babysitting

Bonsai is intentionally human-centered, but that does not mean the developer has to micromanage every file edit.

The coding agent is allowed to maintain execution memory such as `plan.md`, `state.md`, phase plans, and the optional icebox.

The human retains authority over product and architecture truth.

For major durable contract surfaces, Bonsai can use a two-pass contract-first phase. Pass A produces the reviewable contract and tests that demonstrate how it is intended to be used, then stops for human approval. Pass B builds the implementation only after that contract is accepted.

That puts human review at a high-leverage point: after the shape is concrete enough to evaluate, but before a large amount of implementation depends on it.

At meaningful boundaries, Bonsai stops and asks for a decision instead of assuming that reading the prompt means unlimited permission to continue.

The goal is simple:

> **Let the agent manage execution. Keep the developer in control of what is being built and why.**

---

# Large Repositories Need Navigation Memory Too

Project memory answers questions such as:

* What are we building?
* What architecture are we aiming for?
* What phase are we in?
* What happens next?

Large codebases introduce another recurring problem:

* Where is the relevant code?
* Which subsystem owns this behavior?
* What callers or extension points matter?
* What should the agent inspect before changing it?

Bonsai includes layered code maps for that problem.

See:

[Code Maps](.bonsai/maps/README.md)

The maps are not a substitute for reading source code. They help the agent find the right source code faster and avoid rediscovering the same repository structure every session.

---

# Bonsai Is Not an Agent Framework

Bonsai does not try to orchestrate a fleet of agents.

It does not replace `AGENTS.md`, repository instructions, coding standards, or your preferred AI tool.

Those solve different problems.

Bonsai focuses on durable project memory:

* product truth
* architecture truth
* execution roadmap
* current state
* deeper project detail when needed
* repository navigation knowledge

Use it with one assistant, an IDE coding agent, a CLI agent, or a larger multi-agent system.

Better project memory helps all of them.

---

# Add Bonsai to Your Own Repository

Copy:

```text
.bonsai/
```

into the root of your repository.

Create or choose a project directory:

```text
.bonsai/projects/<project>/
```

Shape the project in a Web AI conversation and use:

```text
.bonsai/design_session.md
```

to generate the initial project memory.

Save the generated files under the project directory.

Then start implementation with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: <project>
```

For the detailed workflow, conventions, optional developer context, phase execution rules, and other operating details, see:

[.bonsai/README.md](.bonsai/README.md)

---

# Who Bonsai Is For

Bonsai is for developers who use AI as an engineering collaborator rather than only as autocomplete.

It becomes especially useful when:

* a project spans many AI sessions
* design and implementation happen in different tools
* you are tired of re-explaining the project to every new session
* the codebase is large enough that repository rediscovery costs real time
* you want the agent to manage execution without surrendering product or architecture control
* the project is likely to evolve, pivot, and accumulate deeper detail over time
* you want project memory to live in the repository instead of disappearing into chat history

If you have ever started a new coding session and thought:

> “I know the AI can help, but now I have to teach it the project again.”

Bonsai is meant to remove that part.

---

# Why Bonsai Exists

I built Bonsai out of the friction of using AI on real software projects.

The problem was not that the models could not write code.

The problem was continuity.

One session would contain important design decisions. Another would discover a better architecture. A coding agent would make progress, but the next session would need a careful recap. Large repositories would get rediscovered repeatedly. Old conversation context would become more expensive and less useful at the same time.

The obvious answer seemed to be more context.

For me, the better answer turned out to be **better-structured context**.

Bonsai keeps that structure in plain Markdown because plain Markdown is easy to inspect, diff, edit, version, copy, and hand to almost any AI tool.

The technology is deliberately boring.

The workflow is the product.

---

# Status

Bonsai is an evolving workflow extracted from real AI-assisted software development.

I use it while building software and change it when the workflow gets in my way.

That means the project is opinionated about project memory, human authority, clean handoffs, and selective context, but it is not trying to prescribe your programming language, architecture style, testing philosophy, or coding tool.

The detailed mechanics will keep evolving.

The core idea is stable:

> **Keep the project memory durable, structured, small, and close to the code.**

---

# Name

A bonsai is not wild growth.

It is growth shaped deliberately over time.

AI can generate enormous amounts of motion. Bonsai is about turning that motion into deliberate, maintainable software.
