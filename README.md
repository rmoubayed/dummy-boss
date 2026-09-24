# dummy-boss

A **provider-neutral Agent Skill** for a lightweight boss that delegates substantive thinking and work to subagents.

Use any parent model your agent host supports. Workers handle planning, research, implementation, writing, testing, and review; the parent coordinates and reports verified results. **Astra Low remains the preferred worker default**, and you can select models from any provider available through your host or an already configured integration.

The package follows the open [Agent Skills specification](https://agentskills.io/specification). Model-provider access and real delegation depend on the host: installing a skill cannot add unavailable models or subagent tools.

## Use it

Ask your agent:

```text
Use dummy-boss to build a settings page for this app and verify it works.
```

```text
Use dummy-boss with my host's configured worker model to research these options.
```

```text
Use dummy-boss. Use the available Claude model I selected for implementation
and Astra low for review through my configured worker integration.
```

```text
Use dummy-boss with my selected Gemini model for all workers on this task.
```

Specify an exact available model or configured worker role when needed. Overrides can apply to one role, one task, or the remaining conversation. If Astra is unavailable and no alternative is authorized, the boss asks once for a supported choice. It never silently switches your parent model.

Use your host's invocation syntax: `$dummy-boss` in Codex, `/dummy-boss` in Claude Code, or a natural-language request in hosts that activate skills that way. Named effort levels are provider-specific; if the selected worker has no effort control, the skill reports that and uses native behavior unless you required an exact setting.

## Install

Install the entire repository folder, including `references/`, under the name `dummy-boss` in your host's skill directory. Do not overwrite an existing installation without inspecting it.

### Claude Code

Clone into the personal skill directory, then invoke `/dummy-boss`. Claude Code documents this location and slash invocation in its [skills guide](https://code.claude.com/docs/en/skills).

```sh
git clone https://github.com/rmoubayed/dummy-boss.git "$HOME/.claude/skills/dummy-boss"
```

### Gemini CLI

Use its [skill installer](https://geminicli.com/docs/cli/skills/), then ask it to use dummy-boss:

```sh
gemini skills install https://github.com/rmoubayed/dummy-boss.git
```

Follow the host's activation and reload prompts. Skill installation and worker availability are separate capabilities.

### Codex

For the desktop environment where this skill was originally created, the personal directory is `~/.codex/skills`, or `$CODEX_HOME/skills` when configured. Clone there and invoke `$dummy-boss`:

```sh
git clone https://github.com/rmoubayed/dummy-boss.git "$HOME/.codex/skills/dummy-boss"
```

The clone commands using `$HOME` also work in PowerShell. Follow your host's configured discovery location if different; see the [Codex skill guide](https://learn.chatgpt.com/docs/build-skills).

### Other agent hosts and model providers

Copy or clone the repository into the host's documented Agent Skills directory. If it supports custom instruction files instead, load `SKILL.md` and make its linked references available. This is a manual instruction integration, not automatic skill discovery.

The core requires no OpenAI SDK, account, or tool names. It can coordinate native subagents, configured worker roles, or an already authorized external agent integration. It does not install provider bridges, collect API keys, or create provider accounts.

## How it works

- Delegates substantive planning as well as execution; it does not solve the task first and ask a worker to agree.
- Uses a single worker for small assignments and parallel workers for independent work.
- Supplies clear context, ownership, acceptance checks, and authorization boundaries.
- Handles both shared files and isolated workspaces with explicit artifact integration.
- Routes fixes and substantive review back to workers and reports evidence of completion.
- Adapts to actual model selectors, configured roles, effort controls, and messaging tools without inventing API fields.

Execution workers do their own assignment rather than recursively creating more bosses. The parent retains responsibility for coordination, authorization, and evidence checking.

## Compatibility and validation

**Portable instructions do not mean every provider or app has been live-tested.** The original delegation smoke test ran on a Codex collaboration host. Claude Code and Gemini CLI installation guidance was checked against their documentation; their runtimes were not exercised. Other hosts must provide real delegation for the workflow to run. See [validation details](VALIDATION.md).

If real delegation is unavailable, the skill explains that and asks whether to proceed directly or move to a supported environment. It does not role-play fake workers. Delegation may add latency and token usage; no cost or speed improvement is guaranteed.

## Files

- [SKILL.md](SKILL.md): provider-neutral operating instructions.
- [references/dispatch.md](references/dispatch.md): capability resolution, worker briefs, and integration.
- [references/codex-collaboration.md](references/codex-collaboration.md): optional adapter for the originally tested tool family.
- [agents/openai.yaml](agents/openai.yaml): optional Codex picker metadata; other hosts do not need it.
- [VALIDATION.md](VALIDATION.md): completed checks and their limits.

## License

[MIT](LICENSE).
