# dummy-boss

A Codex skill for a lightweight orchestrator that delegates substantive thinking and work to **Astra Low** subagents.

Choose your parent model yourself, such as **Luna at extra high**, then invoke `$dummy-boss`. Workers handle planning, research, implementation, writing, testing, and review. The parent assigns work, coordinates dependencies, checks completion evidence, and reports the result.

## Use it

```text
$dummy-boss Build a settings page for this app and verify it works.
```

```text
$dummy-boss Research these three options and recommend one with sources.
```

```text
$dummy-boss Use Astra medium for the reviewer; keep the other workers on Astra low.
```

```text
$dummy-boss Use Sol low for all workers on this task.
```

The default worker settings are `gpt-6-astra` and `low`. A user override can target one worker role, the current task, or the remaining conversation. A model-only override retains low effort when supported. The skill never changes the parent's model or account configuration.

## Install

Clone this repository into your personal skills directory as `dummy-boss`. This Codex desktop environment discovers personal skills under `~/.codex/skills`; use `$CODEX_HOME/skills` instead if you have configured a different Codex home. Other hosts may use different discovery locations: consult their current skill documentation.

PowerShell, for the default location:

```powershell
git clone https://github.com/rmoubayed/dummy-boss.git "$HOME/.codex/skills/dummy-boss"
```

macOS/Linux shell, respecting a configured Codex home:

```sh
git clone https://github.com/rmoubayed/dummy-boss.git "${CODEX_HOME:-$HOME/.codex}/skills/dummy-boss"
```

If that directory already exists, inspect it rather than overwriting it. Start a new task or reload skills as supported by your host, then invoke `$dummy-boss`.

## What the boss does

- Delegates substantive planning as well as execution; it does not solve the task first and then ask a worker to agree.
- Uses one worker for a small assignment and independent workers where parallel work helps.
- Gives workers clear context, file ownership, acceptance checks, and the user's authorization boundaries.
- Routes fixes and substantive review back to workers, and reports actual artifacts and validation.
- Preserves model overrides and tells you if the requested delegation cannot run.

Execution workers do their own assigned work; they do not recursively create more bosses. The workflow stays with the current assignment and its follow-ups until you change it.

## Requirements and limits

This is an instruction skill, not a scheduler, plugin, model router service, or automatic billing control. It requires a host with task-local subagents and a supported way to select their model and reasoning effort. A skill cannot override platform restrictions or make an unavailable model available.

The included dispatch example matches a host exposing `collaboration.spawn_agent`. That host requires a fresh or limited-history fork to select a different worker model; a full-history fork inherits the parent. On another host, the agent must inspect the actual tool schema and disclose any mismatch.

The parent still performs coordination and evidence checking. Its selected reasoning effort remains active. Delegation can add latency and token usage; this repository makes no cost or speed guarantee. The skill does not grant new permission to publish, buy, deploy, message others, or perform destructive actions.

## Files

- [SKILL.md](SKILL.md): the operating instructions.
- [agents/openai.yaml](agents/openai.yaml): skill picker metadata and an invocation prompt.
- [references/dispatch.md](references/dispatch.md): tool-specific dispatch and worker brief guidance.
- [VALIDATION.md](VALIDATION.md): behavioral checks and verification limits.

The skill uses the standard `SKILL.md` structure described in the [official skill documentation](https://learn.chatgpt.com/docs/build-skills). For host-level delegation support, see the [official subagent documentation](https://learn.chatgpt.com/docs/agent-configuration/subagents). Runtime-specific field names in this repository come from the active tool schema, not a promise that every Codex host exposes the same API.

## License

[MIT](LICENSE).
