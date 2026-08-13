# AI Architecture

**Project:** <Project name>  
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Architectural Goal & Overview

**Goal:** <Primary architectural optimization target>  
**System Overview:** <Short 4-8 line description of major moving parts>  
**Principles:** [List approved architectural principles]

## Major Subsystems

*If a subsystem has deep complexity, create `architecture/architecture_<SUBSYSTEM>.md` and link
it here.*

* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Approved boundaries or `None`] |
  **Dependencies:** [Approved dependencies or `None`] | **Details:** <Link to subsystem file or `None`>
* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Approved boundaries or `None`] |
  **Dependencies:** [Approved dependencies or `None`] | **Details:** <Link to subsystem file or `None`>

## Module Boundaries & Dependency Shape

* **Human-Digestible Modules:** [Approved major modules/layers/packages, or `Not prescribed`]
* **Module Ownership:** [Approved ownership rules, or `Not prescribed`]
* **Public Seams:** [Externally or durably consumed seams and contracts, or `None`]
* **Dependency Direction:** **Allowed:** [Approved directions or `Not prescribed`] | **Forbidden:** [Explicitly forbidden directions or `None`]
* **Boundary Rules:** [Approved architectural boundaries only, or `None`]
* **Review Anchors:** [Files, schemas, examples, interfaces, entry points, or other artifacts that make important approved design surfaces inspectable, or `None`]

## Canonical Domain Model & Data

* **<Concept>:** <Purpose> | **Owned by:** <Subsystem or `Not prescribed`> | **Properties:** [List] |
  **Lifecycle:** [Rules]
* **State & Persistence:** [List data categories, persistence rules, and ownership boundaries]

## Flow & Dependencies

* **Allowed / Key Flows:** <Trigger> -> <Path 1, 2, 3> -> <Output> (Failure handling: [Rules])
* **Dependency Rules:** **Allowed:** [Approved directions or `Not prescribed`] | **Forbidden:** [Explicitly forbidden directions or `None`]

## Cross-Cutting Constraints

* **Extension Model:** [Approved extension points and rules, or `None`]
* **Error / Recovery:** [Failure domains and recovery rules]
* **Concurrency:** [Execution model and threading rules, if prescribed]
* **Security / Integrity:** [Boundaries and trust domains]
* **Observability:** [Logging, metrics, and diagnostics expectations, if prescribed]
* **Assumptions:** [Build / Runtime assumptions]

## Guardrails & Rejections

* **Implementation Guardrails:** [Strict approved technical constraints, or `None`]
* **Architecture Guardrails:** [Rules required to preserve approved architecture, or `None`]
* **Explicitly Rejected:** [Approach] - [Why rejected]
* **Foundational Open Questions:** [Unresolved architecture-shaping questions that materially affect the target design or first implementation phase, if any]
* **Open Questions:** [Active architecture questions, prioritized by importance]