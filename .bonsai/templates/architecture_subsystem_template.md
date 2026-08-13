# AI Architecture - <Subsystem Name>

**[Meta: Human-owned | Durable Subsystem Truth | Rebuild-Grade]**  
**Project:** <Project name> | **Parent:** `../architecture.md`

## Role & Intent

**Role:** <3-6 lines on what this subsystem does in the overall architecture>  
**Architectural Intent:** <What this specific design is optimizing for>

## Boundaries

* **Owns:** [List specific responsibilities]
* **Must Not Own:** [Explicit approved exclusions, or `None`]

## Interfaces & Domain

* **Public Contract: <Name>:** <Purpose> | **Consumers:** [List] | **Rules:** [List]
* **Domain: <Concept>:** <Purpose> | **Properties:** [List] | **Lifecycle:** [Rules]

If no durable public contract is part of this subsystem's approved architecture, state
`Public Contracts: None`. Do not invent interfaces merely to populate this section.

## Data Flow & Persistence

* **State / Persistence:** [List state categories, where they live, and persistence/ownership rules]
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])
* **Key Flow: <Name>:** <Trigger> -> <Step 1, 2, 3> -> <Output> (Failure: [Handling rule])

## Dependencies

* **Allowed Depends On:** [Approved dependency] - <Why>
* **Forbidden Depends On:** [Explicitly forbidden dependency] - <Why>

If dependency direction is not architecturally prescribed, state that rather than inventing a rule.

## Cross-Cutting Rules

* **Lifecycle:** [Startup/Runtime/Shutdown behavior]
* **Concurrency:** [Threading, locking, and execution rules, if prescribed]
* **Error/Recovery:** [Subsystem-specific fault tolerance]
* **Extension/Config:** [Approved extension points and configuration model, or `None`]
* **Security/Integrity:** [Trust boundaries and validation]
* **Observability:** [Logging, metrics, and diagnostics expectations, if prescribed]
* **Assumptions:** [Build or runtime assumptions]

## Guardrails

* **Implementation Guardrails:** [Approved strict rules preventing architectural regression, or `None`]
* **Architecture Guardrails:** [Rules preserving explicitly approved subsystem responsibility and contracts, or `None`]
* **Rejected Approaches:** [Approach] - [Why rejected]
* **Open Questions:** [Active design questions, prioritized by importance]
* **Fitness Criteria:** [Condition] | [Condition]