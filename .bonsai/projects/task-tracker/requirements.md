# AI Requirements

**Project:** Task Tracker
**[Meta: Human-owned | Current Product Truth | Bounded Scope | No Implementation Detail]**

## Product Goal & Problem

**Goal:** Provide a small Java command-line task tracker that demonstrates a compact Bonsai project memory system while remaining concrete enough to implement and review.  
**Problem Solved:** A user needs a simple local way to track personal tasks by creating them, reviewing them, marking them complete, editing them, and removing them. The example project also needs enough real behavior to demonstrate requirements, architecture, phased execution, contract-first development, and human review without becoming oversized.  
**Primary Users:** [A local CLI user managing a small task list, A developer studying the Bonsai example project]

## Core Outcomes & Workflows

**Core Outcomes:** [Create tasks, Review tasks, Update task status and text, Remove tasks, Preserve tasks between runs]

### Workflows

* **Create Task:** [User submits task text] -> [System validates the text, creates a task, and assigns the next identifier] -> [Task becomes available in later listings] (Failures: [Blank or whitespace-only text])
* **Review Tasks:** [User requests tasks with an optional status filter] -> [System retrieves stored tasks, applies the requested filter, and orders matching tasks by identifier] -> [Matching tasks are displayed] (Failures: [Unsupported filter])
* **Update Task:** [User identifies an existing task and requests completion toggle or text edit] -> [System validates the target task and update input] -> [Updated task is retained] (Failures: [Unknown task identifier, Blank or whitespace-only replacement text])
* **Delete Task:** [User identifies an existing task] -> [System validates the target task and removes it] -> [Task no longer appears in later listings] (Failures: [Unknown task identifier])

## Functional Requirements

* **FR-1 Create Tasks:** The application shall create a task from non-blank user-provided text. (Acceptance: [A new task is created, It receives the next positive numeric identifier, Identifiers begin at 1 and increase for each created task, An identifier is never reused after deletion or application restart, It begins incomplete, Blank or whitespace-only text is rejected])
* **FR-2 List Tasks:** The application shall display tasks using supported task filters. (Acceptance: [All tasks can be listed, Active tasks can be listed, Completed tasks can be listed, Each listed task shows its identifier, completion state, and text, Matching tasks are displayed in ascending identifier order])
* **FR-3 Toggle Completion:** The application shall toggle an existing task between active and completed states. (Acceptance: [An active task can become completed, A completed task can become active again, The task identifier and text are preserved, Unknown task identifiers are rejected])
* **FR-4 Edit Task Text:** The application shall replace the text of an existing task with new non-blank text. (Acceptance: [Task text changes when valid replacement text is supplied, The task identifier and completion state are preserved, Blank or whitespace-only replacement text is rejected, Unknown task identifiers are rejected])
* **FR-5 Delete Tasks:** The application shall remove an existing task. (Acceptance: [A deleted task no longer appears in later listings, Its identifier is not reused, Unknown task identifiers are rejected])
* **FR-6 Persist Tasks Locally:** The application shall retain task data and identifier assignment state between command-line executions. (Acceptance: [Tasks created in one execution are available in a later execution, Completion state and edited text are retained, The next identifier continues increasing across executions, Persisted-data problems fail clearly rather than being treated as an empty task list])
* **FR-7 Command-Line Interface:** The application shall expose the supported task workflows through a fixed command vocabulary. (Acceptance: [`add <text...>` creates a task, `list` or `list all` lists all tasks, `list active` lists incomplete tasks, `list completed` lists completed tasks, `toggle <id>` toggles completion, `edit <id> <text...>` replaces task text, `delete <id>` deletes a task, Unsupported commands, filters, identifiers, or missing arguments fail clearly])
* **FR-8 Run as an Executable JAR:** The application shall be packaged as an executable JAR. (Acceptance: [The Gradle build produces a JAR with a manifest main class, The JAR can be launched with `java -jar`])

## Domain Rules & Constraints

* **Core Concepts:** [Task]: <A single tracked item with a positive numeric identifier, text, and completion state> | [Task Filter]: <A supported selection of all, active, or completed tasks>
* **Behavioral Rules:** [New tasks start incomplete, Task text must contain at least one non-whitespace character, Completion state can be toggled in either direction, Task updates and deletions require an existing task identifier, Task identifiers increase from 1 and are never reused, Task listings are ordered by ascending identifier]
* **System Constraints:** [Java 17 target version, Gradle Wrapper, JUnit 5, Standard single-module Gradle Java project, Command-line application, Executable JAR with manifest main class, Local persistence uses a UTF-8 JSON file named `task-tracker.json` in the current working directory]
* **Quality Requirements:** [Usability: Commands and failures should be understandable from CLI output] | [Reliability: Invalid task operations should fail cleanly] | [Performance: Normal use with a small personal task list should be immediate] | [Integrity: Task state and identifier assignment state should not be intentionally lost between runs]

## Exclusions & Accepted Decisions

* **Out of Scope / Non-Goals:** [Graphical user interface, Swing UI, Accounts or authentication, Multi-user collaboration, Remote sync, Due dates, Reminders, Tags, Projects or categories, Search, Bulk actions]
* **Accepted Decisions:** [The example is a Java 17 CLI application, The build uses the Gradle Wrapper, Tests use JUnit 5, The project uses a standard single-module Gradle Java layout, Task identifiers are positive numeric values assigned sequentially from 1 and never reused, Task listings use ascending identifier order, The CLI vocabulary is `add`, `list`, `toggle`, `edit`, and `delete` with the forms defined by FR-7, Local persistence is a UTF-8 `task-tracker.json` file in the current working directory, The project persists enough identifier state to prevent reuse, The build produces an executable JAR with a manifest main class]
* **Open Questions:** [None]

## Definition of Done

Requirements are satisfied when: [The application supports the defined task workflows and CLI vocabulary, Tasks and identifier assignment state persist between CLI executions, Task listings have stable ascending-identifier ordering, Persisted-data failures are visible, The build produces an executable JAR with the configured main class, Automated tests cover the intended core behavior, The implementation stays within the documented scope]
