# Developer Context

Optional context for AI coding sessions.

This file contains stable developer-specific preferences, local environment notes, and recurring instructions. It is not project truth.

Project requirements, architecture, plans, and state belong in the project memory files.

## Personal Working Preferences

- Prefer simple, direct code over clever abstractions.
- Prefer small, reviewable diffs.
- Ask before broad refactors.

## Coding Preferences

- Prefer existing project patterns over new frameworks.
- Keep public APIs conservative.
- Avoid unnecessary dependencies.

## Local Environment

- SDK locations:
    - Example: `NIAGARA_HOME=...`
- Build tools:
    - Example: Gradle wrapper preferred when available.
- Runtime constraints:
    - Example: Some Niagara projects cannot be tested with normal unit tests.

## AI Session Preferences

- Report assumptions clearly.
- Stop before making large scope changes.
- Treat local paths and machine-specific setup as developer context, not project truth.

## Notes

- Keep secrets out of this file.
- Keep machine-specific copies out of source control unless intentionally shared.