# Bonsai Subsystem Map - <Subsystem>

**[Meta: Agent-maintained | Subsystem Architecture Memory | Lazy Loaded by Need]**

## Scope

<What this subsystem owns and what it is fundamentally responsible for.>

---

## Owning Code Units

- **Path / Unit:** `<path or module>`
    - **Role:** <What it owns>

- **Path / Unit:** `<path or module>`
    - **Role:** <What it owns>

---

## Why It Matters

- <Reason this subsystem is important to developers or system behavior>
- <Reason this subsystem is likely to recur in implementation work>
- <Reason this subsystem is easy to misunderstand, if applicable>

---

## Central Abstractions

- **`<Type / Concept>`:** <Role in the subsystem>
- **`<Type / Concept>`:** <Role in the subsystem>
- **`<Type / Concept>`:** <Role in the subsystem>

Use evidence labels when needed:

- **Observed:** <Confirmed structural fact>
- **Inferred:** <Reasoned but not directly proven>
- **Uncertain:** <Needs verification before relying on it>

---

## Key Workflows

Keep these compact. Preserve flow shape, not implementation narration.

### 1. <Workflow Name>

`<Trigger>` → `<Major Step>` → `<Major Step>` → `<Outcome>`

**Notes:** <Failure behavior, ownership boundary, or important caution if needed>

### 2. <Workflow Name>

`<Trigger>` → `<Major Step>` → `<Major Step>` → `<Outcome>`

**Notes:** <Failure behavior, ownership boundary, or important caution if needed>

---

## Extension Seams

List practical extension points, not every possible subclass.

- **<Seam>:** <How developers plug in or extend behavior>
- **<Seam>:** <How developers plug in or extend behavior>
- **<Seam>:** <How developers plug in or extend behavior>

Name the seam and why it matters here. Move exact registration rules, route syntax, required methods, lifecycle obligations, and canonical usage patterns to the relevant API map.

---

## Risky or Non-Obvious Areas

- <Rule, lifecycle constraint, ownership wrinkle, or likely AI trap>
- <Rule, lifecycle constraint, ownership wrinkle, or likely AI trap>
- <Rule, lifecycle constraint, ownership wrinkle, or likely AI trap>

---

## Related API Maps

- `api_pub.md` - <Use when calling, querying, retrieving, or consuming this subsystem>
- `api_ext.md` - <Use when subclassing, implementing, registering, or extending this subsystem>

Remove either line if the file does not exist or is not justified.

---

## Open Questions

1. <Question requiring further source review or owner input>
2. <Question requiring further source review or owner input>
3. <Question requiring further source review or owner input>