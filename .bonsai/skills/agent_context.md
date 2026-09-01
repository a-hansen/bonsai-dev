# Agent Context

## Purpose

Govern durable, agent-owned operational memory without making it routine startup context or confusing it with
project truth, developer-owned guidance, execution state, or troubleshooting history.

This skill owns optional `agent_context.md` files at developer, repository, and project scopes. It replaces the
Bonsai 1.x tooling-only memory seam; do not read, create, or maintain a `tooling.md` compatibility artifact.

## When to Load

Load this skill only when the current facet may need to apply, discover, correct, or preserve operational
knowledge, including:

- tooling, build, test, runtime, filesystem, or environment working rules;
- stable source locations;
- code-map locations or selection rules;
- another stable operational fact that changes how future work should proceed.

Do not load agent context merely because a file exists or because implementation startup is occurring. Once this
skill is triggered, keep the relevant loaded context available for the current session.

## Scope Layers

Resolve these optional files from the identity supplied by `start.md`:

```text
$BONSAI_HOME/agent_context.md
<repository-home>/.bonsai/agent_context.md
<project-home>/agent_context.md
```

Read only the layers relevant to the current facet, broad to specific. If two resolved paths identify the same
file, read it once. Within agent context, a more-specific statement governs the same subject:

```text
developer-level
    -> repository-level
        -> project-level
```

Apply an entry only when it remains consistent with current evidence, approved project truth, human-owned
developer context, and the authorized scope. Agent context never overrides those authorities and grants no new
authorization.

## Qualification Rule

Preserve a learned fact only when all of these are substantially true:

- **Durable:** likely to remain true across future sessions rather than describe a transient event.
- **Reusable:** likely to prevent meaningful rediscovery in later work.
- **Actionable:** changes how an agent should successfully inspect, build, test, run, navigate, or operate.
- **Sufficiently supported:** direct evidence supports a trustworthy current rule.
- **Operational:** concerns working behavior rather than product intent, architecture, roadmap, or ordinary source
  behavior.

Store the useful current rule, not the discovery story. Do not preserve speculative causes, command-by-command
history, unique temporary paths or process identifiers, or transient failures.

## Choosing the Write Scope

Write a qualifying fact at the narrowest scope that keeps it reusable:

- developer level for a working rule useful across repositories, such as a stable cross-repository source
  location;
- repository level for a rule shared by Bonsai projects in one repository, such as its build invocation;
- project level for facts useful only to the active project, such as its selected external code maps.

Do not store active-project selection in any scope. It is current-session identity, not durable operational
memory.

## Execution-State Boundary

Keep an unresolved current blocker in `<project-home>/agent_state.md`. A separate durable lesson established while
investigating that blocker may also enter the applicable `agent_context.md` when it passes the qualification rule.

Do not use agent context for requirements, architecture, roadmap decisions, phase or pass state, approval state,
the exact next step, dry-run state, or deferred observations.

## Developer-Context Boundary

`developer_context.md` is intentionally supplied and controlled by the developer or team. `agent_context.md` is
learned operational memory maintained by the agent.

- Do not copy discoveries into developer context or silently edit it.
- Do not use agent context to override developer context.
- If direct evidence materially conflicts with developer context, surface the mismatch without reproducing any
  sensitive value. Let the human decide whether human-owned guidance should change.
- A proven operational fact may still be maintained in agent context when it independently passes the
  qualification rule.

## Maintenance

The agent may create, update, consolidate, correct, or prune an applicable `agent_context.md` without a separate
human gate when maintaining qualifying operational truth.

When writing:

- create a file only for the first qualifying fact at that scope;
- organize by current concern, not chronology;
- update or replace a stale entry instead of appending contradictory history;
- consolidate duplicates and prune ambiguous or obsolete rules;
- keep wording concise, operational, and sufficiently explained to be trustworthy;
- omit empty template sections;
- never store credentials, tokens, private keys, or other secrets.

If an existing entry is contradicted by direct evidence, use the current evidence and correct or remove the stale
entry. If it is no longer actionable or sufficiently supported, clarify it when evidence permits; otherwise prune
it.

## Authority Boundary

Agent-context maintenance does not authorize the agent to:

- install or uninstall software;
- change machine, shell, user, or environment configuration;
- modify credentials;
- change project dependencies or build configuration outside approved scope;
- modify developer-owned context or human-owned final truth;
- broaden the exact next step or implementation scope;
- accept failed required checks.

Delegate any such action to the normal execution workflow and its applicable human gate.

## Completion

Maintain qualifying context when the fact is learned or disproved rather than deferring routine correction until
handoff. Context maintenance alone has no final-truth impact.

After applying or maintaining context, return to the exact next step or to the workflow or gate that invoked this
skill. Report any unresolved blocker through execution state, not agent context.
