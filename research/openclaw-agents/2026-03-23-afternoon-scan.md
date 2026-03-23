# OpenClaw Agents Afternoon Scan — 2026-03-23

## Scope
- Domain: OpenClaw ecosystem, agent tooling, browser automation, workflow variants
- Intent: afternoon ecosystem radar
- Time window: since the earlier scan today (roughly 2026-03-23 12:02 Asia/Saigon / 2026-03-23 05:02 UTC onward)
- Research date: 2026-03-23 15:05 Asia/Saigon / 2026-03-23 08:05 UTC
- Depth: light / stop-early scan
- Method note: Brave `web_search` was unavailable in this environment, so this run used direct GitHub API checks and raw primary-source README/PR inspection.

## Executive summary
- A genuinely new repo appeared after the midday scan: `openclaw-deploy`, positioned as a one-command deployment and onboarding stack for OpenClaw plus companion services.
- OpenClaw has a fresh `/status` behavior fix so fallback-model sessions report the effective context window instead of stale persisted values.
- OpenClaw also has a fresh Kimi builtin `$web_search` contract fix, which matters for tool reliability when using Moonshot/Kimi-native search.
- A new plugin hook PR (`agent_error`) would let operators replace raw provider errors before they reach users, which is a practical UX/ops change for production bots.

## Key findings

### 1. New repo: `VibeCodingLabs/openclaw-deploy`
- What happened:
  - New repo created at 2026-03-23T08:03:21Z, after the earlier scan.
  - README positions it as a one-command deploy/onboarding tool for OpenClaw infrastructure, including Open-WebUI, Ollama, ChromaDB, n8n, OpenObserve, workspace bootstrap files, heartbeats, and cron scaffolding.
- Why it matters:
  - This is a real new usage variant: OpenClaw is being packaged as a full-stack deployable agent environment rather than only a local agent runtime.
  - It may surface practical operator patterns around first-run setup, service composition, and opinionated defaults.
- Evidence:
  - README explicitly documents an interactive installer and bundled stack components.
- Link:
  - https://github.com/VibeCodingLabs/openclaw-deploy

### 2. OpenClaw PR #51795: `/status` now recomputes fallback context window correctly
- What happened:
  - Fresh PR `fix(status): recompute fallback context window` updated at 2026-03-23T08:03:44Z.
  - The change recomputes `/status` context-window reporting after the active runtime model is settled, instead of trusting stale persisted `contextTokens` when a fallback model is serving the session.
- Why it matters:
  - This changes operator behavior directly: `/status` becomes more trustworthy for debugging fallback-model sessions and actual context limits.
  - It also matters for automated monitoring and session diagnostics that rely on the status tool.
- Evidence:
  - PR summary explicitly calls out stale `contextTokens`, fallback-model reporting, and regression coverage for status output.
- Link:
  - https://github.com/openclaw/openclaw/pull/51795

### 3. OpenClaw PR #52687: Kimi builtin `$web_search` flow aligned to Moonshot’s official contract
- What happened:
  - Fresh PR `fix(kimi): align builtin $web_search flow with Moonshot official cont.` updated at 2026-03-23T08:02:37Z.
  - It disables `thinking` for the builtin search round-trip, echoes raw `tool_call.function.arguments`, and adds `name` on `role=tool` messages instead of synthesizing custom payloads.
- Why it matters:
  - This is a behavior-impact fix for anyone routing tool use through Kimi/Moonshot: builtin web search should become more predictable and closer to provider-native expectations.
  - Practical takeaway: provider-specific builtin-tool contracts are brittle; OpenClaw integrations need to mirror them closely rather than normalizing too aggressively.
- Evidence:
  - PR summary explicitly contrasts prior custom payload synthesis with the official Moonshot round-trip contract.
- Link:
  - https://github.com/openclaw/openclaw/pull/52687

### 4. OpenClaw PR #52401: new `agent_error` plugin hook before error broadcast
- What happened:
  - Fresh PR `Plugins: add agent_error hook to replace provider errors before broadcast` updated at 2026-03-23T08:02:47Z.
  - It adds a modifying hook in `handleAgentEnd` so plugins can replace raw provider error text with a safer or localized message before the lifecycle error is emitted to the user.
- Why it matters:
  - This is a concrete ops/UX pattern for production deployments: hide noisy quota/provider errors behind friendlier channel-safe messages without rewriting the whole transport path.
  - It also gives plugin authors a new interception point specifically for agent-run failures.
- Evidence:
  - PR body documents the new `agent_error` hook, replacement shape `{ message: string }`, and the reason `message_sending` is not the right seam.
- Link:
  - https://github.com/openclaw/openclaw/pull/52401

## Practical takeaways
- Treat `/status` as an operator surface that needs to reflect the effective runtime model, not just persisted config state.
- For provider-native tools like Kimi builtin search, preserve the provider’s round-trip contract as closely as possible.
- Error-rewrite hooks are becoming a useful pattern for operator-safe production messaging.
- Watch `openclaw-deploy` mainly for real install behavior and defaults, not for hype: the interesting part is whether it encodes reproducible deployment patterns.

## Implications for OpenClaw
- Re-test any workflow that depends on `/status` context-window numbers when fallback models are involved.
- If Moonshot/Kimi support matters, monitor whether this `$web_search` fix lands and whether similar provider-specific contract gaps exist elsewhere.
- Consider whether more lifecycle interception points should be pluginized for operator UX.
- Track whether opinionated deployment repos start standardizing the “OpenClaw + tools + memory + workflow” stack.

## Follow-up actions
- [ ] Recheck PR #51795 for merge status and whether `/status` docs need an operator note.
- [ ] Recheck PR #52687 after merge for any downstream Moonshot/Kimi docs updates.
- [ ] Recheck PR #52401 for merge status and plugin API documentation.
- [ ] Watch `openclaw-deploy` for real install docs, examples, and evidence of adoption.