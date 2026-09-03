# Dry Run Skill

## Purpose

Provide an optional, compact, read-only preview of one approved exact next step. A dry run helps human steering
before execution without becoming a required gate or granting implementation authorization.

It is not a design artifact, implementation walkthrough, or substitute for planning, contract, final-truth, or
execution authorization.

## When to Load

Load this skill only after the human selects Dry Run, whether that selection came from:

- an explicit human request;
- the ordinary Dry Run action under **See more options**; or
- a Dry Run action that the invoking workflow promoted into the primary menu because previewing the exact next
  step would materially reduce mechanical execution risk.

Dry Run applicability and promotion are decided by the invoking workflow before this skill is loaded.
`skills/menu.md` presents the supplied ordinary or promoted action. This skill must not independently advertise,
recommend, or promote itself.

If no approved basis or exact next step exists, return to the applicable owning gate as described below rather
than turning Dry Run into a way around design, planning, review, final-truth, contract, or blocker requirements.

## Required Inputs

Use the most specific approved basis available:

- approved contract, when one governs the step;
- approved active phase plan, when present;
- recorded exact next step;
- current execution memory;
- approved final-truth impact, when known; and
- an existing approved dry-run baseline, only when revising or replacing it.

Read only the project truth, source, maps, developer context, and agent context needed to make the preview
credible. If no approved basis or exact next step exists, return to the applicable design, planning, contract, or
handoff gate. Do not invent scope from repository contents or chat history.

## Read-Only Rules

During preview:

- do not modify source, project memory, Bonsai files, tests, generated output, or external state;
- do not run destructive commands or checks that write durable or generated output;
- use only limited read-only inspection needed to identify credible touch points, checks, uncertainties, and
  scope risks;
- prefer relevant approved architecture and maps before broad source exploration;
- describe artifacts, file groups, or subsystems instead of speculative line-by-line edits;
- do not restate detail already available in the approved basis;
- distinguish evidence from inference and state material uncertainty;
- do not turn assumptions into approved scope; and
- do not invent interfaces, module seams, abstractions, test structure, or coding conventions.

The preview itself performs no implementation and grants no authorization.

## Procedure

1. Preserve the invoking workflow and gate.
2. Identify the exact next step and approved basis.
3. Inspect only enough read-only context to produce a credible preview.
4. Identify expected touch points at artifact, file-group, or subsystem level.
5. State the intended result concretely.
6. Classify anticipated final-truth impact as `None`, `Clarification`, or `Revision` and name affected documents.
7. List planned checks without executing write-producing checks.
8. State material scope concerns and uncertainties, or `None`.
9. Load `skills/menu.md`, present the Dry Run Review Gate, and stop.

## Preview Format

Keep the output decision-focused:

```markdown
## Dry Run: <exact next step>

Basis:
- <approved contract, phase plan, or recorded exact step>

Expected touch points:
- <artifact, file group, or subsystem>

Intended result:
- <concrete outcome>

Planned checks:
- <test, build, static check, scenario, or review>

Anticipated final-truth impact: <None | Clarification | Revision>
Affected final-truth documents: <None or paths>
Required update before implementation: <None, proposed clarification, or required revision>

Scope concerns / uncertainties:
- <None or concise concern>
```

Add detail only when it materially helps the authorization decision. If the preview becomes design work, stop and
return to the appropriate design, planning, contract, or final-truth gate.

## Dry Run Review Gate

For `None` or `Clarification`, supply these choices to `skills/menu.md`:

1. Approve this preview and return to the invoking gate.
2. Request revisions to the preview.
3. Discard the preview and return to the invoking gate.
4. Stop here.

Approval records any warranted baseline but does not execute the work. The refreshed invoking gate remains the
place where the human authorizes the exact next step. If a clarification is required before execution, delegate to
`skills/final_truth_update.md` at that gate.

For `Revision`, do not offer implementation approval. Supply:

1. Draft proposed updates to the affected final-truth documents for review.
2. Request revisions to the preview.
3. Discard the preview and return to the invoking gate.
4. Stop here.

If option 1 is selected, delegate to `skills/final_truth_update.md`. After that subordinate workflow completes,
return through its invoking-gate rules unless a new mandatory gate supersedes the dry-run review.

## Approved Baseline Lifecycle

After the human approves the preview, record a compact baseline in `agent_state.md` only when it adds
resume-critical constraints or is needed to compare later execution with the approved preview. Do not create a
baseline merely to log that a dry run occurred.

A baseline contains only:

- approved basis;
- intended result;
- expected touch points;
- anticipated final-truth impact and affected documents when applicable; and
- planned checks.

The baseline supplements but never expands approved scope. Execute only after the human separately authorizes the
exact step at the refreshed invoking gate. During execution, stop before any material deviation from the baseline
or approved project direction and use the applicable planning, contract, correction, or final-truth gate.

At handoff, compare actual touch points, result, checks, and final-truth impact with an active baseline. Remove the
baseline after the step completes, is abandoned, materially changes, or is redirected. A changed exact next step
must not retain a stale baseline.

## Return to the Invoking Gate

After approval, revision, discard, or cancellation, reconcile any baseline change and return to the parent gate
with refreshed choices. Replace the parent only when preview findings create a required planning, contract,
final-truth, design, or blocker gate.

Never begin the previewed work merely because the dry run finished or was approved.

## Stop Conditions

Stop or return to the owning gate when:

- no approved basis or exact next step exists;
- credible preview requires broader design or planning;
- preview requires a write or destructive action;
- affected final-truth documents are unclear;
- anticipated impact is `Revision` and final truth is not approved; or
- the human requests revision, discard, discussion, or stop.

