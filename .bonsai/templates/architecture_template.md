# AI Architecture

**Project:** <Project name>  
**[Meta: Human-owned | Target Implementation Truth | Rebuild-Grade | No Execution Plans]**

## Architectural Goal & Overview

**Goal:** <Optimization target, e.g., modularity, speed, isolation>  
**System Overview:** <Short 4-8 line description of major moving parts>  
**Principles:** [List core architectural principles]

## Major Subsystems

*If a subsystem has deep complexity, create `architecture/architecture_<SUBSYSTEM>.md` and link
it here.*

* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Boundaries] |
  **Dependencies:** [List] | **Details:** <Link to subsystem file or `None`>
* **<Subsystem Name>:** <Purpose> | **Owns:** [Responsibilities] | **Must Not Own:** [Boundaries] |
  **Dependencies:** [List] | **Details:** <Link to subsystem file or `None`>

## Module Boundaries & Dependency Shape

* **Human-Digestible Modules:** [List major modules/layers/packages the implementation should preserve]
* **Module Ownership:** [Module]: <Responsibilities owned by this module> | [Module]: <Responsibilities owned by this module>
* **Public Seams:** [Seam/Interface]: <Purpose, consumers, and stability expectation> | [Seam/Interface]: <Purpose, consumers, and stability expectation>
* **Dependency Direction:** **Allowed:** [Directions] | **Forbidden:** [Directions]
* **Boundary Rules:** [Rules that keep protocol, domain, runtime, adapters, persistence, UI, or infrastructure concerns separated]
* **Review Anchors:** [Files, interfaces, tests, examples, or module entry points that should make the generated implementation easy for a human to inspect]

## Canonical Domain Model & Data

* **<Concept>:** <Purpose> | **Owned by:** <Subsystem> | **Properties:** [List] |
  **Lifecycle:** [Rules]
* **State & Persistence:** [List data categories, where they live, persistence rules, and ownership boundaries]

## Flow & Dependencies

* **Allowed / Key Flows:** <Trigger> -> <Path 1, 2, 3> -> <Output> (Failure handling: [Rules])
* **Dependency Rules:** **Allowed:** [Directions] | **Forbidden:** [Directions]

## Cross-Cutting Constraints

* **Extension Model:** [Extension points and rules]
* **Error / Recovery:** [Failure domains and recovery rules]
* **Concurrency:** [Execution model and threading rules]
* **Security / Integrity:** [Boundaries and trust domains]
* **Observability:** [Logging, metrics, and diagnostics expectations]
* **Assumptions:** [Build / Runtime assumptions]

## Guardrails & Rejections

* **Implementation Guardrails:** [Strict technical boundaries to prevent regression]
* **Modularity Guardrails:** [Rules preventing collapsed responsibilities, convenience dependencies, oversized classes, leaky adapters, or cross-module shortcuts]
* **Explicitly Rejected:** [Approach] - [Why rejected]
* **Foundational Open Questions:** [Unresolved architecture-shaping questions that materially affect the target design, module boundaries, dependency direction, or first implementation phase, if any]
* **Open Questions:** [Active architecture questions, prioritized by importance]