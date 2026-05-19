# Bonsai Maps

**Layered repository memory for AI-assisted implementation.**

Bonsai project memory tells an AI:

* what the product is
* what architecture is intended
* what phase of work is active
* what exact step should happen next

Bonsai maps answer a different question:

> **Where in this repository should the AI look, and what structural understanding should it carry forward?**

Maps are durable codebase navigation memory. They help future AI sessions:

* orient quickly
* route to the right subsystem
* avoid repeated repo rediscovery
* understand important architectural boundaries
* preserve non-obvious caller and extension mechanics
* read the right source first instead of wandering

Maps do **not** replace source inspection.
They reduce blind searching and repeated relearning.

---

# TL;DR

## Prepare repository mapping guidance

For a serious repository, first use a Web UI AI session to synthesize:

```text
.bonsai/maps/map_repo.md
```

Paste into the conversation:

```text
.bonsai/maps/repo_prompt.md
```

along with:

```text
.bonsai/maps/templates/map_repo_template.md
```

The AI will turn your repository discussion into a durable mapping addendum.

---

## Build or refresh maps

Start a coding-agent session with:

```text
Read .bonsai/maps/map_prompt.md and follow its instructions.
```

The agent will read the normal mapping-session inputs, determine the current mapping state, consult
the relevant templates when creating new artifacts, and continue the next mapping step.

`map_system.md` is **not** a normal mapping-session startup read. It is the durable map-system
specification, and it is loaded when an agent is editing Bonsai map artifacts or changing the map
system itself.

---

## Map one subsystem per clean session

For serious mapping work:

> **Start a clean AI session for each subsystem.**

Do not map a large repository, then several subsystems, then API mechanics, all in one increasingly
bloated session. Let `map_state.md` preserve the baton pass and restart cleanly when switching focus.

---

# What Maps Are For

A coding agent entering a mature repository often wastes time on the same work repeatedly:

* rediscovering where concepts live
* misjudging which module owns what
* over-reading low-value internals
* missing the real extension seam
* assuming a theoretical architecture that production code does not actually use
* reopening the same source files across session after session

Bonsai maps capture the **reusable orientation layer**.

They should help an AI answer:

* What subsystems matter here?
* Which subsystem owns this concept?
* Which package or module should I inspect first?
* What deeper map should I load?
* What API mechanics are worth remembering?
* What rules are easy to get wrong?

---

# Where Maps Fit in Bonsai

Bonsai has two complementary memory systems.

## Project memory

Lives under:

```text
.bonsai/projects/<project>/
```

Typical files:

* `requirements.md`
* `architecture.md`
* `plan.md`
* `state.md`

These define:

* what to build
* how it should be shaped
* how implementation is sequenced
* what is happening right now

---

## Repository map memory

Lives under:

```text
.bonsai/maps/
```

Typical files:

* `repo_prompt.md`
* `map_prompt.md`
* `map_system.md`
* `map_repo.md`
* `map_state.md`
* `code_map.md`
* `templates/...`
* `subsystems/<subsystem>/...`
* optional TSV lookup artifacts

These define:

* how repository mapping is prepared
* how map-building sessions operate
* what repo-specific priorities should guide exploration
* how the repository is organized
* what subsystems exist
* where important code lives
* what caller and extension mechanics deserve durable memory

---

## How they work together

During an implementation session:

* **Project memory** tells the agent **what to do**
* **Code maps** help the agent determine **where and how to do it safely**

A well-shaped implementation prompt should read the shared code map first, then project memory,
then drill into deeper map files only when needed.

---

# Directory Layout

```text
.bonsai/
└── maps/
    ├── README.md
    ├── repo_prompt.md
    ├── map_prompt.md
    ├── map_system.md
    ├── map_repo.md
    ├── map_state.md
    ├── code_map.md
    ├── namespace_router.tsv               # Optional generated artifact
    ├── manifest.tsv                       # Optional generated artifact
    ├── symbol_index.tsv                   # Optional generated artifact
    ├── templates/
    │   ├── map_repo_template.md
    │   ├── map_state_template.md
    │   ├── code_map_template.md
    │   ├── subsystem_map_template.md
    │   ├── api_pub_template.md
    │   ├── api_ext_template.md
    │   ├── namespace_router_template.tsv
    │   ├── manifest_template.tsv
    │   └── symbol_index_template.tsv
    └── subsystems/
        ├── <subsystem>/
        │   ├── map.md
        │   ├── api_pub.md
        │   └── api_ext.md
        └── <subsystem>/
            ├── map.md
            ├── api_pub.md
            └── api_ext.md
```

---

# File Roles

## `repo_prompt.md`

**The Web UI synthesis prompt for repository calibration.**

Use this before the first serious mapping pass when you want help constructing:

```text
map_repo.md
```

It asks a Web AI to synthesize your conversation into durable human-owned repo guidance.

This is useful because repository owners often know things source scanning cannot reliably infer:

* which modules matter most
* which examples reflect real usage
* which huge areas should not dominate mapping
* which small abstractions are foundational
* which directories are stale, generated, misleading, or low value
* which development patterns future agents should prioritize

---

## `map_prompt.md`

**The coding-agent mapping prompt.**

Use this to start or continue a map-building session:

```text
Read .bonsai/maps/map_prompt.md and follow its instructions.
```

It tells the coding agent:

* what mapping work is
* what files to read first
* how to determine the current mapping objective
* what kinds of map files to create or update
* when to consult templates
* how to keep maps useful without bloating them

---

## `map_system.md`

**The durable map-system specification.**

Defines:

* file taxonomy
* map layers
* subsystem/API mapping order
* package / namespace routing policy
* prioritization rules
* done criteria
* compression discipline
* drift-prevention guidance

This file explains **how the mapping system itself works**.

It should change rarely. It should be loaded when an agent is **editing Bonsai map artifacts** or
changing the map system itself, not merely when an implementation agent is using existing maps.

---

## `map_repo.md`

**Human-owned repository calibration.**

This is where the developer gives mapping agents repo-specific guidance:

* source roots
* packaging units
* runtime surfaces
* owner weighting
* important entry points
* practical calibration sources
* ignored directories
* known oddities

This file matters. Without it, a mapping agent may over-rank the wrong parts of a repository merely
because they are large, central, or easy to identify.

---

## `map_state.md`

**The current mapping baton pass.**

This is volatile, agent-maintained state for the mapping workflow.

It should say:

* what mapping objective is active
* which pass or focus is active
* what was recently confirmed
* what remains uncertain
* what exact mapping step should happen next
* what AI level is appropriate

It should stay short.

`map_state.md` is not a historical log and not a findings archive. Durable findings belong in the
actual map files.

---

## `code_map.md`

**The top-level repository compass.**

This is the map most likely to be loaded during ordinary implementation sessions.

It should remain compact and answer:

* what the major subsystems are
* what broad boundaries shape the repository
* what execution or integration entry points matter
* what map file to read next
* which **high-value** package or namespace prefixes materially improve first-pass routing

It is a routing tool, not a full architecture manual and not a full package registry.

When fuller package / namespace ownership lookup is useful, `code_map.md` should point to:

```text
namespace_router.tsv
```

when that optional file exists.

It should also tell an agent that, **if it is about to edit Bonsai map artifacts**, it must first read:

```text
.bonsai/maps/map_system.md
```

That does not make `map_system.md` part of ordinary implementation startup. It is an edit-time
guardrail for agents that are maintaining the maps.

---

# Templates

Templates live under:

```text
.bonsai/maps/templates/
```

They define the expected shape of generated mapping artifacts.

The mapping agent should consult the corresponding template whenever it creates a new file.

## Available templates

| Template                        | Generated artifact                  |
| ------------------------------- | ----------------------------------- |
| `map_repo_template.md`          | `map_repo.md`                       |
| `map_state_template.md`         | `map_state.md`                      |
| `code_map_template.md`          | `code_map.md`                       |
| `subsystem_map_template.md`     | `subsystems/<subsystem>/map.md`     |
| `api_pub_template.md`           | `subsystems/<subsystem>/api_pub.md` |
| `api_ext_template.md`           | `subsystems/<subsystem>/api_ext.md` |
| `namespace_router_template.tsv` | `namespace_router.tsv`              |
| `manifest_template.tsv`         | `manifest.tsv`                      |
| `symbol_index_template.tsv`     | `symbol_index.tsv`                  |

Templates exist to prevent the agent from inventing new document shapes every time it maps a repo.

They should not force artifact creation. For example, the presence of:

```text
api_ext_template.md
```

does **not** mean every subsystem should get an `api_ext.md`.

---

# TSV Lookup Artifacts

Three optional map artifacts use TSV instead of Markdown:

```text
namespace_router.tsv
manifest.tsv
symbol_index.tsv
```

They are structured lookup tables, not narrative map documents.

TSV keeps them:

* compact
* token-efficient
* easy to scan
* easy to parse
* less likely to become over-written pseudo-documentation

## `namespace_router.tsv`

Optional lazy-loaded fuller package / namespace ownership lookup.

Use this when:

* the repository has enough package / namespace breadth that fuller routing is useful
* preserving that routing inside `code_map.md` would make the startup map too large
* future agents benefit from a deeper lookup table when placing unfamiliar packages or namespaces

Recommended columns:

```tsv
namespace_prefix	subsystem	owning_path_or_module	notes
```

This file should remain a routing aid, not a universal package inventory.

`code_map.md` may retain a short curated high-value namespace table for first-load orientation. The
fuller or more detailed package / namespace lookup belongs here.

---

## `manifest.tsv`

Optional deterministic subsystem registry.

Useful when:

* the repo is large
* subsystem/source-root enumeration will be reused
* mapping will proceed over many sessions
* semi-automated follow-on passes benefit from a stable list

It should stay narrow. It is not a second code map.

---

## `symbol_index.tsv`

Optional selective symbol lookup accelerator.

Create this only if agents repeatedly waste time finding:

* central symbols
* symbol ownership
* defining files
* path locations for important cross-boundary types

Do not create it by default.

Do not index everything. Add only symbols that are:

* central
* frequently searched
* cross-boundary
* expensive to rediscover

---

# Subsystem Files

Each substantial subsystem gets its own directory:

```text
.bonsai/maps/subsystems/<subsystem>/
```

## `map.md`

**Subsystem architecture memory.**

Subsystems are architectural domains, not build units. One build unit may produce multiple subsystem maps. One subsystem may span multiple build units.

Use this to capture:

* subsystem scope
* owning code units
* why it matters
* central abstractions
* key workflows
* extension seams
* risky or non-obvious areas
* links to API maps

This should describe the subsystem well enough that an implementation agent knows what it is looking
at before reading source.

It should not become an encyclopedia.

---

## `api_pub.md`

**Caller-facing mechanics.**

Use this only when a subsystem has reusable public mechanics that future agents are likely to need
again.

Examples:

* service lookup
* query patterns
* cursor lifecycles
* event subscription
* required parameter semantics
* non-obvious null or availability behavior

This file should preserve exact, reusable caller mechanics that are easy to misuse or expensive to
rediscover.

---

## `api_ext.md`

**Extension-facing mechanics.**

Use this only when a subsystem exposes meaningful extension seams.

Examples:

* subclassing patterns
* provider registration
* plugin registration
* lifecycle hooks
* required event sequencing
* synchronization constraints
* service tracker patterns
* super-call expectations

This file should preserve exact, reusable extension mechanics that are easy to get wrong.

---

# Full Usage Guide

## Stage 1: Prepare repository calibration

Before asking a coding agent to map a serious repository, create:

```text
.bonsai/maps/map_repo.md
```

There are two ways to do that.

---

## Option A: Fill `map_repo.md` manually

Use:

```text
.bonsai/maps/templates/map_repo_template.md
```

and write the repo-specific guidance yourself.

This works well when you already know exactly what you want to tell the mapping agent.

---

## Option B: Use a Web UI synthesis session

This is the recommended path for large, mature, or politically complicated codebases.

Start a Web UI AI conversation about the repository. Discuss:

* what the repo is
* what the major components are
* which areas are most important
* which modules or packages should be prioritized
* what real-world examples best show intended usage
* what should be ignored or deprioritized
* what structural oddities may mislead an outsider
* what assumptions an AI mapping agent is likely to get wrong

Then paste:

```text
.bonsai/maps/repo_prompt.md
```

into the conversation, along with:

```text
.bonsai/maps/templates/map_repo_template.md
```

The AI should return a completed:

```text
map_repo.md
```

Copy it into:

```text
.bonsai/maps/map_repo.md
```

---

## Stage 2: Build the repository compass

Start a coding-agent session:

```text
Read .bonsai/maps/map_prompt.md and follow its instructions.
```

The first pass should establish or refresh:

* `code_map.md`
* `map_state.md`

Optionally:

* `namespace_router.tsv`
* `manifest.tsv`
* `symbol_index.tsv`, only if an early real lookup need exists

This phase should identify:

* source roots
* build and packaging boundaries
* major runtime surfaces
* likely subsystem boundaries
* the first subsystem or subsystems worth mapping deeply
* the small set of high-value namespace prefixes worth keeping in `code_map.md`
* whether fuller package / namespace routing should live in `namespace_router.tsv`

The agent should consult:

```text
templates/code_map_template.md
templates/map_state_template.md
templates/namespace_router_template.tsv
templates/manifest_template.tsv
templates/symbol_index_template.tsv
```

when creating those files.

---

## Review the initial map

After the top-level map is built, inspect it.

Questions worth asking:

* Did it identify the right major subsystems?
* Did it over-rank something large but unimportant?
* Did it miss the most developer-relevant areas?
* Does the drill-down order feel right?
* Is `code_map.md` still compact?
* Did the high-value namespace router stay genuinely high-value?
* If broader package routing exists, does it belong in `namespace_router.tsv` instead of the startup map?

If needed, revise:

```text
map_repo.md
```

and run a correction pass.

---

# Stage 3: Map one subsystem per clean session

This is the most important operating rule.

> **Start a fresh AI session for each subsystem.**

For example:

```text
Read .bonsai/maps/map_prompt.md and follow its instructions.
Focus on the history subsystem.
```

or:

```text
Read .bonsai/maps/map_prompt.md and follow its instructions.
Map the driver subsystem next.
```

A clean subsystem session should:

1. read the normal mapping-session inputs required by `map_prompt.md`

2. read the current `code_map.md`

3. identify the targeted subsystem

4. inspect only the relevant source, examples, and tests

5. create or update:

   ```text
   subsystems/<subsystem>/map.md
   ```

6. immediately decide whether `api_pub.md` or `api_ext.md` are genuinely warranted for that same subsystem

7. create or update any justified API maps before selecting another subsystem

8. consult the relevant templates when creating those files

9. update `map_state.md`

10. update `code_map.md` only if top-level routing changes

11. update `namespace_router.tsv` only if fuller package / namespace ownership lookup materially changes or becomes worth preserving

12. update `manifest.tsv` or `symbol_index.tsv` only when their narrow lookup role justifies it

The unit of progress is not merely “a subsystem map exists.”
The active subsystem is complete enough to move past only after its architecture map exists and its
API-map need has been evaluated, with any warranted API maps created or refreshed.

---

## Why fresh subsystem sessions matter

Subsystem mapping is deceptively context-heavy.

A mapping agent accumulates:

* source observations
* architectural hypotheses
* terminology
* call-site patterns
* uncertainties
* decisions about what matters and what does not

If you map one subsystem and then immediately continue into another within the same long session,
the later subsystem gets analyzed through the residue of the earlier one.

That increases the risk of:

* accidental analogy
* stale assumptions
* overloading the context window
* preserving too much “just in case”
* weaker compression judgment

Bonsai’s general philosophy applies here too:

> **Keep durable memory outside the chat. Start clean sessions often.**

`map_state.md` carries the baton. The chat does not need to.

---

# Stage 4: Add API maps only when they earn their keep

Subsystem architecture maps are common. API maps should be more selective.

However, that selectivity is evaluated **immediately after the subsystem architecture map**, not
deferred until after mapping unrelated subsystems. This prevents foundational subsystems from being
left architecturally mapped but mechanically under-documented while the agent wanders into fringe
areas.

Do **not** automatically create:

```text
api_pub.md
api_ext.md
```

for every subsystem.

Create them only when they capture exact mechanics that are:

* reusable
* non-obvious
* likely to recur
* easy for AI to get wrong
* valuable enough to load separately

---

## Good reasons to create `api_pub.md`

* Callers must use a specific retrieval pattern.
* A cursor or iterator has a lifecycle rule.
* Query parameters have non-obvious semantics.
* Return values can be stale, partial, or availability-sensitive.
* Event subscription requires cleanup.
* A public method looks simple but has important fallback behavior.

---

## Good reasons to create `api_ext.md`

* Providers must register through a specific capability or service mechanism.
* Subclassers must override hooks in a particular sequence.
* Event notifications must occur after mutation.
* Object identity matters.
* Lifecycle timing matters.
* A future or callback must eventually complete.
* A required super-call is easy to miss.

---

## Bad reasons to create API maps

* The subsystem simply has public interfaces.
* The code has many methods.
* The AI can extract signatures easily.
* “It might be useful someday.”
* The map feels incomplete without one.

A map system that documents everything eventually stops helping.

---

# Stage 5: Calibrate against real usage

After mapping an important subsystem, consider a calibration pass.

Use:

* representative production modules
* realistic examples
* tests
* owner-identified hot spots

The purpose is to catch mismatches between:

* what the subsystem appears designed to do
* what developers actually do with it

Calibration is especially useful for:

* frameworks
* extension systems
* driver stacks
* plugin systems
* long-lived repositories with evolved conventions

---

# Stage 6: Maintain maps without over-updating them

Maps should evolve when the repository meaningfully changes.

Update maps after code changes that alter:

* public structure
* extension points
* lifecycle rules
* major architectural relationships
* rebuild-relevant behavior
* reusable caller or extension mechanics
* package / namespace ownership guidance that future agents will reuse

Do **not** update maps for:

* local bug fixes
* private implementation refactors with no structural significance
* routine tests
* cosmetic code cleanup
* temporary debugging work

The implementation workflow should keep this distinction sharp.

---

# Recommended Session Cadence

## Good cadence

### Session 1

Web UI repo-calibration session:

* produce `map_repo.md`

### Session 2

Initial coding-agent mapping pass:

* build `code_map.md`
* build `map_state.md`
* maybe build `namespace_router.tsv`
* maybe build `manifest.tsv`

### Session 3

Clean session: map subsystem A and evaluate/create its warranted API maps.

### Session 4

Clean session: map subsystem B and evaluate/create its warranted API maps.

### Session 5

Clean session: map subsystem C and evaluate/create its warranted API maps.

### Session 6

Clean session: calibrate subsystem A against representative real usage.

### Session 7

Clean session: compress or refine top-level routing if needed.

---

## Poor cadence

One giant session that:

* invents `map_repo.md`
* maps the repository
* maps six subsystems
* creates twelve API maps
* builds a giant package router in `code_map.md`
* creates lookup files without a clear use
* tries to compress itself at the end

That is exactly how a mapping workflow gets noisy, overconfident, and bloated.

---

# Using Maps During Implementation

The normal Bonsai implementation flow should read:

```text
.bonsai/maps/code_map.md
```

at startup, then drill into deeper subsystem maps only when the current implementation step requires
them.

For example:

* load `subsystems/history/map.md` when working in history
* load `subsystems/history/api_pub.md` when calling the history API
* load `subsystems/history/api_ext.md` when implementing a history extension point
* load `namespace_router.tsv` only when fuller package / namespace ownership lookup is useful

This keeps implementation context selective.

`code_map.md` should also tell an agent that, **if it is about to edit Bonsai map artifacts**, it
must first read:

```text
.bonsai/maps/map_system.md
```

That does not make `map_system.md` part of ordinary implementation startup. It is an edit-time
guardrail for agents that are maintaining the maps.

Optional lookup artifacts can help when they exist:

* `namespace_router.tsv` for fuller package / namespace ownership lookup
* `manifest.tsv` for compact subsystem-to-path lookup
* `symbol_index.tsv` for selected high-value symbol-to-path lookup

They should not replace `code_map.md`.

---

# Refreshing Maps After Architecture Changes

After meaningful code changes, the implementation agent may need to update relevant maps.

When it does, `code_map.md` should route it to:

```text
.bonsai/maps/map_system.md
```

before it edits those map artifacts.

The threshold is structural significance, not mere code churn.

Good update triggers:

* new public service API
* changed extension point
* changed lifecycle sequence
* new major subsystem boundary
* package ownership change
* a discovered non-obvious mechanic that should not be forgotten
* broader package / namespace routing that should be preserved outside `code_map.md`

---

# Quality Standard

A good Bonsai map system should feel:

* **small enough to load**
* **specific enough to matter**
* **layered enough to stay selective**
* **grounded enough to trust**
* **restrained enough not to become a second codebase**

The maps are succeeding when an implementation agent:

* starts faster
* routes better
* asks fewer dumb questions of the repo
* reopens less irrelevant source
* gets important extension and caller patterns right earlier

---

# What Not To Do

## Do not map everything equally

Not every module deserves a subsystem map.
Not every subsystem deserves API maps.

Invest where future sessions will benefit.

---

## Do not preserve all findings

A mapping session may discover many interesting things.
Only some deserve durable memory.

Durable maps should contain reusable signal, not session residue.

---

## Do not let `map_state.md` become a report

If it starts accumulating:

* completed-work history
* long findings lists
* subsystem summaries
* old decisions

then it is failing.

State is for handoff, not archival memory.

---

## Do not let API maps replace source

API maps should prevent repeated avoidable mistakes.
They should not aspire to make source reading unnecessary.

---

## Do not let `code_map.md` become the package registry

A small high-value namespace router belongs in `code_map.md` when it improves first-load orientation.

A fuller router belongs in:

```text
namespace_router.tsv
```

when it is worth preserving.

If the `code_map.md` router starts feeling like a lookup database, it has crossed the line.

---

## Do not let TSV lookup artifacts sprawl

`namespace_router.tsv`, `manifest.tsv`, and `symbol_index.tsv` are narrow support data.

Do not turn them into:

* prose documentation
* exhaustive inventories without a clear routing purpose
* a substitute for `code_map.md`
* a substitute for source search

---

## Do not keep extending a stale session

When you finish one subsystem, stop.
Start fresh for the next one.

That is one of the core Bonsai habits.

---

# Suggested Starter Sequence for a New Repository

For a substantial unfamiliar repo:

1. Use a Web UI calibration session to produce `map_repo.md`
2. Run the initial coding-agent mapping pass:

    * `code_map.md`
    * `map_state.md`
    * maybe `namespace_router.tsv`
    * maybe `manifest.tsv`
3. Clean session: first foundational subsystem, plus its justified API maps
4. Clean session: second foundational subsystem, plus its justified API maps
5. Clean session: primary developer-facing extension subsystem, plus its justified API maps
6. Clean session: main external entry point or API surface, plus its justified API maps
7. Calibration pass against real usage examples
8. Stop and evaluate whether the existing maps are already enough

Do not aim to finish “the entire map system.”
Aim to reach the point where future implementation sessions are materially better.

---

# Relationship to Rebuildability

Bonsai projects preserve the final intended product shape.

Bonsai maps preserve the repository understanding needed to work effectively toward that shape.

They are different forms of durable memory, but they reinforce each other:

* project memory prevents implementation drift
* map memory prevents codebase rediscovery drift

Together, they let AI-assisted work stay both intentional and efficient over long periods.

---

# Status

The Bonsai mapping workflow is intended to be:

* lightweight
* incremental
* selective
* friendly to frequent fresh sessions
* especially valuable for large, mature, or framework-heavy repositories

The core operating principle is simple:

> **Teach the repository once. Preserve only what future sessions will reuse.**
