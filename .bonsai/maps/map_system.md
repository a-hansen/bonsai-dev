# Bonsai Map System

**[Meta: Human-owned | Durable Map-System Truth | File Model, Workflow, and Editing Rules]**

## Purpose

Define the Bonsai code-mapping system:

* target file set
* map layers
* artifact responsibilities
* mapping workflow
* build order
* prioritization rules
* evidence discipline
* editing rules
* compression rules
* completion criteria
* drift prevention

This file defines how the mapping system works.
It does not contain repository-specific facts or current mapping state.

This file should be loaded when an agent is **editing Bonsai code-map artifacts**.
It should not be loaded merely to use existing maps during normal implementation work.

---

## Memory Root

Canonical map root:

```text
.bonsai/maps/
```

All Bonsai code-map files live under this directory unless explicitly stated otherwise.

---

## File Set

### Control files

* `repo_prompt.md`
* `map_prompt.md`
* `map_system.md`
* `map_repo.md`
* `map_state.md`

### Templates

* `templates/map_repo_template.md`
* `templates/map_state_template.md`
* `templates/code_map_template.md`
* `templates/subsystem_map_template.md`
* `templates/api_pub_template.md`
* `templates/api_ext_template.md`
* `templates/namespace_router_template.tsv`
* `templates/manifest_template.tsv`
* `templates/symbol_index_template.tsv`

### Layer 1: Repository compass

* `code_map.md`

### Layer 2: Subsystem architecture maps

* `subsystems/<subsystem>/map.md`

### Layer 3: Lazy-loaded coding mechanics

* `subsystems/<subsystem>/api_pub.md`
* `subsystems/<subsystem>/api_ext.md`

### Optional lookup artifacts

* `namespace_router.tsv`
* `manifest.tsv`
* `symbol_index.tsv`

---

## Control File Responsibilities

### `repo_prompt.md`

**Purpose:** Web UI prompt for producing or refreshing repository calibration.

Use this to help a human work with an AI conversation to synthesize:

```text
map_repo.md
```

It defines the repo-calibration workflow, not the durable map-editing rules.

---

### `map_prompt.md`

**Purpose:** CLI prompt for running a mapping session.

It should:

* initialize the mapping workspace when needed
* load `map_system.md`, `map_repo.md`, `map_state.md`, and existing top-level map artifacts as needed
* determine the best next mapping step
* present the startup gate to the human
* wait for explicit human approval or redirection before substantive mapping work begins
* update `map_state.md` after the approved work is completed
* define the mapping-session response style

It should not duplicate the durable artifact-editing rules defined in this file.

---

### `map_system.md`

**Purpose:** Canonical system document for editing Bonsai map artifacts.

This file owns:

* the map file model
* layer boundaries
* template-use rules
* evidence discipline
* subsystem selection and mapping order
* artifact maintenance rules
* compression discipline
* completion standards
* drift prevention
* the rules that apply whenever an agent edits map artifacts

Any agent that creates, updates, compresses, or maintains Bonsai map artifacts should follow this file.

---

### `map_repo.md`

**Purpose:** Human-owned repository calibration.

It may define:

* source roots
* major build or packaging boundaries
* owner priorities
* known architectural distinctions
* candidate subsystems
* paths to ignore or deprioritize
* practical evidence sources such as tests, examples, or production call sites
* repo-specific caveats that should shape mapping attention

`map_repo.md` is guidance, not proof.
Observed source, tests, examples, and build artifacts remain the source of truth.

---

### `map_state.md`

**Purpose:** Agent-maintained baton pass for mapping work.

It should stay short and practical.

It should record:

* current mapping objective
* active pass or focus
* recently confirmed findings needed for handoff
* unresolved uncertainties that matter for the next session
* exact next mapping step
* success condition for that next step
* recommended AI level for the next mapping session

It is current working state, not a knowledge database or work log.

---

## Layer Responsibilities

### `code_map.md`

**Purpose:** First-load orientation and routing.

Should answer:

* What are the major subsystems?
* What broad boundaries shape the repository?
* Where does execution or integration enter?
* Which subsystem map should I read next?
* Which high-value package or namespace prefixes materially improve first-pass routing?

Must remain compact.

It may include a **small, curated, high-value package or namespace router** when that improves first-load
orientation. It must not become the full package or namespace registry.

When broader package or namespace ownership lookup is useful, the fuller table belongs in:

```text
namespace_router.tsv
```

It must also tell agents that are **editing Bonsai code-map artifacts** to read:

```text
.bonsai/maps/map_system.md
```

That instruction belongs in `code_map.md` because `code_map.md` is the map artifact most likely to be
available to implementation agents that later need to update the maps after changing code.

---

### `namespace_router.tsv`

**Purpose:** Optional lazy-loaded fuller package or namespace ownership lookup.

Create this when package or namespace routing is useful, but a reasonably complete router would make
`code_map.md` too large for startup orientation.

It should help agents answer:

* Which subsystem most likely owns this package or namespace?
* Which path, source root, or module is the best first location to inspect?
* Are there short disambiguation notes that prevent common routing mistakes?

Recommended columns:

```tsv
namespace_prefix	subsystem	owning_path_or_module	notes
```

Use stable package or namespace prefixes, not every leaf symbol.
Prefer rows that improve routing decisions.
Do not turn this into a universal source inventory.

This file is lazy-loaded. It is not required for normal startup unless the current task needs fuller
package or namespace ownership lookup.

---

### `subsystems/<subsystem>/map.md`

**Purpose:** Durable architectural map for one subsystem.

Should answer:

* What does this subsystem own?
* Why does it matter?
* What major abstractions shape it?
* What are the key workflows?
* Where are the extension seams?
* What areas are risky or easy to misunderstand?
* Which API maps should be loaded when writing code?

Must remain architectural.
It should not become a local encyclopedia.

When API maps exist, `map.md` may name an important caller or extension seam and summarize why it matters,
but exact usage mechanics, registration rules, signatures, and reusable coding patterns belong in
`api_pub.md` or `api_ext.md`.

Subsystem boundaries should reflect durable architectural domains.
Modules, packages, source roots, and subprojects are evidence, but they are not automatically the correct
subsystem boundary.

A subsystem should exist because it captures a meaningful architectural responsibility that improves
future implementation reasoning. Do not create subsystem maps merely by translating top-level folders,
modules, source roots, or package groups into map names.

Before promoting a candidate subsystem, verify that it has at least one of these qualities:

* a coherent domain responsibility
* durable ownership boundaries
* distinct lifecycle, data, or execution concerns
* reusable public or extension mechanics
* meaningful cross-boundary interactions future agents need to reason about
* enough implementation relevance that mapping it will reduce repeated confusion

If a repository structure unit does not clear that bar, it may still belong in routing or lookup
artifacts without becoming its own subsystem map.

---

### `subsystems/<subsystem>/api_pub.md`

**Purpose:** Caller-facing mechanics.

Use when future agents are likely to repeatedly need the same non-obvious information to call, query,
retrieve, configure, or consume the subsystem correctly.

Examples:

* service lookup pattern
* query syntax
* cursor lifecycle
* required parameter conventions
* event subscription pattern
* failure modes callers commonly mishandle

Each major API-map entry should make clear:

* When to use this surface
* What exact behavior, contract, or constraint matters
* What caller pattern is canonical, when a repeatable pattern exists

Must be lazy-loaded.

It should preserve **decision-ready mechanics**, not merely enumerate that an API exists.

---

### `subsystems/<subsystem>/api_ext.md`

**Purpose:** Extension-facing mechanics.

Use when future agents are likely to repeatedly need the same non-obvious information to subclass,
implement, register, contribute, or extend the subsystem correctly.

Examples:

* registration pattern
* required lifecycle hooks
* mandatory super-calls
* event firing rules
* identity or synchronization constraints
* expected implementation shape

Each major API-map entry should make clear:

* When to use this surface
* What exact behavior, contract, or constraint matters
* What extension pattern is canonical, when a repeatable pattern exists

Must be lazy-loaded.

It should preserve **decision-ready mechanics**, not merely enumerate that an extension point exists.

---

### `manifest.tsv`

**Purpose:** Optional compact subsystem registry.

Create only when:

* the repo is large enough that subsystem or source-root enumeration will be reused
* mapping will occur over multiple sessions
* semi-automated mapping passes benefit from a stable subsystem list

It should be a terse lookup table, not prose.

Recommended columns:

```tsv
subsystem	owning_path	role	notes
```

Do not let it become a second `code_map.md`.

---

### `symbol_index.tsv`

**Purpose:** Optional selective symbol lookup accelerator.

Create only when agents repeatedly waste time locating important symbols, ownership, or defining
files.

It should be a terse lookup table, not prose.

Recommended columns:

```tsv
symbol	kind	subsystem	path	notes
```

This is **not** a universal repository symbol inventory.
It is a curated routing aid for symbols whose location or ownership is repeatedly useful to future
agents.

Do not index every symbol. Add only symbols that are:

* central
* frequently searched
* cross-boundary
* expensive to rediscover
* unusually easy to confuse with nearby concepts
* valuable as anchors for future code inspection

Do not create it by default.
Do not attempt to reproduce `ctags`, IDE indexing, language-server lookup, or exhaustive static analysis
through a hand-maintained map artifact.

---

## Lookup Artifact Formatting

The TSV lookup artifacts are intentionally compact, flat tables:

```text
namespace_router.tsv
manifest.tsv
symbol_index.tsv
```

They are optimized for:

* low token cost
* fast human scanning
* simple machine validation when tooling is added
* lightweight lazy loading by future agents

When creating or updating any TSV artifact:

1. Preserve the exact header row and column order defined by its template or current file.
2. Use **literal tab characters** between columns, not spaces.
3. Keep exactly one logical record per physical line.
4. Do not create multiline cells.
5. Do not add ad hoc columns.
6. Keep notes concise and single-line.
7. Avoid tab characters, newline characters, or formatting that would break the row shape inside cell values.
8. Preserve terse lookup-table style. Do not turn a cell into a paragraph.
9. If a value does not fit cleanly into the fixed TSV shape, summarize it more tightly or move the richer explanation into the appropriate Markdown map artifact.
10. When materially editing TSV artifacts, perform a quick structural self-check before finishing:

    * header preserved
    * row column counts consistent
    * separators remain tabs
    * no accidental prose blocks or wrapped multiline records

TSV files should remain strict lookup artifacts. Their discipline is part of their value.

---

## Template Responsibilities

Templates constrain document shape when new artifacts are created.

| Template                                  | Generated artifact                  |
| ----------------------------------------- | ----------------------------------- |
| `templates/map_repo_template.md`          | `map_repo.md`                       |
| `templates/map_state_template.md`         | `map_state.md`                      |
| `templates/code_map_template.md`          | `code_map.md`                       |
| `templates/subsystem_map_template.md`     | `subsystems/<subsystem>/map.md`     |
| `templates/api_pub_template.md`           | `subsystems/<subsystem>/api_pub.md` |
| `templates/api_ext_template.md`           | `subsystems/<subsystem>/api_ext.md` |
| `templates/namespace_router_template.tsv` | `namespace_router.tsv`              |
| `templates/manifest_template.tsv`         | `manifest.tsv`                      |
| `templates/symbol_index_template.tsv`     | `symbol_index.tsv`                  |

When creating a new mapping artifact:

1. consult the corresponding template
2. follow its established structure
3. fill only the sections justified by the current work
4. create optional artifacts only when the criteria in this file justify them

The presence of a template does not imply that its corresponding optional artifact should always be
created.

When updating an existing artifact:

* preserve its established structure unless a template-alignment cleanup is explicitly part of the work
* do not rewrite structure merely because the template has evolved
* improve the current artifact in place unless the human explicitly requests a broader normalization pass

---

## Evidence Discipline

Maps should distinguish durable findings from plausible interpretation.

Use these labels when non-obvious claims matter:

* **Observed:** Confirmed directly from source, tests, examples, build files, or other concrete repository evidence.
* **Inferred:** Reasoned from observed structure, but not directly established.
* **Uncertain:** Plausible, but should not be relied on until confirmed.

Evidence labels are most useful when documenting:

* subsystem ownership
* lifecycle behavior
* extension contracts
* cross-subsystem flows
* non-obvious developer workflows
* package or namespace ownership where the boundary is not obvious
* risky areas that are easy to misread

Use repo guidance as bias, not proof.

`map_repo.md` may prioritize where to look or reflect owner judgment, but observed source wins when the
repository contradicts the calibration document.

Avoid overstating.
A useful map that says “Uncertain” is better than a confident map that teaches future agents the wrong
thing.

---

## General Editing Rules

1. **Preserve real repository structure.**
   Respect actual modules, packages, services, runtime splits, UI splits, tooling boundaries, and
   extension surfaces.

2. **Keep layers distinct.**

    * `code_map.md` = orientation and routing
    * `subsystems/<subsystem>/map.md` = subsystem architecture
    * `api_pub.md` / `api_ext.md` = lazy-loaded coding mechanics
    * `namespace_router.tsv` = optional fuller namespace ownership lookup
    * `manifest.tsv` = optional compact subsystem registry
    * `symbol_index.tsv` = optional selective symbol locator

3. **Keep `code_map.md` startup-sized.**
   It may include only a concise, high-value package or namespace router.
   If broader package or namespace lookup is worth preserving, use `namespace_router.tsv` rather than
   expanding `code_map.md` into a registry.

4. **Do not turn maps into documentation bloat.**

    * no exhaustive file inventories
    * no full API handbooks
    * no method dumps unless a small set of signatures is essential to prevent repeated errors
    * no duplication of material that belongs in another map layer or lookup artifact

5. **Prefer durable navigation over exhaustive extraction.**
   Preserve what future agents are likely to reuse across implementation sessions.

6. **Do not assume modules, subprojects, source roots, packages, or directories are the subsystem boundaries.**
   Use them as evidence, but map architectural domains at the level that best supports future
   implementation work.

   A candidate subsystem should be justified by durable architectural responsibility, not by repository
   layout alone. If a proposed subsystem is merely a folder, Gradle module, package cluster, or source
   root restated as a map boundary, reconsider it.

7. **Use TSV lookup artifacts only within their strict flat-table format.**

    * fixed headers
    * literal tab separators
    * one record per line
    * no multiline cells
    * no ad hoc column invention
    * concise lookup notes only

   Rich explanation belongs in Markdown map artifacts, not TSV cells.

8. **Treat `symbol_index.tsv` as a selective routing aid, not an exhaustive symbol inventory.**

   Add symbols only when they materially improve future orientation or repeated lookup. Do not use the
   file to mirror everything a language server, IDE index, or generated symbol database could provide.

9. **API maps should preserve decision-ready mechanics.**

   They should clarify:

    * when to use a surface
    * what exact rule prevents mistakes
    * what canonical calling or extension pattern should be reused, when one exists

10. **Update dependent map files together.**
    If a mapping change alters top-level routing, lookup support, or current mapping status, update the
    affected related artifacts in the same pass.

11. **Finish the active subsystem before moving to another subsystem.**
    After creating or refreshing `subsystems/<subsystem>/map.md`, immediately evaluate whether
    `api_pub.md` and/or `api_ext.md` are justified for that subsystem. Create or refresh those API maps
    when warranted before selecting a different subsystem.

12. **Do not casually rewrite mapping-control files.**
    Do not modify:

    ```text
    map_prompt.md
    map_system.md
    map_repo.md
    ```

    unless the human explicitly requests it.

13. **Code remains the source of truth.**
    Bonsai maps should point agents toward the right code with the right expectations, not replace
    source inspection.

---

## What Mapping Should Look For

Prioritize mapping evidence that materially improves future implementation sessions.

Look for:

* source roots and build or packaging boundaries
* major runtime surfaces
* major subsystems and ownership boundaries
* central abstractions
* public service APIs
* extension seams
* registries
* factories
* trackers
* coordinators
* dispatchers
* lifecycle patterns
* cross-subsystem flows
* practical developer workflows
* non-obvious rules likely to affect correct implementation
* areas the repository owner explicitly weights highly
* package or namespace ownership cues that materially improve routing decisions
* risky-to-change systems
* areas with frequent AI confusion or misimplementation risk

Deprioritize:

* narrow helpers
* low-value utility classes
* generated code
* shallow symbol inventories
* purely incidental implementation detail
* domain-specific one-off code unless it establishes a reusable pattern
* package or namespace rows that do not improve routing or disambiguation
* details that source inspection reveals immediately and reliably

---

## Recommended Build Order

### Pass 0: Repository Calibration

Create or refresh:

```text
map_repo.md
```

This is typically done before coding-agent mapping begins.

Recommended path:

1. Use a Web UI AI conversation to discuss the repository.
2. Paste:

    * `repo_prompt.md`
    * `templates/map_repo_template.md`
3. Copy the generated `map_repo.md` into `.bonsai/maps/`.

Manual authoring is also valid when the repository owner already knows exactly what to write.

---

### Pass 1: Repository Orientation

Create or refresh:

1. `code_map.md`
2. `map_state.md`

Optionally create:

3. `manifest.tsv`
4. `namespace_router.tsv`, only if meaningful package or namespace routing exists and the fuller lookup
   would be valuable without belonging in `code_map.md`
5. `symbol_index.tsv`, only if a real early lookup need exists

Goal:

* establish source roots
* establish build or packaging boundaries
* identify major subsystem candidates
* distinguish architectural subsystem candidates from merely visible repository layout
* identify likely first drill-down targets
* preserve only the highest-value namespace hints in `code_map.md`
* externalize broader package or namespace lookup when it would otherwise bloat `code_map.md`

---

### Pass 2: Priority Subsystem Mapping Cycles

Map one subsystem at a time.
For each selected subsystem, complete the subsystem map and any justified API maps **before moving to another subsystem**.

For the active subsystem:

1. Create or refresh:

```text
subsystems/<subsystem>/map.md
```

2. Immediately evaluate whether reusable coding mechanics justify:

```text
subsystems/<subsystem>/api_pub.md
subsystems/<subsystem>/api_ext.md
```

3. Create or refresh those API maps when warranted.

4. Update:

    * `map_state.md`
    * `code_map.md`, only if top-level routing or drill-down guidance changed
    * `namespace_router.tsv`, only if package or namespace ownership lookup materially changed or became worth preserving
    * `manifest.tsv`, only if subsystem registry facts changed
    * `symbol_index.tsv`, only if the selective lookup set materially improves

5. Only then select the next subsystem.

Selection priority:

1. owner-weighted in `map_repo.md`
2. architecturally foundational
3. developer-facing
4. cross-boundary
5. widely reused
6. risky to change or easy to misunderstand

Goal:

* build complete reusable memory for the highest-value subsystem areas first
* avoid leaving core subsystems architecturally mapped but API-empty while moving on to fringe areas

---

### Pass 3: Calibration

Validate or correct maps using:

* representative production code
* realistic examples
* tests
* owner-identified hot spots
* observed call sites
* observed extension patterns

Goal:

* distinguish theoretical architecture from how the repo is actually used

Calibration may cause updates to:

* subsystem maps
* API maps
* `code_map.md`
* `namespace_router.tsv`
* `map_state.md`

---

### Pass 4: Maintenance After Code Changes

Update shared maps only when the code change alters durable reusable memory, such as:

* public structure
* extension points
* lifecycles
* major architectural relationships
* rebuild-relevant behavior
* recurring non-obvious calling or extension mechanics
* broader package or namespace ownership guidance worth preserving

Do not update maps for routine local implementation changes.

When maintaining maps for a changed subsystem:

1. Update the subsystem map if durable architectural understanding changed.
2. Re-evaluate its API maps if reusable calling or extension mechanics changed.
3. Update `code_map.md` only if top-level orientation or first-load routing changed.
4. Update `namespace_router.tsv` only if fuller package or namespace ownership lookup changed materially.
5. Update `manifest.tsv` only if subsystem registry facts changed.
6. Update `symbol_index.tsv` only if the selective lookup set materially improves.
7. Update `map_state.md` when mapping work status or next mapping direction changes.

---

### Pass 5: Cleanup and Compression

Use cleanup or compression passes when map artifacts have drifted into:

* excessive length
* duplicated guidance
* wrong-layer content
* stale lookup rows
* subsystem maps that have become API manuals
* API maps that have become broad reference docs
* `map_state.md` that has become a work log
* top-level routing that has grown beyond startup usefulness

Goal:

* restore map artifacts to their intended role
* keep reusable memory compact
* remove duplication without deleting durable guidance future agents still need

Cleanup work should follow the compression discipline in this file.

---

## Compression Discipline

When a map file grows, prefer cutting before adding.

### `code_map.md`

Cut:

* long repository tours
* deep subsystem explanations
* large build detail sections
* information already captured by `map_repo.md`, `manifest.tsv`, or `namespace_router.tsv`
* low-value package or namespace router rows that do not materially improve first-load orientation

Keep:

* top-level repository compass
* major subsystem boundaries
* first drill-down routing
* small, high-value orientation cues
* explicit pointer to `map_system.md` for agents editing maps

---

### `namespace_router.tsv`

Cut:

* prefixes that do not improve routing decisions
* rows that merely restate obvious source paths
* excessive leaf-package fragmentation
* notes that become prose mini-documentation
* malformed or overstuffed rows that no longer behave like clean lookup data

Keep:

* stable prefixes
* ownership cues that reduce routing mistakes
* first-inspection paths or modules when materially useful
* terse disambiguation notes
* strict one-line TSV row structure

---

### `subsystems/<subsystem>/map.md`

Cut:

* exhaustive package inventories
* implementation walkthroughs better left to source
* API signature detail better suited to `api_pub.md` or `api_ext.md`
* local mechanics that matter only once

Keep:

* subsystem scope
* central abstractions
* recurring workflows
* extension seams
* sharp edges
* architectural relationships future agents are likely to need again

---

### API Maps

Cut:

* full interface dumps
* trivial getters or setters
* background architecture prose
* mechanics that are obvious from a single source read and unlikely to be repeatedly misused
* content that belongs in the subsystem architecture map

Keep:

* exact usage or extension rules that prevent mistakes
* recurring caller patterns
* registration or lifecycle mechanics
* compact signatures or snippets only where they remove repeated ambiguity

---

### `manifest.tsv`

Cut:

* prose-like notes
* registry detail that does not improve future mapping work
* duplicated guidance already in `code_map.md`
* rows or notes that violate compact single-line TSV discipline

Keep:

* compact subsystem registry facts
* concise owning paths
* short role or disambiguation notes only where useful
* strict one-line TSV row structure

---

### `symbol_index.tsv`

Cut:

* symbols that are easy to locate
* leaf-level local symbols
* entries that no longer justify maintenance cost
* rows that attempt exhaustive coverage instead of selective orientation value
* notes that over-explain instead of pointing efficiently

Keep:

* central symbols
* cross-boundary symbols
* frequently searched symbols
* symbols that are costly to rediscover
* symbols that act as strong anchors for future source inspection
* strict one-line TSV row structure

---

### `map_state.md`

Cut:

* stale session history
* verbose findings that belong in maps
* general observations no longer needed for handoff
* abandoned or superseded next-step ideas

Keep:

* the current baton pass
* the most recent confirmed findings needed for continuation
* unresolved uncertainties that matter next
* the exact next mapping step
* the recommended AI level for the next mapping session

---

## Done Criteria

### `code_map.md`

Done when it:

* fits first-load orientation
* identifies major subsystem boundaries
* identifies major entry points or integration surfaces when relevant
* gives useful drill-down routing
* includes only a compact, high-value package or namespace router when that materially improves navigation
* points to `namespace_router.tsv` when fuller routing exists and may be useful
* stays compact enough to remain safe as a startup read
* tells agents editing Bonsai map artifacts to read `map_system.md`
* makes clear that `map_system.md` is not a normal implementation-time dependency

---

### `namespace_router.tsv`

Done when it:

* provides useful fuller package or namespace ownership lookup without bloating `code_map.md`
* maps prefixes to likely owning subsystems and useful first-inspection paths or modules
* includes only terse notes that improve routing decisions
* remains lookup data, not prose documentation
* preserves a strict single-line TSV table shape
* avoids attempting exhaustive universal source coverage unless the repository structure genuinely makes
  that both compact and useful

---

### `subsystems/<subsystem>/map.md`

Done when it:

* defines subsystem scope
* identifies owning code units
* explains why the subsystem matters
* captures the central abstractions
* summarizes the key recurring workflows
* identifies extension seams and risky areas
* links to relevant API maps when they exist
* avoids collapsing into implementation documentation
* reflects an architectural responsibility, not merely a repository folder or build unit relabeled as a subsystem

---

### `subsystems/<subsystem>/api_pub.md`

Done when it:

* captures the non-obvious mechanics needed to call or consume the subsystem safely
* includes minimal exact signatures or snippets only where they prevent repeated error
* includes practical examples when they clarify the expected pattern
* avoids becoming a general API reference
* makes it clear when a future agent should use the described surface, not merely that the surface exists

---

### `subsystems/<subsystem>/api_ext.md`

Done when it:

* captures the non-obvious mechanics needed to extend or implement the subsystem safely
* documents required hooks, registration, lifecycles, and sharp edges when relevant
* includes minimal examples when they prevent common mistakes
* avoids becoming a general implementation guide
* makes it clear when a future agent should use the described surface, not merely that the surface exists

---

### `manifest.tsv`

Done when it:

* provides a compact reusable subsystem-to-path registry
* supports future mapping passes without repeating repository enumeration
* uses short roles and notes only where they improve lookup
* preserves a strict single-line TSV table shape
* does not duplicate the richer guidance in `code_map.md`

---

### `symbol_index.tsv`

Done when it:

* improves lookup for central, cross-boundary, frequently searched, or costly-to-rediscover symbols
* stays selective
* points future agents to the most useful defining path
* preserves a strict single-line TSV table shape
* avoids becoming a manually maintained universal symbol database

---

### `map_state.md`

Done for a mapping pass when it:

* records the current mapping objective
* identifies the active pass or focus
* captures only the most recent confirmed findings needed for handoff
* captures unresolved uncertainties
* identifies the exact next mapping step
* states the success condition for that next step
* recommends the AI level for the next mapping session
* stays short enough to be read at every mapping-session startup

---

## Update Triggers

### Update `repo_prompt.md` when

* the Web UI repo-calibration workflow changes
* the desired synthesis behavior for `map_repo.md` changes

### Update `map_prompt.md` when

* mapping-session startup behavior changes
* startup-gate behavior changes
* human approval or redirect behavior changes
* session output formatting changes
* the CLI mapping workflow changes in a way that is not durable map-system doctrine

### Update `map_system.md` when

* file taxonomy changes
* subsystem or API mapping order changes
* package or namespace routing policy changes
* prioritization logic changes
* evidence discipline changes
* compression rules change
* done criteria change
* map-system philosophy changes
* edit-time map-maintenance rules change

### Update `map_repo.md` when

* repository structure becomes clearer
* source roots or build units change
* owner priorities change
* ignore paths change
* practical calibration sources change
* repository-specific caveats change

### Update `map_state.md` when

* a meaningful mapping pass completes
* active focus changes
* a major uncertainty resolves
* the next exact mapping step changes
* the recommended AI level for the next session changes

### Update `code_map.md` when

* the top-level subsystem view changes
* first-load routing guidance changes
* high-value package or namespace routing changes materially
* drill-down order changes materially
* edit-time guidance for code-map maintainers changes

### Update `namespace_router.tsv` when

* broader package or namespace ownership lookup changes materially
* a new prefix meaningfully improves routing
* an existing prefix becomes misleading, stale, or too granular
* routing detail should move out of `code_map.md` to keep first-load orientation compact
* malformed row structure or overgrown notes need correction

### Update `subsystems/<subsystem>/map.md` when

* durable architectural understanding changes materially
* the current map boundary proves to mirror repository layout more than architectural responsibility

### Update API maps when

* reusable caller or extension mechanics are discovered, corrected, simplified, or invalidated

### Update `manifest.tsv` when

* subsystem registry facts change
* owning paths change
* short role or disambiguation notes need correction
* malformed row structure or overgrown notes need correction

### Update `symbol_index.tsv` when

* a central indexed symbol moves
* a listed lookup becomes stale
* a new symbol clears the selective inclusion bar
* an existing symbol no longer justifies inclusion
* the file begins drifting toward exhaustive inventory rather than selective routing value
* malformed row structure or overgrown notes need correction

---

## Prioritization Rules

Prioritize:

* foundational abstractions
* owner-weighted areas
* public service APIs
* practical extension seams
* cross-boundary infrastructure
* developer workflows that recur
* risky-to-change systems
* areas with frequent AI confusion or misimplementation risk
* registries, coordinators, dispatchers, and lifecycle controls that shape real work
* package or namespace ownership cues that materially improve routing decisions

Deprioritize:

* narrow helpers
* leaf utilities
* generated code
* sample-only patterns that are not representative
* internal machinery with little developer relevance
* shallow inventories
* detail that source inspection reveals immediately and reliably
* package or namespace rows that do not materially improve lookup or disambiguation

---

## Drift Prevention

Watch for:

* `code_map.md` becoming a repo encyclopedia
* the high-value package or namespace router in `code_map.md` growing into a large registry
* `namespace_router.tsv` becoming a universal source inventory rather than a routing aid
* lookup TSVs accumulating malformed rows, extra columns, multi-line cells, prose-like notes, or space-separated pseudo-tables
* subsystem maps becoming API manuals
* subsystem boundaries collapsing into directory, package, source-root, or build-unit mirrors without architectural justification
* API maps becoming exhaustive reference documentation
* `map_state.md` becoming a work log or knowledge database
* `manifest.tsv` becoming a second code map
* `symbol_index.tsv` becoming a hand-maintained ctags clone or universal symbol database
* repeated coding mechanics across `map.md` and API maps
* subsystem maps being completed while corresponding justified API maps are indefinitely deferred
* agents loading `map_system.md` during normal implementation reads instead of only when editing map artifacts
* stale assumptions surviving after code inspection
* repo-owner guidance being treated as proof when source evidence disagrees
* optional artifacts being created merely because templates exist
* structural rewrites of existing artifacts during routine updates without explicit need

When API maps exist, the subsystem map should retain only the architecture-level summary and direct future
agents to the API map for coding mechanics.

---

## Naming Rules

### Subsystem Directories

Use stable architectural domain names:

```text
subsystems/runtime/
subsystems/history/
subsystems/driver/
subsystems/security/
```

Prefer domain names over incidental package or module names unless the package or module is the true
architectural boundary.

Subsystems are architectural domains, not build units.
One build unit may produce multiple subsystem maps. One subsystem may span multiple build units.

A subsystem name should reflect the durable responsibility being mapped, not merely the most obvious
folder, source root, package prefix, or module label encountered during orientation.

---

### Standard Files Inside a Subsystem

```text
map.md
api_pub.md
api_ext.md
```

This keeps related subsystem memory grouped in directory listings and avoids top-level filename
sprawl.

---

### Lookup Artifacts

Use TSV for compact structured support data:

```text
namespace_router.tsv
manifest.tsv
symbol_index.tsv
```

These are optional lookup tables, not Markdown narrative documents.

They must preserve strict flat-table discipline:

* fixed columns
* literal tabs
* one record per line
* no multiline cells
* concise single-line notes

---

## Operating Stance

* Bonsai mapping is incremental, not a big-bang repo dump.
* A subsystem is not really done enough to move past until its architecture map is complete and its
  API-map need has been evaluated.
* `code_map.md` should preserve first-load orientation, not absorb every useful lookup table.
* Full or fuller namespace routing belongs in `namespace_router.tsv` when it would otherwise bloat the
  code map.
* `symbol_index.tsv` should remain a selective semantic routing aid, not an exhaustive source-derived
  database.
* Lookup TSVs should remain compact, strict, and structurally boring.
* Smaller reusable memory beats larger impressive memory.
* Maps should reduce repeated confusion, not document everything.
* Repo calibration should guide attention, not override observed evidence.
* Uncertainty should be marked rather than hidden.
* Code remains the source of truth.
* Bonsai maps should point agents toward the right code with the right expectations.
