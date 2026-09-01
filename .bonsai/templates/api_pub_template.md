# <Source> API Map — <Subsystem> Caller Mechanics

**[Meta: Agent-maintained | Optional Caller Mechanics | Strictly Lazy Loaded | Keep Selective]**

## Scope

Non-obvious reusable caller-facing mechanics for `<Subsystem>`.

Use this file only when writing or reviewing code that locates the subsystem, calls its public API, queries its
data, subscribes to events, consumes results, or configures supported public surfaces. For architecture and
ownership, read [`map.md`](map.md).

Do not turn this file into an API inventory. Actual source is authoritative for full signatures and options.

## Core Caller Surfaces

Include only surfaces needed to use common caller behavior correctly.

### `<Type or surface>`

**Purpose:** <Why callers use it>

```
<Minimal relevant signature or usage shape>
```

**Caller notes:**

- <Important behavior>
- <Constraint, failure, return-value, nullability, or lifecycle rule>

## Expected Caller Patterns

### <Pattern name>

<Short explanation of the reusable pattern.>

```
<Minimal, syntactically credible example>
```

**Must remember:**

- <Correctness rule>
- <Common pitfall>

## Sharp Edges

Preserve only recurring, source-backed, non-obvious caller risks.

- **<Issue>:** <What can go wrong and how to avoid it>
- **<Issue>:** <What can go wrong and how to avoid it>

Label material claims as **Observed**, **Inferred**, or **Uncertain** when their evidence status is not otherwise
clear.

## Consult Source When

- <Behavior varies by implementation>
- <Full signatures, exhaustive options, or exact sequencing matter>
- <The selected source snapshot may not align with this map>

## Open Questions

1. <Question requiring source verification or owner input>
