# Automatic provider defaults

The pattern is a lightweight parent coordinating strong workers at low effort. The user chooses the parent; this skill chooses workers automatically. Do not switch the parent or require an explicit worker choice for ordinary use.

## Selection order

1. Honor the user's explicit worker model, provider, role, and effort instructions within their stated scope. A previous explicit selection persists for that scope.
2. Otherwise identify the active model provider from the session or configured backend. Native Claude Code normally implies Anthropic, native Gemini CLI Google, and native Codex OpenAI. Explicit backend configuration takes precedence over the app's branding. Claude on Bedrock is still the Claude model family; a multi-provider router is not itself the model family.
3. Choose the matching preferred worker family below from the host's available catalog or configured roles. Resolve a current supported alias or exact ID using host evidence. Do not invent version numbers, assume subscription access, or choose a preview merely because its name looks newer. Keep the resolved choice stable for the assignment.
4. If that family is absent, select the strongest suitable available general-purpose reasoning/coding worker from the same provider using host descriptions or documented capability ordering. Disclose the fallback once and continue. Do not default to the lightweight parent just because inheritance is convenient. If only one suitable same-provider model exists, use it and explain the limitation.
5. Ask only if the active provider is ambiguous, no suitable same-provider worker is available, capability ordering cannot be resolved, or an explicit user choice cannot be honored. Do not ask for an Astra alternative on a Claude or Gemini host.

## Preferred families

- **OpenAI:** Astra at low effort. In the originally tested host this is `gpt-6-astra` with `reasoning_effort: "low"`. A Luna parent keeps its own selected effort.
- **Anthropic / Claude:** Opus at low effort. Prefer the host's supported Opus alias or its current available Opus ID. A Haiku parent keeps its own settings. For example, if the host resolves Opus to Opus 5.5, use that worker without requiring the user to name it.
- **Google / Gemini:** the available Gemini Pro family at low thinking/effort where exposed. A Flash parent keeps its settings. Resolve the actual Pro ID from the host; there is no universal Pro version or effort argument.
- **Other providers and local models:** choose the strongest suitable available general-purpose reasoning/coding model in the active provider/backend, using its catalog or configured roles. Use a documented low-effort control when available; otherwise report native behavior. Do not manufacture a family ranking from model names or parameter counts.

These are this skill's routing preferences, not benchmark claims. User-selected overrides always win. Cross-provider workers require an explicit user choice or previously authorized routing preference and an available integration.

## Effort and actual configuration

Model selection and effort configuration are separate. A prompt saying "use low effort" is not evidence that the runtime was configured to low. Use the host's real per-worker control or a loaded role that declares it. Never lower the parent's effort to affect workers.

For Claude Code, inspect the actual Agent tool and loaded subagent definitions. Its documented subagent definition supports `model: opus` and `effort: low`; the spawn tool may not expose an effort argument. Prefer an available worker role configured with those values. Do not invent a tool field or edit a shared role while workers are running. If low requires an uninstalled role, disclose that setup limitation and use the selected model's native behavior unless the user explicitly requires exact low effort. Do not claim low was applied. See [Claude's subagent configuration](https://code.claude.com/docs/en/sub-agents).

For Gemini CLI, inspect its available subagents and model configuration rather than assuming an OpenAI-style effort field. See [Gemini's subagent documentation](https://geminicli.com/docs/core/subagents/). Apply only supported thinking controls; otherwise report native behavior.

Announce the resolved worker family and effort briefly at the first dispatch. Distinguish requested, configured, and runtime-confirmed settings. No repeated model confirmation is needed once selection is resolved.
