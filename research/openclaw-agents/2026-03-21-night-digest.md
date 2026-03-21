# OpenClaw Agents Night Digest

## Scope
- Domain: OpenClaw ecosystem, AI agents, browser automation, repo variants, forks, evals, guardrails, and practical usage patterns
- Intent: usage-radar / repo-radar / domain-update
- Time window: last ~12-24 hours
- Research date: 2026-03-21 09:58 Asia/Saigon / 2026-03-21 02:58 UTC
- Depth: normal

## Collection notes
- `web_search` was unavailable in this environment because the Brave API key is not configured.
- I stayed on primary sources: GitHub PRs, commits, and release pages.
- Browser automation fallback was not required.
- I did **not** find a genuinely new high-signal OpenClaw-adjacent repo or meaningful new fork in this window; the real signal was operator-impacting repo/release/docs movement.

## Executive summary
- `browser-use` merged a meaningful CLI/ops redesign centered on a per-session daemon, a new `browser-use cloud` REST flow, `--connect` auto-discovery, and built-in upload support.
- `agent-browser` shipped two practical reliability fixes in quick succession: remote-browser keepalive hardening (`v0.21.3`) and auth-login readiness improvements (`v0.21.4`).
- OpenClaw landed a concrete Telegram multi-account safety fix that prevents silent wrong-bot routing when `accountId` is missing from config.
- OpenClaw docs/plugin surface is being actively normalized: `Extensions` → `Plugins`, clearer Tools/Skills/Plugins explanation, and more public runtime barrel exports.
- Two fresh OpenClaw PRs remain worth watching because they affect real operator behavior: skill-policy parity / reactive snapshot refresh and sandbox image reliability.

## Key findings

### 1. `browser-use` merged a major CLI workflow shift
- What happened:
  - `browser-use/browser-use` merged PR #4364 (`huge cli update`) at `2026-03-20T17:01:28Z`.
  - The PR summary says the CLI was rebuilt around a per-session daemon, adds stdlib `browser-use cloud` REST commands, introduces Chrome auto-discovery via `--connect`, adds `upload`, consolidates state under `~/.browser-use`, and simplifies install/setup.
- Why it matters:
  - This changes the expected operating model for wrappers, long-lived sessions, and browser lifecycle handling.
  - For operators, this is a workflow change, not cosmetic churn.
- Evidence / link:
  - GitHub PR #4364: https://github.com/browser-use/browser-use/pull/4364

### 2. `agent-browser` shipped two high-value reliability fixes within hours
- What happened:
  - `v0.21.3` (`2026-03-20T13:59:38Z`) adds WebSocket ping frames and TCP keepalive for remote browsers, fixes `xpath=` selector handling, and short-circuits diffing for identical snapshots.
  - `v0.21.4` (`2026-03-20T14:18:41Z`) improves `auth login` by waiting for usable selectors, doing staged username/email detection, and avoiding `networkidle` hangs on SPA-style pages.
- Why it matters:
  - These fixes directly reduce two common browser-agent failure modes: silent remote-browser disconnects and flaky login readiness.
- Evidence / links:
  - `v0.21.3`: https://github.com/vercel-labs/agent-browser/releases/tag/v0.21.3
  - `v0.21.4`: https://github.com/vercel-labs/agent-browser/releases/tag/v0.21.4

### 3. OpenClaw fixed a high-risk Telegram routing failure mode
- What happened:
  - Commit `4e45a66` explicitly prevents fallback to the channel-level bot token when a non-default `accountId` is specified but not found.
  - The patch adds a refusal path instead of silently routing through the wrong bot token.
- Why it matters:
  - This is a correctness/safety fix for multi-account Telegram setups.
  - Silent misdelivery is worse than visible failure because automations can appear healthy while using the wrong identity.
- Evidence / link:
  - Commit `4e45a66`: https://github.com/openclaw/openclaw/commit/4e45a663e79c897b948de3f9f5c673d1f2cf39d5

### 4. OpenClaw docs and plugin surface are being cleaned up in ways that affect usage guidance
- What happened:
  - Commit `ad4536f` renames docs grouping from `Extensions` to `Plugins` and rewrites parts of the building guide.
  - Commit `3d097f1` rewrites the tools landing page to explain the tools / skills / plugins layering more clearly.
  - Commit `a2e1991` routes bundled runtime barrels through public subpaths and re-exports more plugin SDK/runtime types and helpers.
- Why it matters:
  - This is practical documentation/interface convergence: it affects how users should name things, where they import from, and how plugin-related examples should be written.
- Evidence / links:
  - Docs rename: https://github.com/openclaw/openclaw/commit/ad4536fd7eb165b973f82c2031b2df2f7390e622
  - Tools/skills/plugins explainer rewrite: https://github.com/openclaw/openclaw/commit/3d097f10527c026780cbd1eb1f0967d7796bf534
  - Public subpath/runtime export update: https://github.com/openclaw/openclaw/commit/a2e1991ed315968b0a57f1c60d90a05f314c4d7d

### 5. Two open PRs are worth monitoring because they may change operator practice soon
- What happened:
  - PR #51165 adds agent-scoped skill-policy parity plus reactive skill snapshot refresh when policy/filter changes, not just version bumps.
  - PR #51166 aims to fix sandbox-image behavior by pulling a prebuilt GHCR image instead of relying on a plain `debian:bookworm-slim` path that misses required tooling; review comments also highlight ARM64 tag selection and dead fallback-path risk.
- Why it matters:
  - #51165 matters for specialized-agent isolation and predictable skill boundaries.
  - #51166 matters because sandbox file editing can fail for installed users if the image/tooling path is wrong.
- Evidence / links:
  - PR #51165: https://github.com/openclaw/openclaw/pull/51165
  - PR #51166: https://github.com/openclaw/openclaw/pull/51166

## Practical takeaways
- Re-check any wrapper or skill that assumes older `browser-use` CLI verbs or a non-daemon session model.
- For remote browser sessions, keepalive behavior and login-readiness handling now look like first-class reliability requirements rather than optional polish.
- In Telegram multi-account deployments, prefer loud failure over silent fallback; recent OpenClaw behavior is moving in the right direction.
- When writing OpenClaw docs/examples, align terminology with `Plugins`, not `Extensions`, and expect more public subpath-based imports.
- Watch the sandbox-image PR closely if you rely on coding/file-edit agents, especially on non-amd64 hosts.

## Implications for OpenClaw
- The most important fresh ecosystem signal is a shift toward more durable browser-session infrastructure: daemonized control, cloud/REST paths, keepalive hardening, and explicit login-readiness logic.
- OpenClaw itself is tightening correctness at the edges that matter operationally: account routing, skill scoping, and sandbox-image reliability.
- Documentation cleanup is not just cosmetic; it is converging the mental model for tools, skills, and plugins, which should reduce user/operator confusion.

## Follow-up actions
- [ ] Check whether any local OpenClaw browser skills still assume pre-#4364 `browser-use` CLI behavior.
- [ ] Watch whether PR #51166 merges quickly; if it does, treat it as a real sandbox reliability upgrade worth folding into operator guidance.
- [ ] Watch whether PR #51165 lands without the snapshot-refresh regressions flagged in review.
- [ ] Update future OpenClaw examples/notes to use `Plugins` terminology consistently.

Usage: 5h 96% left (4h54m) · week 84% left (6d13h)
