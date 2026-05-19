# Bonsai API Map - <Subsystem> Caller Mechanics

**[Meta: Agent-maintained | Exact Caller-Facing Mechanics | Strictly Lazy Loaded]**

## Scope

Caller-facing mechanics for `<Subsystem>`.

Use this file when writing code that:

- retrieves or locates this subsystem
- calls its public API
- queries its data
- subscribes to its events
- consumes its results or cursors
- configures it through supported public surfaces

For subsystem architecture, read `map.md`.

---

## Core Interfaces / Classes

Include only the types needed to write or review common caller code correctly.

For each included surface, capture why a caller reaches for it, the exact rule that matters, and the usage shape that prevents common misuse.

### `<TypeName>`

**Purpose:** <Why callers care>

```java
<Minimal relevant signature or usage shape>
```

**Caller notes:**

- <Important behavior>
- <Important constraint>
- <Important return / null / lifecycle rule>

---

### `<TypeName>`

**Purpose:** <Why callers care>

```java
<Minimal relevant signature or usage shape>
```

**Caller notes:**

- <Important behavior>
- <Important constraint>

---

## Expected Caller Patterns

### <Pattern Name>

<Short explanation of the common pattern.>

```java
// Minimal, syntactically credible example
```

**Must remember:**

- <Correctness rule>
- <Common pitfall>

---

### <Pattern Name>

<Short explanation of the common pattern.>

```java
// Minimal, syntactically credible example
```

**Must remember:**

- <Correctness rule>
- <Common pitfall>

---

## Sharp Edges

Preserve only recurring, non-obvious caller risks.

- **<Issue>:** <What can go wrong and how to avoid it>
- **<Issue>:** <What can go wrong and how to avoid it>
- **<Issue>:** <What can go wrong and how to avoid it>

---

## Consult Source When

Read source directly when:

- <Condition where this file intentionally stops short>
- <Condition where behavior may vary by implementation>
- <Condition where full signature or exhaustive options matter>

---

## Open Questions

1. <Question requiring further source review or owner input>
2. <Question requiring further source review or owner input>