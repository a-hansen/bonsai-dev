# Bonsai Code Map

**[Meta: Agent-maintained | Top-Level Repository Compass | Fast Orientation | Always Loaded for Implementation]**

## How to Use This Map

1. Read this file first for broad repository orientation.
2. Use the subsystem index to identify the likely owning area.
3. Use the high-value package / namespace router, when present, for first-pass routing.
4. Load `namespace_router.tsv`, when present, only when fuller package / namespace ownership lookup is needed.
5. Load `subsystems/<subsystem>/map.md` for subsystem architecture.
6. Load `subsystems/<subsystem>/api_pub.md` only when writing caller-facing code for that subsystem.
7. Load `subsystems/<subsystem>/api_ext.md` only when extending or implementing that subsystem.
8. Read source before relying on any non-obvious behavior not captured by the relevant map files.

---

## If Editing Bonsai Code Maps

If you are creating, updating, reorganizing, or compressing Bonsai code-map artifacts, first read:

```text
.bonsai/maps/map_system.md
```

`map_system.md` defines the mapping file model, artifact responsibilities, build order, update rules,
and drift-prevention guidance.

Do **not** load `map_system.md` merely to use the maps for implementation work.
Load it only when editing the map system or map artifacts themselves.

---

## Repository Snapshot

**Repository:** <Repository name>
**Domain:** <Product or framework domain>
**Primary language(s):** <Languages>
**Build / packaging model:** <Short summary>

---

## Subsystem Index

| Subsystem     | Role            | Primary Path(s) | Map                             |
| ------------- | --------------- | --------------- | ------------------------------- |
| `<Subsystem>` | <1-2 line role> | `<path>`        | `subsystems/<subsystem>/map.md` |
| `<Subsystem>` | <1-2 line role> | `<path>`        | `subsystems/<subsystem>/map.md` |
| `<Subsystem>` | <1-2 line role> | `<path>`        | `subsystems/<subsystem>/map.md` |

---

## Major Boundaries

Capture only boundaries that materially help navigation.

* **<Boundary>:** <What it separates and why it matters>
* **<Boundary>:** <What it separates and why it matters>
* **<Boundary>:** <What it separates and why it matters>

Examples:

* public API vs implementation internals
* runtime vs tooling
* protocol entry points vs core domain model
* server vs client
* generated vs handwritten
* framework layer vs application layer

---

## Major Entry Points

List execution, integration, or extension origins that help agents route into the repo.

* **<Entry Point>:** <What originates here>
* **<Entry Point>:** <What originates here>
* **<Entry Point>:** <What originates here>

---

## Recommended Drill-Down Order

Use when a repository has a clear learning sequence.

1. **<Subsystem>** - <Why it should be understood first>
2. **<Subsystem>** - <Why it follows>
3. **<Subsystem>** - <Why it follows>

---

## High-Value Package / Namespace Router

Include only the prefixes that materially improve first-load repository orientation.

This table should stay compact.
It is not the full package / namespace registry.

For broader package / namespace ownership lookup, load:

```text
namespace_router.tsv
```

when that optional file exists and the current task needs it.

| Package / Namespace Prefix | Owning Subsystem | Owning Path or Module | Why It Is High-Value                              |
| -------------------------- | ---------------- | --------------------- | ------------------------------------------------- |
| `<prefix>`                 | `<Subsystem>`    | `<path or unit>`      | <Why this prefix materially improves orientation> |
| `<prefix>`                 | `<Subsystem>`    | `<path or unit>`      | <Why this prefix materially improves orientation> |
| `<prefix>`                 | `<Subsystem>`    | `<path or unit>`      | <Why this prefix materially improves orientation> |

---

## Repository Rules That Affect Navigation

Keep this short. Capture only routing-relevant facts.

* **Testing:** <Where meaningful tests live, if that affects mapping or implementation work>
* **Packaging:** <Build or module fact that helps orient future agents>
* **API Boundary:** <Export, visibility, or dependency rule that affects code reading>
* **Ignored / Low-Value Areas:** <Generated, legacy, or non-representative areas worth avoiding>

---

## Related Map Files

* `map_repo.md` - Repository-specific mapping calibration and priorities
* `map_state.md` - Current mapping baton pass
* `map_system.md` - Map-system rules; read only when editing Bonsai code-map artifacts
* `namespace_router.tsv` - Optional lazy-loaded fuller package / namespace ownership lookup
* `manifest.tsv` - Optional compact subsystem registry, when present
* `symbol_index.tsv` - Optional selective symbol lookup support, when present
