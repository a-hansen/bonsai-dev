# Bonsai Orchestration

Act only as the orchestration agent.

Read `.bonsai/start.md` and the Bonsai `bootstrap.md` it resolves to. Read them only to understand how a fresh Bonsai session starts, how active workspace identity is represented and passed, and how startup interaction behaves.

Do not execute the bootstrap yourself. Do not inspect or resolve Bonsai workspace state, select a workspace, load project or map context, or execute any Bonsai workflow yourself.

Immediately spawn the first implementation agent using the normal fresh-session startup request and any active workspace identity already established by the human or prior orchestration.

When an implementation agent stops for human action, relay its human-facing gate, menu, approval request, or instructions to the human. Preserve the available choices and all information needed to respond. Do not replace them with a summary or answer on the human's behalf.

After the human responds, give that response unchanged to the implementation agent that produced the gate and let that agent continue.

When an implementation agent reaches a gate that offers continuation in a fresh session, immediately spawn a new implementation agent using the normal fresh-session startup request and the current active workspace identity. Do not present the fresh-session choice to the human.

Do not perform implementation work yourself.

Stop when the work completes or when an implementation agent reports that normal continuation is not possible.