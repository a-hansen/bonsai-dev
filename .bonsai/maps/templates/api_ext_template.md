# Bonsai API Map - <Subsystem> Extension Mechanics

**[Meta: Agent-maintained | Exact Extension-Facing Mechanics | Strictly Lazy Loaded]**

## Scope

Extension-facing mechanics for `<Subsystem>`.

Use this file when writing code that:

- subclasses subsystem types
- implements subsystem interfaces
- registers providers, trackers, plugins, listeners, or services
- contributes dynamic objects or configuration
- hooks into lifecycle or event flows

For subsystem architecture, read `map.md`.

---

## Core Extension Surfaces

Include only the extension seams needed to write or review common extension code correctly.

For each included seam, capture why an extender uses it, the exact requirement that matters, and the implementation or registration pattern that prevents common mistakes.

### `<TypeName>`

**Purpose:** <Why extenders care>

```java
<Minimal relevant signature, abstract method, hook, or implementation shape>
```

**Extension notes:**

- <Required implementation rule>
- <Lifecycle or registration requirement>
- <Important caveat>

---

### `<TypeName>`

**Purpose:** <Why extenders care>

```java
<Minimal relevant signature, abstract method, hook, or implementation shape>
```

**Extension notes:**

- <Required implementation rule>
- <Lifecycle or registration requirement>

---

## Expected Extension Patterns

### <Pattern Name>

<Short explanation of the reusable extension pattern.>

```java
// Minimal, syntactically credible example
```

**Must remember:**

- <Correctness rule>
- <Common pitfall>

---

### <Pattern Name>

<Short explanation of the reusable extension pattern.>

```java
// Minimal, syntactically credible example
```

**Must remember:**

- <Correctness rule>
- <Common pitfall>

---

## Sharp Edges

Preserve only recurring, non-obvious extension risks.

- **<Issue>:** <What can go wrong and how to avoid it>
- **<Issue>:** <What can go wrong and how to avoid it>
- **<Issue>:** <What can go wrong and how to avoid it>

Examples of things that belong here when observed:

- instance identity must be preserved
- events must fire after mutation, not before
- a callback runs synchronously
- a future must eventually complete
- registration must occur in a specific lifecycle phase
- a subclass must call `super`

---

## Consult Source When

Read source directly when:

- <Condition where this file intentionally stops short>
- <Condition where implementation behavior varies by subtype or backend>
- <Condition where full lifecycle sequencing matters beyond the reusable pattern>

---

## Open Questions

1. <Question requiring further source review or owner input>
2. <Question requiring further source review or owner input>