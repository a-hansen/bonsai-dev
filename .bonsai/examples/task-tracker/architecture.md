# AI Architecture

**Project:** Task Tracker
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Architectural Goal & Overview

**Goal:** Keep the task tracker small, explicit, and testable by separating core task behavior from CLI handling, persistence, and build packaging concerns.  
**System Overview:** The application is a Java 17 single-module Gradle project packaged as an executable JAR. It consists of a command-line entry point, a task-focused application/domain layer, and a local persistence boundary. The command-line layer receives user intent and delegates task operations. The core task behavior is designed to be reviewable and testable before implementation details are finalized. Persistence retains task state between runs but should not control task rules.  
**Principles:** [Small surface area, Clear boundaries, Contract-first behavior design, Tests demonstrate intended usage, Avoid architecture that exceeds the example’s needs]

## Major Subsystems

* **CLI Entry Point & Command Handling:** <Accepts command-line input, selects the requested operation, and renders user-facing output> | **Owns:** [Main application entry point, Command dispatch, User-facing success and failure messages] | **Not Owns:** [Task rules, Task mutation behavior, Persistence format] | **Dependencies:** [Task application service] | **Details:** None
* **Task Application / Domain:** <Defines the task model and supported task operations> | **Owns:** [Task concept, Task filters, Task behavior contract, Create/list/toggle/edit/delete operations] | **Not Owns:** [CLI parsing syntax, Executable JAR packaging, Concrete storage representation] | **Dependencies:** [Task persistence boundary] | **Details:** None
* **Persistence Boundary:** <Retains task state between CLI executions> | **Owns:** [Loading stored tasks, Saving stored tasks, Hiding storage details from the task application layer] | **Not Owns:** [Business rules for task validity, CLI interaction] | **Dependencies:** [Task model] | **Details:** None
* **Build & Packaging:** <Produces a Java 17 executable application artifact> | **Owns:** [Gradle Wrapper project, JUnit 5 test configuration, JAR manifest main-class configuration] | **Not Owns:** [Task behavior, CLI command semantics] | **Dependencies:** [Gradle Java application build configuration] | **Details:** None

## Canonical Domain Model & Data

* **Task:** <A single tracked item in the task list> | **Owned by:** Task Application / Domain | **Properties:** [Identifier, Text, Completion state] | **Lifecycle:** [Created incomplete, May be toggled complete or incomplete, May have text replaced, May be deleted]
* **Task Filter:** <A supported selector for visible tasks> | **Owned by:** Task Application / Domain | **Properties:** [All, Active, Completed] | **Lifecycle:** [Used during listing only, Not persisted unless later requirements explicitly change]
* **Task Collection:** <The current set of tasks known to the application> | **Owned by:** Task Application / Domain in behavior, Persistence Boundary in storage | **Properties:** [Tasks retained between runs, Ordering behavior remains an implementation question unless requirements later settle it] | **Lifecycle:** [Loaded for application use, Mutated through supported task operations, Saved after state-changing operations]
* **State & Persistence:** [Task records persist locally between executions, CLI input is transient, Build configuration is source-controlled project metadata, Test data is isolated from normal application state]

## Flow & Dependencies

* **Allowed / Key Flows:** <CLI invocation> -> <Command handling identifies requested task operation> -> <Task application validates and executes behavior> -> <Persistence boundary stores resulting state when needed> -> <CLI renders output> (Failure handling: [Invalid task operations or unsupported input produce user-facing failure output])
* **Allowed / Key Flows:** <List command> -> <Command handling identifies filter> -> <Task application retrieves matching tasks> -> <CLI renders matching tasks> (Failure handling: [Unsupported filter is rejected])
* **Dependency Rules:** **Allowed:** [CLI -> Task Application, Task Application -> Persistence Boundary, Build configuration -> Application main class and tests] | **Forbidden:** [CLI -> Concrete storage internals, Persistence Boundary -> CLI, Task Application -> Gradle/build concerns]

## Cross-Cutting Constraints

* **Extension Model:** [New user-facing task actions should enter through CLI command handling and be backed by explicit task behavior, Persistence details may change without redefining task behavior, Additional product scope should be reflected in requirements before implementation]
* **Error/Recovery:** [Invalid user operations should be represented as controlled failures, Persistence failures should not be hidden, The CLI should report failures clearly enough for a user to correct input]
* **Concurrency:** [No concurrent editing model is defined, The example is designed for simple local CLI use]
* **Security/Integrity:** [User-supplied task text and task identifiers are inputs that require validation, Stored state must not bypass task-domain validation when reconstructed]
* **Observability:** [Automated tests are the primary correctness signal during development, CLI output provides runtime feedback to the user, Additional logging is not a stated requirement]
* **Assumptions:** [Java 17 runtime, Gradle Wrapper is used for builds, JUnit 5 is used for tests, Standard single-module Gradle Java layout, Executable JAR has a configured manifest main class]

## Guardrails & Rejections

* **Implementation Guardrails:** [Do not combine task rules, CLI parsing, and persistence into one monolithic class, Do not implement a graphical UI for this example, Do not expand scope beyond the compact task tracker requirements, Preserve the two-pass review gate for the first phase, Keep build configuration explicit rather than implied]
* **Explicitly Rejected:** [Swing UI - It would broaden the example and distract from the Bonsai workflow being demonstrated] | [Unspecified build tooling - The project explicitly uses Gradle Wrapper] | [Framework-heavy architecture - It is not justified by the project scope]
* **Open Questions:** [What exact CLI command vocabulary should be used?, What persistence format should be used?, What task identifier format should be chosen?]