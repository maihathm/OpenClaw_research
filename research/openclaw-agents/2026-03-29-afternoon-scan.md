# OpenClaw Agents Afternoon Scan — 2026-03-29

## Scope
- Domain: OpenClaw ecosystem, agent tooling, operator workflows
- Intent: afternoon ecosystem radar
- Time window: roughly 2026-03-29 12:02–15:02 Asia/Saigon
- Depth: light, source-first scan
- Method: fast-forward-only pull, repo/profile/reference review, direct primary-source GitHub/API checks on OpenClaw core and adjacent agent-browser surface; stopped early once external new-repo signal stayed weak

## Executive summary
- Fresh afternoon signal again came mostly from OpenClaw core rather than from a credible new repo/fork launch.
- The highest-value changes were operator-facing reliability fixes for session/model visibility, Telegram stream-order sanitation, subagent inline announce attribution, and provider/runtime compatibility.
- Outside OpenClaw, the only adjacent practical change worth keeping was in `vercel-labs/agent-browser`: saved browser state now captures cross-domain cookies and localStorage, which matters for SSO-heavy automations.
- New repo signal was weak: search surfaced mostly zero-star toy repos/templates, not meaningful variants worth elevating.

## Key findings

### 1. OpenClaw sessions/model visibility moved again after the midday scan
- What happened: OpenClaw merged `fix: prefer transcript model in sessions list (#55628)`.
- Why it matters: this changes what operators see when inspecting active sessions/subagents. The commit explicitly prefers transcript model identity, keeps live subagent model rows, and avoids bad fallback behavior on cost-only reads.
- Evidence:
  - OpenClaw commit — https://github.com/openclaw/openclaw/commit/ebb919e311a08b7fa0a278bc4512c9a55c55d4ad
- Practical takeaway: if you rely on session lists or Control UI to confirm which model actually ran, this is a meaningful trust/observability fix rather than a cosmetic update.

### 2. Telegram/subagent delivery reliability got two same-window operator fixes
- What happened:
  - `fix(telegram): sanitize invalid stream-order errors (#55999)`
  - `fix(subagents): preserve requester agent for inline announces (#55998)`
- Why it matters: both affect real delivery behavior. One reduces noisy/invalid stream-order failure surfaces on Telegram; the other preserves the requester agent identity when subagents announce inline, which matters for attribution and routing clarity.
- Evidence:
  - OpenClaw commit — https://github.com/openclaw/openclaw/commit/d6a4ec6a3d94c58a3d5dd7370bdfb8c1bfae1884
  - OpenClaw commit — https://github.com/openclaw/openclaw/commit/9777781001579eae57510e0c53d11352c7fbd6b6
- Practical takeaway: for chat-driven OpenClaw usage, afternoon changes were more about making message delivery/announce behavior less brittle than about adding new surface area.

### 3. Provider/runtime compatibility kept tightening inside OpenClaw core
- What happened:
  - `fix(agents): repair btw reasoning and oauth snapshot refresh (#56001)`
  - `fix: apply Mistral compat across proxy transports`
  - `Memory/LanceDB: fix bundled runtime manifest lookup (#56623)`
- Why it matters: this cluster suggests active hardening around cross-provider behavior and runtime packaging edges, not just isolated bugfix noise.
- Evidence:
  - OpenClaw commit — https://github.com/openclaw/openclaw/commit/aec58d4cde647502c2cb3cfc9cfd78fa8319b16a
  - OpenClaw commit — https://github.com/openclaw/openclaw/commit/c664b67796e36d46eafac819a4d992ff1a552e73
  - OpenClaw commit — https://github.com/openclaw/openclaw/commit/8bdb518bde3ea0e07e10c07908b29b5246ef19c5
- Practical takeaway: if you mix OAuth-backed providers, proxy transports, or bundled memory/runtime setups, today’s risk surface is still compatibility and runtime state—not discoverability of a new external project.

### 4. Adjacent practical usage change: agent-browser fixed state export for cross-domain auth
- What happened: `vercel-labs/agent-browser` merged `fix: save_state captures cross-domain cookies and localStorage (#1064)`.
- Why it matters: this directly improves browser automation flows that cross login boundaries or SSO/CAS domains. The change switches cookie capture to `Network.getAllCookies` and tracks visited origins to export localStorage beyond only the current origin.
- Evidence:
  - agent-browser commit — https://github.com/vercel-labs/agent-browser/commit/dc26ff76679a1f3b0cf22651d06d79e40dfe88fe
- Practical takeaway: if OpenClaw/browser-agent workflows depend on persisted logged-in state across domains, saved sessions should now be materially more reusable.

## Practical takeaways
- Afternoon signal favored operator correctness and persistence reliability over ecosystem expansion.
- The best external usage signal was not a new repo, but a better state-capture behavior in agent-browser for SSO-style browsing flows.
- Searches for same-day browser/agent repos produced mostly low-signal zero-star projects, so they were intentionally excluded.

## Implications for OpenClaw
- Continue prioritizing direct GitHub/core checks during short daytime runs; they are currently yielding more signal than broad ecosystem discovery.
- For OpenClaw operators, today’s practical wins are in session/model trust, Telegram delivery hygiene, subagent attribution, and saved-browser-state reliability.
- Keep watching for a genuine repo/fork/variant, but do not force one into the digest when the real movement is in core behavior.

## Follow-up actions
- [ ] Watch whether the session/model identity fixes surface in release notes or changelog rollups.
- [ ] Re-check Telegram and inline subagent announce behavior in the next scan window.
- [ ] Track whether agent-browser’s cross-domain state export gets docs/examples, because it is now a stronger real-world persistence pattern.
