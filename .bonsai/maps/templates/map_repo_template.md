# Bonsai Map Repository Addendum

**[Meta: Human-owned | Repository-Specific Mapping Calibration | Priority and Evidence Guidance]**

## Purpose

Capture repository-specific guidance for Bonsai code mapping.

Use this file to tell mapping agents:

- where meaningful source lives
- how the repo is packaged
- what the owner considers important
- which code reflects real usage
- which paths usually do not matter
- which repository-specific caveats should shape exploration

This file sets mapping priority and caution.  
Observed source remains authoritative.

---

## Repository Identity

- **Name:** <Repository name>
- **Domain:** <Product / framework / application domain>
- **Primary language(s):** <Languages>
- **Build system(s):** <Build tools>
- **Primary runtime surface(s):** <Runtime environments, servers, bundles, clients, etc.>
- **Primary extension surface(s):** <Public APIs, plugin seams, service interfaces, subclass hooks, etc.>

---

## Repository Shape

### Source Roots

List each meaningful source root.

- **Path:** `<path>`
    - **Purpose:** <What lives here>
    - **Importance:** <High | Medium | Low>
    - **Type:** <Primary | Secondary | Sample | Test | Tooling | Generated | Legacy>

- **Path:** `<path>`
    - **Purpose:** <What lives here>
    - **Importance:** <High | Medium | Low>
    - **Type:** <Primary | Secondary | Sample | Test | Tooling | Generated | Legacy>

---

### Build / Packaging Units

List real top-level ownership or packaging units.

Examples:

- modules
- Gradle subprojects
- Maven modules
- OSGi bundles
- plugins
- apps
- libraries

- **Unit:** `<name>`
    - **Path:** `<path>`
    - **Role:** <What it owns>
    - **Importance:** <High | Medium | Low>

- **Unit:** `<name>`
    - **Path:** `<path>`
    - **Role:** <What it owns>
    - **Importance:** <High | Medium | Low>

---

### Runtime Surfaces

List major runtime boundaries when known.

- **Surface:** `<name>`
    - **Scope:** <What behavior enters or runs here>
    - **Notes:** <Anything mapping agents should keep in mind>

- **Surface:** `<name>`
    - **Scope:** <What behavior enters or runs here>
    - **Notes:** <Anything mapping agents should keep in mind>

---

## Owner Weighting Guidance

Capture human judgment that should influence mapping priority.

- **Item:** `<module | package | service | directory | pattern>`
    - **Weight:** <High | Medium | Low>
    - **Reason:** <Why this matters>
    - **Confidence:** Owner-provided

- **Item:** `<module | package | service | directory | pattern>`
    - **Weight:** <High | Medium | Low>
    - **Reason:** <Why this matters>
    - **Confidence:** Owner-provided

---

## Priority Areas

### Priority Build Units

Ordered list.

1. `<unit>`
2. `<unit>`
3. `<unit>`

### Priority Packages / Namespaces

Ordered list.

1. `<package or namespace>`
2. `<package or namespace>`
3. `<package or namespace>`

### Priority Entry Points

Ordered list.

1. `<entry point>`
2. `<entry point>`
3. `<entry point>`

---

## Intended Mapping Scope

Use this section to distinguish:

- what the current mapping effort is intended to cover
- what may be consulted only as supporting evidence
- what should not be mapped unless the human explicitly expands scope

This is a scope boundary, not merely a priority hint.

### In Scope for This Mapping Effort

List the subsystems, build units, architectural domains, or repository areas that should receive
actual Bonsai mapping artifacts during this mapping effort.

1. `<subsystem, build unit, or architectural area>`
2. `<subsystem, build unit, or architectural area>`
3. `<subsystem, build unit, or architectural area>`

### Calibration-Only Areas

List areas that may be inspected to validate patterns, confirm real usage, or provide representative
examples, but should not receive their own subsystem maps or API maps unless scope is explicitly
expanded.

- `<path or area>`
    - **Use for:** <What it helps confirm>
    - **Do not:** <What mapping work should not be created from it>

- `<path or area>`
    - **Use for:** <What it helps confirm>
    - **Do not:** <What mapping work should not be created from it>

### Out of Scope Unless Explicitly Requested

List areas the mapping agent should not turn into mapping artifacts during the current effort.

- `<area>`
- `<area>`
- `<area>`

### Scope Handling Rule

The mapping agent should:

- create mapping artifacts only for areas listed as **In Scope for This Mapping Effort**
- inspect **Calibration-Only Areas** only when they help validate or refine in-scope maps
- avoid creating subsystem maps, API maps, manifest entries, or symbol-index entries for
  **Out of Scope** areas unless the human explicitly expands the mapping scope
- record a scope concern in `map_state.md` rather than silently widening the mapping effort

---

## Practical Calibration Sources

Identify code that reflects day-to-day implementation reality better than abstract API theory.

- **Path:** `<path>`
    - **Why it matters:** <Why this is representative>
    - **Teaches:** <What patterns it reveals>
    - **Use as tie-breaker when:** <When to prefer this evidence over assumptions>

- **Path:** `<path>`
    - **Why it matters:** <Why this is representative>
    - **Teaches:** <What patterns it reveals>
    - **Use as tie-breaker when:** <When to prefer this evidence over assumptions>

---

## Naming / Convention Notes

Record naming or structural conventions worth preserving.

- **Convention:** `<name>`
    - **Meaning:** <What it implies>
    - **Confidence:** <Owner-provided | Observed | Inferred>

- **Convention:** `<name>`
    - **Meaning:** <What it implies>
    - **Confidence:** <Owner-provided | Observed | Inferred>

---

## Architectural Biases to Preserve

Capture repo-specific mapping biases that should shape exploration.

- **Bias:** <Guidance>
    - **Reason:** <Why this matters>

- **Bias:** <Guidance>
    - **Reason:** <Why this matters>

Examples:

- Prefer developer relevance over internal centrality.
- Keep packaging boundaries explicit.
- Use representative production examples as a tie-breaker.
- Do not over-weight giant legacy modules simply because they contain many files.
- Distinguish practical extension seams from internal machinery.

---

## Known Exceptions / Oddities

Capture facts likely to mislead a future mapping agent.

- **Item:** `<path | pattern | unit>`
    - **Issue:** <What is misleading>
    - **Handling Rule:** <How the agent should treat it>

- **Item:** `<path | pattern | unit>`
    - **Issue:** <What is misleading>
    - **Handling Rule:** <How the agent should treat it>

---

## Directories to Ignore or Deprioritize

- **Path:** `<path>`
    - **Reason:** <Why it is normally not useful for mapping>

- **Path:** `<path>`
    - **Reason:** <Why it is normally not useful for mapping>

---

## Evidence Hierarchy

Default evidence order:

1. observed source
2. representative production code
3. representative tests or examples
4. owner weighting and repository addendum guidance
5. naming hints and comments

Adjust only when this repository clearly requires a different hierarchy.

---

## Optional Manifest Guidance

Create:

```text
.bonsai/maps/manifest.tsv
```

when:

- subsystem boundaries are clear enough to enumerate
- subsystem-to-source-root mapping will be reused
- later mapping passes benefit from a stable registry

Keep it compact and deterministic.

Suggested columns:

```tsv
subsystem	owning_path	role	notes
```

---

## Optional Symbol Index Guidance

Create:

```text
.bonsai/maps/symbol_index.tsv
```

only when agents repeatedly waste time locating important symbols.

Keep it selective. Include only symbols that are:

- central
- frequently searched
- cross-boundary
- expensive to rediscover

Suggested columns:

```tsv
symbol	kind	subsystem	path	notes
```

---

## Open Repository-Specific Questions

1. <Question>
2. <Question>
3. <Question>