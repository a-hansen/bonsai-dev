# Developer Context

Optional context for AI coding sessions.

This file contains stable developer-specific preferences, intentionally supplied local environment notes, and recurring instructions. It is not project truth.

Project requirements, architecture, plans, and state belong in the project memory files.

This file is developer/team-maintained. Do not automatically append operational facts discovered by the agent.
Durable learned tooling/environment facts belong in optional `.bonsai/tooling.md`, governed by
`.bonsai/skills/tooling_memory.md`.

## Personal Working Preferences

- Prefer simple, direct code over clever abstractions.
- Prefer small, reviewable diffs.
- Ask before broad refactors.

## Coding Preferences

- Prefer existing project patterns over new frameworks.
- Keep public APIs conservative.
- Avoid unnecessary dependencies.

## Declared Local Environment

- SDK locations:
    - Example: `NIAGARA_HOME=...`
- Build tools:
    - Example: Gradle wrapper preferred when available.
- Runtime constraints:
    - Example: Some Niagara projects cannot be tested with normal unit tests.

## AI Session Preferences

- Report assumptions clearly.
- Stop before making large scope changes.
- Treat intentionally supplied local paths and machine-specific setup as developer context, not project truth.
- Keep learned operational workarounds out of this file unless the developer/team explicitly chooses to promote them here.

## Notes

- Keep secrets out of this file.
- Keep machine-specific copies out of source control unless intentionally shared.

- If observed environment behavior conflicts with this file, surface the mismatch rather than silently editing
  developer-owned context.
- Agent-discovered tooling facts are maintained separately in `.bonsai/tooling.md` only when they satisfy the
  tooling-memory skill's durability and usefulness rules.
