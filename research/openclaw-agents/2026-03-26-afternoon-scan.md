# OpenClaw Agents Afternoon Scan — 2026-03-26

## Scope
- Domain: OpenClaw ecosystem / adjacent agent tooling
- Intent: ecosystem radar
- Time window: since the earlier 2026-03-26 midday scan (~2026-03-26 12:02 Asia/Saigon) through ~15:10 Asia/Saigon
- Depth: light scan
- Method: direct primary-source checks first (GitHub commits, repo contents, READMEs); stopped early once enough signal appeared

## Executive summary
- OpenClaw upstream landed a real provider expansion plus several operator-facing fixes after the midday scan: Microsoft Foundry provider support, Codex websocket routing/tool-warning preservation, and BlueBubbles inbound image hydration.
- Two fresh same-day repos stood out as more than placeholder noise: `plugin-creator` (plugin design/debugging skill) and `openclaw-termhand` (remote local-terminal bridge for OpenClaw).
- A same-day `OpenClawMiddleware` repo also appeared with a more security-first transport pattern: encrypted multi-client WebSocket middleware in front of Gateway.
- Signal was adequate but still early-stage; most other same-day repos looked empty or too thin to keep.

## Key findings

### 1. OpenClaw upstream added Microsoft Foundry provider support and several behavior-impacting fixes
- What happened:
  - `feat: Add Microsoft Foundry provider with Entra ID authentication (#51973)` landed, adding a bundled `extensions/microsoft-foundry` provider/plugin surface.
  - Follow-up wiring/docs commits landed immediately after: contract registry hookup and refreshed config baseline.
  - Additional operator-facing fixes landed in the same window:
    - Codex responses routed over websocket while preserving explicit tool warnings.
    - CLI-routed BlueBubbles turns regained inbound image embedding/hydration.
- Why it matters:
  - This is not just docs churn; it expands provider surface and fixes concrete routed-session/media behavior.
  - Operators using Codex-backed or message-routed flows get fewer broken media/tool-warning edge cases.
- Primary sources:
  - Foundry feature commit: https://github.com/openclaw/openclaw/commit/a16dd96694c99f6f0c2d4c13f651c6d83a7c7d31
  - Foundry contract registry fix: https://github.com/openclaw/openclaw/commit/7ea17965d0b9c6b09fb3f8a658219f6248b7cbcf
  - Foundry config baseline docs refresh: https://github.com/openclaw/openclaw/commit/7858441d2ca8519288c4f35c77d83f69ebfd0f6b
  - Codex websocket/tool-warning fix: https://github.com/openclaw/openclaw/commit/d72cc7ab240f9054b68af67f9a117b6af25b80e0
  - BlueBubbles inbound image hydration fix: https://github.com/openclaw/openclaw/commit/00e932ad6fbb72d1d3302c62ef4d5b293ff512ff

### 2. New repo: `vrcms/openclaw-termhand`
- What happened:
  - A new same-day repo describes a pattern where OpenClaw on a VPS controls a user's local terminal over a token-authenticated WebSocket bridge.
  - The repo exposes a small HTTP control surface for session creation, input, output polling, and kill operations.
- Why it matters:
  - This is a concrete new usage pattern, not generic agent chatter: browser control gets paired with terminal control from a remote OpenClaw instance.
  - Notable design choices: local bridge initiates the outbound connection, local machine exposes no inbound port, sessions are stateful, and Windows UTF-8 handling is called out explicitly.
- Primary sources:
  - Repo: https://github.com/vrcms/openclaw-termhand
  - README: https://raw.githubusercontent.com/vrcms/openclaw-termhand/master/README.md

### 3. New repo: `pazyork/plugin-creator`
- What happened:
  - A new skill repo focused specifically on building/debugging OpenClaw plugins.
  - The README/SKILL position it around plugin boundary decisions: hook vs tool vs command vs skill, pre-install validation, and debugging “loaded but unusable” cases.
- Why it matters:
  - The signal here is not novelty for novelty’s sake; it encodes a practical design framework for when a behavior should become a plugin surface versus remain a skill or command.
  - Useful as ecosystem evidence that plugin authoring is starting to get its own dedicated workflow/documentation layer.
- Primary sources:
  - Repo: https://github.com/pazyork/plugin-creator
  - README: https://raw.githubusercontent.com/pazyork/plugin-creator/main/README.md
  - SKILL: https://raw.githubusercontent.com/pazyork/plugin-creator/main/SKILL.md

### 4. New repo: `lebacco-zhou/OpenClawMiddleware`
- What happened:
  - A same-day .NET middleware service appeared, positioned as a secure encrypted communication layer in front of OpenClaw Gateway.
  - Repo structure and status doc show implemented services for token auth, RSA key exchange, AES-GCM encryption, multi-client WebSockets, heartbeat cleanup, rate limiting, and Gateway proxying.
- Why it matters:
  - This is an early but concrete variant pattern: put a dedicated transport/security layer between clients and Gateway instead of exposing Gateway directly.
  - Especially relevant for remote/mobile deployments where operators may want client isolation and explicit transport controls.
- Primary sources:
  - Repo: https://github.com/lebacco-zhou/OpenClawMiddleware
  - README: https://raw.githubusercontent.com/lebacco-zhou/OpenClawMiddleware/main/README.md
  - Status doc: https://raw.githubusercontent.com/lebacco-zhou/OpenClawMiddleware/main/PROJECT_STATUS.md

## Practical takeaways
- Watch Microsoft Foundry support as a real new provider path, not a cosmetic addition; it likely changes onboarding/config surfaces soon.
- `openclaw-termhand` is worth treating as a new operator pattern: remote OpenClaw controlling a local shell without exposing the shell host publicly.
- `plugin-creator` suggests plugin-authoring guidance is becoming a sub-domain of its own; useful for improving extension ergonomics.
- `OpenClawMiddleware` is early, but the transport-wrapper pattern is worth monitoring for self-hosted security-sensitive setups.

## Implications for OpenClaw
- Consider a future experiment note on “remote local terminal bridge” patterns and their guardrail requirements.
- Track whether Microsoft Foundry docs mature into a recommended enterprise/provider setup path.
- Plugin authoring/debugging could justify a more explicit OpenClaw-side best-practices guide if this niche keeps growing.
- Middleware/proxy patterns may become important if more users try to separate Gateway exposure from end clients.

## Follow-up actions
- [ ] Re-check `openclaw-termhand` later for protocol details and threat model gaps.
- [ ] Watch OpenClaw docs/changelog for user-facing Microsoft Foundry setup guidance.
- [ ] See whether `plugin-creator` gains reference examples that are reusable in this repo.
- [ ] Revisit `OpenClawMiddleware` after first build/test evidence appears.
