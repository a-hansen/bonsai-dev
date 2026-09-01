# <Source> API Map — <Subsystem> Extension Mechanics

**[Meta: Agent-maintained | Optional Extension Mechanics | Strictly Lazy Loaded | Keep Selective]**

## Scope

Non-obvious reusable extension-facing mechanics for `<Subsystem>`.

Use this file only when subclassing or implementing subsystem types, registering providers or listeners,
contributing dynamic objects or configuration, or joining lifecycle and event flows. For architecture and
ownership, read [`map.md`](map.md).

Do not turn this file into an extension-surface inventory. Actual source is authoritative for full signatures and
options.

## Core Extension Surfaces

Include only seams needed to implement or register common extensions correctly.

### `<Type or seam>`

**Purpose:** <Why extenders use it>

```
<Minimal relevant signature, hook, registration, or implementation shape>
```

**Extension notes:**

- <Required implementation rule>
- <Lifecycle, identity, ordering, or registration requirement>

## Expected Extension Patterns

### <Pattern name>

<Short explanation of the reusable extension pattern.>

```
<Minimal, syntactically credible example>
```

**Must remember:**

- <Correctness rule>
- <Common pitfall>

## Sharp Edges

Preserve only recurring, source-backed, non-obvious extension risks.

- **<Issue>:** <What can go wrong and how to avoid it>
- **<Issue>:** <What can go wrong and how to avoid it>

Label material claims as **Observed**, **Inferred**, or **Uncertain** when their evidence status is not otherwise
clear.

## Consult Source When

- <Behavior varies by subtype, backend, or registration path>
- <Full lifecycle sequencing or exhaustive options matter>
- <The selected source snapshot may not align with this map>

## Open Questions

1. <Question requiring source verification or owner input>
