# OpenClaw Agents Midday Scan

## Scope
- Domain: OpenClaw ecosystem, AI agents, browser automation, repo variants, forks, evals, guardrails, and practical usage patterns
- Intent: repo-radar / usage-radar / domain-update
- Time window: last ~18 hours through 2026-03-22 05:02 UTC
- Research date: 2026-03-22 12:02 Asia/Saigon / 2026-03-22 05:02 UTC
- Depth: quick-scan

## Collection notes
- `web_search` was unavailable because Brave API is not configured in this environment.
- I stayed on primary sources: GitHub commits, PRs, changelog diffs, and repo metadata.
- Browser automation fallback was not required.
- I checked for fresh repo/fork signal, but the strongest genuinely usable updates this window were behavior-changing commits/PRs and a new docs-driven usage pattern rather than a fully credible new OpenClaw-adjacent codebase.

## Executive summary
- OpenClaw shipped a concrete startup-latency reduction for embedded runs by caching `models.json` readiness across turns instead of paying repeated model-catalog startup work.
- OpenClaw also has two fresh operator-facing PRs worth watching immediately: one to preserve AGENTS.md standing instructions across overflow compaction, and one to add Kiro CLI as a first-class coding-agent backend.
- `browser-use` committed a large docs/skill split that is more than docs churn: it now documents Cloud/Open Source separately and explicitly spells out subagent, tools-integration, and OpenClaw usage patterns.
- `agent-browser` opened a practical upgrade-path fix so installs done via pnpm/yarn/bun can self-detect and upgrade cleanly.
- I did not find a sufficiently credible new repo/fork in this window to keep; several newly created OpenClaw-named repos were empty or too thin to treat as real signal yet.

## Key findings

### 1. OpenClaw reduced repeated model-catalog startup work for embedded runs
- What happened:
  - OpenClaw merged commit `2b210703` (`fix(models): cache models.json readiness for embedded runs`) at `2026-03-22T04:58:10Z`.
  - The patch adds a readiness cache keyed by config/auth-file state and updates tests/changelog accordingly.
- Why it matters:
  - This is direct operator signal: embedded runner turns should stop repeatedly rebuilding model-catalog readiness before replies.
  - It fits the repo’s recent pattern of shaving cold-start/turn latency instead of adding flashy surface area.
- Evidence / links:
  - Commit: https://github.com/openclaw/openclaw/commit/2b210703a3b99f4740897ad1643c42ff76090546

### 2. OpenClaw has a fresh compaction-safety PR to preserve AGENTS.md grounding after overflow
- What happened:
  - Draft PR `#52080` (`fix: re-inject AGENTS.md context after overflow compaction`) was opened/updated in this window.
  - It adds post-compaction AGENTS.md re-injection in the embedded runner path and updates compaction instructions to preserve standing user directives.
- Why it matters:
  - If merged, this would directly reduce a nasty class of “agent forgot my standing instructions after context overflow” failures.
  - For OpenClaw-heavy workflows, that is behavior-impacting, not cosmetic.
- Evidence / links:
  - PR: https://github.com/openclaw/openclaw/pull/52080

### 3. OpenClaw also has a fresh coding-agent expansion PR: Kiro CLI support
- What happened:
  - PR `#52091` (`feat(coding-agent): add Kiro CLI as a supported coding agent`) opened at `2026-03-22T05:03:31Z`.
  - The PR proposes `kiro-cli chat --no-interactive --trust-all-tools`, custom `--agent` / `--model` support, and background/auto-notify patterns inside the coding-agent skill.
- Why it matters:
  - This is a genuine new usage path for OpenClaw’s ACP/coding workflow surface: another first-class backend, not just another community wrapper.
  - Worth watching if you want more backend optionality without inventing custom shell glue.
- Evidence / links:
  - PR: https://github.com/openclaw/openclaw/pull/52091

### 4. `browser-use` turned its docs into agent-usable skills and explicitly documented OpenClaw/subagent patterns
- What happened:
  - Commit `73e11b0` added separate `skills/cloud/*` and `skills/open-source/*` trees plus focused guides for chat UI, subagent delegation, tool-level integration, CDP browser access, and an OpenClaw-specific pattern section.
  - The new docs explicitly cover: CLI passthrough for coding agents, task-in/result-out subagent usage, `liveUrl` chat UIs, CDP browser sessions, and OpenClaw deployment patterns.
- Why it matters:
  - This is high-signal “cách dùng mới,” not mere documentation cleanup.
  - It lowers integration friction for using browser-use as either a delegated browser subagent or a tool provider inside agent systems.
- Evidence / links:
  - Commit: https://github.com/browser-use/browser-use/commit/73e11b0bba8c1986639e1b04edab6b3e9b315a38

### 5. `agent-browser` is fixing upgrade-path fragility across package managers
- What happened:
  - PR `#960` adds pnpm/yarn/bun detection, an install-time `.install-method` marker, stronger path heuristics, and package-manager probing for the `upgrade` command.
- Why it matters:
  - Small patch, real ops value: upgrade flows are a common support/debug path, and “could not detect installation method” is exactly the kind of avoidable friction that slows adoption in mixed JS environments.
- Evidence / links:
  - PR: https://github.com/vercel-labs/agent-browser/pull/960

## Practical takeaways
- Re-test embedded OpenClaw responsiveness after the `models.json` readiness cache change; this is a real candidate for reducing turn startup drag.
- Watch `#52080` closely if instruction persistence after compaction matters in your deployments; it is one of the most operator-relevant in-flight fixes this morning.
- Treat `browser-use`’s new docs split as an integration playbook: it now cleanly separates “delegate the whole web task” from “give my agent browser tools.”
- If you use `agent-browser` via npm alternatives, the upgrade detection PR is worth monitoring because it removes install-method guesswork.

## Implications for OpenClaw
- Today’s strongest signal is operational reliability and integration clarity, not new model hype.
- OpenClaw itself is still optimizing the hard parts: startup cost, context retention, and backend flexibility.
- Adjacent browser tooling is increasingly publishing concrete integration patterns rather than leaving operators to reverse-engineer them from examples.

## Follow-up actions
- [ ] Re-check whether PR `#52080` lands; if it does, raise the priority of compaction/instruction-persistence guidance.
- [ ] Re-check whether PR `#52091` lands; if it does, note Kiro as a first-class coding-agent option in future OpenClaw operator summaries.
- [ ] Mine `browser-use`’s new `subagent` and `tools-integration` guides for concrete patterns worth porting into OpenClaw workflows.
- [ ] Re-check `agent-browser` PR `#960` for merge/release status before treating the upgrade fix as generally available.

Usage: 5h 97% left (4h55m) · week 73% left (5d11h)
