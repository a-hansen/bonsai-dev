# Task Tracker Example Project

This directory demonstrates Bonsai using a small task-tracker project.

You can use this example in two ways:

1. **Design your own version** using your preferred language and tools.
2. **Explore the included project memory** for a Java command-line implementation using Gradle.

The Task Tracker scenario is intentionally small, but substantial enough to demonstrate requirements, architecture, planning, implementation handoff, contract-first development, human review gates, dry runs, completion summaries, and final-truth updates.

## Start Here: Design the Project in Your Preferred Stack

The best way to experience Bonsai is to begin with a design session rather than adopt the included implementation choices.

Start a new AI session and provide:

1. `.bonsai/design_session.md`
2. The project prompt below

```markdown
I want to design a small example project called **Task Tracker**.

The application should let one user manage a short personal task list from the command line. It should be small enough to serve as a clear example project, but substantial enough to exercise requirements, architecture, planning, implementation handoff, and human review gates.

The application should support:

- Adding a task from non-blank text.
- Listing tasks, with views for all tasks, active tasks, and completed tasks.
- Showing enough information in a task listing to identify the task and its current status.
- Marking a task complete and reopening a completed task.
- Editing the text of an existing task.
- Deleting a task.
- Preserving task data between application runs.
- Clear user-facing errors for invalid input, unsupported filters, or unknown task identifiers.

Important behavioral expectations:

- Each task has a stable identifier, text, and completion state.
- New tasks begin incomplete.
- Task listings should have stable, predictable ordering.
- Blank or whitespace-only task text must be rejected when creating or editing a task.
- Updating or deleting an unknown task must fail clearly.
- Persisted data problems should fail clearly rather than silently discarding or mutating task data.

Keep the project intentionally compact:

- It is a local, single-user command-line application.
- It does not need accounts, networking, synchronization, a graphical interface, reminders, priorities, due dates, categories, or collaboration features.
- Avoid framework-heavy or unnecessarily elaborate architecture.
- Preserve clear boundaries between core task behavior, command-line interaction, and persistence.

This project is also intended to demonstrate a contract-first workflow. The initial implementation phase should define a reviewable core task API or structural contract, along with behavior-focused tests or usage examples, and stop for human review before the full implementation proceeds.

Use the supplied `design_session.md` instructions to conduct the design session and produce the appropriate Bonsai project memory documents. Ask me about any important design decisions that must be settled before the documents can be finalized.
```

The prompt intentionally does not specify implementation language or tooling. The design session should identify those as decisions to resolve rather than silently choosing them.

## Included Reference Memory: Java CLI with Gradle

This directory also contains a completed Bonsai project memory package for one specific implementation choice:

- Command-line application
- Java implementation
- Gradle build and test workflow

The included memory files represent the output of a completed design session. They are ready to hand off to an IDE or CLI coding agent for implementation.

Use this path when you want to inspect a completed Bonsai memory package or exercise the implementation workflow without first conducting a new design session.

### Requirements

To implement and test the included reference project, your environment must support:

- Java
- Gradle, or a Gradle wrapper once one has been added to the project

Developers who do not want to use Java or Gradle should start with the design-session path above and select their own language and tools.

### Begin the Included Implementation Workflow

From the repository root, provide this instruction to your IDE or CLI coding agent:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker.
```

The coding agent should:

1. Read the included project memory.
2. Summarize the current execution state.
3. Identify the exact next implementation step.
4. Recommend an AI effort level.
5. Stop for human approval or redirection before making changes.

The included memory files are reference project artifacts, not a completed application.