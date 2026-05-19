# Task Tracker Example

This directory contains a complete **Bonsai design-session output** for a small example project:
a Java command-line task tracker.

The design work has already been completed. The files in this directory are the preserved project
memory produced from that design session:

```text
requirements.md
architecture.md
plan.md
state.md
```

Together, they define:

* what the task tracker should do
* how the system should be shaped
* the initial implementation roadmap
* the exact execution state the coding agent should pick up from

This example exists to demonstrate the handoff from:

1. **Web AI design and synthesis**
2. **IDE / CLI AI implementation**

---

# How to Use This Example

Copy the entire `task-tracker` directory into:

```text
.bonsai/projects/
```

so the resulting path is:

```text
.bonsai/projects/task-tracker/
```

Then start your coding agent with:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker
```

The coding agent should:

1. read the Bonsai implementation prompt
2. load the task-tracker project memory
3. summarize the active project state
4. identify the exact next step
5. recommend the appropriate AI level
6. stop for human approval before proceeding

---

# What This Example Demonstrates

The task tracker is intentionally small, but not trivial.

It is designed to show how Bonsai preserves enough structured memory for a coding agent to begin
serious work without requiring the human to restate the project from scratch.

The example demonstrates:

* a bounded product definition
* explicit architectural boundaries
* phased implementation planning
* stateful session handoff
* an implementation workflow where the agent may refine phase execution strategy before writing code

---

# Important

The task-tracker directory is not meant to be copied into a source-code location.

It belongs under:

```text
.bonsai/projects/
```

It is project memory, not the Java application source tree itself.

The coding agent will use these documents to drive implementation in the repository workspace.