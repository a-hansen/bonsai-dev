# Final-Truth Update Skill

## Purpose

Protect human-owned durable meaning when proposed, discovered, or completed work clarifies or changes project or
Bonsai final truth. This skill classifies impact, obtains explicit authorization, applies only approved updates,
reconciles downstream execution memory, and returns control to the workflow that invoked it.

Normal maintenance of `agent_plan.md`, `agent_state.md`, phase plans, maps, agent context, or icebox content is not
by itself a final-truth change.

## When to Load

Load this skill when a proposed or completed step may require a `Clarification` or `Revision` to requirements,
architecture, the Bonsai specification, or another explicitly designated human-owned final-truth document.

## Required Inputs

- The invoking workflow and gate, when this is subordinate work.
- The approved execution basis.
- The proposed, discovered, or completed change.
- Current affected human-owned final truth.
- Relevant `agent_plan.md`, `agent_state.md`, and active phase plan needed to evaluate consequences.

Do not infer durable intent from chat history, execution memory, maps, context, or current implementation behavior.

## Authority and Ownership

Normal project final truth includes:

- `requirements.md` and applicable `requirements/requirements_<AREA>.md` files;
- `architecture.md` and applicable `architecture/architecture_<SUBSYSTEM>.md` files; and
- project-specific contracts or design artifacts explicitly designated by the human as final truth.

When Bonsai itself is the product, the active Bonsai Home's `../specification.md` is human-owned framework final
truth. Prompts, skills, templates, bootstrap files, README guidance, helper scripts, execution memory, and observed
workflow behavior implement or describe that specification; they are not peer authorities and cannot silently
redefine it. The specification keeps this authority whether it is staged, embedded, or installed in Bonsai Home.

Agent plans, state, phase plans, maps, agent/developer context, and icebox content may inform work but do not
authorize a final-truth change. Follow applicable ownership rules for every file; this skill does not turn an
agent-owned artifact into human-owned truth or vice versa.

## Impact Classification

Classify the actual durable-meaning impact, not the file type being edited.

### None

Use `None` when approved human-owned final truth already covers the work. No final-truth update is required;
ordinary execution-memory maintenance may still be necessary.

### Clarification

Use `Clarification` only when intended behavior, constraints, boundaries, and architecture remain unchanged but
approved final truth should state the existing intent more precisely. Examples include making an implied approved
decision explicit, tightening ambiguous wording, or correcting wording that conflicts with other approved truth.

A clarification cannot conceal changed behavior or design. It requires explicit human authorization before the
human-owned document is changed.

### Revision

Use `Revision` when intended behavior, constraints, product or system boundaries, architecture, or another
rebuild-relevant decision changes. Stop substantive implementation until the revision and affected documents are
explicitly approved and updated. Implementation behavior alone never makes a revision authoritative.

## Procedure

1. Preserve the identity of the invoking workflow and gate.
2. Identify the approved execution basis and compare the proposed or completed work with current final truth.
3. Classify impact as `None`, `Clarification`, or `Revision`.
4. Name every affected human-owned final-truth document, or explicitly report `None`.
5. For `None`, report that no final-truth update is required and return to the invoking workflow.
6. For `Clarification` or `Revision`, draft the exact proposed document changes for review without applying them.
7. Load `skills/menu.md`, present the applicable approval gate, and stop.
8. After explicit approval, apply only the reviewed changes.
9. Re-read the affected truth and reconcile downstream execution memory.
10. Recompute phase-plan validity, contract validity, exact next step, blockers, and execution readiness.
11. Return to the invoking gate with refreshed choices unless the reconciliation created a new required gate.

If the affected document or intended durable meaning is unclear, stop instead of guessing a patch.

## Human Gates

For a clarification, supply these choices to `skills/menu.md`:

1. Approve and apply the named clarification.
2. Request revisions to the clarification.
3. Discuss concerns before deciding.
4. Leave human-owned final truth unchanged and return to the invoking gate.

For a revision, supply:

1. Approve and apply the named final-truth revision.
2. Request revisions to the proposed update.
3. Discuss concerns before deciding.
4. Return to the prior planning or execution gate without changing final truth.

Do not offer substantive implementation while a required revision remains unresolved. Approval authorizes only
the reviewed final-truth edits and their necessary execution-memory reconciliation; it does not silently authorize
an invalidated implementation step.

## Execution-Memory Consequences

After an approved update, reconcile only memory whose current truth changed:

- roadmap sequencing or phase state in `agent_plan.md`;
- scope, mode, contract basis, steps, or approval status in an active phase plan;
- blockers, exact next step, readiness, active files, and compact resume truth in `agent_state.md`.

An approved change may invalidate an active plan or contract. Mark it accurately and route to `Phase planning
required`, `Awaiting human review`, or another applicable gate instead of preserving stale `Ready to execute`
state. Remove superseded facts rather than appending a change history.

These consequences maintain workflow consistency; they do not expand the set of final-truth documents.

## Return to the Invoking Gate

This skill is normally subordinate to startup, handoff, phase-plan review, contract review, dry run, observation
triage, or a deviation/correction gate. Completing, declining, or cancelling final-truth work does not discard that
parent gate.

After the action:

1. reconcile current execution memory;
2. recompute exact next step and readiness;
3. reload `skills/menu.md`; and
4. return to the invoking gate with refreshed concrete choices.

Present a new gate instead only when the approved update creates a planning, contract, design, blocker, or other
required gate that supersedes the parent decision.

## Forbidden Changes

- Do not silently edit human-owned final truth.
- Do not use `Clarification` to hide a revision.
- Do not bury product, architecture, or framework-specification changes in execution memory.
- Do not treat implementation behavior, README wording, prompts, skills, templates, maps, plans, context, or
  icebox content as authority over approved final truth.
- Do not let final-truth completion erase its invoking gate.
- Do not claim revised work complete while its required final-truth update remains unresolved.

## Completion Checks

Before returning, verify that the classification and affected documents are explicit, required authorization was
obtained, approved edits match the reviewed proposal, execution-memory consequences are current, and the invoking
or superseding gate is identified.

