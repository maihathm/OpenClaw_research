# OpenClaw Agents Afternoon Scan

## Scope
- Domain: OpenClaw ecosystem, AI agents, browser automation, repo variants, forks, evals, guardrails, and practical usage patterns
- Intent: repo-radar / usage-radar
- Time window: since the earlier 2026-03-21 midday scan (~2026-03-21 05:02 UTC to 2026-03-21 08:02 UTC)
- Research date: 2026-03-21 15:02 Asia/Saigon / 2026-03-21 08:02 UTC
- Depth: light afternoon radar

## Collection notes
- `web_search` remained unavailable here because Brave API is not configured, so I stayed on direct primary-source checks via GitHub API/commit metadata.
- I re-checked OpenClaw, `agent-browser`, and `browser-use` for post-midday movement only.
- `agent-browser` showed no meaningful new post-midday movement in this window.
- No genuinely new repo or meaningful new fork surfaced; the real signal was behavior-changing OpenClaw work and one breaking usage change in `browser-use`.

## Executive summary
- OpenClaw shipped a meaningful device-pairing UX/security change: `/pair qr` now prefers real PNG QR delivery across supported channels, adds explicit expiry/cleanup guidance, and adds cleanup/revoke paths for bootstrap tokens.
- OpenClaw also fixed two operator pain points that can change day-to-day usage: `gateway status --timeout` now respects the full timeout for active local loopback probes, and iOS pairing now avoids silently reusing stale stored device tokens when a fresh bootstrap token was scanned.
- `browser-use` removed `CodeAgent` / `browser_use.code_use.*` entirely on mainline, which is a breaking usage change for wrappers that depended on the code-use flow.
- No new repo/fork signal was strong enough to keep.

## Key findings

### 1. OpenClaw materially changed `/pair qr` from ASCII fallback into real multi-channel QR delivery
- What happened:
  - Commit `2fd3728` (2026-03-21T06:10:29Z) overhauled device pairing.
  - `/pair qr` now generates PNG QR images, can send them through supported channels (Telegram, Discord, Slack, Signal, iMessage, WhatsApp, webchat), adds explicit expiry and `/pair cleanup` guidance, and exposes bootstrap-token cleanup/revoke helpers.
- Why it matters:
  - This is a practical new usage pattern, not cosmetic cleanup.
  - It makes remote device pairing more usable on real chat surfaces and tightens token hygiene by making cleanup/revocation first-class.
- Evidence / links:
  - Commit: https://github.com/openclaw/openclaw/commit/2fd372836e52a7734a24ae5dd47f4038e410affe

### 2. OpenClaw fixed two real operator footguns in gateway probing and pairing auth flow
- What happened:
  - Commit `5bb5d7d` makes `gateway status --timeout` honor the caller timeout for active local loopback probes, while still keeping inactive remote-mode loopback checks fast.
  - Commit `2fd3728` also changes pairing so a freshly scanned bootstrap token wins over any old stored device token, with tests covering the path.
- Why it matters:
  - Slow local/containerized gateways should now produce fewer false timeout reads during diagnostics.
  - Fresh setup-code scans are less likely to fail in confusing ways because of stale remembered auth state.
- Evidence / links:
  - Loopback probe timeout fix: https://github.com/openclaw/openclaw/commit/5bb5d7dab4b29e68b15bb7665d0736f46499a35c
  - Pairing/auth-flow fix bundle: https://github.com/openclaw/openclaw/commit/2fd372836e52a7734a24ae5dd47f4038e410affe

### 3. `browser-use` landed a breaking usage change: `CodeAgent` was removed
- What happened:
  - Commit/PR `54aa7c3` (`rm code agent`, merged 2026-03-21T06:11:33Z) removes `CodeAgent`, `browser_use.code_use.*`, associated helpers, and the `code` extra.
  - The PR notes explicitly point users to migrate back to `Agent` plus action-based flows and to replace `CodeAgentTools` with `Tools` from `browser_use.tools.service`.
- Why it matters:
  - This is the strongest post-midday non-OpenClaw signal because it changes wrapper compatibility and example code immediately.
  - Any OpenClaw-side experimentation or notes that assumed browser-use “code-use” mode now needs migration attention.
- Evidence / links:
  - Merged change: https://github.com/browser-use/browser-use/commit/54aa7c3ef8c9799d56fe11337997ebf84094582c

## Practical takeaways
- Treat OpenClaw device pairing as newly more chat-native: QR delivery is now a real supported interaction, not just setup-code paste or ASCII fallback.
- For sensitive pairing flows, `/pair cleanup` should become part of the normal operator habit after successful onboarding.
- Re-test any local diagnostics or automation that rely on `gateway status --timeout`, especially on slower localhost/container setups.
- Audit any `browser-use` examples/wrappers that still reference `CodeAgent` or `browser_use.code_use.*`.

## Implications for OpenClaw
- The strongest afternoon signal is improved operator ergonomics: pairing got more distribution-aware and more security-explicit.
- OpenClaw continues to move toward better “works in the messy real world” behavior: channel-aware QR delivery, bootstrap-token hygiene, and more faithful timeout semantics.
- On adjacent tooling, the `browser-use` ecosystem is still unstable enough that wrapper assumptions can break intraday; migration-aware notes matter more than generic release watching.

## Follow-up actions
- [ ] Update local OpenClaw usage notes/examples to reflect that `/pair qr` now sends image QR codes on supported chat surfaces and supports `/pair cleanup`.
- [ ] Watch for release-note or docs surfacing of the new pairing flow, because this is strong operator-facing behavior change.
- [ ] Mark any `browser-use` integration notes that mention `CodeAgent` as migration-required.
