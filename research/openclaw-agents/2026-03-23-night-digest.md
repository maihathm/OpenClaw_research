# OpenClaw Agents Night Digest — 2026-03-23

## Scope
Focused operator-relevant scan for the `openclaw-agents` profile, prioritizing the last 12–24 hours and stopping once the run was decision-useful. Search-provider queries were unavailable in this environment, so this digest used direct GitHub release / issue / PR / repo inspection.

## Highest-signal items

1. **OpenClaw `v2026.3.22` shipped today with several operator-impacting migration changes**  
   Source: GitHub Release `v2026.3.22` — https://github.com/openclaw/openclaw/releases/tag/v2026.3.22  
   Why it matters:
   - bare `openclaw plugins install <package>` now prefers **ClawHub before npm** for npm-safe names
   - legacy **Chrome extension relay** path is removed; host-local browser users are supposed to migrate via `openclaw doctor --fix`
   - bundled `nano-banana-pro` wrapper is gone; image generation now standardizes on core `image_generate`
   - plugin authors now need `ChannelMessageActionAdapter.describeMessageTool(...)`; older message-tool discovery methods are removed
   Operator take: this is not a "just upgrade" release. It changes install precedence, browser automation assumptions, image-generation defaults, and plugin SDK/message-tool expectations in one shot.

2. **Fresh same-day regression cluster: `2026.3.22` Control UI assets missing in packaged installs**  
   Sources: issue #52977 — https://github.com/openclaw/openclaw/issues/52977 ; issue #52987 — https://github.com/openclaw/openclaw/issues/52987  
   Why it matters:
   - both `install.sh` and npm/global-install users report `Control UI assets not found`
   - reports point to packaged UI assets not being present in the published build/tarball
   Operator take: treat `2026.3.22` as risky for hosts where dashboard/UI availability matters. If you manage headless-only systems this is less severe, but for operator dashboards it is a real same-day packaging regression.

3. **Same-day fix landed fast for message-tool breakage across Discord / Slack / Feishu**  
   Sources: PR #52991 — https://github.com/openclaw/openclaw/pull/52991 ; issue #52970 — https://github.com/openclaw/openclaw/issues/52970 ; issue #52962 — https://github.com/openclaw/openclaw/issues/52962  
   Why it matters:
   - `2026.3.22` introduced schema/discovery problems where Discord actions could wrongly require `components`
   - Slack DM `media` sends and Feishu `media` sends were broken/ignored
   - maintainer PR #52991 was merged within minutes to make Discord `components` and Slack `blocks` optional where appropriate and route Feishu `media` through outbound media handling
   Operator take: if you rely on message actions or file/image sends, watch for the first patch after `2026.3.22` rather than pinning blindly to the initial release.

4. **Same-day operator guardrail fix in progress: isolated cron sessions were not truly isolated**  
   Source: PR #52862 — https://github.com/openclaw/openclaw/pull/52862  
   Why it matters:
   - current behavior reused a stable session key (`cron:${job.id}`) even for `sessionTarget: "isolated"`
   - proposed fix changes isolated cron runs to unique keys like `cron:isolated:${jobId}:${timestamp}:${random}`
   Operator take: if you depend on isolated cron jobs for clean context boundaries, verify your deployed version. Before this fix, repeated cron runs could leak context across executions.

5. **New repo today: `arch-conscience` — an OpenClaw-native ADR/architecture contradiction watcher for PRs**  
   Source: repo README — https://github.com/thaneeshshanand/arch-conscience  
   Why it matters:
   - practical OpenClaw pattern: GitHub webhook -> PR diff summary -> Qdrant ADR retrieval -> LLM contradiction detection -> Telegram/Slack/WhatsApp alert
   - notable usage lesson: it treats “no relevant ADR chunks found” as a **corpus-gap signal**, which is a useful operator pattern for production RAG/guardrail systems
   Caveat: early project / portfolio-grade implementation, but the design pattern is strong and transferable.

6. **New repo today: `agent-browser-hub` packages `agent-browser` into a single-binary YAML automation hub**  
   Source: repo README — https://github.com/Xiechengqi/agent-browser-hub  
   Why it matters:
   - turns browser automation into declarative YAML pipelines with JSON/YAML/table/CSV/Markdown output modes
   - adds Web UI + REST API around the browser layer, which may appeal to operators who want reproducible script catalogs rather than free-form browser prompting
   Caveat: this is adjacent rather than core OpenClaw, but it is a credible same-day usage variant for teams exploring more structured browser-task execution.

## Bottom line
Tonight’s strongest signal is not generic “agent news”; it is the combination of:
- a large `v2026.3.22` release with real migration surface,
- immediate same-day packaging regressions affecting Control UI installs,
- immediate same-day message-tool regressions plus a rapid maintainer fix,
- and one meaningful cron-isolation correctness fix still in flight.

For operators, the most actionable stance tonight is **upgrade carefully, especially if you need dashboard reliability or message/media delivery across channel plugins**.

Usage: 49k in / 8.5k out; cache 93%; session usage 5h 94% left, week 57% left.
