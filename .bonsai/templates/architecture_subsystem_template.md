# AI Architecture - <Subsystem Name>

**[Meta: Human-owned | Durable Subsystem Truth | Rebuild-Grade]**  
**Project:** <Project name> | **Parent:** `../architecture.md`

## Role & Intent

**Role:** <3-6 lines on what this subsystem does in the overall architecture>  
**Architectural Intent:** <What this specific design is optimizing for>

## Boundaries

* **Owns:** [List specific responsibilities]
* **Must Not Own:** [List explicit boundary exclusions]

## Interfaces & Domain

* **Interface: <Name>:** <Purpose> | **Consumers:** [List] | **Rules:** [List]
* **Domain: <Concept>:** <Purpose> | **Properties:** [List] | **Lifecycle:** [Rules]

## Data Flow & Persistence

* **State / Persistence:** [List state categories, where they live, and persistence/ownership rules]
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])

## Dependencies

* **Allowed Depends On:** [Dependency] - <Why>
* **Forbidden Depends On:** [Forbidden Dependency] - <Why>

## Cross-Cutting Rules

* **Lifecycle:** [Startup/Runtime/Shutdown behavior]
* **Concurrency:** [Threading, locking, and execution rules]
* **Error/Recovery:** [Subsystem-specific fault tolerance]
* **Extension/Config:** [Extension points and configuration model]
* **Security/Integrity:** [Trust boundaries and validation]
* **Observability:** [Logging, metrics, and diagnostics expectations]
* **Assumptions:** [Build or runtime assumptions]

## Guardrails

* **Implementation Guardrails:** [List strict rules preventing regression]
* **Rejected Approaches:** [Approach] - [Why rejected]
* **Open Questions:** [Active design questions, prioritized by importance]
* **Fitness Criteria:** [Condition] | [Condition]