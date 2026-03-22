# OpenClaw Agents Afternoon Scan

## Scope
- Domain: OpenClaw ecosystem, AI agents, browser automation, repo variants, forks, evals, guardrails, and practical usage patterns
- Intent: repo-radar / usage-radar / domain-update
- Time window: new items since the earlier 2026-03-22 midday scan (roughly 2026-03-22 05:02 UTC -> 08:03 UTC)
- Research date: 2026-03-22 15:03 Asia/Saigon / 2026-03-22 08:03 UTC
- Depth: light afternoon radar

## Collection notes
- Started from primary sources only: GitHub repo activity, PRs, and commits.
- `web_search` was not used because Brave API is still unavailable in this environment.
- Browser automation fallback was not required.
- I stopped early once the incremental signal weakened.

## Executive summary
- No genuinely new repo or meaningful new fork surfaced after the earlier scan.
- The strongest fresh OpenClaw delta was a new PR to abort stalled skill-download streams end-to-end, which is a real behavior fix rather than cosmetic churn.
- A second fresh OpenClaw PR adjusts websocket handshake timeout behavior for loopback clients, but it already has correctness pushback in review, so it is worth watching rather than treating as landed guidance.
- `browser-use` added a practical installer fix for shell PATH configuration, useful for CLI-first operators but smaller than the morning’s docs/usage-pattern update.

## Key findings

### 1. OpenClaw opened a real hang-prevention fix for skill downloads
- What happened:
  - PR `#52140` (`fix(skills): propagate abort signal to download pipeline`) opened after the midday scan.
  - The change moves timeout handling outward so one `AbortController` covers both the HTTP fetch and `stream/promises.pipeline()`, explicitly fixing cases where a server sends headers then stalls mid-stream.
- Why it matters:
  - This is operator-facing behavior impact: skill installation/download flows should stop hanging indefinitely on partial/stalled responses.
  - It also tightens cleanup for early failures so timeout handles do not linger unnecessarily.
- Evidence / link:
  - OpenClaw PR: https://github.com/openclaw/openclaw/pull/52140

### 2. OpenClaw also has a fresh websocket-handshake timeout PR, but review risk is visible already
- What happened:
  - PR `#52142` (`fix(gateway): extend websocket handshake timeout for loopback clients`) opened near the end of this scan window.
  - The proposed behavior is already being challenged in review because using raw `remoteAddr` can misclassify clients behind a local reverse proxy as loopback.
- Why it matters:
  - This is behavior-impacting if it lands, but the current implementation may weaken unauthenticated socket handling for proxied remote clients.
  - Net: useful to monitor, not yet something to operationalize.
- Evidence / link:
  - OpenClaw PR: https://github.com/openclaw/openclaw/pull/52142

### 3. `browser-use` shipped a smaller but practical installer-path fix
- What happened:
  - PR `#4457` changes shell detection in the install script to use the user’s login shell (`$SHELL`) rather than inferring from the shell that executed `curl ... | bash`.
  - It also adds a `.profile` fallback for non-bash/zsh shells.
- Why it matters:
  - This is not a big ecosystem event, but it is a real usage fix: zsh users were getting PATH written to `~/.bashrc`, leaving the `browser-use` command unavailable after install.
- Evidence / link:
  - browser-use PR: https://github.com/browser-use/browser-use/pull/4457

## Practical takeaways
- Re-check OpenClaw `#52140` first; it is the clearest afternoon item with direct user-visible behavior impact.
- Treat OpenClaw `#52142` as watchlist material until the loopback/proxy classification concern is resolved.
- If you rely on `browser-use`’s installer for fresh environments, keep `#4457` in view; it removes one common shell-setup footgun.

## Implications for OpenClaw
- This afternoon window was mostly reliability and install-friction cleanup, not new surface area.
- The most useful delta remains operational: preventing hangs, avoiding misclassified network trust paths, and smoothing tool installation.

## Follow-up actions
- [ ] Re-check whether OpenClaw `#52140` merges; if yes, raise it in the next digest as a concrete operator fix.
- [ ] Re-check the review outcome on OpenClaw `#52142`; only promote it if the trusted-proxy concern is addressed.
- [ ] Re-check whether `browser-use` `#4457` merges/releases before treating the installer fix as broadly available.

Usage: 5h 92% left (1h56m) · week 72% left (5d8h)