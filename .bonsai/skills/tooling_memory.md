# Tooling Memory

## Purpose

Preserve durable operational knowledge learned while working in a repository without bloating routine startup
context or turning troubleshooting history into project memory.

This skill governs optional:

```text
.bonsai/tooling.md
```

`tooling.md` is agent-maintained learned operational memory. It is not project truth, execution authority,
developer-owned context, or a session log.

## When to Load

Load this skill when any of the following is true:

* `state.md` identifies a tooling/environment blocker.
* The exact next step is explicitly to diagnose or change tooling/environment behavior.
* Execution encounters an unexpected tooling, build, test-runner, filesystem, temporary-directory,
  command-availability, dependency/tool-version, permission, or runtime-environment issue.

Do not load this skill merely because normal implementation will compile, test, package, or run code.

## Lazy-Load Rule

After this skill is loaded:

1. Read optional `.bonsai/tooling.md` when present before doing non-trivial troubleshooting.
2. Apply relevant current entries when they do not conflict with higher-authority instructions or approved scope.
3. If `.bonsai/tooling.md` is absent, continue normally. Do not create it until a newly learned fact qualifies
   for preservation.
4. Keep the skill and tooling memory available for the remainder of the current session once loaded.

Routine implementation startup does not read `.bonsai/tooling.md`.

## What Qualifies for Preservation

Record a learned fact only when all of these are substantially true:

* **Durable:** it is likely to remain true across future sessions rather than being a transient failure.
* **Reusable:** encountering the same condition again would otherwise cause meaningful rediscovery or wasted work.
* **Actionable:** the fact changes how the agent should successfully build, test, inspect, run, or manipulate
  repository artifacts.
* **Evidence-based:** enough direct evidence exists to state a useful current rule or workaround.
* **Operational:** the fact concerns the working environment or tool execution rather than product intent,
  architecture, roadmap scope, or ordinary source-code behavior.

Prefer the current working rule over the discovery story.

Good:

```text
- Prefer repository-local `.tmp/` for intermediate artifacts because this environment does not reliably permit
  the required operation under `/tmp`.
```

Poor:

```text
- `/tmp/foo-48392` failed, then `/tmp/foo-61723` worked.
```

## Appropriate Content

Examples include:

* required wrapper or launcher usage
* installed tools that are unavailable through the expected command or `PATH`
* stable tool/version limitations that change available commands
* reliable repository-specific build or test invocation quirks
* recurring filesystem, permission, or temporary-directory constraints
* known cache or runtime behavior that changes how work must be executed
* known harmless warnings that would otherwise trigger repeated investigation
* a proven workaround for a recurring local execution problem

## Do Not Preserve

Do not write the following to `tooling.md`:

* command typos or malformed one-off invocations
* unique temporary paths or process identifiers
* transient network/service failures without evidence of a durable rule
* speculative causes that have not been established
* every failed attempt made while debugging
* historical sequences once the current rule is known
* current execution blockers merely because they are active
* project requirements, architecture decisions, roadmap decisions, or phase status
* general software-engineering knowledge that is not specific to this repository/environment
* secrets, credentials, tokens, private keys, or sensitive values

If an unresolved tooling issue blocks the exact next step, record the blocker in `state.md` according to normal
Bonsai state rules. If the investigation also establishes a durable operational fact, that separate fact may be
recorded in `tooling.md`.

## Relationship to Developer Context

`.bonsai/developer_context.md` is intentionally supplied and maintained by the developer or team.

`.bonsai/tooling.md` is learned by the agent from actual repository/environment work.

Do not automatically copy learned tooling facts into `developer_context.md`.

Do not use `tooling.md` to override explicit developer-context instructions. If observed behavior materially
conflicts with developer context:

* surface the mismatch when it matters to current execution,
* preserve a proven operational fact in `tooling.md` only if it still satisfies the normal preservation rules,
* do not silently edit `.bonsai/developer_context.md`,
* allow the human to decide whether developer context should be corrected or updated.

## Authority Boundary

The agent may create, update, consolidate, or prune qualifying `.bonsai/tooling.md` entries without human
approval.

That maintenance does **not** authorize the agent to:

* install or uninstall software
* change system or user configuration
* modify credentials
* change dependency versions
* alter repository build configuration outside approved scope
* modify `.bonsai/developer_context.md`
* broaden the exact next step
* accept failed required checks

Those actions remain subject to the normal Bonsai execution and human-gate rules.

## Maintenance Rules

When writing `.bonsai/tooling.md`:

* create it only when the first qualifying fact exists
* organize by current concern, not chronology
* update an existing entry instead of appending a newer contradictory history entry
* consolidate duplicates
* remove or correct entries when direct evidence shows they are stale
* keep wording concise and operational
* preserve enough explanation to make the rule trustworthy and usable
* avoid timestamps unless time itself is operationally relevant
* keep secrets out

A useful default structure is:

```text
# Tooling Memory

Agent-maintained learned operational knowledge for this repository/environment.
Current rules and workarounds only. Not project truth or troubleshooting history.

## Build and Test

## Tools and Versions

## Filesystem and Temporary Files

## Runtime and Environment

## Known Issues and Workarounds
```

Do not create empty sections merely to satisfy the template.

## Applying Existing Memory

When existing `tooling.md` contains a relevant entry:

1. Treat it as a useful learned observation, not unquestionable authority.
2. Apply it when consistent with current evidence, developer context, project truth, and approved scope.
3. If current evidence disproves it, use the current environment behavior and correct or remove the stale entry.
4. If it is ambiguous or no longer actionable, prefer pruning or clarifying it over preserving uncertainty.

## Completion

Update qualifying tooling memory when the fact is learned or corrected. Do not defer routine tooling-memory
maintenance until handoff.

Tooling-memory maintenance does not itself create a final-truth `Clarification` or `Revision`.

If tooling-memory maintenance was triggered by a blocker, return to the exact next step once the blocker is
resolved or report the remaining blocker through normal Bonsai execution state.
