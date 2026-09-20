# Agent Context

## Purpose

Govern durable, agent-owned operational memory without making it routine startup context or confusing it with project truth, developer-owned guidance, execution state, or troubleshooting history.

This skill owns optional `agent_context.md` files at developer, repository, and project scopes. It replaces the Bonsai 1.x tooling-only seam; do not read, create, or maintain a `tooling.md` compatibility artifact.

## When to Load

Before choosing or executing a build, test, run, package, interpreter, toolchain, or other environment-sensitive command, load this skill and the applicable existing agent context.

Also load it when the current work requires an operational choice involving durable filesystem/environment behavior, source locations, code-map locations/selections, or when a qualifying operational discovery may need preservation.

Trigger prospectively. Do not first try the literal command or path from planning memory, and do not wait for an operation to fail before consulting applicable context.

Do not load agent context merely because a file exists or because implementation startup is occurring. Trigger it only when the current work reaches an operational facet it can govern.

Once triggered, keep relevant loaded context available for the session.

## Scope and Authority

Resolve relevant optional files from the identity supplied by `start.md`:

```text
$BONSAI_HOME/agent_context.md
<repository-home>/.bonsai/agent_context.md
<project-home>/agent_context.md
```

Read relevant layers broad to specific; read identical resolved paths once. For the same subject:

```text
developer-level -> repository-level -> project-level
```

More-specific context governs only while consistent with current evidence, approved project truth, human-owned developer context, and authorized scope. Agent context never overrides those authorities or grants authorization.

## Applying Existing Context

Applicable context governs concrete operational choices within those boundaries. Agent-owned execution memory may name an intended build, test, run, or inspection command, but applicable environment context may resolve literal syntax when the authorized operation and success condition remain unchanged.

Example: if planning memory says `python -m unittest -q` and applicable context establishes `python3`, run `python3 -m unittest -q`. This is operational resolution, not a phase-plan, roadmap, or final-truth change. Human-owned instructions intentionally requiring an exact literal command remain authoritative.

Using an existing correct rule is read-only and is not discovery. Do not rewrite, normalize, reorder, touch, or restate `agent_context.md` merely because it was loaded or applied. Maintain it only for newly learned, materially corrected, consolidated, or disproved qualifying operational truth.

## Qualification Rule

Preserve a learned fact only when all are substantially true:

- **Durable:** likely to persist across future sessions.
- **Reusable:** likely to prevent meaningful rediscovery.
- **Actionable:** changes how an agent should successfully inspect, build, test, run, navigate, or operate.
- **Sufficiently supported:** direct evidence supports a trustworthy current rule.
- **Operational:** concerns working behavior, not product intent, architecture, roadmap, or ordinary source behavior.

Store the useful current rule, not its discovery story. Exclude speculative causes, command history, unique temporary paths/process identifiers, and transient failures.

## Write Scope

Use the narrowest reusable scope:

- **developer:** useful across repositories, such as a stable cross-repository source location;
- **repository:** shared by Bonsai projects in one repository, such as its build invocation;
- **project:** useful only to the active project, such as selected external code maps.

Never store active-project selection; it is current-session identity, not durable operational memory.

## Project Code-Map Associations

Association maintenance is entered only through **Manage Code Maps**. The invoking workflow must supply one validated active project, the independently resolved active generated-map store, one concrete generated-map identity, and the human-selected add/remove operation.

Immediately before writing, revalidate all identities:

- project home is one immediate child of `<repository-home>/.bonsai/projects/` and contains readable `agent_plan.md` and `agent_state.md`; the containing `projects/` path establishes project type without a workspace-local manifest;
- map name is one directory component; its immediate active-map-store directory contains readable agent-owned `code_map.md`;
- repository-local map workspaces, including same-named ones, are never association evidence or substitutes for the generated-map check.

Any validation failure: stop without mutation.

Otherwise modify only `<project-home>/agent_context.md`, using at most one unambiguous canonical block:

```text
Useful code maps:
- barcache
- tickerview
```

Preserve existing selection order and unrelated project context.

- **Add:** append only if absent; existing selection is a no-op.
- **Remove:** delete only the exact selected item; absent selection is a no-op.
- Never create duplicates.
- If removal empties the block, remove the block and its associated excess blank line.
- If the file is then otherwise empty, remove the file.

Later, when map-guided navigation is relevant, these entries are the selected map identities. Resolve each named `<active-map-store>/<map>/code_map.md` directly; do not enumerate the map store to rediscover selections. A missing/unreadable named entry is stale context: surface it, do not rely on that map, and do not silently rewrite selection outside an authorized association action.

Association maintenance must not discover dependencies, infer selections from project truth, copy all usable maps into project context, or modify developer/repository context. It never changes a generated map, repository-local map workspace, project execution memory, project final truth, or active workspace/session identity.

Verify only the selected project's context changed, report mutation versus no-op, then return control to the invoking code-map workflow.

## Execution-State Boundary

Keep unresolved current blockers in `<project-home>/agent_state.md`. A separate durable lesson learned while investigating a blocker may also enter applicable `agent_context.md` if it passes the qualification rule.

Do not use agent context for requirements, architecture, roadmap decisions, phase/pass state, approval state, exact next step, dry-run state, or deferred observations.

## Developer-Context Boundary

`developer_context.md` is intentional human-owned guidance; `agent_context.md` is learned agent-owned operational memory.

- Do not copy discoveries into or silently edit developer context.
- Do not use agent context to override developer context.
- If direct evidence materially conflicts with developer context, surface the mismatch without reproducing sensitive values; the human decides whether human-owned guidance changes.
- A proven operational fact may still be maintained in agent context when it independently passes the qualification rule.

## Maintenance

The agent may create, update, consolidate, correct, or prune applicable `agent_context.md` without a separate human gate when maintaining qualifying operational truth. Do not write merely because context was loaded/applied; leave already-correct guidance unchanged.

When writing:

- create a file only for the first qualifying fact at that scope;
- organize by current concern, not chronology;
- replace stale entries rather than append contradictory history;
- consolidate duplicates; prune ambiguous or obsolete rules;
- keep wording concise, operational, and sufficiently explained to remain trustworthy;
- omit empty template sections;
- never store credentials, tokens, private keys, or other secrets.

If direct evidence contradicts an entry, use current evidence and correct/remove the stale entry. If it is no longer actionable or sufficiently supported, clarify when evidence permits; otherwise prune it.

## Authority Boundary

Agent-context maintenance does not authorize:

- software installation/uninstallation;
- machine, shell, user, or environment configuration changes;
- credential changes;
- project dependency or build-configuration changes outside approved scope;
- modification of developer-owned context or human-owned final truth;
- broadening the exact next step or implementation scope;
- acceptance of failed required checks.

Delegate such actions to the normal execution workflow and applicable human gate.

## Completion

Maintain qualifying context when learned or disproved; do not defer routine correction until handoff. Context maintenance alone has no final-truth impact.

After applying or maintaining context, return to the exact next step or invoking workflow/gate. Report unresolved blockers through execution state, not agent context.
