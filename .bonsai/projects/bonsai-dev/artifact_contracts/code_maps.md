# Artifact Contracts — Code Maps

**Project:** `bonsai-dev`  
**Status:** Seeded; deep Phase 1 archaeology required before implementation

> **Staging note:** Mapping implementation artifacts are first built under `bonsai/`. Runtime map storage still follows the v2 specification and is distinct from generated test output. The temporary staging directory is not itself the runtime map store.

## Mapping Preservation Stance

The old mapping subsystem is the largest body of accumulated Bonsai implementation knowledge.

The v2 integration changes the control plane, storage model, and relationship to projects. It does **not** justify discarding mature map structures that still solve useful navigation problems.

Actual source remains authoritative.

Project memory and map calibration inform what deserves attention, but they never replace source evidence.

---

## Artifact: `bonsai/prompts/create_map_repo.md`

**Classification:** Adapt from `.bonsai/maps/repo_session.md`

### Role

Provide an optional Web UI calibration workflow for a source repository that needs human weighting before or alongside code-map creation.

### Loaded when

The human wants to create or refine source-specific mapping guidance, especially when:

- the source has no Bonsai project memory; or
- project memory exists but additional mapping emphasis is useful.

### Inputs

Natural design/calibration conversation about the source, plus any explicitly supplied repository information.

### Responsibilities

Synthesize optional human-owned:

```text
map_repo.md
```

containing useful mapping calibration such as:

- repository identity and shape;
- source roots;
- build/packaging units;
- runtime surfaces;
- owner weighting;
- priority areas;
- intended mapping scope;
- calibration-only areas;
- out-of-scope areas;
- practical calibration sources;
- naming/convention notes;
- architectural interpretation guidance;
- known exceptions/oddities;
- directories to ignore/deprioritize;
- evidence hierarchy;
- open repository-specific questions.

### Must not

- invent repository facts;
- turn developer guesses into asserted architecture;
- make `map_repo.md` product requirements or project architecture;
- force calibration when actual source plus existing project memory is already sufficient;
- treat calibration as a substitute for source inspection.

### Preserve from existing version

The existing `repo_session.md` has mature distinctions to preserve:

- repository facts vs owner weighting;
- mapping scope vs calibration-only vs out-of-scope;
- human judgment may guide emphasis without being overstated as fact;
- no invented repository detail;
- practical calibration sources and evidence hierarchy;
- optional guidance for lookup artifacts rather than automatic expansion.

### v2 changes

- rename to `create_map_repo.md`;
- place among standard Web UI prompts;
- output belongs with the named source map in the active Bonsai map store;
- may complement project memory instead of operating as a standalone mapping subsystem prerequisite.

### Validation cases

- external source with no Bonsai memory;
- source with strong project memory plus extra owner weighting;
- human provides uncertain claims that must remain qualified;
- no calibration needed.

---

## Artifact: `bonsai/skills/code_maps.md`

**Classification:** Major Adapt from `.bonsai/maps/map_prompt.md` + applicable control behavior from `.bonsai/maps/map_system.md`

### Role

Integrate code-map lifecycle management into the normal Bonsai workflow.

### Loaded when

- human selects **Manage Code Maps**;
- explicit startup request asks for map management;
- implementation needs map-guided navigation or source/map identity validation;
- a substantial existing codebase lacks a useful map and first-use behavior makes creation contextually relevant;
- map maintenance is required by material structural change.

### Inputs

- active Bonsai map store;
- source being mapped;
- source identity;
- relevant source project memory when available;
- optional source `map_repo.md`;
- relevant agent context such as durable source locations or useful map-selection rules;
- existing map data when inspecting/updating.

### Responsibilities

Provide lifecycle actions equivalent to:

- Create Code Map;
- Inspect Code Maps;
- Update or Rebuild Code Map;
- Remove Code Map;
- Inspect Map/Source Identity.

For creation/update:

- identify the source independently from the active Bonsai project;
- use actual source as authority;
- use relevant project memory and/or `map_repo.md` as calibration;
- store output in the active Bonsai map store;
- preserve map/source identity;
- avoid silent use of incompatible map snapshots;
- preserve stable source-location or mapping rules in the appropriate agent-context scope when they qualify;
- return to the invoking Bonsai gate after subordinate map work.

### Must not

- name maps after the consuming Bonsai project when source identity differs;
- require source to have Bonsai project memory;
- duplicate one repository map per Bonsai project;
- assume a current development checkout matches a released dependency;
- treat maps as project truth;
- replace source inspection with map assertions;
- pressure greenfield repositories to create low-value maps;
- rewrite mature map data solely to make the v2 architecture look cleaner.

### Reads

- actual source;
- applicable project memory;
- optional `map_repo.md`;
- relevant agent context;
- existing map entry/index/subsystem artifacts;
- detailed map-system rules only when the specific mapping operation requires them.

### Writes

Under the active map store:

```text
$BONSAI_HOME/maps/<source>/
```

or embedded:

```text
repo/.bonsai/maps/<source>/
```

The exact internal file set remains subject to archaeological validation.

Qualifying durable source-location knowledge may also be written through `agent_context.md`.

### Delegates to

- menu skill;
- agent-context skill;
- source-navigation/map-format procedures extracted from the old map system.

### Human gates

- selection among lifecycle actions;
- first-use creation choice when promoted contextually;
- any destructive removal/rebuild action that requires explicit authorization;
- ambiguous source identity/version alignment.

### Preserve from existing version

Deep extraction must preserve useful behavior from `map_prompt.md` and `map_system.md`, including candidates such as:

- bounded mapping sessions with explicit current scope;
- mapping state that supports fresh-session continuation without becoming a report;
- repository compass before deep subsystem mapping;
- priority subsystem mapping cycles;
- calibration against real usage;
- layered maps from repository orientation to subsystem/API details;
- namespace routing and optional lookup artifacts;
- evidence discipline and confidence;
- selective source inspection;
- code maps as navigation aids, not source substitutes;
- compression and anti-sprawl rules;
- bounded updates rather than constant full rebuilds;
- explicit done criteria per map artifact;
- drift prevention;
- stable naming rules;
- API maps only when they earn their keep;
- one-subsystem/fresh-session discipline where it materially improves mapping quality.

These are preservation candidates, not automatic v2 requirements. Phase 1 must determine which survive unchanged, which adapt, and which are obsolete because integrated routing replaces the old standalone control plane.

### v2 changes

- entry moves under normal Bonsai menu/startup routing;
- active map store is Bonsai Home or embedded map store;
- source identity is independent of active project;
- relevant project memory can calibrate mapping;
- `create_map_repo.md` is optional Web UI calibration;
- stable source locations/map rules belong in scoped agent context;
- subordinate mapping returns to invoking gate;
- project-level `agent_context.md` may identify relevant maps for a consuming project.

### Validation cases

- map current repository with project memory;
- map external repository without project memory;
- map with both project memory and `map_repo.md`;
- several projects reuse one repository map;
- `investment-app` consumes `barcache` and `tickerview` maps;
- map source mismatch is detected;
- greenfield source does not trigger repeated map pressure;
- declined first-use map creation remains available under secondary options.

---

# Map Data Contract Candidates

The following existing formats are not yet assigned final v2 source-distribution paths. Their behavioral value must be extracted before deciding whether they remain separate templates/files.

## `code_map.md`

**Existing role candidate:** Layer-1 repository compass and normal map entry document.

Preservation questions:

- What minimum orientation belongs here?
- Which details should route deeper rather than accumulate?
- What source identity must the entry document carry in v2?
- How does it remain compact enough for selective loading?

The v2 specification explicitly retains `code_map.md` as the normal map entry document.

## `namespace_router.tsv`

**Existing role candidate:** Cheap deterministic routing from namespaces/packages/source regions to deeper subsystem map material.

Preservation question: retain only if it materially reduces navigation cost without becoming a package registry.

## `subsystems/<subsystem>/map.md`

**Existing role candidate:** Deeper structural and implementation-oriented subsystem map.

Preservation question: preserve the old bounded role and avoid turning subsystem maps into source replicas.

## `api_pub.md`

**Existing role candidate:** Optional map of public API surface.

Preservation question: create only when public API structure materially benefits repeated navigation.

## `api_ext.md`

**Existing role candidate:** Optional extension/integration API map.

Preservation question: retain when extension points are significant enough to deserve independent navigation memory.

## `manifest.tsv`

**Existing role candidate:** Optional lookup artifact for targeted source/file navigation.

Preservation question: avoid automatic generation and sprawl.

## `symbol_index.tsv`

**Existing role candidate:** Optional high-value symbol lookup.

Preservation question: keep selective rather than indexing everything.

## `map_state.md`

**Existing role candidate:** Agent-owned current mapping resume state.

Preservation questions:

- What remains active mapping state in v2?
- Where should it live inside a named map?
- Which old fields are control-plane artifacts that disappear after integration?
- How aggressively should completed/stale state be compressed?

---

# Old Mapping Control Artifacts to Reconcile

## `.bonsai/maps/map_prompt.md`

Likely split between:

- lifecycle/session behavior that moves to `skills/code_maps.md`;
- current mapping-state routing that remains map-local;
- standalone menu/startup assumptions that are dropped.

## `.bonsai/maps/map_system.md`

This is archaeological specification for the mature mapping internals, not v2 framework authority.

Phase 1 should extract it in bounded sections:

1. file/layer responsibilities;
2. evidence discipline;
3. editing rules;
4. what mapping looks for;
5. build order;
6. compression;
7. done criteria;
8. update triggers;
9. prioritization;
10. drift prevention;
11. naming;
12. operating stance.

Each rule should be classified before the file is replaced or split.

## `.bonsai/maps/README.md`

Human-facing guidance should be reconciled against the integrated v2 README.

Do not automatically copy all standalone mapping instructions into `bonsai/README.md`; retain only user-facing detail that still helps the integrated workflow.

---

# Phase 1 Mapping Archaeology Boundary

Do not begin with the 1,300+ line `map_system.md`.

First stabilize core workflow contracts so the v2 control-plane boundary is clear.

Then treat mapping as its own archaeological batch and preserve its internal knowledge deliberately.

The intended result is not "new mapping from scratch."

It is:

```text
mature mapping internals
        +
v2 source/project/context identity
        +
integrated Bonsai routing
        =
Bonsai v2 code maps
```
