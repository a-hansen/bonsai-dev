# Code Maps

## Purpose

Create, inspect, update, rebuild, remove, and use selective source-navigation maps through Bonsai's normal
identity, menu, context, and human-gate model.

Maps describe actual source. They are reusable navigation aids, not source authority, project truth, project
execution memory, or exhaustive documentation.

## When to Load

Load this skill only when:

- the human selects **Manage Code Maps**;
- an explicit startup request asks for a code-map action;
- current implementation needs map-guided navigation or map/source alignment checking;
- the human accepts a contextual first-use mapping action for substantial existing source; or
- the human accepts bounded maintenance after a known material structural source change.

Do not load the editing workflow merely because a map exists, and do not treat routine source edits as map
maintenance. Ordinary map consumption reads `code_map.md` first and only the deeper artifact needed for the current
facet.

## Authority and Boundaries

Use these authorities in order:

1. actual selected source, including its build files, tests, examples, and representative uses;
2. approved project final truth and archaeological analysis as attention and interpretation context;
3. optional human-owned `map_repo.md` as source-specific calibration;
4. existing map data as navigation memory that must remain aligned with source.

Project memory and `map_repo.md` may guide where to look, but they do not prove source behavior or determine map
identity. When they disagree with observed source, source wins and the mismatch remains visible until corrected.

Do not require a Bonsai project for source mapping. Do not create project memory merely to map an external source.
Do not put active project, phase, pass, approval, requirement-tracking, icebox, or session status into map data.

## Runtime Map Model

Resolve the active map store from the session identity supplied by `start.md`:

- when a configured Bonsai Home is active: `<bonsai-home>/maps/`;
- for Embedded Bonsai without a configured external home: `<repository-home>/.bonsai/maps/`.

Resolve that store independently from the source location. Mapping source in another repository, directory, or
archive does not place output beside that source by default.

Several projects may reuse one named source map, and one project may select several relevant source maps. Do not
duplicate a map per consuming project or treat the active project's name as the map identity.

Each named source map may contain:

```text
<map-store>/<source>/
    map_repo.md                       # Optional, human-owned calibration
    code_map.md                       # Required entry for a usable map
    map_state.md                      # Optional active mapping continuation
    namespace_router.tsv              # Optional fuller namespace routing
    manifest.tsv                      # Optional subsystem/path registry
    symbol_index.tsv                  # Optional selective symbol routing
    subsystems/<subsystem>/map.md
    subsystems/<subsystem>/api_pub.md # Optional caller mechanics
    subsystems/<subsystem>/api_ext.md # Optional extension mechanics
```

Write runtime map data only beneath the resolved active map store. Never instantiate a template back into the
Bonsai standard, write generated map data into a staged distribution, or treat a standard template as runtime map
state.

The named source directory is a storage boundary, not a blanket ownership boundary. Map lifecycle operations own
only agent-owned map artifacts they actually create or manage. They never own `map_repo.md`, a supplied source
archive, source checkout, or another colocated file merely because it is under that directory.

## Resolve the Mapping Context

Before proposing substantive mapping work, resolve only enough context to make the action and gate trustworthy:

1. Retain the invoking Bonsai workflow or gate so this subordinate workflow can return to it.
2. Resolve the active map store without creating or modifying it.
3. Resolve the requested lifecycle action. If none was supplied, present the action menu below.
4. Identify the actual source independently from the active project:
   - logical source name;
   - source type, such as repository checkout, released source archive, or supplied source tree;
   - exact source location;
   - version, Git revision, artifact coordinate, checksum, or other smallest useful snapshot evidence.
5. Resolve the proposed map identity from the source universe, not the consuming project. Never silently derive a
   map name when several identities or snapshots are plausible.
6. Inspect only the named map entry or directory metadata needed to determine whether the map exists, whether its
   identity aligns, and which files are map-owned. A colocated non-map file does not prove a map exists.
7. Read relevant project memory or `map_repo.md` only when it can materially calibrate the selected action.
8. Load `skills/agent_context.md` only when stable source locations, relevant map selection, or another qualifying
   operational rule may need to be applied or maintained.

If the source location, map store, map identity, source snapshot, or ownership boundary remains materially
ambiguous, stop and ask the human to resolve it. Do not invent a source resolver, downloader, registry, manifest
schema, dependency-to-map matcher, or source-location convention.

If **Create Code Map** resolves to an existing usable `code_map.md`, do not overwrite it as creation. Offer a
bounded update, a separately gated rebuild, or a distinct source identity as appropriate.

## Lifecycle Action Menu

When the human has entered **Manage Code Maps** without selecting an action, load `skills/menu.md` and present only
the applicable choices:

1. Create Code Map.
2. Inspect Code Maps.
3. Update or Rebuild Code Map.
4. Remove Code Map.
5. Inspect Map/Source Identity.
6. Cancel and return to `<invoking gate>`.

If a choice is unavailable because its source, map, or store cannot be resolved, explain why instead of presenting
it as executable. Stop for the human's choice.

## Mapping Proposal Gate

Before substantive source inspection or any mutation, present:

- **Action:** selected lifecycle action;
- **Source:** logical name, type, location, and available snapshot identity;
- **Map identity:** selected named source map;
- **Map store / target:** resolved store and proposed map-owned target set;
- **Scope:** repository orientation, one named subsystem, API mechanics, calibration, maintenance, cleanup, or
  another concrete bound;
- **Alignment:** `Aligned`, `Mismatch`, `Insufficient evidence`, or `Not applicable for new map`;
- **Inputs:** actual source plus any project or human calibration that will be consulted;
- **Proposed next step:** one concrete action and why it is next;
- **Risks / uncertainties:** only those that can change the proposed action.

Load `skills/menu.md` and offer concrete choices to proceed, redirect scope or identity, discuss a material
ambiguity, or cancel and return to the invoking gate. Wait for explicit human direction.

Approval covers only the displayed action, source, map identity, scope, and non-destructive target set. It does not
authorize a later destructive rebuild, removal, scope expansion, source mutation, or high-cost optional index.

When the current mapping scope is already complete, say so and do not invent another objective merely to continue.

## Map and Source Alignment

`code_map.md` is the normal identity and routing entry. Use the smallest available evidence that prevents an
incompatible snapshot from being silently trusted.

Classify alignment as:

- **Aligned:** the map identity and selected source snapshot agree sufficiently for the intended use;
- **Mismatch:** available evidence shows a different version, revision, coordinate, source type, or artifact;
- **Insufficient evidence:** alignment cannot be established for a non-obvious claim;
- **Not applicable for new map:** no prior entry exists and creation will record identity from observed source.

On mismatch or insufficient evidence, do not rely on non-obvious map claims. Present concrete choices to inspect
the source, update the existing map, request a gated rebuild, select another map, select another source, or stop.
Do not assume an active development checkout matches a released dependency.

## Action: Create Code Map

After the proposal is approved:

1. Inspect actual source for orientation before deep mapping. Use build structure, representative source, tests,
   examples, and call sites only as needed for the approved scope.
2. Treat relevant project truth and optional `map_repo.md` as calibration, not source proof. Preserve material
   disagreements as uncertainty.
3. Resolve the exact map-owned files to create. Preserve every pre-existing human-owned or otherwise unowned file,
   including supplied source artifacts colocated with the target map.
4. Instantiate only justified artifacts from `<bonsai-home>/templates/`:
   - `code_map_template.md` for the required entry;
   - `map_state_template.md` only when active continuation benefits;
   - `subsystem_map_template.md` for each approved architectural subsystem;
   - `api_pub_template.md` and `api_ext_template.md` only when non-obvious reusable mechanics justify them;
   - `namespace_router_template.tsv`, `manifest_template.tsv`, and `symbol_index_template.tsv` only when their
     narrow lookup value exceeds maintenance cost.
5. Record the logical source and the smallest useful snapshot identity in `code_map.md`. Keep all drill-down links
   relative to the named source map.
6. Build one active subsystem at a time. Complete its architecture map and evaluate both API-map needs before
   moving to another subsystem.
7. When apparent design and actual use may differ, check at least one representative production use, test,
   example, call site, or extension before recording the mechanic as durable.
8. Update related routing and lookup artifacts together only when their contracted role is affected.
9. Validate the created artifacts under the structural and completion rules below.

Creating a map store or named source directory after approval does not transfer ownership of existing contents.
Template presence never authorizes optional output.

Before creating a costly optional artifact or materially expanding an optional index, show why its repeated
navigation value exceeds its maintenance cost, identify the exact output and scope, and stop for explicit human
approval.

## Action: Inspect Code Maps

Inspection is read-only.

1. For store-level inspection, list only plausible named maps and distinguish directories that lack `code_map.md`
   from usable maps. Do not treat arbitrary colocated files as generated map data.
2. For one map, load `code_map.md` first and verify alignment with the selected source when source-dependent claims
   matter.
3. Load only the subsystem, API, namespace, manifest, or symbol facet needed for the inspection question.
4. Use actual source to verify non-obvious behavior; report map claims as navigation, not authority.
5. Report missing, stale, mismatched, uncertain, or malformed data without changing it.

Inspection does not create `map_state.md`, normalize existing files, update identity metadata, or preserve context
unless the human separately authorizes the applicable action.

## Action: Update or Rebuild Code Map

First determine whether the requested work is a bounded update or a destructive rebuild.

### Bounded update

Use an update for known material changes to source identity, public structure, extension mechanics, lifecycle,
architectural relationships, subsystem ownership, rebuild-relevant behavior, or reusable routing.

1. Verify map/source alignment and the approved scope.
2. Improve existing artifacts in place. Preserve their established structure unless normalization was explicitly
   included in the approved scope.
3. Update only map-owned artifacts whose durable content changed.
4. Update dependent entry, subsystem, API, lookup, and active state artifacts together when their narrow roles are
   affected.
5. Re-check representative usage when a caller or extension mechanic changed.

Routine bug fixes, private refactors, tests, cosmetic cleanup, and ordinary churn do not justify map updates by
themselves. Bonsai does not continuously scan for drift or silently update maps after implementation work.

### Destructive rebuild

A rebuild requires a separate explicit gate after inspection, even when the broader **Update or Rebuild Code Map**
action was previously selected.

Before that gate:

1. resolve and display every existing agent-owned target that would be replaced or removed;
2. display every known preserved item, including `map_repo.md`, supplied source inputs, and other unowned files;
3. show the source snapshot, map identity, rebuild scope, proposed replacement artifacts, and validation plan; and
4. stop for explicit approval, revision, discussion, or cancellation.

After approval, replace only the displayed agent-owned targets. Never delete the named source directory as a
shortcut. Never move, rename, modify, or delete a supplied source artifact. If safe replacement cannot be completed
within the approved target set, stop with the existing unowned content preserved.

## Action: Remove Code Map

Removal is destructive and always requires its own explicit gate.

Before the gate:

1. inspect the selected named map without mutation;
2. resolve the exact agent-owned artifact paths proposed for removal;
3. distinguish and list preserved human-owned calibration, supplied source inputs, and other unowned files;
4. report ambiguity rather than claiming ownership from directory location; and
5. show the exact verification that will confirm preserved files remain unchanged.

Load `skills/menu.md` and offer approval of the exact removal target set, revision of that set, discussion, or
cancellation and return. Stop for explicit approval.

After approval, remove only the displayed map-owned artifacts. Do not recursively delete the named source
directory. Verify the preserved target set still exists and that no transient inspection data entered the durable
map store. Report the map removed only when no usable agent-owned `code_map.md` remains for that selected map.

## Action: Inspect Map/Source Identity

This action is read-only.

1. read the selected map's identity from `code_map.md`;
2. inspect the selected source only enough to establish its logical and snapshot identity;
3. keep source location, source identity, map identity, consuming project, and map-store location distinct;
4. classify alignment using this skill's alignment states; and
5. report the evidence, uncertainty, and safe follow-up choices.

Do not write identity metadata merely to make inspection conclusive. If richer universal metadata or automatic
resolution appears necessary, report that as a design question instead of inventing a registry or schema.

## Mapping and Editing Rules

### Layer responsibilities

- `code_map.md`: compact source identity, orientation, and drill-down routing.
- `subsystems/<subsystem>/map.md`: one durable architectural domain, not a folder or module inventory.
- `api_pub.md`: optional decision-ready caller mechanics.
- `api_ext.md`: optional decision-ready extension mechanics.
- `namespace_router.tsv`: optional fuller namespace ownership routing.
- `manifest.tsv`: optional compact subsystem/path registry, never the sole identity proof.
- `symbol_index.tsv`: optional selective high-value symbol routing, never an exhaustive index.
- `map_state.md`: optional current mapping continuation only.

Do not duplicate one layer in another. Prefer durable navigation and recurring non-obvious mechanics over source
extraction. Smaller reusable memory is better than a comprehensive-looking map.

### Subsystem selection and order

A subsystem must represent a demonstrated architectural responsibility, ownership boundary, lifecycle, data or
execution concern, reusable API/extension surface, or cross-boundary behavior. A directory, module, source root,
or package group is evidence, not automatically a subsystem.

Prioritize owner-weighted, foundational, developer-facing, cross-boundary, widely reused, risky, or repeatedly
misunderstood areas. Deprioritize generated code, narrow helpers, leaf utilities, shallow inventories, obvious
details, and non-representative examples.

Finish the approved active subsystem and decide whether each API map is justified before selecting a new one. A
new subsystem or expanded scope requires human direction.

When subsystem mapping has accumulated enough context to reduce confidence or compression quality, reconcile the
concise `map_state.md` and offer current-session and fresh-session continuation as peer choices. A fresh session is
useful advice, not a mandatory map artifact rule, and Bonsai does not control the host session.

### Evidence discipline

Use these labels when a non-obvious claim's status matters:

- **Observed:** confirmed directly from source, tests, examples, build files, or representative use;
- **Inferred:** reasoned from observed structure but not directly established;
- **Uncertain:** requires verification before reliance.

Do not overstate confidence. Correct stale map content when authorized; otherwise make the mismatch or uncertainty
visible.

### TSV discipline

For `namespace_router.tsv`, `manifest.tsv`, and `symbol_index.tsv`:

1. preserve the canonical header and column order;
2. use literal tab characters between fixed columns;
3. keep one logical record per physical line;
4. use no multiline cells, ad hoc columns, prose blocks, or tabs/newlines inside cell values;
5. keep notes terse; and
6. validate the header, separators, and consistent column count after material edits.

Move detail that does not fit the fixed shape into the appropriate Markdown layer.

### Compression and drift prevention

When an artifact grows, cut before adding:

- keep `code_map.md` startup-sized and move fuller namespace routing to its optional TSV;
- keep subsystem maps architectural rather than exhaustive;
- keep API maps focused on mechanics that prevent recurring mistakes;
- keep lookup tables selective and structurally boring;
- keep `map_state.md` current rather than historical; and
- remove duplicated, stale, wrong-layer, obvious, or low-value content.

Do not structurally normalize an existing map during routine maintenance. Do not create optional artifacts because
a template exists. Do not turn maps into project/session guides, API manuals, filesystem mirrors, prose indexes,
or hand-maintained language-server databases.

## Map State

Create or read `<map-store>/<source>/map_state.md` only for an active mapping continuation when it materially helps
the work resume. It is not an input to ordinary map consumption.

Keep only:

- current mapping objective;
- active source/subsystem/artifact focus;
- unresolved uncertainty or risk that changes the next action;
- exact next mapping step or `Mapping scope complete`; and
- the observable success condition.

Replace stale content rather than appending history. Move durable findings to their owning map layer. Remove
`map_state.md` when no active continuation benefits from it. Do not store active project or general session state
there.

## Agent Context

When mapping establishes or disproves a stable source location, project-relevant map selection, or another durable
operational rule, load `skills/agent_context.md` and apply its qualification and narrowest-scope rules.

Do not store active-project selection, transient extraction paths, one-run inspection locations, speculative source
identity, map workflow state, or map content in agent context. Context maintenance grants no permission to broaden
the mapping action.

## Contextual First Use and Maintenance

- A substantial existing source without a useful map may receive one contextual creation action.
- If the human declines, return that result to the invoking workflow so creation moves under **See more options**
  rather than interrupting again in the same context. Do not create a placeholder map or state file for a decline.
- Greenfield source with little stable structure receives no map pressure.
- Surface maintenance only for an explicit request or a known material structural change.
- Do not continuously discover drift, repeatedly offer declined work, or update maps after routine changes.

Preserve a longer-lived source or selection rule only when it independently qualifies under `skills/agent_context.md`.

## Transient Source Inspection

Inspect a supplied archive directly when practical. If extraction or another inspection area is needed:

- keep it outside the durable map store;
- treat it as disposable and non-authoritative working state;
- do not copy it into a project merely to enable mapping;
- do not preserve it in agent context or map data; and
- remove or abandon it without modifying the supplied source artifact.

The physical location of one supplied archive never establishes a general source-location convention. Create,
update, rebuild, and removal preserve that archive even when it is colocated with map artifacts.

## Completion Checks

Before reporting an approved mapping scope complete:

1. verify `code_map.md` identifies the source sufficiently for intended alignment and remains compact;
2. verify entry, subsystem, API, calibration, state, and lookup content stays in its contracted layer;
3. verify each mapped subsystem has a demonstrated responsibility and source-backed owning paths;
4. verify each active subsystem's caller and extension map needs were created or deliberately found unnecessary;
5. verify non-obvious claims are source-backed or visibly inferred/uncertain;
6. verify relative links and optional-artifact references match files that actually exist;
7. validate every materially edited TSV header, literal-tab separator, fixed column count, and one-line row;
8. verify only approved map-owned targets changed;
9. verify supplied source, `map_repo.md`, and other unowned files remain unchanged;
10. verify no transient inspection became durable map data;
11. reconcile concise `map_state.md` or remove it when no longer useful; and
12. maintain only qualifying agent context through `skills/agent_context.md`.

If the current scope has no real next step, mark it complete rather than inventing more mapping work.

## Completion and Invoking-Gate Return

At completion, cancellation, or a declined contextual offer:

1. report the action, source, map identity, bounded result, changed map-owned files, checks actually performed,
   preserved unowned files, remaining uncertainty, and whether qualifying agent context changed;
2. reconcile `map_state.md` and any qualifying agent context;
3. do not silently revise human-owned `map_repo.md`, project final truth, or project execution memory;
4. return control to the workflow that invoked code mapping;
5. let the owning workflow reconcile its own project execution state; and
6. load `skills/menu.md` and re-present the refreshed invoking gate unless mapping created a new required blocker,
   design, final-truth, or review gate.

Do not silently end the parent workflow because mapping completed or was cancelled. Do not select a new mapping
scope automatically. Stop at the refreshed gate for the human's direction.

## Output Style

Use concise wording, exact paths, stable headings, explicit uncertainty, and no filler. Distinguish observed facts
from inference. Do not claim a source, map, identity, mutation, removal, or check that was not actually inspected or
performed.
