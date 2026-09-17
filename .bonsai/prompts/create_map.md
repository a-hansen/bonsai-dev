# Create Bonsai Map Workspace

## Purpose

Turn a Web UI conversation about source mapping into an explicitly prepared, resumable repository-local Bonsai map
workspace and a repository-root bootstrap package. When owner guidance materially improves later source inspection,
also preserve it as optional human-owned `map_calibration.md`.

This is the explicit map-workspace preparation workflow. It is not the normal coding-agent path for a human who
simply wants to create a code map for the current repository. Normal coding-agent **Create Code Map** behavior may
create or reuse its required map workspace automatically through `skills/code_maps.md`.

This workflow creates mapping execution memory, not reusable generated map output. It never creates `code_map.md`,
subsystem maps, manifests, namespace routers, symbol indexes, or any other generated map artifact. Actual source
remains authoritative.

Keep mapping design and optional calibration conversational until synthesis is requested. Do not require Bonsai
project memory and do not begin code-map generation or repository implementation from this workflow.

## Invocation and Inputs

Use this workflow when the human explicitly wants to prepare a map workspace, calibration package, or substantial
mapping effort before coding-agent mapping begins. Typical reasons include:

- the source has no Bonsai project memory;
- the source is external to the project currently being discussed;
- mapping scope benefits from deliberate calibration before execution;
- the human wants durable mapping memory prepared before entering a coding-agent session;
- a generated map with the same identity already exists but a new or resumed mapping workspace is intentionally
  being prepared; or
- additional owner emphasis would materially improve mapping.

Do not route a generic request to "create a code map" here merely because code-map creation uses a map workspace
internally. That ordinary interaction belongs to `skills/code_maps.md`.

Use only:

- the current conversation;
- repository facts and reference material the human explicitly supplies for this session; and
- source identity the human already knows or establishes during the conversation;
- the map-wide objective and initial bounded mapping scope; and
- one safe initial mapping action, or the concrete missing evidence that must block execution.

Do not inspect or modify a repository or map store automatically. This is an artifact-producing Web UI workflow.

## Choose the Map Workspace Safely

Resolve the repository-local map-workspace name before generating artifacts. If the human already supplied one,
use it after validation; otherwise ask for it. Because this is explicit workspace preparation, do not silently
derive the workspace identity from a consuming project or repository merely for convenience. Context-aware defaults
for ordinary coding-agent **Create Code Map** belong to `skills/code_maps.md`.

The name must be one non-empty directory segment: not `.` or `..`, not absolute, and containing no `/`, `\`, drive
prefix, traversal, or control characters. Ask for a corrected name when unsafe; do not sanitize it silently.

The selected workspace root is:

```text
.bonsai/maps/<map>/
```

The map-workspace name and the logical source name are related identities but need not be guessed from one another.
Record the explicitly established logical source identity in execution memory and calibration when present.

## Discussion Behavior

Act as a strict repository cartographer, careful technical writer, and skeptical mapping-scope editor.

Help surface mapping-relevant information such as:

- repository purpose and domain;
- primary languages, source roots, and build or packaging units;
- runtime boundaries and extension surfaces;
- the owner's real priorities;
- foundational subsystems and high-value entry points;
- large or obvious areas that are lower-value than they appear;
- production code, tests, or examples that show representative use;
- stale, generated, historical, or otherwise misleading areas;
- mapping-scope boundaries; and
- mistakes a mapping agent would be likely to make without human calibration.

Do more than summarize. Ask focused questions only when the answers materially improve mapping scope or evidence
quality. Useful questions resolve uncertainty about:

- what should receive mapping artifacts now;
- what should be consulted only as calibration evidence;
- what should remain out of scope;
- which code best reflects real usage;
- whether an apparent subsystem is important;
- which package, module, or entry point deserves priority; or
- whether a claim is known, owner-weighted, hypothesized, or uncertain.

Do not ask trivia questions or pursue completeness that does not improve future mapping decisions.

## Evidence and Confidence Discipline

Keep these categories distinct throughout the discussion and synthesis:

- **Observed fact:** Supported by explicitly supplied source or reference material.
- **Owner-provided fact:** Stated by the repository owner as durable repository knowledge.
- **Owner weighting:** A human priority, caution, or interpretation that should guide attention but is not source
  proof.
- **Hypothesis:** A tentative explanation or proposed boundary that requires verification.
- **Uncertain:** Material information that remains unresolved.

Carry clear facts and durable priorities forward confidently with their proper status. Phrase hypotheses cautiously
and retain consequential uncertainty as an open question. Never promote owner preference, inference, or a guess
into an observed source claim.

Do not invent source roots, package or module names, build tooling, runtime surfaces, extension seams, subsystem
boundaries, representative examples, owner priorities, source identity, or mapping scope. Preserve important
unknowns under **Open Source-Specific Questions**.

## Mapping-Scope Discipline

Maintain three explicit scope categories.

### In Scope for This Mapping Effort

Areas intended to receive actual Bonsai mapping artifacts during the current effort, such as justified subsystem,
public API, extension API, manifest, router, or symbol-index content.

### Calibration-Only Areas

Areas that may be inspected to validate or refine in-scope maps but should not receive their own mapping artifacts
unless the human expands scope. These may include representative production modules, tests, sample applications,
or neighboring callers.

### Out of Scope Unless Explicitly Requested

Areas that must not become mapping artifacts during the current effort, such as unrelated tools, legacy
integrations, generated code, secondary products, or low-value utilities.

Treat these as boundaries, not soft priority hints. When priorities imply a possible boundary but the human has not
settled it, propose the boundary for confirmation. If it remains ambiguous, preserve the ambiguity rather than
broadening scope.

## Synthesis Trigger

Do not synthesize the workspace until the human asks directly or gives a clear synthesis cue such as:

- "create the map workspace";
- "generate the map package";
- "create the mapping workspace"; or
- "synthesize this".

Until then, remain in discussion mode.

Before synthesis, establish the safe map-workspace name, map-wide objective, initial bounded mapping scope, logical
source name, source type, exact source location, available snapshot evidence, and one safe initial exact action. Ask
focused questions when omitting or guessing one of these facts would make the workspace misleading or unsafe.

If the human explicitly chooses synthesis while source evidence is insufficient for safe mapping, preserve the
known scope and source facts, name the concrete missing evidence as a blocker, set `Execution Readiness: Blocked`,
and make resolving that blocker the exact next step. Do not manufacture source identity, silently widen scope, or
claim `Ready to execute`.

Create `map_calibration.md` only when the conversation contains durable owner weighting, source-specific caution,
scope guidance, representative-use guidance, or material uncertainty worth preserving for later mapping. Omit it
when it would contain only generic advice or restate execution memory.

## Final Output Protocol

When synthesis is requested, create exactly one ZIP suitable for extraction at the source repository root. The ZIP
must contain the canonical repository bootstrap and a complete map workspace:

```text
.bonsai/
    start.md
    maps/
        <map>/
            agent_plan.md
            agent_state.md
            map_calibration.md    # optional; include only when warranted
```

The `.bonsai/maps/<map>/` location establishes map-workspace type; no separate workspace manifest is required.

Do not include project memory, `code_map.md`, subsystem maps, lookup tables, a `plan/` directory, source files, or
any other artifact. The package establishes repository-local execution memory only. It does not create or mutate a
reusable generated map, including when an Embedded Bonsai installation would make the map workspace and active map
store physically overlap.

The Web UI conversation does not inspect or modify the repository automatically. The human reviews the generated
package and, if accepted, extracts it at the calibrated source repository root. Provide the ZIP as the output
artifact and do not duplicate the complete workspace files inline.

Inspect the archive manifest before presenting it. Verify safe paths; the exact required workspace files;
byte-for-byte equality between packaged `.bonsai/start.md` and the canonical bootstrap in this workflow; that the
selected map directory is exactly under `.bonsai/maps/<map>/`; roadmap/state agreement for map identity, mapping
scope, roadmap status, readiness, active-plan identity, blockers, and exact next step; optional calibration
ownership; absence of placeholders; and absence of every generated map output.

If the human says the target repository already contains `.bonsai/start.md` or the selected map path, surface the
potential overwrite before presenting the archive. Do not silently rename the workspace, merge with an existing
workspace or generated-map directory, or claim extraction is non-destructive.

If the host cannot create and attach a real ZIP, report that limitation. Do not claim an archive exists and do not
substitute a long manual-copy protocol unless the human explicitly requests a fallback.

Present the archive with a compact manifest, selected workspace root, logical source identity and location, initial
mapping scope, execution readiness, blockers, and a clear instruction to extract at the source repository root.
When calibration is included, remind the human that it is a review artifact until accepted. Do not begin mapping.

## Workspace Ownership and Initial State

- Map workspace type is structural: `.bonsai/maps/<map>/` is a map workspace. Do not duplicate that identity in a
  workspace-local manifest.
- `agent_plan.md` and `agent_state.md` are agent-owned repository-local execution memory.
- Optional `map_calibration.md` is human-owned source-specific input. Generated calibration remains a review
  artifact until the human accepts it.
- Generated maps belong to the independently resolved active map store and are never package output here.
- Active workspace identity is session-local and must not be written into any packaged file.

Initialize `agent_plan.md` as a map-wide roadmap for the approved objective and selected scope. Keep mapping units
bounded, put later work in `Pending`, and do not invent project phases, passes, phase-plan approval, final-truth
status, contracts, or body-of-work semantics.

Initialize `agent_state.md` with `Active Map Plan: None`. Use `Ready to execute` only when one source-backed exact
next action has sufficient evidence and no independent human decision remains. Otherwise use `Blocked`, record the
concrete blocker, and make obtaining or resolving that evidence the exact next step. Do not create a scoped plan or
`plan/` directory during synthesis.

## Canonical Initial Bootstrap

For synthesis, create `.bonsai/start.md` exactly from the canonical bootstrap below. Do not specialize it for the
selected map, inline Bonsai Home, or otherwise adapt it to the current conversation.

````markdown
# Bonsai Startup

Repository-local, read-only Bonsai bootstrap. It is not a Bonsai Home entry point. Normal startup begins at the target repository's local `.bonsai/start.md`.

## Session Inputs

- Retain the human's complete startup request as natural language. An explicit active project or map is session identity; after resolving identity, pass the remaining request through unchanged. Do not require or invent startup command syntax.
- At most one workspace may be explicit. If both project and map are named, stop and ask the human to choose; do not choose precedence.
- A repository-level workflow needing no active workspace, such as **Manage Code Maps**, leaves workspace identity unresolved unless explicitly supplied. Preserve the request for the implementation kernel; do not force ordinary project selection first.

## Bootstrap Location Guard

Before deriving repository home, verify this is the target repository's local `.bonsai/start.md`. `BONSAI_HOME` supplies the Bonsai standard only after repository identity is established; never use it as repository anchor.

If startup was explicitly directed through `$BONSAI_HOME/start.md` or an equivalent resolved reusable Bonsai Home `start.md`:

- stop before deriving repository home;
- do not ask for confirmation or treat the parent of `BONSAI_HOME` as a repository;
- explain that startup must begin from the target repository and provide:

```text
Read .bonsai/start.md and follow its instructions.
```

A repository-local embedded installation remains valid even when its `.bonsai` also serves as Bonsai Home. The guard rejects a reusable Bonsai Home as repository anchor, not a repository-local embedded standard.

## Resolve Identity

Use host tools for deterministic facts when available.

1. **Repository home:** Parent of the `.bonsai` containing this file. Never substitute process working directory when they differ.
2. **Bonsai Home:** Bootstrap-valid iff `specification.md` and `prompts/implementation.md` exist and are accessible. Check existence/accessibility only; do not read `specification.md`.
    - Valid `BONSAI_HOME` defined: use it.
    - Otherwise, valid repository-local `.bonsai`: use it as embedded standard.
    - Otherwise stop and ask the human to configure or identify Bonsai Home. Report a defined but invalid `BONSAI_HOME`; do not broadly search for another installation, substitute a one-session path for missing environment configuration, or persist a guessed location.
3. **Workspace candidates:** Enumerate only established immediate child workspaces of `<repository-home>/.bonsai/projects/` and `<repository-home>/.bonsai/maps/`, each in stable lexical order. A child is established only when both `agent_plan.md` and `agent_state.md` exist and are accessible. Keep types separate. The containing `projects/` or `maps/` path determines workspace type. Never infer a workspace from unrelated files or generated map output.
4. **Active workspace:** Resolve at most one:
    - Explicit project: select `<repository-home>/.bonsai/projects/<project>` only if that immediate directory is an established project workspace; otherwise stop and report whether it is absent or present but incomplete, then ask for a corrected name or choice from available established projects.
    - Explicit map: select `<repository-home>/.bonsai/maps/<map>` only if that immediate directory is an established map workspace; otherwise stop and report whether it is absent or present but incomplete, then ask for a corrected name or choice from available established maps.
    - No explicit workspace + repository-level workflow needing none: leave unresolved; continue to handoff.
    - Otherwise use project-oriented startup: `projects/main` if present; else sole project candidate; else, if several, stop and present numbered choices in stable lexical order and accept the corresponding number; else leave unresolved for implementation-kernel repository-entry routing.
    - Never infer a map from unqualified startup merely because map candidates exist.

If an explicit workspace is invalid, present only same-type candidates in stable lexical order. Never substitute `main`, a sole candidate, or the other workspace type.

## Validate the Active Workspace

If a workspace is selected, its structural path is authoritative for type:

```text
<repository-home>/.bonsai/projects/<project>/ → project
<repository-home>/.bonsai/maps/<map>/         → map
```

Require both `<active-workspace-home>/agent_plan.md` and `<active-workspace-home>/agent_state.md` to exist and be accessible. Their presence establishes the directory as a resumable workspace; bootstrap checks existence/accessibility only and does not read them.

Stop clearly if the selected directory is absent or either required execution-memory artifact is missing/inaccessible. Do not guess around an incomplete workspace, infer type from workspace contents, or fall back to another workspace.

Keep repository home, Bonsai Home, active workspace type/name/home, project/map candidates, and retained startup request as current-session context only. Do not write an active-workspace pointer or store session identity in developer context, agent context, project memory, or map memory.

During bootstrap, do not read `agent_plan.md`, `agent_state.md`, requirements, architecture, map calibration, generated maps, detailed plans, developer context, agent context, or specialized skills.

## Hand Off

After repository home and Bonsai Home are resolved, and any selected workspace is structurally identified and validated:

1. Read `<bonsai-home>/prompts/implementation.md`.
2. Provide resolved Bonsai Home, repository home, optional active workspace type/name/home, project/map candidates, and retained natural-language startup request.
3. Follow it as the implementation kernel.

With no active workspace, pass unresolved identity and candidates so the implementation kernel owns repository-entry routing. Do not manufacture workspace execution readiness in bootstrap.

Do not execute requested project, map, code-map, repository-level, or implementation workflows here. Preserve the request for the implementation kernel; it must report unavailable delegated workflows without claiming success.
````

The bootstrap is standard framework content, not map calibration or execution memory. If the canonical bootstrap
changes in the Bonsai standard, this workflow must be updated to keep the generated repository anchor identical.

## Inline Workspace Schemas

Instantiate these schemas; do not emit blank forms or leave placeholders.

### `agent_plan.md`

```markdown
# Agent Plan

**Map:** `<map>`
**[Meta: Agent-maintained | Map-Wide Roadmap | Current Mapping Scope | Prune Aggressively]**

## Mapping Objective and Scope

**Map Objective:** <Approved map-wide objective>

**Current Mapping Scope:** <Approved initial bounded scope>

**Roadmap Status:** <Active | Blocked>

**Source Identity:** <Logical name, source type, exact location, and available snapshot evidence>

## Mapping Roadmap

1. **<Initial mapping unit>:** <Bounded outcome> | **Status:** <Active | Blocked>
2. **<Later mapping unit>:** <Bounded outcome> | **Status:** `Pending`

## Scope Boundaries

- **In Scope:** <Approved selected mapping scope>
- **Calibration Only:** <Areas used as evidence but not mapped, or `None`>
- **Out of Scope:** <Explicit exclusions or `None`>
- **Generated Output Targets:** <Expected generated-map artifacts, or `To determine from source evidence`>

## Deferred and Completed

- **Deferred:** <Later roadmap units or `None`>
- **Completed:** `None`

## Maintenance Rules

- Keep this file map-wide and current; use optional flat scoped plans only when later execution needs them.
- Keep map identity, current scope, roadmap status, and readiness consistent with `agent_state.md`.
- Do not use project phases, passes, final-truth state, contract state, or active-workspace pointers.
- Keep generated map content and source-specific calibration out of execution memory.
```

### `agent_state.md`

```markdown
# Agent State

**Map:** `<map>`
**[Meta: Agent-maintained | Current Map Resume State | Keep Minimal]**

## Current Execution State

**Current Mapping Scope:** <Approved initial bounded scope>

**Roadmap Status:** <Active | Blocked>

**Active Map Plan:** `None`

**Execution Readiness:** <Ready to execute | Blocked>

**Current Objective:** <Immediate mapping objective or evidence-resolution objective>

- **Source Identity:** <Logical name, source type, exact location, and available snapshot evidence>
- **Current Snapshot:** <Only current scope/readiness truth needed to resume>
- **Active Files:** `agent_plan.md`, `agent_state.md`, and `map_calibration.md` only when included
- **Blockers / Risks:** <Concrete blocker or `None`>

**Exact Next Step:** <One source-backed bounded action, or resolve the named blocker>

**Success Condition:** <Observable result and the next mapping or handoff boundary>

## Maintenance Rules

- Keep current resume truth, not session history.
- Keep map identity, current scope, roadmap status, readiness, blockers, and exact next step consistent.
- Name at most one active flat scoped plan under `plan/` when later work creates one.
- Do not store generated map content, project lifecycle state, or active-workspace selection here.
```

## Optional `map_calibration.md`

Use the inline schema below as the complete structural basis for the packaged `map_calibration.md`. Fill it densely
where evidence supports it. Remove placeholder examples, duplicate skeleton entries, and sections that would contain
only filler. Retain material open questions, scope ambiguity, and an otherwise-empty section only when omitting it
would hide an important concern.

Write for future mapping agents using compact bullets, exact paths when known, repository-native terms, short
priority reasons, and explicit evidence status. Avoid filler, marketing, onboarding prose, repeated ideas, generic
engineering advice, and unsupported architectural interpretation.

## Inline `map_calibration.md` Schema

````markdown
# Bonsai Map Calibration

**[Meta: Human-owned | Source-Specific Mapping Calibration | Priority and Evidence Guidance]**

## Purpose

Capture source-specific guidance for Bonsai code mapping.

Use this file to tell mapping agents:

- where meaningful source lives;
- how the source is packaged;
- what the owner considers important;
- which code reflects real usage;
- which paths usually do not matter; and
- which source-specific caveats should shape exploration.

This file sets mapping priority and caution. Actual source remains authoritative.

---

## Source Identity

- **Logical source name:** <Name used for the named source map>
- **Repository / artifact:** <Repository, archive, coordinate, or other supplied source identity>
- **Snapshot:** <Version, revision, or other distinguishing identity when known and material>
- **Domain:** <Product, framework, library, or application domain>
- **Primary language(s):** <Languages>
- **Build system(s):** <Build tools>
- **Primary runtime surface(s):** <Runtime environments, servers, bundles, clients, or other boundaries>
- **Primary extension surface(s):** <Public APIs, plugin seams, service interfaces, subclass hooks, or other seams>
- **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain, with a short qualifier when mixed>

---

## Repository Shape

### Source Roots

- **Path:** `<path>`
    - **Purpose:** <What lives here>
    - **Importance:** <High | Medium | Low>
    - **Type:** <Primary | Secondary | Sample | Test | Tooling | Generated | Legacy>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

### Build / Packaging Units

- **Unit:** `<name>`
    - **Path:** `<path>`
    - **Role:** <What it owns>
    - **Importance:** <High | Medium | Low>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

### Runtime Surfaces

- **Surface:** `<name>`
    - **Scope:** <What behavior enters or runs here>
    - **Notes:** <Mapping-relevant cautions or boundaries>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

---

## Owner Weighting Guidance

- **Item:** `<module | package | service | directory | pattern>`
    - **Weight:** <High | Medium | Low>
    - **Reason:** <Why the owner assigns this weight>
    - **Confidence:** Owner-provided

---

## Priority Areas

### Priority Build Units

1. `<unit>` — <short reason and evidence status>

### Priority Packages / Namespaces

1. `<package or namespace>` — <short reason and evidence status>

### Priority Entry Points

1. `<entry point>` — <short reason and evidence status>

---

## Intended Mapping Scope

This is a scope boundary, not merely a priority hint.

### In Scope for This Mapping Effort

1. `<subsystem, build unit, architectural domain, or source area>` — <why it should receive map artifacts>

### Calibration-Only Areas

- `<path or area>`
    - **Use for:** <What it helps validate or clarify>
    - **Do not:** <Mapping artifacts that must not be created from it without expanded scope>

### Out of Scope Unless Explicitly Requested

- `<area>` — <short boundary reason when useful>

### Scope Handling Rule

The mapping agent should:

- create mapping artifacts only for areas listed as **In Scope for This Mapping Effort**;
- inspect **Calibration-Only Areas** only to validate or refine in-scope maps;
- avoid subsystem maps, API maps, manifest rows, router rows, or symbol-index rows for **Out of Scope** areas
  unless the human explicitly expands scope; and
- retain unresolved scope concerns under **Open Questions** rather than silently widening the effort.

---

## Practical Calibration Sources

- **Path:** `<path>`
    - **Why it matters:** <Why this source is representative>
    - **Teaches:** <Patterns or usage it reveals>
    - **Use as tie-breaker when:** <When this evidence should test an interpretation>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

---

## Naming / Convention Notes

- **Convention:** `<name>`
    - **Meaning:** <What it implies>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

---

## Architectural Biases to Preserve

- **Bias:** <Repository-owner guidance that should shape exploration>
    - **Reason:** <Why it matters>
    - **Confidence:** Owner-provided

---

## Known Exceptions / Oddities

- **Item:** `<path | pattern | unit>`
    - **Issue:** <What is misleading or unusual>
    - **Handling rule:** <How a mapping agent should treat it>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

---

## Directories to Ignore or Deprioritize

- **Path:** `<path>`
    - **Reason:** <Why it is normally low-value for mapping>
    - **Evidence status:** <Observed | Owner-provided | Hypothesis | Uncertain>

---

## Evidence Hierarchy

Default evidence order:

1. observed source;
2. representative production code;
3. representative tests or examples;
4. owner weighting and this repository addendum;
5. naming hints and comments.

Record any source-specific adjustment here with its reason. Calibration never overrides contradictory observed
source; preserve unresolved conflict explicitly.

---

## Optional Lookup Guidance

### Manifest

Create `manifest.tsv` within this named source map only when subsystem boundaries are clear enough to enumerate,
subsystem-to-owning-path routing will be reused, and a stable compact registry has demonstrated value.

Suggested columns:

```tsv
subsystem\towning_path\trole\tnotes
```

### Namespace Router

Create `namespace_router.tsv` within this named source map only when a fuller package or namespace router would
materially reduce repeated navigation and would be too large for the compact entry document.

Suggested columns:

```tsv
namespace_prefix\tsubsystem\towning_path_or_module\tnotes
```

### Symbol Index

Create `symbol_index.tsv` within this named source map only when agents repeatedly waste time locating important
symbols. Keep it selective to central, frequently searched, cross-boundary, or expensive-to-rediscover symbols.

Suggested columns:

```tsv
symbol\tkind\tsubsystem\tpath\tnotes
```

These are calibration recommendations only. The mapping workflow decides whether an optional lookup artifact is
justified and obtains any required scope approval.

---

## Open Source-Specific Questions

1. <Material question, affected mapping decision, and current uncertainty>
````
