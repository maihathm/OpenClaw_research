# OpenClaw Agents Midday Scan — 2026-03-23

## Scope
- Domain: OpenClaw ecosystem, agent tooling, browser automation, workflow variants
- Intent: midday ecosystem radar
- Time window: roughly last 18 hours
- Research date: 2026-03-23 12:02 Asia/Saigon / 2026-03-23 05:02 UTC
- Depth: quick scan
- Method note: Brave `web_search` was unavailable in this environment, so this run used direct GitHub API checks and raw primary-source fetches.

## Executive summary
- OpenClaw has a fresh behavior-impact PR to pass provider-specific model `options` through config and recover Ollama tool calls for weaker local models.
- OpenClaw also has an active recovery PR for subagent runs after gateway restart, which matters for long-running isolated research and coding tasks.
- `agent-browser` has a fresh state-persistence fix: state-management commands no longer accidentally start a daemon before `session_name` is set.
- A new repo, `automation-daemon`, is a notable browser-first automation runtime with durable jobs, Playwright execution, OTP/email-verification handling, and browser-profile persistence.

## Key findings

### 1. OpenClaw PR #51356: model `options` passthrough + Ollama tool-call recovery
- What happened:
  - New OpenClaw PR `fix(agents): accept model options in config and safely recover Ollama tool calls` was updated at 2026-03-23T05:03:11Z.
  - It adds provider-specific `options` passthrough in model config and uses `options.num_ctx` as a context-window fallback.
  - It also adds tool-call recovery for local models that understand tool semantics but do not emit native `tool_calls` cleanly.
- Why it matters:
  - This changes practical operator behavior for local-model setups: `openclaw.json` can carry provider-specific knobs instead of silently dropping them.
  - It directly addresses “memory loss” symptoms caused by small default Ollama context windows and improves tool usability for weaker local models.
- Evidence:
  - PR body explicitly calls out rejected `num_ctx`, dropped `options`, and silent tool-call failure for local models.
- Link:
  - https://github.com/openclaw/openclaw/pull/51356

### 2. OpenClaw PR #43497: recover subagent runs after gateway restart
- What happened:
  - Fresh OpenClaw PR `fix(agents): recover subagent runs after gateway restart` was updated at 2026-03-23T05:02:47Z.
  - The proposal rehydrates missing session-store entries, classifies resumability into replay/fresh/announce-only/orphaned states, and resumes or replays runs instead of failing them blindly.
- Why it matters:
  - This is directly relevant to OpenClaw workflows that rely on isolated runs, cron jobs, and long-running research/coding tasks.
  - If merged, gateway restarts should stop causing false failures or lost completions for in-flight subagents.
- Evidence:
  - PR body details transcript-based recovery, session-store rehydration, and direct completion/re-dispatch logic.
- Link:
  - https://github.com/openclaw/openclaw/pull/43497

### 3. agent-browser PR #964: state commands no longer break session persistence
- What happened:
  - `vercel-labs/agent-browser` has a fresh PR `fix: prevent state commands from starting daemon without session_name` updated at 2026-03-23T04:55:33Z.
  - The bug: running `state clear --all` or similar before exporting `AGENT_BROWSER_SESSION_NAME` could start the daemon too early, so cookies/localStorage never got tied to the intended named session.
  - The fix moves state-management commands to local CLI-side file operations before daemon startup.
- Why it matters:
  - This is a real operator-facing workflow fix: users relying on persistent session state should avoid pre-session state commands on current versions, and should retest after this lands.
  - It is a concrete implementation trick too: pure state-file operations should not implicitly spawn the browser daemon.
- Evidence:
  - PR includes root-cause analysis, before/after sequence diagrams, and a manual E2E test showing `localStorage` + cookies restored after restart.
- Link:
  - https://github.com/vercel-labs/agent-browser/pull/964

### 4. New repo: `automation-daemon` — durable browser-first background runtime
- What happened:
  - New GitHub repo `clawboy1776-de/automation-daemon` was created on 2026-03-22 and updated within the scan window.
  - README presents a persistent browser-automation daemon with SQLite job storage, Playwright-backed execution, browser-profile persistence, artifact storage, OTP/email-verification handling, auth-aware waiting-human escalation, and a Fastify API + CLI.
- Why it matters:
  - This is a meaningful variant in the agent/browser-automation surface: background-job durability, browser identity persistence, and email/OTP handoff are handled as first-class runtime concerns rather than ad hoc scripts.
  - Several design choices map cleanly to OpenClaw-adjacent workflows: durable job IDs, resumable auth flows, and a dedicated daemon boundary for browser-first jobs.
- Evidence:
  - README enumerates SQLite-backed durable jobs, Playwright executor, credential backends, login recipes, email verification services, and artifact storage.
- Link:
  - https://github.com/clawboy1776-de/automation-daemon

## Practical takeaways
- For OpenClaw local-model setups, explicitly watch for provider-option passthrough support (`num_ctx`, provider-specific knobs) instead of assuming config reaches runtime.
- For daemonized browser tools, keep file-state commands separate from process boot paths; otherwise session persistence can fail in non-obvious ways.
- For long-running agent jobs, transcript-based replay/recovery is becoming a practical resilience pattern worth borrowing.
- Browser-first automation stacks are increasingly baking OTP/email verification and durable browser identities into the runtime, not just into user scripts.

## Implications for OpenClaw
- Test whether OpenClaw should expose and document provider-specific model `options` more aggressively for local-model users.
- Track whether subagent resumability lands, since it materially changes reliability expectations for cron/isolated runs.
- Borrow the `agent-browser` lesson: avoid side-effectful daemon startup from commands that should be pure local state operations.
- Evaluate whether browser-first OpenClaw workflows need a more durable job/identity layer for auth-heavy flows.

## Follow-up actions
- [ ] Recheck OpenClaw PR #51356 for merge status and resulting docs/changelog updates.
- [ ] Recheck OpenClaw PR #43497 for merge status and any operator-facing recovery semantics.
- [ ] Recheck `agent-browser` PR #964 and note the first release containing the fix.
- [ ] Watch `automation-daemon` for actual usage examples, release tags, and evidence of operator adoption.