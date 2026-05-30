# Dry Run Skill

## Purpose

Provide a compact, read-only execution preview before files are modified.

A dry run supports human steering. It is not a design document, implementation walkthrough, or substitute for a required approval gate.

## Required Inputs

Use the most specific approved execution basis available:

* Approved contract.
* Active phase plan.
* Recorded exact next step.
* Approved final-truth impact, when already known.
* Approved dry-run baseline, when revising or replacing a prior dry run.

If no approved execution basis exists, do not invent one. Return to the applicable planning, contract, or handoff gate.

## Rules

* Do not modify files, update Bonsai documents, write code, or run destructive commands during a dry run.
* Perform only limited read-only inspection needed to identify credible touch points, checks, or scope risks.
* Prefer Bonsai maps and architecture guidance before broad source exploration.
* Keep the output compact.
* Identify file groups, subsystems, or artifacts rather than speculative line-by-line edits.
* Do not restate requirements, architecture, or contract detail already available in the approved basis.
* Surface uncertainty explicitly.
* Do not turn assumptions into approved scope.
* Classify anticipated final-truth impact using `None`, `Clarification`, or `Revision`.
* A `Revision` may be previewed, but cannot authorize substantive implementation before affected final-truth documents are updated and approved.

## Procedure

1. Identify the exact next step being previewed.
2. Identify the approved basis for the work.
3. Inspect only enough existing project context to produce a credible execution preview.
4. Identify expected touch points at the file-group, subsystem, or artifact level.
5. State the intended result in concrete terms.
6. Classify anticipated final-truth impact.
7. List planned checks.
8. Surface material scope concerns or report `None`.
9. Present the dry-run approval choices.

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

Final-truth impact: <None | Clarification | Revision>
- Affected documents: <None, or final-truth document paths>
- Required update before implementation: <None, proposed clarification, or required approved revision>

Planned checks:
- <test, build, validation, or review check>

Scope concerns:
- <None, or concise potential deviation>

1. Approve this dry run and proceed with the described work.
2. Request revisions to this dry run.
3. Return to the prior gate.
4. Stop here.
````

For a `Revision`, replace option 1 with:

````markdown
1. Draft proposed updates to the affected final-truth documents for review.
````

Add detail only when needed to prevent material ambiguity.

## Approval Handling

If the user approves the dry run:

1. Record a compact approved execution baseline in `state.md`.
2. Include the basis, intended result, expected touch points, anticipated final-truth impact, affected final-truth documents when applicable, and planned checks.
3. Execute only against that baseline and already-approved project direction.
4. Do not implement work classified as `Revision` until affected final-truth documents have been updated and approved.
5. Before implementing a material deviation, stop and use the applicable gate from `implementation_prompt.md`.
6. At completion, compare actual changes, checks, and final-truth impact against the approved baseline.
7. Remove or replace the active baseline after completion or redirection.

## Compactness Test

Before presenting a dry run, remove any detail that does not help the human decide whether to authorize the stated work.

If the preview becomes a design discussion, stop and return to the appropriate planning or contract gate.

## Stop Conditions

Stop instead of presenting or executing a dry run when:

* There is no approved basis for the proposed work.
* The requested work changes requirements, architecture, system boundaries, or intended behavior without approved final-truth updates.
* The dry run would require destructive commands, code edits, or Bonsai document updates before approval.
* The preview cannot be made credible without broader design or planning work.
* The user chooses to return to the prior gate or stop here.
