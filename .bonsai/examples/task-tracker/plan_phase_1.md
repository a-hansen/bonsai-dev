# AI Plan - Phase 1: Task Behavior Contract

**[Meta: Agent-maintained | Active Phase Detail | Compress when done]**
**Project:** Task Tracker | **Parent:** `plan.md`
**Status:** Active
**Mode:** Two-pass contract-first

## Objective & Scope

**Objective:** Define and review the task tracker’s core API/structural contract and behavior-focused tests before implementation work proceeds.  
**Inputs:** [Requirements: Core Outcomes & Workflows, Functional Requirements, Domain Rules & Constraints] | [Architecture: Task Application / Domain, Canonical Domain Model & Data, Flow & Dependencies] | [Prior Phase Output: None]
**In Scope:** [Task model shape, Supported task operations, Task filtering concept, Task-facing contract suitable for later CLI use, Behavior-focused JUnit 5 tests or usage examples, Human review gate]
**Out of Scope / Do Not Do Yet:** [CLI command syntax implementation, Local persistence implementation, Executable JAR runtime validation, Swing or any graphical UI, Out-of-scope product features]
**Expected Deliverables:** [Reviewable task API / structural contract, Behavior-focused JUnit 5 tests or usage examples, Any minimal scaffolding strictly necessary to express the contract, Updated `state.md` reflecting the review gate]

## Ordered Work

### Pass A: Contract (Review Gate)

* **Step A1 Define Reviewable Task Contract:** <Create the task model shape and supported task-operation contract needed to express create, list/filter, toggle completion, edit text, and delete behavior without implementing full behavior> | **Files:** [Main-source contract files under the standard Gradle Java layout] | **Done:** <The contract makes the intended capabilities and boundaries concrete enough for human review>
* **Step A2 Create Behavior-Focused Tests / Usage Examples:** <Create JUnit 5 tests or equivalent usage examples that demonstrate intended behavior and edge cases for the defined contract> | **Files:** [Test-source files under the standard Gradle Java layout] | **Done:** <The tests or usage examples make expected behavior concrete for human review, including important success and failure cases>
  *(Stop here for Human Review of API/Tests before Pass B)*

### Pass B: Implementation (Or Single-Pass)

* **Step B1 Implement Against the Approved Contract:** <Implement the core task behavior so it conforms to the approved Pass A contract and tests> | **Files:** [Main-source implementation files under the standard Gradle Java layout] | **Done:** <Approved behavior-focused tests pass without expanding the contract beyond reviewed intent>
* **Step B2 Finalize Phase State:** <Update project planning memory to reflect the completed contract phase and prepare for the CLI interaction phase> | **Files:** [`plan.md`, `state.md`, `plan_phase_1.md`] | **Done:** <Phase 1 status is accurate, Phase 2 is clearly next, and completed phase detail is ready for later compression>

## Validation & Done Criteria

* **Validation Strategy:** [Human review of the API/structural contract, Human review of behavior-focused tests or usage examples, JUnit 5 execution after Pass B implementation, Check that Phase 1 did not absorb CLI or persistence implementation]
* **Definition of Done:** [Pass A contract and tests/examples were explicitly reviewed before Pass B, Faithful to approved contract, Core task behavior is implemented and validated after approval, The phase remains within the documented scope]

## Context & Wrap-up

* **Dependencies:** [Java 17, Gradle Wrapper, JUnit 5, Standard single-module Gradle Java project]
* **Risks:** [Overbuilding the contract for a small example, Letting deferred CLI or persistence questions leak into the task behavior contract, Creating tests that reflect accidental implementation detail rather than intended behavior]
* **Open Questions:** [Does the Pass A contract require a task identifier format decision now, or can that remain implementation-flexible?, Should filtering be expressed as a dedicated type or a narrower method-level choice?]
* **Completion Summary:** *(Fill when done)* **Outcome:** [Results] |
  **Unlocked:** [A reviewed task behavior foundation ready for CLI implementation]