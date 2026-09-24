# Validation

Initial version checked on 2026-09-24 in a Codex desktop host exposing `collaboration.spawn_agent`. The live test below applies to that original version; it is not a live test of every provider or the later portability revision.

## Provider-neutral revision

The automatic-defaults revision supersedes the earlier universal Astra preference and the historical unavailable-Astra scenario below. Ordinary use now resolves OpenAI to Astra, Claude to Opus, Gemini to Pro, and other providers to a suitable flagship worker. Missing automatic defaults fall back within the same provider; explicit user choices retain their stricter override behavior. No other provider was live-tested.

This revision passed the skill validator, UI metadata and local-link checks, and whitespace checks. Independent paper review covered Claude/Haiku to Opus, Gemini/Flash to Pro, OpenAI/Luna to Astra, same-provider fallback, unavailable explicit choices, nonnative backends, and missing effort selectors. It found one stale restriction on configured roles; the final wording now explicitly permits the resolved automatic selection. No cross-provider runtime test was performed.

The revision separates host-independent operating instructions from an optional Codex collaboration adapter. It covers provider-specific model selection, configured roles, absent effort controls, authorized external integrations, and shared versus isolated workspaces.

The open [Agent Skills specification](https://agentskills.io/specification), [Claude Code installation and invocation documentation](https://code.claude.com/docs/en/skills), and [Gemini CLI skill installer documentation](https://geminicli.com/docs/cli/skills/) were consulted. These establish packaging and documented installation paths, not successful end-to-end execution on those hosts. No Claude, Gemini, or other external provider runtime was launched.

The revised package passed frontmatter validation, optional UI metadata checks, relative Markdown link checks, and `git diff --check`. An independent paper review covered a selected Claude role without effort controls, a selected Gemini worker with an isolated workspace, unavailable Astra without a fallback, an authorized fixed host-default worker, and no delegation capability. It found no blocking provider assumptions. An effort-only override ambiguity was corrected to preserve the currently selected model. These scenarios were not live provider tests.

## Structural checks

- The bundled skill-creator `quick_validate.py` accepted `SKILL.md`.
- `agents/openai.yaml` parsed successfully; its short description meets the 25-64 character constraint and its default prompt includes `$dummy-boss`.
- The entrypoint is below 500 lines and the dispatch reference exists.
- All relative Markdown file links were checked before publication.

## Live forward test

An independent evaluating agent read the skill and applied it to this request:

> Use $dummy-boss to write a short plain-language explanation of why shared-file edits from concurrent workers need coordination, with one concrete example.

The evaluator spawned an actual execution worker with `model: "gpt-6-astra"`, `reasoning_effort: "low"`, and `fork_turns: "none"`. While that worker wrote, the evaluator reviewed the skill and README. The worker completed and returned:

> When several workers edit the same file at once, one person's changes can overwrite another's or leave the file inconsistent. For example, two workers updating an asset list might give different assets the same ID. Assign one worker to maintain that shared list, let the others send their proposed additions, and check the combined result before accepting it.

The dispatch accepted the requested settings and the agent listing confirmed completion. The runtime returned a worker identifier but did not independently report its model or effort. This verifies a real delegation path and a completed writing result; it does not establish model telemetry, cost savings, or broad task reliability.

## Paper-reviewed scenarios

- Default workers request Astra Low explicitly.
- A reviewer-only Astra medium override leaves other workers at Astra Low.
- An all-workers Sol override without an effort requests Sol low where supported.
- An unsupported model produces a capability explanation and a request for an alternative.
- An override affecting active workers requires interruption and replacement when in-place changes are unavailable; a follow-up alone does not change their model.

These override and recovery scenarios were reviewed against the instructions and active tool schema, not exercised as live runs. The evaluator found no internal contradiction in the operating instructions. Its missing-link finding was resolved by adding this validation record.

## Untested

Luna extra high as the actual parent, other hosts, code implementation, concurrent file edits, model switching, error recovery, reload/discovery in a new task, and quantitative latency or cost comparisons were not tested. The package is an instruction skill, so behavior also depends on the host's tools and higher-priority instructions.
