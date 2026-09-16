# Menu Skill

## Purpose

Present Bonsai human gates consistently. The invoking workflow owns gate meaning, applicability, authorization, execution decisions, and durable state. This skill owns presentation only.

## When to Load

Load for a human decision or contextual secondary-action menu.

The invoking workflow supplies the gate; available concrete choices; applicable/available secondary actions; any promoted secondary action and, when relevant, its reason; host free-form-input availability; active workspace type/name when pointer rendering needs it; and, when relevant, whether this is the first continuation boundary after fresh-session entry with no substantive work yet performed.

## Primary Menu

1. Show only the decision immediately required by the invoking workflow.
2. Name concrete actions; use the actual artifact/next step when useful.
3. Use supported structured choices when available; otherwise concrete numbered choices.
4. Use **Approve** for a reviewed artifact/contract. Use **Proceed**, **Continue**, or another accurate verb for an action being authorized.
5. A choice that only leaves the gate without taking the offered action is **Exit for now**. Do not substitute `Stop`, `Stop here`, `Do not continue`, or `Do not continue right now` for that meaning.
6. When both current-session and fresh-session continuation are useful, present them as peer choices, not unequal recommendations. The fresh-session choice must say the exact next action will execute automatically there. Do not offer fresh-session continuation by default. If this session itself began through fresh-session continuation and no substantive work has occurred, omit another fresh-session choice at the first resulting continuation gate unless the human requests it. This is session-local presentation context; never persist it in workspace memory.
7. After presenting a gate, stop for the human choice. Rendering never authorizes action.

## Repository Entry Gate

When supplied because no active workspace is selected:

1. List available project directories in stable lexical order as numbered primary choices.
2. Put **Manage Code Maps** after projects as a peer primary choice. This is an invoking-workflow-owned exception to its normally secondary placement; infer no other repository-level promotions from it.
3. Keep supplied **Manage Projects** and other less-frequent repository actions under **See more options**.
4. Do not interpret no active project as `Design required`.
5. After project selection, let the invoking workflow establish the current-session active project and replace this gate with that project's normal startup orientation.

## Exit for Now

**Exit for now** has one Bonsai-wide session-boundary meaning. When selected:

1. Do not authorize, approve, discard, execute, or otherwise resolve the action/gate being left.
2. Do not change durable state merely to record the exit.
3. Present the ordinary canonical startup pointer, never the auto-execute continuation prompt, introduced by `You can resume later with:`.
4. Active project: omit the qualifier only if unqualified startup deterministically resolves that same project; otherwise append only `Active project: <project>.` using the project directory name.
5. Active map: always append only `Active map: <map>.` using the map directory name.
6. No active workspace: use the unqualified pointer; normal startup routing resolves the next gate.
7. Stop.

The lead-in is not part of the copyable pointer. The pointer must be exactly one of:

```text
Read .bonsai/start.md and follow its instructions.
```

```text
Read .bonsai/start.md and follow its instructions. Active project: <project>.
```

```text
Read .bonsai/start.md and follow its instructions. Active map: <map>.
```

Starting a new host session remains the human's action. The pointer grants no execution authorization. Unqualified startup follows ordinary bootstrap selection, not map/non-default-project resume. Pointer formatting must not load or modify workspace memory. A later session reconstructs canonical durable state and normally reaches the applicable gate or execution condition.

## See More Options

Put less-frequent actions under **See more options**; include it only if at least one secondary action is currently applicable and available.

It is standalone navigation, never a child-action summary. Do not append, preview, summarize, or inline child names in its label, even when only one exists.

When selected, retain the invoking gate and show a separate contextual submenu containing only supplied secondary actions. Keep the submenu even for one action, and provide a return path to the invoking gate without taking an action.

Manage Projects, Manage Code Maps, Create Bonsai Home, Dry Run, diagnostics, and maintenance are examples, not a fixed display list. Never turn the submenu into a capability catalog.

A normally secondary action may be primary only when the invoking workflow says it is necessary or directly relevant. Do not duplicate a promoted action under **See more options**. This skill renders supplied promotions; it does not infer them.

### Dry Run Presentation

- Ordinary applicable Dry Run: keep under **See more options**.
- Invoking-workflow-promoted Dry Run because previewing the exact next step would materially reduce mechanical execution risk: put it in the primary menu; present the supplied concrete reason concisely with or immediately before the choices; do not duplicate it under **See more options**; do not call it required, default-recommended, or an approval gate.
- The invoking workflow owns that risk assessment. Importance, size, complexity, or architectural significance alone never causes promotion.

Naming an action does not implement or authorize its workflow. Never present an unavailable subordinate workflow as executable or report it complete merely because selected.

## Host Free-Form Input

If the host already provides free-form input such as `Other (type your answer)`, preserve it without adding generic `Other`.

If no host free-form path exists and open-ended input is required, the invoking workflow must ask a concrete question; this skill does not manufacture a catch-all choice.

## Subordinate Workflows

The invoking workflow retains the parent gate and ownership of authorization/durable-memory changes.

After **See more options** and a secondary-action selection:

1. Retain parent-gate identity.
2. Delegate only to the selected available workflow.
3. Let it complete, decline, or stop at its own required gate.
4. Reconcile execution-state changes under the owning workflow's rules.
5. Recompute the parent gate and return with refreshed choices.

Replace the parent gate only if subordinate work creates a new required gate or materially changes execution state. Otherwise completion, decline, or cancellation must not make it disappear.

## Boundaries

- Presentation only: this skill does not define gate meaning or decide authorization/applicability.
- Do not discover, inspect, validate, enumerate, read, or write domain state merely to render a menu. The invoking workflow supplies status summaries and applicable choices.
- Delegate only to the human-selected subordinate workflow.
