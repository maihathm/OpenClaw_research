# OpenClaw Agents Midday Scan — 2026-04-25

Time window scanned: roughly the last 18 hours through 2026-04-25 13:53 UTC.
Profile: `openclaw-agents`

## What mattered

### 1) New variant repo: `gabdevbr/openclaw-vento`
- New repo created today and updated within minutes of scan.
- Positioning: an OpenClaw fork that bundles `ventomem-cross-session-sync` as an extension instead of keeping cross-session memory sync as a separate add-on.
- Why it matters: this is a more opinionated packaging pattern for users who want memory sync “baked in” rather than layered later. It is closer to a productized distribution variant than a generic fork.
- Caveat: zero stars and very fresh; worth tracking as a packaging pattern more than as validated adoption.
- Sources:
  - GitHub repo: https://github.com/gabdevbr/openclaw-vento
  - Search metadata (created 2026-04-25T10:53:57Z, pushed 2026-04-25T13:50:09Z): https://api.github.com/repos/gabdevbr/openclaw-vento

### 2) New practical automation: `carlosrpi/openclaw-thinking-watchdog`
- New repo created today; external watchdog that reads OpenClaw usage and auto-adjusts `thinking` (`low`/`medium`/`high`) without changing model.
- Implementation pattern is practical: run outside OpenClaw via `systemd --user` timer, call official CLI/RPC, patch defaults and live sessions only when thresholds are crossed.
- Why it matters: this is one of the first concrete examples of quota-aware control loops around OpenClaw itself, using `openclaw status --json --usage` plus config/session patching rather than hacking internals.
- Sources:
  - GitHub repo: https://github.com/carlosrpi/openclaw-thinking-watchdog
  - README: https://raw.githubusercontent.com/carlosrpi/openclaw-thinking-watchdog/main/README.md

### 3) New local-memory implementation trick: `bbj375767338-arch/openclaw-onnx-embed`
- New repo created today for a local ONNX embedding provider targeting `bge-large-zh-v1.5`.
- Notable implementation details: process-local ONNX runtime, no HTTP hop, auto-register as memory embedding provider, and explicit note that users should whitelist in `plugins.allow` rather than forcing `plugins.entries` because Gateway may reconcile entries.
- Why it matters: this is a concrete “offline memory embeddings” pattern for OpenClaw workflows, especially relevant for Chinese-language/local-first deployments.
- Caveat: repo is extremely new and currently narrow (single model, large memory footprint).
- Sources:
  - GitHub repo: https://github.com/bbj375767338-arch/openclaw-onnx-embed
  - README: https://raw.githubusercontent.com/bbj375767338-arch/openclaw-onnx-embed/main/README.md

### 4) New plugin usage pattern: `Almured/almured-openclaw-plugin`
- New repo/plugin published today exposing an agent-to-agent consultation marketplace as 8 native OpenClaw tools.
- Why it matters: it is a live example of turning a third-party network into tool-native capability rather than an MCP sidecar or browser wrapper. Operationally, it also leans on plugin config secrets (`plugins.entries.<name>.config.apiKey`) instead of shell envs.
- Signal level: conceptually interesting as a usage pattern; real adoption still unproven.
- Sources:
  - GitHub repo: https://github.com/Almured/almured-openclaw-plugin
  - README: https://raw.githubusercontent.com/Almured/almured-openclaw-plugin/main/README.md

### 5) Upstream OpenClaw behavior-impact fixes worth noting
- `fix(openrouter): add resolveDefaultThinkingLevel hook` closed today. The PR notes the provider now resolves per-model thinking defaults so auto/non-reasoning models can get `minimal`/`low` instead of inheriting bad defaults such as `off`; root cause cited was 400s on MiniMax slug generation when reasoning was too low. Source: https://github.com/openclaw/openclaw/pull/60969
- `fix(discord): avoid duplicate ACP fallback replies` closed today. Discord now treats routed ACP block replies as already-visible output so end-of-turn fallback text is not replayed. Source: https://github.com/openclaw/openclaw/pull/60972
- Open issue closed today documenting MCP streamable-http interoperability failures (`Missing session ID` / invalid params), useful as a practical warning sign for current OpenClaw MCP workflows using HTTP transport. Source: https://github.com/openclaw/openclaw/issues/61079
- ACP harness issue `--format` flag ordering (`acpx` backend) was also filed and closed today; relevant if Claude Code ACP spawning behaves oddly on older bundled `acpx`. Source: https://github.com/openclaw/openclaw/issues/61116

## Bottom line
Most of today’s real signal is not generic agent news; it is packaging and operationalization around OpenClaw:
- productized fork with bundled cross-session memory,
- quota-aware thinking control loop,
- local/offline embedding provider,
- tool-native marketplace plugin,
- and upstream fixes around thinking defaults, Discord ACP duplication, and MCP/ACP edge cases.
