# Dry Run Procedure

## Purpose

Provide a compact, read-only execution preview before files are modified. It supports human steering; it is not a design document or implementation walkthrough.

## When to Use

Read this file only when the user requests a dry run at an execution authorization gate.

## Rules

* Do not modify files, update Bonsai documents, write code, or run destructive commands during a dry run.
* Use the approved contract, active phase plan, or recorded exact next step as the execution basis.
* Perform only limited read-only inspection needed to identify credible touch points, checks, or scope risks. Prefer Bonsai maps and architecture guidance before broad source exploration.
* Keep the output compact. Identify file groups or subsystems rather than speculative line-by-line edits.
* Do not restate requirements, architecture, or contract detail already available in the approved basis.
* Surface uncertainty explicitly. Do not turn assumptions into approved scope.

## Output

Output:

````markdown
## Dry Run: <exact next step>

Basis:
- <approved contract, phase plan, or recorded next step>

Expected touch points:
- <file group, subsystem, or artifact>

Intended result:
- <concrete outcome>

Planned checks:
- <test, build, validation, or review check>

Scope concerns:
- <None, or concise potential deviation>

1. Approve this dry run and proceed with the described work.
2. Request revisions to this dry run.
3. Return to the prior gate.
4. Stop here.
````

Add detail only when needed to prevent material ambiguity.

## After Approval

If the user approves the dry run:

1. Record in `state.md` a compact approved execution baseline: basis, intended result, expected touch points, and planned checks.
2. Execute only against that baseline and already-approved project direction.
3. Before implementing a material deviation, STOP and use the Material Deviations gate in `implementation_prompt.md`.
4. At completion, compare actual changes and checks against the approved baseline.
5. Remove or replace the active baseline after completion or redirection.

## Compactness Test

Before presenting a dry run, remove any detail that does not help the human decide whether to authorize the stated work. If the preview becomes a design discussion, stop and return to the appropriate planning or contract gate.
