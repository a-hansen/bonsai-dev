# Task Tracker Example Project

This directory is an example Bonsai project memory package.

It represents the output of a completed Web AI design session for a small command-line task tracker.
The project memory is ready to hand off to an IDE / CLI coding agent for implementation.

To begin the implementation workflow from the repository root, run:

```text
Read .bonsai/implementation_prompt.md and follow its instructions. Active project: task-tracker.
```

The coding agent should:

1. read this project memory,
2. summarize the current execution state,
3. identify the exact next implementation step,
4. recommend an AI effort level, and
5. stop for human approval or redirection before making changes.

The files in this directory are example Bonsai memory artifacts, not an implemented application.

## Optional: Try the Design Session Yourself

The completed Task Tracker project is included as a working Bonsai example. You can also use the same project idea to see how a Bonsai design session begins from a simple product request.

Start a new AI session and provide:

1. `.bonsai/design_session.md`
2. The following project prompt:

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

The prompt intentionally does not specify implementation language or tooling. A successful design session should identify those as decisions to resolve rather than silently choosing them.