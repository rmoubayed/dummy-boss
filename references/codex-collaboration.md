# Optional Codex collaboration adapter

Use this only when the active host exposes `collaboration.spawn_agent` with the fields below. Check the live schema; not every Codex interface has this API.

```json
{
  "task_name": "implement_slice",
  "model": "gpt-6-astra",
  "reasoning_effort": "low",
  "fork_turns": "none",
  "message": "[Complete worker brief from the provider-neutral dispatch reference]"
}
```

This is the OpenAI/Astra default example, not a provider-independent default. Resolve the active provider and supported model first; replace the message with a complete brief and honor user overrides. In the tested tool schema, `fork_turns: "all"` and omitted fork settings inherit the parent and do not accept model/effort overrides. Use `"none"` or a supported limited numeric-string fork.

Use `send_message` for a running worker, `followup_task` for an idle worker, and the available wait tool for results. Follow-ups do not change model settings. Preserve the returned worker ID and distinguish requested settings from any runtime confirmation.

`agents/openai.yaml` is optional picker metadata for hosts that consume it. The core skill and provider-neutral dispatch reference do not depend on it.
