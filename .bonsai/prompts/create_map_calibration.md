# Create Bonsai Map Calibration

## Purpose

Turn a Web UI conversation about a source repository into optional, human-owned mapping calibration named
`map_calibration.md`. Preserve repository-owner judgment that source inspection alone may not reveal reliably, including
mapping priorities, representative usage, misleading areas, scope boundaries, and material uncertainty.

This artifact guides later code-map creation. It is not product truth, architecture truth, source evidence, or map
identity. Actual source remains authoritative.

Keep calibration conversational until synthesis is explicitly requested. Do not require Bonsai project memory and
do not begin code-map creation from this workflow.

## Invocation and Inputs

Use this workflow when the human wants to calibrate mapping for a named source, especially when:

- the source has no Bonsai project memory; or
- project memory exists but additional owner emphasis would improve mapping.

Use only:

- the current conversation;
- repository facts and reference material the human explicitly supplies for this session; and
- source identity the human already knows or establishes during the conversation.

Do not inspect or modify a repository or map store automatically. This is an artifact-producing Web UI workflow.

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

Do not synthesize `map_calibration.md` until the human asks directly or gives a clear synthesis cue such as:

- "generate the map calibration";
- "create map_calibration";
- "create the mapping calibration package"; or
- "synthesize this".

Until then, remain in discussion mode.

Before synthesis, establish the logical source name because it determines the packaged path. If the human already
supplied a valid logical source name, use it without asking again. A packaged source name must be a single safe
directory name: non-blank, not `.` or `..`, and containing no `/` or `\` path separator. If the source name remains
materially ambiguous or invalid, ask the human to resolve it. Do not derive map identity silently from a consuming
Bonsai project.

## Final Output Protocol

When synthesis is requested, create exactly one ZIP suitable for extraction at the calibrated source repository
root. The ZIP must contain exactly:

```text
.bonsai/
    maps/
        <source-name>/
            map_calibration.md
```

Do not include `.bonsai/start.md`, project memory, `code_map.md`, `map_state.md`, subsystem maps, lookup tables,
source files, or any other artifact. This package adds source-specific human calibration only. It does not create a
code map and does not by itself make the source repository a Bonsai project or Embedded Bonsai installation.

The Web UI conversation does not inspect or modify the repository automatically. The human reviews the generated
package and, if accepted, extracts it at the calibrated source repository root. Provide the ZIP as the output
artifact and do not duplicate the complete calibration inline.

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
- record unresolved scope concerns in `map_state.md` rather than silently widening the effort.

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
