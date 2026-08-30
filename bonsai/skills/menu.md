# Menu Skill

## Purpose

Present Bonsai human gates consistently while leaving each invoking workflow in control of its decisions,
authorization, and durable state.

## When to Load

Load this skill when a workflow must present a human decision or a contextual secondary-action menu.

The invoking workflow supplies:

- the gate being presented;
- the concrete choices currently available;
- the secondary actions that are applicable and available;
- whether the host already supplies a free-form choice.

## Primary Menu

1. Keep the primary menu limited to the decision immediately required by the invoking workflow.
2. Name choices as concrete actions using the actual artifact or next step when useful.
3. Use a supported structured-choice mechanism when the host provides one; otherwise use concrete numbered
   choices.
4. Say **Approve** for a reviewed artifact or contract. Say **Proceed**, **Continue**, or another accurate action
   verb for an action the human is authorizing.
5. Do not make current-session and fresh-session continuation unequal recommendations. They are peer choices.
6. After presenting a gate, stop for the human's choice. Rendering a menu does not authorize an action.

## See More Options

Put less-frequent actions under **See more options**. Include that choice only when at least one secondary action is
applicable and available in the current context.

Possible secondary actions include Manage Projects, Manage Code Maps, Create Bonsai Home, Dry Run, diagnostics,
and maintenance. This is not a fixed list to display. Include only actions supplied by the invoking workflow; do
not turn the submenu into a catalog of every Bonsai capability.

A normally secondary action may appear directly in the primary menu when it is necessary or directly relevant to
the current decision. Do not duplicate it under **See more options** when promoted.

Naming an action in a menu does not implement or authorize its workflow. Do not present an unavailable subordinate
workflow as executable, and do not report it as completed merely because it was selected.

## Host Free-Form Input

When the host already provides a free-form choice such as `Other (type your answer)`, do not add a generic `Other`
menu item. Preserve the host's free-form path without duplicating it.

When no host free-form path exists and open-ended input is required, the invoking workflow must ask a concrete
question; this skill does not manufacture a generic catch-all choice.

## Subordinate Workflows

The invoking workflow remains the owner of the parent gate and any authorization or durable-memory changes.

When the human selects a secondary action:

1. retain the identity of the invoking gate;
2. delegate only to the selected available workflow;
3. let that workflow complete, decline, or stop at its own required gate;
4. reconcile any execution-state changes under the owning workflow's rules;
5. recompute the parent gate and return to it with refreshed choices.

Replace the parent gate only when the subordinate action creates a new required gate or materially changes the
execution state. Otherwise, completing, declining, or cancelling subordinate work must not make the parent gate
disappear.

## Boundaries

- This skill owns presentation mechanics, not the meaning of a gate.
- It does not decide which actions are authorized or applicable.
- It does not read or write durable project memory merely to render a menu.
- It delegates only to the subordinate workflow selected by the human.
