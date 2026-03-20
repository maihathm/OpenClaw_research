# OpenClaw Agents Midday Scan

## Scope
- Domain: OpenClaw ecosystem, AI agents, browser automation, repo variants, forks, evals, guardrails, and practical usage patterns
- Intent: repo-radar / usage-radar
- Time window: last ~18 hours
- Research date: 2026-03-21 01:01 Asia/Saigon / 2026-03-20 18:01 UTC
- Depth: quick-scan

## Collection notes
- `web_search` was unavailable in this environment because the Brave API key is not configured.
- I continued with direct primary-source checks via GitHub API/release pages and repo metadata.
- Browser automation fallback was not required for this run.

## Executive summary
- `browser-use` merged a meaningful CLI/ops redesign: per-session daemon, new `browser-use cloud` REST workflow, `--connect` auto-discovery, and built-in `upload` support.
- `agent-browser` shipped two practical fixes in quick succession: remote-browser keepalive hardening (`v0.21.3`) and a targeted auth-login readiness fix (`v0.21.4`).
- OpenClaw itself had fresh behavior-impacting movement around Telegram account routing, plugin/docs terminology, and two operator-relevant PRs for skills policy enforcement and sandbox image correctness.
- I did not find a genuinely new OpenClaw-adjacent repo or meaningful new fork in this window; the signal was mostly release/PR/workflow movement.

## Key findings

### 1. `browser-use` merged a major CLI workflow change
- What happened:
  - `browser-use/browser-use` merged PR #4364 (`huge cli update`) at `2026-03-20T17:01:28Z`.
  - The change rebuilds the CLI around a per-session daemon, adds a stdlib `browser-use cloud` REST command, introduces Chrome auto-discovery via `--connect`, adds `upload`, consolidates state under `~/.browser-use`, and removes older `run` / remote task flows.
- Why it matters:
  - This is a real operator-facing change, not cosmetic churn.
  - It changes how long-lived browser sessions should be managed and makes file-input workflows more first-class.
  - Any OpenClaw wrapper/skill that shells out to `browser-use` may need compatibility updates.
- Evidence:
  - PR summary explicitly calls out daemon lifecycle, `cloud` REST command, `--connect`, `upload`, and migration/removal notes.
- Link:
  - GitHub PR: https://github.com/browser-use/browser-use/pull/4364

### 2. `agent-browser` shipped two practical browser-control fixes within hours
- What happened:
  - `vercel-labs/agent-browser` released `v0.21.3` at `2026-03-20T13:59:38Z` and `v0.21.4` at `2026-03-20T14:18:41Z`.
  - `v0.21.3` adds WebSocket ping + TCP keepalive for remote browsers and fixes XPath selector handling.
  - `v0.21.4` changes `auth login` to wait for usable selectors with staged username/email detection, reducing SPA timing failures and `networkidle` hangs.
- Why it matters:
  - These are exactly the kinds of fixes that reduce flaky agent-browser sessions in real automation.
  - Together they improve two common pain points: idle proxy disconnects and brittle login flows.
- Evidence:
  - Release notes explicitly mention remote-browser keepalive, XPath support, and auth login readiness changes.
- Links:
  - `v0.21.4`: https://github.com/vercel-labs/agent-browser/releases/tag/v0.21.4
  - `v0.21.3`: https://github.com/vercel-labs/agent-browser/releases/tag/v0.21.3

### 3. OpenClaw landed a fresh Telegram account-routing fix with direct behavior impact
- What happened:
  - OpenClaw commit `4e45a66` (`fix(telegram): prevent silent wrong-bot routing when accountId not in config`) landed at `2026-03-20T05:13:01Z`.
  - A follow-up changelog commit `35ac1f6` was added at `2026-03-20T17:51:53Z`.
- Why it matters:
  - This is a concrete delivery-correctness fix for multi-account Telegram setups.
  - It matters operationally because silent wrong-bot routing is worse than a loud failure; it can make automations look healthy while delivering from the wrong identity.
- Evidence:
  - The commit subject is explicit, and the repo immediately added a changelog entry for the same fix.
- Links:
  - Fix commit: https://github.com/openclaw/openclaw/commit/4e45a663e79c897b948de3f9f5c673d1f2cf39d5
  - Changelog commit: https://github.com/openclaw/openclaw/commit/35ac1f6e07aa6c9ac4884f6658b3ec481ad77b13

### 4. OpenClaw docs/plugin surface is being actively renamed and normalized
- What happened:
  - OpenClaw pushed a cluster of docs + SDK commits around `2026-03-20T17:17Z`–`18:00Z`, including:
    - `a2e1991` — route bundled runtime barrels through public subpaths
    - `ad4536f` — rename Extensions to Plugins and rewrite the building guide
    - `5f600e1` / `3d097f1` — restructure the Tools/Plugins landing pages
- Why it matters:
  - This looks like a real documentation/interface consolidation rather than typo churn.
  - The practical signal: plugin/SDK terminology and public import paths are being cleaned up, which affects how users should structure extensions/plugins and read the docs.
- Evidence:
  - The commit subjects explicitly reference public subpaths, renaming Extensions → Plugins, and rewriting the tools landing page.
- Links:
  - SDK/public-subpaths commit: https://github.com/openclaw/openclaw/commit/a2e1991ed315968b0a57f1c60d90a05f314c4d7d
  - Docs rename commit: https://github.com/openclaw/openclaw/commit/ad4536fd7eb165b973f82c2031b2df2f7390e622
  - Tools landing rewrite: https://github.com/openclaw/openclaw/commit/3d097f10527c026780cbd1eb1f0967d7796bf534

### 5. Two open OpenClaw PRs are especially worth watching because they change operator behavior
- What happened:
  - PR #51165 (`feat(skills): agent-scoped policy parity + reactive snapshot refresh`) was opened at `2026-03-20T17:31:44Z`.
  - PR #51166 (`fix(sandbox): pull pre-built image from GHCR instead of plain debian:bookworm-slim`) was opened at `2026-03-20T17:32:59Z`.
- Why it matters:
  - #51165 points toward stricter per-agent skill boundaries and snapshot refresh behavior — directly relevant for specialized-agent setups.
  - #51166 fixes a very practical sandbox regression: file write/edit failures caused by missing `python3` in the pulled image.
  - These are not merged yet, so they are watch items rather than landed guidance.
- Evidence:
  - PR descriptions explicitly mention skill-policy enforcement gaps and the sandbox `python3: not found` root cause.
- Links:
  - PR #51165: https://github.com/openclaw/openclaw/pull/51165
  - PR #51166: https://github.com/openclaw/openclaw/pull/51166

## Practical takeaways
- Re-check any local OpenClaw browser wrappers that assume older `browser-use` CLI verbs or non-daemon behavior.
- For remote browser control, prefer tools that now explicitly harden keepalive and login readiness; these two fixes remove common flaky edges.
- In multi-account Telegram deployments, treat recent account-routing fixes as high priority because they affect delivery correctness, not just UX.
- Watch OpenClaw’s plugin terminology/public-subpath cleanup before writing new plugin docs or examples.
- If you rely on sandboxed coding/file edits, monitor the GHCR sandbox-image PR closely.

## Implications for OpenClaw
- The biggest fresh ecosystem signal is not “new repo” but “new operating pattern”: browser tools are shifting toward more durable daemons, explicit remote/cloud paths, and sturdier auth flows.
- OpenClaw’s near-term operator surface is moving toward stricter agent scoping and clearer plugin boundaries.
- For practical workflows, Telegram routing correctness and sandbox image correctness remain more urgent than headline features.

## Follow-up actions
- [ ] Check whether any local OpenClaw browser skills assume pre-#4364 `browser-use` CLI behavior.
- [ ] Watch whether PR #51166 merges quickly; if yes, note it in the next scan as a sandbox reliability upgrade.
- [ ] Track whether the Extensions → Plugins terminology shift propagates into docs/examples that this repo references.
- [ ] Keep watching for a real new repo/fork signal; this window was mostly behavior-changing updates, not new project launches.
