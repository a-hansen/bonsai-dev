# Task Tracker Example Project

This is Bonsai's canonical Embedded Getting Started project. It demonstrates the v2 workflow with a small Java command-line application while keeping one reviewable source of project truth.

The project can be used in two ways:

1. Design your own Task Tracker in a preferred language and toolchain.
2. Start from the included Java 17 and Gradle project memory.

The included memory is intentionally at a clean post-design checkpoint. Requirements and architecture are settled, but Phase 1 has not been planned or implemented.

## Design Your Own Version

Start a Web UI design conversation with the Task Tracker prompt below. When the design is mature, use Bonsai's project-memory workflow:

```text
.bonsai/prompts/create_project_memory.md
```

During this repository's v2 staging period, the candidate copy is available at `bonsai/prompts/create_project_memory.md`. After promotion, `.bonsai/prompts/create_project_memory.md` is canonical.

Use this design prompt:

```markdown
I want to design a small example project called **Task Tracker**.

The application should let one user manage a short personal task list from the command line. It should support adding, listing, completing, reopening, editing, and deleting tasks; preserve data between runs; and report invalid input or unknown identifiers clearly.

Each task needs a stable identifier, non-blank text, and a completion state. New tasks begin incomplete, listings have stable ordering, and persisted-data problems must fail visibly.

Keep the project local, single-user, compact, and free of accounts, networking, synchronization, GUI, reminders, priorities, due dates, categories, or collaboration features. Preserve clear boundaries between core task behavior, command-line interaction, and persistence.

Use a contract-first initial phase: define a reviewable core task API or structural contract plus behavior-focused tests or usage examples, then stop for human review before full implementation.

Help me settle the language, tooling, and other material design choices. When the design is ready, follow `prompts/create_project_memory.md` to produce the Bonsai project memory.
```

## Use the Included Java Reference Memory

The included project truth specifies:

- Java 17;
- a command-line application;
- a Gradle Wrapper and JUnit 5;
- UTF-8 JSON persistence in `task-tracker.json`;
- an executable JAR.

From the repository root, start a fresh coding-agent session with:

```text
Read .bonsai/start.md and follow its instructions. Active project: task-tracker.
```

The agent should resolve Embedded Bonsai, select `task-tracker`, read `requirements.md`, `architecture.md`, `agent_plan.md`, and `agent_state.md`, and report the normal startup gate.

The initial checkpoint is deliberately blocked on phase planning:

- Current phase: Task Behavior Contract
- Mode: Two-pass contract-first
- Pass: Phase Planning
- Readiness: Phase planning required
- Exact next step: draft `plan/agent_plan_phase_1.md` for human review

After authorization, the agent creates the Phase 1 plan from `.bonsai/templates/plan_phase_template.md`, updates `agent_plan.md` and `agent_state.md`, and stops at the phase-plan approval gate. Pass A contract review and Pass B implementation follow only after their required approvals.

The checked-in example is project memory, not a completed application.
