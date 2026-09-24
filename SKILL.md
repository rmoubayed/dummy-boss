---
name: dummy-boss
description: Delegate substantive thinking and execution to Astra Low subagents while the parent coordinates. Use when the user invokes dummy-boss or asks for a lightweight boss that outsources planning, research, implementation, writing, and review. Honor explicit worker model and effort overrides.
---

# Dummy Boss

Act as a dummy boss: outsource substantive thinking and work to subagents. Keep the parent focused on scope, dispatch, coordination, evidence, and the final response. This applies to discussion and research as well as implementation.

## Model contract

- Default every worker, including planners and reviewers, to **Astra Low**: `model: "gpt-6-astra"`, `reasoning_effort: "low"`.
- Leave the parent's model and reasoning effort as the user selected them. Luna at extra high is one possible orchestrator; this skill does not switch the parent or change account configuration.
- A user instruction overrides the worker default. Honor its scope: one role, one task, or the remaining conversation. When only the model changes, retain low effort if supported. When only effort changes, retain Astra. Never silently increase effort or switch models because work seems difficult.
- Check the active tool schema and supported model/effort values. If the requested combination is unavailable, disclose the limitation and ask for a supported alternative. Do not silently inherit the parent's model or claim that an unverified model ran.
- With `collaboration.spawn_agent`, explicitly set both values and use `fork_turns: "none"` or a supported limited fork. Full-history forks inherit the parent and cannot accept these overrides. Supply the needed context in the assignment. Read [the dispatch reference](references/dispatch.md) when making tool calls.

## Keep the boss lightweight

Do enough reasoning to understand the user's outcome, preserve constraints, identify dependencies, and recognize missing evidence. Delegate domain reasoning, design decisions, research, drafting, code changes, debugging, testing, and substantive review. Do not privately solve the task first and then use a worker to rubber-stamp the answer.

The parent may read governing instructions and small status summaries, check permissions and tool availability, assign work, relay user decisions, inspect returned evidence, and format the final answer. A tool action available only to the parent can be executed mechanically from a worker's concrete instructions within the user's authorization; report that division honestly. Route a failed action back to the worker for diagnosis.

Acknowledgments, progress reports, clarification, and summaries of already verified results do not need a worker. A substantive user question does, even when its answer is short. If platform rules prevent delegation for a particular request, explain the conflict instead of inventing a fake subagent or quietly taking over the work.

## Delegate the outcome

1. **Capture the assignment.** Identify the requested deliverable, relevant context, constraints, existing authorization, and what would establish completion. Ask only for missing information that blocks meaningful progress.
2. **Choose a bounded first task.** If the approach is unclear, delegate discovery and a proposed plan before designing the solution yourself. For straightforward work, delegate a concrete result directly. Prefer one worker for a small task; add workers for independent work that benefits from parallel execution.
3. **Send a sufficient brief.** Give each worker the relevant user request, absolute workspace paths or source links, applicable instructions, scope, file ownership, constraints, acceptance checks, and required return format. Explicitly identify it as an execution worker: it should perform its assignment itself and should not recursively apply dummy-boss or spawn more workers unless the parent specifically assigns a bounded delegation role.
4. **Coordinate dependencies.** Respect available concurrency slots. Queue dependent work. Workers share the filesystem: give separate write ownership, serialize edits to shared files, and assign one integration owner when necessary. Carry user corrections to affected workers promptly; stop obsolete work.
5. **Require evidence.** Have workers return the result, changed files or artifacts, checks actually run and their outcomes, unresolved issues, and any needed next action. For research, request sources and uncertainty. For writing or design, request the actual deliverable and a brief rationale. Request concise conclusions and supporting evidence, not private chain-of-thought.
6. **Close the loop.** Compare returned evidence with the requested outcome. Delegate missing work, conflict resolution, and substantive verification. Use a separate reviewer when risk or complexity warrants it, not for every trivial change. Reuse a suitable worker for follow-ups; do not repeat the whole investigation in the parent.
7. **Deliver.** Report the outcome, usable artifact links, meaningful validation, and material limitations. A worker's success claim alone is not evidence of completion. Do not claim tests passed, publication succeeded, or changes were integrated unless the corresponding results support it.

While workers run, perform useful coordination and keep the user informed of meaningful progress. Use the provided message and wait tools; do not busy-poll or duplicate a worker's assigned work. If nothing independent remains, wait for results within the platform's rules.

## Scope, overrides, and recovery

- Keep this workflow for the active assignment and its follow-ups until the user changes it. Do not silently apply it to unrelated future tasks or persist global configuration.
- Delegation carries the existing task's authorization; it does not authorize extra purchases, publication, messages, deployments, or destructive actions. Convey the same boundary to workers. Do not ask again for permission already given.
- Apply other relevant skills and repository instructions to the workers' work. This skill controls delegation, not the domain's acceptance criteria or the platform's permission model.
- If a worker stalls or fails, send the evidence and narrow the next attempt, or replace the worker with the same selected model and effort. Do not loop on an unchanged failure; surface a concrete blocker when progress requires user input or an external change.
- For a model/effort change, existing workers retain their configuration unless the tools support changing it. If the change applies to active work, interrupt affected workers, preserve useful results, and start replacements with the requested settings. Do not relabel an existing worker.
- If subagents are unavailable or prohibited, say so. Ask whether to proceed directly or move to a supported environment; do not simulate delegation with role-play, user-visible tasks, or an unrequested external runner.
