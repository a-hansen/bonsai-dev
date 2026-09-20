# <Source> Subsystem Map — <Subsystem>

**[Meta: Agent-maintained | Subsystem Architecture | Load by Need | Keep Compact]**

## Scope

<What this architectural domain owns and is fundamentally responsible for.>

**Out of scope:** <Nearby responsibilities that belong elsewhere when the boundary is easy to confuse>

For source-wide orientation, return to [`../../code_map.md`](../../code_map.md).

## Owning Source Units

- **Path / unit:** `<path or module>`
  - **Role:** <What it owns>
- **Path / unit:** `<path or module>`
  - **Role:** <What it owns>

Owning paths must be backed by actual source. Do not define a subsystem merely to mirror a directory or build
module.

## Why It Matters

- <Why this subsystem recurs in implementation or source navigation>
- <Why its responsibility or boundary is easy to misunderstand, when applicable>

## Central Abstractions

- **`<Type or concept>`:** <Role in the subsystem>
- **`<Type or concept>`:** <Role in the subsystem>
- **`<Type or concept>`:** <Role in the subsystem>

Label material non-obvious claims as **Observed**, **Inferred**, or **Uncertain**. Actual source is authoritative.

## Key Workflows

Preserve flow shape and ownership boundaries, not implementation narration.

### 1. <Workflow name>

`<Trigger>` → `<Major step>` → `<Major step>` → `<Outcome>`

**Notes:** <Failure behavior, lifecycle rule, ownership boundary, or caution when useful>

### 2. <Workflow name>

`<Trigger>` → `<Major step>` → `<Major step>` → `<Outcome>`

**Notes:** <Failure behavior, lifecycle rule, ownership boundary, or caution when useful>

## Extension Seams

List demonstrated practical extension points, not every possible subclass or configuration hook.

- **<Seam>:** <How source consumers extend or contribute behavior>
- **<Seam>:** <How source consumers extend or contribute behavior>

Keep exact caller or extension mechanics in an optional API map when they justify the maintenance cost.

## Risky or Non-Obvious Areas

- <Rule, lifecycle constraint, ownership wrinkle, or likely navigation trap>
- <Rule, lifecycle constraint, ownership wrinkle, or likely navigation trap>

## Related API Maps

Keep only links for justified files that exist.

- [`api_pub.md`](api_pub.md) — Caller-facing mechanics
- [`api_ext.md`](api_ext.md) — Extension-facing mechanics

## Open Questions

Keep only uncertainties that matter to using or maintaining this map.

1. <Question requiring source verification or owner input>
