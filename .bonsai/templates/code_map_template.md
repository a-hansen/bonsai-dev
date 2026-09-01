# <Source> Code Map

**[Meta: Agent-maintained | Source Navigation | Load First for This Map | Keep Compact]**

## Source Identity

**Logical source:** <Stable source-universe name>  
**Source type / location:** <Repository, released source artifact, or other source information when it helps selection>  
**Snapshot identity:** <Version, Git revision, artifact coordinate, checksum, or other smallest useful alignment evidence>

This map describes the source snapshot above. Actual source is authoritative. If the selected source does not align
with this identity, do not silently rely on non-obvious map claims; inspect the source identity and update, rebuild,
or select another map as appropriate.

## How to Use This Map

1. Read this file first for broad source orientation.
2. Use the subsystem index to identify the likely owning area.
3. Use the compact namespace router below for first-pass routing.
4. Load `namespace_router.tsv` only when that optional fuller lookup exists and is needed.
5. Load `subsystems/<subsystem>/map.md` for the relevant subsystem architecture.
6. Load that subsystem's optional `api_pub.md` for caller mechanics or `api_ext.md` for extension mechanics only
   when the current work needs them.
7. Use `manifest.tsv` or `symbol_index.tsv` only for their narrow lookup roles when present.
8. Verify non-obvious behavior in source before depending on it.

## Source Snapshot

**Domain:** <Product, library, framework, or source domain>  
**Primary language(s):** <Languages>  
**Build / packaging model:** <Short durable summary>

Record durable source structure and navigation facts only. Do not include active project status, requirements
traceability, plans, session state, or planned-but-absent source behavior.

## Subsystem Index

List only durable architectural domains or source areas that materially improve navigation. Do not mirror folders
or build modules unless they represent meaningful responsibility boundaries.

| Subsystem     | Role            | Primary Path(s) | Map                             |
| ------------- | --------------- | --------------- | ------------------------------- |
| `<Subsystem>` | <1–2 line role> | `<path>`        | `subsystems/<subsystem>/map.md` |
| `<Subsystem>` | <1–2 line role> | `<path>`        | `subsystems/<subsystem>/map.md` |

## Major Boundaries

Capture only boundaries that materially help source navigation.

- **<Boundary>:** <What it separates and why it matters>
- **<Boundary>:** <What it separates and why it matters>

## Major Entry Points

List execution, integration, or extension origins that help route into the source.

- **<Entry point>:** <What originates here>
- **<Entry point>:** <What originates here>

## Recommended Drill-Down Order

Include only when the source has a useful code-navigation learning sequence.

1. **<Subsystem>** — <Why it should be understood first>
2. **<Subsystem>** — <Why it follows>

## High-Value Package / Namespace Router

Keep this small. Do not duplicate the optional fuller `namespace_router.tsv`.

| Package / Namespace Prefix | Owning Subsystem | Owning Path or Module | Why It Is High-Value                 |
| -------------------------- | ---------------- | --------------------- | ------------------------------------ |
| `<prefix>`                 | `<Subsystem>`    | `<path or unit>`      | <Why this improves first-load routing> |
| `<prefix>`                 | `<Subsystem>`    | `<path or unit>`      | <Why this improves first-load routing> |

## Source Rules That Affect Navigation

Keep only durable routing-relevant facts.

- **Testing:** <Where representative tests live, when that affects source interpretation>
- **Packaging:** <Build or module fact that improves navigation>
- **API boundary:** <Export, visibility, or dependency rule that affects source reading>
- **Ignored / low-value areas:** <Generated, legacy, or non-representative areas worth avoiding>

## Evidence and Uncertainty

Label non-obvious claims when their status is material:

- **Observed:** <Source-backed fact>
- **Inferred:** <Reasoned conclusion not directly established by source>
- **Uncertain:** <Claim requiring verification before reliance>

When source and this map disagree, correct the map or keep the mismatch explicit.

## Related Map Files

Keep only entries for files that exist. All paths are relative to this named-source map.

- `map_repo.md` — Optional human-owned source calibration; mapping guidance, not source proof
- `map_state.md` — Optional current mapping continuation state; not an ordinary map-consumption input
- `namespace_router.tsv` — Optional fuller namespace ownership lookup
- `manifest.tsv` — Optional compact subsystem/path registry
- `symbol_index.tsv` — Optional selective high-value symbol lookup
- `subsystems/<subsystem>/map.md` — Subsystem architecture, with optional sibling API maps
