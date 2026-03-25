# OpenClaw Agents Night Digest — 2026-03-25

## Scope
Focused operator-relevant scan for the `openclaw-agents` profile, prioritizing the last 12–24 hours and stopping once the run was decision-useful. Search-provider queries were unavailable in this environment, so this digest used direct GitHub PR / issue / repo inspection plus selected adjacent same-day repo checks.

## Highest-signal items

1. **OpenClaw merged a real install-surface hardening fix for local copied package installs**  
   Sources: PR #54543 — https://github.com/openclaw/openclaw/pull/54543
   
   Why it matters:
   - OpenClaw previously ran `npm install` from a staged package root where a malicious staged `.npmrc` could influence install-time behavior.
   - The merged fix hides the staged root `.npmrc` during install and restores it afterward.
   - This narrows the pre-trust execution surface for copied local plugins/hooks without changing normal runtime trust semantics.
   
   Operator take: if you allow local plugin/hook installs or test copied package workflows, this is a meaningful security-hardening change, not cosmetic cleanup.

2. **OpenClaw has two same-day cron reliability fixes in flight: malformed payload tolerance and tighter fatal-error recovery**  
   Sources: PR #54550 — https://github.com/openclaw/openclaw/pull/54550 ; PR #54525 — https://github.com/openclaw/openclaw/pull/54525
   
   Why it matters:
   - PR #54550 adds UI tolerance for malformed cron payloads so Control UI navigation does not crash on bad cron entries.
   - PR #54525 tightens the heuristic that decides whether a cron run really recovered after an error; short progress text should no longer suppress fatal-state detection.
   - PR #54525 also clears `channel` after promotion to `target`, reducing downstream routing ambiguity.
   
   Operator take: this is directly relevant if you rely on cron-delivered digests/reminders and use Control UI to inspect them. The pattern is clear: cron payload shape and recovery logic were still sharp edges today.

3. **OpenClaw has a same-day proposal to reduce poll loops for background jobs via `exec(..., onComplete="notify")`**  
   Source: PR #54549 — https://github.com/openclaw/openclaw/pull/54549
   
   Why it matters:
   - The proposal adds an `onComplete="notify"` mode that implies background execution and wakes the parent session when the process exits.
   - If merged, that would replace a common anti-pattern: repeated `process(action=poll)` loops that waste turns and clutter history.
   - This fits a real operator pain point for long-running repo scans, builds, and coding subroutines.
   
   Operator take: not merged yet, but worth watching because it would change best practice for OpenClaw background execution.

4. **OpenClaw merged a same-day auth fix for `trusted-proxy` mode so local-direct traffic still requires tokens**  
   Source: PR #54536 — https://github.com/openclaw/openclaw/pull/54536
   
   Why it matters:
   - The fix restores the intended boundary: same-host direct requests should use token auth instead of accidentally bypassing checks meant only for trusted-proxy header flows.
   - The PR explicitly tests valid token / wrong token / missing token / fail-closed proxy-config scenarios.
   - This is a good example of an operator-relevant guardrail lesson: “proxy-aware” auth modes can easily widen trust if local-direct fallback paths are not explicit.
   
   Operator take: if you deploy OpenClaw behind a trusted proxy, re-check whether your current version preserves token requirements for local-direct callers.

5. **Recent-important fallback: OpenClaw is also fixing packaging validation around workspace templates in npm releases**  
   Source: PR #54546 — https://github.com/openclaw/openclaw/pull/54546
   
   Why it matters:
   - The PR adds `docs/reference/templates/*.md` to npm release checks so packaged installs do not silently miss workspace bootstrap templates.
   - It was opened in response to a missing-templates report and turns that failure mode into a pre-publish check.
   
   Operator take: this is fallback rather than the top same-day item because it is a safeguard PR, not a shipped release, but it is durable operational signal for anyone distributing or consuming npm/global installs.

6. **New same-day adjacent repo: `cliany.site` turns browser-use/CDP exploration into replayable CLI commands**  
   Sources: repo — https://github.com/pearjelly/cliany.site ; README — https://raw.githubusercontent.com/pearjelly/cliany.site/master/README.md
   
   Why it matters:
   - Instead of only “agent drives browser now,” it records/explores a workflow, then emits structured Click commands for replay.
   - It uses Chrome CDP + accessibility-tree understanding + persistent sessions + JSON output, which is a credible operator pattern for repeatable browser automation.
   - This is more interesting than most browser-use wrappers because the abstraction boundary is explicit: discover once, replay as CLI later.
   
   Caveat: early repo, low proof yet. But the usage pattern is worth stealing for teams who want browser-use-style discovery without staying in a purely conversational loop.

## Bottom line
Tonight’s highest-value signal is not “new agent hype”; it is a cluster of OpenClaw operator fixes around install trust boundaries, cron robustness, and auth correctness, plus one same-day adjacent browser-use pattern that converts exploration into reproducible CLI automation.

Most actionable stance tonight:
- treat local package install paths and trusted-proxy auth as upgrade-worthy surfaces,
- expect cron payload/recovery behavior to still be an active stabilization area,
- and watch the `onComplete="notify"` proposal because it could materially improve how long-running background tasks should be run.

Usage: 218k in / 5.6k out; cache 73%; session usage 5h 84% left, week 47% left.