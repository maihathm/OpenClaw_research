# OpenClaw Agents Midday Scan — 2026-04-02

## Scope
- Domain: OpenClaw ecosystem / agent tooling / practical operator patterns
- Intent: midday ecosystem radar (`openclaw-agents`)
- Time window: roughly last 18 hours
- Research date: 2026-04-02 12:03 Asia/Saigon / 2026-04-02 05:03 UTC
- Method: primary-source-first checks across tracked repos plus selective GitHub repo discovery; stopped after enough real signal
- Constraints: Brave `web_search` unavailable due to missing API key; used direct GitHub release / API / README checks instead

## Executive summary
- OpenClaw upstream shipped a fresh `v2026.4.1` release with real operator impact: a chat-native `/tasks` board, bundled SearXNG for `web_search`, per-cron tool allowlists, global default provider params, and several approval/task-delivery fixes that change day-to-day use.
- `clawlink` has effectively turned into `woclaw`, and the newest movement is more meaningful than a rename: it now ships a dedicated OpenAI Codex CLI integration package, a Dockerized hub image, and zero-install/quickstart docs that make the shared-memory hub pattern much more runnable.
- A new repo, `sealofyou/hackathon-copilot`, is worth a watch as a concrete OpenClaw workflow pattern: skill-first intake of hackathon intel into Feishu records, todo plans, and task bundles via explicit CLI bridges instead of vague “agent automation” claims.

## Key findings

### 1. OpenClaw `v2026.4.1` is a meaningful workflow release, not routine churn
- What happened:
  - `openclaw/openclaw` published `v2026.4.1` on 2026-04-01.
- Why it matters:
  - `/tasks` makes background work more visible inside chat instead of forcing operators to piece it together from `/status` or task logs.
  - Bundled SearXNG support gives `web_search` a more self-host-friendly path.
  - `openclaw cron --tools` adds per-job tool allowlists, which is a practical control-surface upgrade for automation safety.
  - `agents.defaults.params` and the failover/auth-profile retry changes are direct operator knobs, not internal refactors.
  - The release also tightens approval/task behavior in ways that reduce false approval dead-ends, stale task noise, and delivery friction.
- Evidence:
  - Release notes call out `/tasks`, SearXNG support, Bedrock Guardrails, cron tool allowlists, default provider params, retry/failover controls, and multiple approval/task fixes.
- Links:
  - Release: https://github.com/openclaw/openclaw/releases/tag/v2026.4.1
  - Changelog: https://raw.githubusercontent.com/openclaw/openclaw/main/CHANGELOG.md

### 2. `clawlink` is no longer just an idea repo — `woclaw` now has a Codex path and operator-ready packaging
- What happened:
  - `XingP14/clawlink` now redirects to `XingP14/woclaw`.
  - Multiple commits in the scan window added a dedicated `woclaw-codex` package, updated the README with Codex install instructions, added a zero-install trial section, and fixed plugin auto-connect on gateway startup.
- Why it matters:
  - The notable change is not branding; it is usability. The shared-memory/pub-sub hub pattern now reaches OpenAI Codex CLI directly, which makes cross-agent memory/session handoff more plausible in mixed-agent workflows.
  - Docker image docs and plugin auto-connect reduce the amount of custom glue needed to try the hub in practice.
- Evidence:
  - Recent commits include `feat(codex): add OpenAI Codex CLI WoClaw integration package`, README/docs updates, and `fix(plugin): add setRuntime hook for auto-connect on gateway startup`.
  - The current README lists `woclaw-hub`, `xingp14-woclaw`, `woclaw-mcp`, `woclaw-hooks`, and the new `woclaw-codex` package, plus Docker Hub and MCP usage examples.
- Links:
  - Repo: https://github.com/XingP14/woclaw
  - README: https://github.com/XingP14/woclaw/blob/master/README.md
  - Codex package commit: https://github.com/XingP14/woclaw/commit/6ebbd0faba81795223b1c65d3a1e221345a1d0f2
  - Auto-connect fix commit: https://github.com/XingP14/woclaw/commit/18eaf076e917cb0603e3c8205719c17e2cccb064

### 3. New watchlist repo: `hackathon-copilot` is a practical skill-suite pattern, not generic agent fluff
- What happened:
  - `sealofyou/hackathon-copilot` was created during the scan window.
  - The repo positions itself explicitly as an OpenClaw skill suite, not a standalone app.
- Why it matters:
  - The practical pattern is strong: turn messy hackathon links/docs/posters into structured intel, then into personal todo plans, then into task bundles for downstream execution.
  - The repo already exposes concrete CLI surfaces (`feishu:doctor`, `feishu:intel-upsert`, `feishu:todo-upsert`, `feishu:task-bundle`) instead of stopping at promptware.
  - This is relevant to OpenClaw workflows because it shows a more executable “skills + CLI bridge + external system” packaging style.
- Evidence:
  - README describes a skill-first repo structure (`skills/`, `docs/`, `templates/`, `config/`, `examples/payloads/`, `src/`) and explicit Feishu write/export commands.
- Links:
  - Repo: https://github.com/sealofyou/hackathon-copilot
  - README: https://github.com/sealofyou/hackathon-copilot/blob/main/README.md

## Practical takeaways
- For OpenClaw operators, `v2026.4.1` is mainly about better operational control: background task visibility, safer cron surfaces, and more explicit failover/default-provider behavior.
- For ecosystem variants, `woclaw` is more interesting now because it is becoming runnable across multiple agent runtimes rather than staying a conceptual shared-memory pitch.
- For skill authors, `hackathon-copilot` is a useful packaging pattern: keep the intelligence workflow in skills, but expose deterministic write/export steps through a narrow CLI bridge.

## Implications for OpenClaw
- Core OpenClaw still deserves first priority when it ships operator-facing control-surface changes; this release is clearly above routine noise.
- Shared-memory hubs should only be promoted when they lower integration friction with real packages, install paths, or auto-connect behavior; `woclaw` is getting closer.
- The most reusable new ecosystem signal today is not another model wrapper; it is the emergence of more executable skill+integration bundles around OpenClaw.

## Follow-up actions
- [ ] Revisit whether local OpenClaw installs should switch some search workflows to SearXNG now that bundled provider support exists.
- [ ] Test whether `/tasks` materially changes cron/subagent observability compared with `/status` in real usage.
- [ ] Re-check `woclaw` after the Codex package gets a few real-world install/use reports.
- [ ] Watch whether `hackathon-copilot` develops beyond Feishu-specific plumbing into a broader reusable operator pattern.
