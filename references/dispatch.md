# Dispatch reference

Use the runtime's actual tool schema as the authority. This example is for a host that exposes `collaboration.spawn_agent`; it is not a universal API signature.

```json
{
  "task_name": "implement_slice",
  "model": "gpt-6-astra",
  "reasoning_effort": "low",
  "fork_turns": "none",
  "message": "You are an execution worker. Perform this assignment yourself; do not recursively apply dummy-boss or spawn subagents. Outcome: ... Workspace: ... Read these governing instructions: ... Relevant user request and context: ... Own these files: ... Constraints and authorization: ... Validate with: ... Return the actual result, changed paths, checks and outcomes, and unresolved issues."
}
```

Replace the placeholders with a complete, bounded brief. Default workers, planners, and reviewers all use these explicit model and effort values. Override only the values and scope the user changes.

## Host differences

- Some hosts expose another spawn tool or configure worker roles in agent files. Use an equivalent mechanism only if its model and effort are verifiable. Do not invent arguments, launch a nested CLI, or modify global settings to force support.
- In `collaboration.spawn_agent`, `fork_turns: "all"` and omitted fork settings inherit the parent and do not accept model/effort overrides. Use `"none"` with a self-contained brief by default. A limited numeric-string fork may be used if necessary and supported.
- Obey host restrictions on when delegation is allowed. This skill does not override system or developer instructions. If a host requires a worker to run alongside useful local work, reserve actual coordination, context preparation, or evidence checking for the parent; do not manufacture busywork to qualify.
- Use task-local subagents, not tools that create separate user-owned conversations.
- Record the returned worker ID and the requested model/effort. Report runtime confirmation only if the tool actually provides it; otherwise distinguish requested settings from confirmed settings.

## Brief patterns

**Discovery:** Supply the outcome and raw context. Ask the worker to inspect the relevant sources, identify options and blockers, and return a proposed approach with bounded work units and validation. Let the worker do the substantive planning.

**Execution:** Supply the approved scope or clear user request, owned files, dependencies, acceptance checks, and any exclusions. Ask for the completed artifact, not merely a plan.

**Review:** Supply the original requirements, the actual diff or deliverable, and raw validation evidence. Ask for independently supported defects and missing acceptance evidence. Avoid feeding the reviewer the desired verdict.

## Follow-up and completion

Use `send_message` to steer a running worker, `followup_task` to give an idle worker more work, and the available wait tool to await results. A follow-up does not change its model or effort. Recreate a worker when a requested setting change cannot be applied in place.

Keep a compact record of each worker's ID, selected settings, owned files, current assignment, and result. For work spanning compaction, save it in the project's existing handoff mechanism. Keep credentials and unrelated conversation history out of briefs and public artifacts.
