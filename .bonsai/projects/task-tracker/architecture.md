# AI Architecture

**Project:** Task Tracker
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Architectural Goal & Overview

**Goal:** Keep the task tracker small, explicit, and testable by separating core task behavior from CLI handling, persistence, and build packaging concerns.  
**System Overview:** The application is a Java 17 single-module Gradle project packaged as an executable JAR. It consists of a command-line entry point, a task-focused application/domain layer, and a local JSON persistence boundary. The command-line layer receives user intent and delegates task operations. The core task behavior exposes a small, explicit surface that is straightforward to test independently of CLI and persistence mechanics. Persistence retains both task state and the next identifier between runs but does not control task validity or mutation rules.  
**Principles:** [Small surface area, Clear boundaries, Explicit behavior boundaries, Tests demonstrate intended usage, Deterministic user-visible behavior, Avoid architecture that exceeds the example’s needs]

## Major Subsystems

* **CLI Entry Point & Command Handling:** <Accepts command-line input, selects the requested operation, and renders user-facing output> | **Owns:** [Main application entry point, Parsing the fixed command vocabulary, User-facing success and failure messages] | **Not Owns:** [Task rules, Task mutation behavior, Persistence representation] | **Dependencies:** [Task application service] | **Details:** [Supported forms are `add <text...>`, `list [all|active|completed]`, `toggle <id>`, `edit <id> <text...>`, and `delete <id>`; plain `list` means `list all`]
* **Task Application / Domain:** <Defines the task model and supported task operations> | **Owns:** [Task concept, Task filters, Task behavior contract, Create/list/toggle/edit/delete operations, Identifier assignment behavior, Ascending-identifier listing order] | **Not Owns:** [CLI parsing mechanics, Executable JAR packaging, JSON serialization mechanics] | **Dependencies:** [Task persistence boundary] | **Details:** [Task identifiers are represented as positive Java `long` values, begin at 1, increase for each created task, remain stable for the task lifetime, and are never reused]
* **Persistence Boundary:** <Retains complete application state between CLI executions> | **Owns:** [Loading stored application state, Saving complete application state, Hiding JSON storage mechanics from task behavior] | **Not Owns:** [Business rules for task validity, Identifier assignment policy, CLI interaction] | **Dependencies:** [Task model and persisted application-state representation] | **Details:** [Storage is a UTF-8 JSON file named `task-tracker.json` in the current working directory; persisted state contains the retained tasks and the next identifier; loading or decoding invalid stored state fails visibly rather than becoming an empty state]
* **Build & Packaging:** <Produces a Java 17 executable application artifact> | **Owns:** [Gradle Wrapper project, JUnit 5 test configuration, JAR manifest main-class configuration] | **Not Owns:** [Task behavior, CLI command semantics] | **Dependencies:** [Gradle Java application build configuration] | **Details:** None

## Canonical Domain Model & Data

* **Task:** <A single tracked item in the task list> | **Owned by:** Task Application / Domain | **Properties:** [Identifier: positive Java `long`, Text: non-blank string retained as supplied, Completion state: boolean] | **Lifecycle:** [Created incomplete, May be toggled complete or incomplete, May have text replaced, May be deleted; identifier does not change and is never reused]
* **Task Filter:** <A supported selector for visible tasks> | **Owned by:** Task Application / Domain | **Properties:** [All, Active, Completed] | **Lifecycle:** [Used during listing only, Not persisted]
* **Task State:** <The complete application state required to continue behavior across executions> | **Owned by:** Task Application / Domain in behavior, Persistence Boundary in storage | **Properties:** [Retained tasks, Next identifier] | **Lifecycle:** [Loaded at application start, Mutated through supported task operations, Saved after state-changing operations]
* **Ordering:** <Stable user-visible task order> | **Owned by:** Task Application / Domain | **Rule:** [List results are returned in ascending task identifier order after filtering]
* **State & Persistence:** [Task records and next-identifier state persist locally between executions, CLI input is transient, Build configuration is source-controlled project metadata, Test data is isolated from normal application state]

## Flow & Dependencies

* **Allowed / Key Flows:** <CLI invocation> -> <Command handling identifies requested task operation> -> <Task application validates and executes behavior> -> <Persistence boundary stores complete resulting state when needed> -> <CLI renders output> (Failure handling: [Invalid task operations or unsupported input produce user-facing failure output; persistence failures remain visible])
* **Allowed / Key Flows:** <List command> -> <Command handling identifies filter> -> <Task application retrieves matching tasks in ascending identifier order> -> <CLI renders matching tasks> (Failure handling: [Unsupported filter is rejected])
* **Allowed / Key Flows:** <Application startup> -> <Persistence boundary loads stored tasks and next identifier> -> <Task application validates reconstructed state> (Failure handling: [Missing storage begins with an empty task list and next identifier 1; unreadable, malformed, or invalid existing storage fails visibly])
* **Dependency Rules:** **Allowed:** [CLI -> Task Application, Task Application -> Persistence Boundary, Persistence Boundary -> Persisted state representation, Build configuration -> Application main class and tests] | **Forbidden:** [CLI -> Concrete JSON storage internals, Persistence Boundary -> CLI, Persistence Boundary -> Task policy decisions, Task Application -> Gradle/build concerns]

## Cross-Cutting Constraints

* **Extension Model:** [New user-facing task actions should enter through CLI command handling and be backed by explicit task behavior, Persistence mechanics may change only through an approved architecture change, Additional product scope should be reflected in requirements before implementation]
* **Error/Recovery:** [Invalid user operations should be represented as controlled failures, Persistence failures should not be hidden, Existing malformed persistence must not be silently discarded, The CLI should report failures clearly enough for a user to correct input]
* **Concurrency:** [No concurrent editing model is defined, The example is designed for simple local CLI use]
* **Security/Integrity:** [User-supplied task text and task identifiers are inputs that require validation, Stored state must not bypass task-domain validation when reconstructed, Persisted next-identifier state must remain greater than every retained task identifier]
* **Observability:** [Automated tests are the primary correctness signal during development, CLI output provides runtime feedback to the user, Additional logging is not a stated requirement]
* **Assumptions:** [Java 17 runtime, Gradle Wrapper is used for builds, JUnit 5 is used for tests, Standard single-module Gradle Java layout, Executable JAR has a configured manifest main class, Normal use is a small local task list]

## Guardrails & Rejections

* **Implementation Guardrails:** [Do not combine task rules, CLI parsing, and persistence into one monolithic class, Do not implement a graphical UI for this example, Do not expand scope beyond the compact task tracker requirements, Keep build configuration explicit rather than implied, Do not replace the settled identifier, ordering, CLI, or persistence decisions during implementation without a final-truth revision]
* **Explicitly Rejected:** [Swing UI - It would broaden the example and distract from the Bonsai workflow being demonstrated] | [Unspecified build tooling - The project explicitly uses Gradle Wrapper] | [Framework-heavy architecture - It is not justified by the project scope] | [Identifier reconstruction from the greatest retained task - It permits identifier reuse after deletion and conflicts with the settled never-reuse rule]
* **Open Questions:** [None]
