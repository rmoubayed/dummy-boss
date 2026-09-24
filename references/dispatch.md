# Provider-neutral dispatch

The host's exposed tools and configured worker roles are authoritative. There is no universal spawn API, model alias, reasoning control, or workspace-sharing rule.

## Resolve capabilities

1. Identify real delegation tools or an already authorized worker integration. Loading a skill does not itself create subagents.
2. Resolve the user's worker selection, or the Astra Low preference, against available models and roles. If unavailable, use an already authorized fallback or ask for a supported choice. Do not assume that Claude, Gemini, OpenAI, or another provider's models are interchangeable or accessible from every host.
3. Use only supported controls. Map the user's effort preference to a documented compatible setting; do not equate token budgets with another provider's named effort levels. When no control exists, disclose native behavior and omit the field, unless an exact user requirement makes that a blocker.
4. Check context inheritance, concurrency, tool permissions, and shared versus isolated workspaces. Pass required instructions explicitly if workers do not inherit them.
5. Dispatch through the actual interface. Record the returned identifier, selected model or role, available configuration evidence, assignment, ownership, and result. Runtime confirmation may be absent; do not present requested settings as independently verified.

Use the [Codex collaboration adapter](codex-collaboration.md) only when the host exposes that exact tool family. Other hosts should use their own available interfaces, without copying Codex argument names. A host may expose predefined specialist tools instead of a generic spawn tool; select an appropriate configured worker and verify its scope and model before use.

## Worker brief

Send the following information as a prompt or the host's equivalent task payload:

```text
You are an execution worker. Perform this assignment yourself; do not
recursively apply dummy-boss or spawn workers unless explicitly assigned to.

Outcome: [concrete deliverable]
Context: [relevant user request and source material]
Instructions: [applicable repository rules and domain skills]
Workspace: [paths, accessible resources, and whether edits are shared]
Ownership: [files or artifacts this worker may change]
Constraints: [scope, dependencies, authorization, and exclusions]
Acceptance: [checks or evidence needed to establish completion]
Return: [actual result, changed files or transferable artifacts,
         checks performed and outcomes, unresolved issues]
```

Use paths accessible to the worker. For remote workers, transfer only authorized, necessary context through the configured integration; a local absolute path alone may be unusable.

**Discovery:** Give the outcome and raw context. Ask for an evidence-based approach, bounded work units, and validation. Let the worker do the substantive planning.

**Execution:** Give the clear user request or approved scope, dependencies, and acceptance checks. Ask for the completed artifact, not merely a plan.

**Review:** Give the original requirements, actual deliverable or diff, and raw evidence. Ask for independently supported defects and missing acceptance evidence; do not supply the desired verdict.

## Follow-up and integration

Use the host's message, resume, status, wait, and cancellation mechanisms where available. If a capability is absent, disclose the limitation and avoid conflicting replacement work. A message does not change an existing worker's model. If cancellation cannot be confirmed, prevent overlapping writes or wait for the old worker before replacing it.

For shared workspaces, preserve other workers' changes. For isolated workers, obtain a patch, branch, or artifact, integrate it through a designated owner, and validate the combined result. Report completion only after required integration succeeds.

Obey host restrictions on when delegation is allowed. Where a host requires useful local work alongside a worker, reserve actual coordination, context preparation, or evidence checking; do not manufacture busywork. Prefer task-local workers over creating separate user-owned conversations. Preserve the worker record in the project's handoff mechanism for long tasks.
