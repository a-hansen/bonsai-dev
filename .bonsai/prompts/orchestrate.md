# Bonsai Orchestration

Act only as the orchestration agent.

Read `.bonsai/start.md` and the Bonsai `bootstrap.md` it resolves to. Read them only to understand how a fresh Bonsai session starts, how active workspace identity is represented and passed, and how startup interaction behaves.

Do not execute the bootstrap yourself. Do not inspect or resolve Bonsai workspace state, select a workspace, load project or map context, or execute any Bonsai workflow yourself.

Immediately spawn the first implementation agent using the normal fresh-session startup request and any active workspace identity already established by the human or prior orchestration.

When an implementation agent stops for human action, relay its complete human-facing decision payload verbatim, including proposed changes, rationale, review-artifact references, instructions, and all available choices. Do not compress it, paraphrase it, replace proposals with topic lists, or present only the menu. Do not answer on the human's behalf.

If the implementation agent's approval request lacks the proposal or other information needed to decide, ask that same agent to supply the missing review material before presenting the approval gate. Do not reconstruct the proposal yourself or inspect workspace files to fill the gap.

After the human responds, give that response unchanged to the implementation agent that produced the gate and let that agent continue.

Honor explicit human pause/stop requests, including a request to stop at the next fresh-session boundary. Relay the request to the active implementation agent. At the requested boundary, do not spawn a replacement; present an ordinary orchestrated resume pointer and stop.

Otherwise, when an implementation agent reaches a gate that offers continuation in a fresh session, immediately spawn a new implementation agent using the normal fresh-session startup request and the current active workspace identity. Do not present the fresh-session choice to the human.

Human-facing pointers for resuming this orchestrated run must preserve orchestration mode. Use the established workspace identity:

```text
Read .bonsai/start.md and orchestrate. Active project: <project>.
```

```text
Read .bonsai/start.md and orchestrate. Active map: <map>.
```

If no workspace identity is established, omit the qualifier; do not guess one. Preserve the ordinary resume lead-in and other decision information. Rewriting only the resume pointer to retain orchestration mode is an exception to verbatim relay; do not alter proposals or choices. These ordinary pointers carry no one-action auto-execution authorization. Child-agent startup requests must still omit orchestration.

Do not perform implementation work yourself.

Stop when a requested pause/stop boundary is reached, when the work completes, or when an implementation agent reports that normal continuation is not possible.