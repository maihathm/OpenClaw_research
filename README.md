# OpenClaw Research Base

A living research repo for tracking the **OpenClaw ecosystem**, adjacent agent tooling, practical operator workflows, and meaningful implementation variants over time.

This repo is not meant to be a generic news archive. It is meant to be a **high-signal working memory** for:
- new repos worth watching
- meaningful forks or variants
- practical usage patterns
- release/docs/issues that change operator behavior
- notes that remain useful after the daily crawl is over

---

## At a glance

### Primary goal
Track the OpenClaw / agent-tooling ecosystem with a practical bias:
- what changed
- why it matters
- what is actually usable
- what should be tested, watched, or copied into future workflow design

### Core output of this repo
Every crawl should produce:
1. a dated note under `research/openclaw-agents/`
2. a small README refresh so the repo front page stays useful

### Current focus
- OpenClaw core behavior changes
- OpenClaw-adjacent repos and plugins
- browser / automation / tooling patterns useful for agents
- practical deployment, debugging, rate-limit, and orchestration lessons
- meaningful variants, forks, wrappers, and operator-facing integrations

---

## Recommended reading order

If you are new to this repo, read in this order:

1. `README.md`
2. `SKILL.md`
3. `profiles/openclaw-agents.json`
4. `references/CRAWL_PLAN.md`
5. `references/FOCUS.md`
6. latest files in `research/openclaw-agents/`

---

## What gets updated after each crawl

After each daily crawl, update this README lightly.

### Always refresh
- **Latest update**
- **Important rolling notes**
- **OpenClaw variants / useful repos watch table**

### Do not turn README into a dump
Only keep:
- durable takeaways
- current watchlist signal
- operator-relevant changes
- patterns likely to matter again

Push transient detail into the dated daily note instead.

---

## Latest update

- **Latest scan note:** `research/openclaw-agents/2026-03-31-midday-scan.md`
- **Last meaningful README refresh:** 2026-03-31
- **Current short read of the landscape:**
  - OpenClaw core is still the strongest signal source when same-day behavior-changing commits land.
  - The most useful ecosystem movement right now is coming from **practical operator variants** rather than broad “new agent framework” noise.
  - Voice bridges, model/persona switching, regional search fallback, and rate-limit-aware orchestration are currently more actionable than generic launch hype.

---

## Important rolling notes

Keep this section short and durable. Replace or reorder items when the signal changes.

### 1. OpenClaw core commit flow is high priority
Recent core changes around Telegram routing, cron isolated retry behavior, detached execution, and SSRF hardening had direct workflow impact.

Why it matters:
- chat/thread continuity can break delivery semantics
- cron and isolated execution changes affect scheduled workflows
- security hardening changes may alter network behavior or safe defaults

### 2. Practical operator patterns are more valuable than broad framework churn
The strongest external signal has recently come from operator-facing patterns such as:
- model-aware persona/bootstrap switching
- regional search fallback plugins
- hosted browser execution wrappers
- rate-limit-aware pause/resume orchestration
- OpenClaw-shaped voice bridges

### 3. Early repos should stay on watchlist status until they prove depth
A repo being new is not enough.

Promote only when one or more appear:
- real docs depth
- reproducible setup
- concrete workflow value
- active issue/release movement
- evidence that the pattern is transferable

### 4. Prefer pattern extraction over repo admiration
For many new repos, the most reusable signal is not the repo itself but the pattern behind it:
- how it handles fallback
- how it resumes interrupted work
- how it patches routing or session behavior
- how it packages browser or voice capabilities into OpenClaw-friendly workflows

---

## OpenClaw variants / useful repos watch table

This table should be updated lightly after crawls. Keep only items that are hot, useful, or structurally important.

| Project / Variant | Type | Why it matters | Current status | What to watch next |
|---|---|---|---|---|
| `openclaw/openclaw` | Core upstream | Primary source for behavior-changing commits, cron/session/runtime changes, routing fixes, security hardening | **Highest priority** | Release notes, routing behavior, cron/executor changes, security defaults |
| `frankekn/openclaw-model-switcher` | Plugin / workflow variant | Treats model switching as persona/bootstrap/workspace switching | **Useful pattern** | safety of file swap/restore behavior, profile examples, real operator adoption |
| `z-imagine/openclaw-baidu-search` | Search plugin | Adds China-oriented search coverage with API + scraper fallback pattern | **Useful but early** | install reliability, anti-bot robustness, query quality |
| `Aston1690/vercel-sandbox` | Deployment wrapper | Packages `agent-browser` + Chrome into Vercel microVM flow | **Interesting deployment pattern** | production caveats, stability, cost/latency tradeoffs |
| `TotzkePaul/OpenClawDiscordVC` | Voice integration | Concrete OpenClaw-shaped Discord voice pipeline with debug detail | **High practical interest** | reliability, voice quality, setup friction, media decryption edge cases |
| `akhilc08/mission-control` | Orchestration / ops pattern | Shows a useful rate-limit-aware pause/resume workflow even if the repo is rough | **Pattern worth extracting** | whether the pattern becomes OpenClaw-native, queueing/resume robustness |
| `XingP14/clawlink` | Coordination / multi-agent adjacent | Potentially relevant for multi-agent coordination, but current signal is still mostly docs/roadmap level | **Watchlist** | real implementation depth, behavior changes, interop usefulness |

### Table maintenance rule
For each crawl:
- add new item only if it is genuinely useful or structurally important
- update `Current status` when conviction changes
- remove stale entries when they no longer matter
- prefer fewer, better rows over a long catalog

---

## Repo layout

```text
OpenClaw_research/
├── README.md
├── SKILL.md
├── profiles/
│   └── openclaw-agents.json
├── references/
│   ├── AGENT_PROMPT.md
│   ├── CRAWL_PLAN.md
│   ├── FOCUS.md
│   ├── SELENIUM_FALLBACK.md
│   └── sources.json
└── research/
    └── openclaw-agents/
        └── YYYY-MM-DD-<slug>.md
```

---

## Output contract for each research note

Each crawl should create one markdown note at:

`research/<profile-or-domain>/YYYY-MM-DD-<slug>.md`

Recommended note structure:

```md
# Title

## Scope
- Domain:
- Intent:
- Time window:
- Research date:

## Executive summary
3-8 bullets.

## Key findings
### 1. <item>
- What happened
- Why it matters
- Evidence
- Link

## Practical takeaways
- Tactic 1
- Tactic 2
- Tactic 3

## Implications for OpenClaw
- Prompt changes
- Workflow changes
- What to test
- What to watch

## Follow-up actions
- [ ] Add source to database
- [ ] Create experiment note
- [ ] Compare with previous item
```

---

## README maintenance contract

Every crawl should also decide whether README needs a small refresh.

### Update README when one of these is true
- a new repo/variant is worth adding to the watch table
- a prior watch item changed status materially
- a new operator pattern is important enough to preserve on the front page
- core OpenClaw changes alter the current landscape summary

### Typical README edits per crawl
- update `Latest update`
- refresh `Important rolling notes`
- add/remove/update rows in the watch table

### Keep edits small
README should remain:
- readable in under 3 minutes
- useful as a front page
- curated rather than exhaustive

---

## Research principles

- **Signal over noise**: reject generic hype and thin rewrites
- **Primary-source first**: official docs, repos, release notes, issues, PRs, engineering posts
- **Practical bias**: code, workflows, measurable outcomes, failure modes, deployment lessons
- **Pattern extraction**: pull out reusable tactics, not just headlines
- **Living archive**: every run leaves behind a dated note and can also update the front-page memory
- **Browser fallback only when needed**: prefer static fetch/search first, escalate only for blocked or JS-heavy sources

---

## Browser fallback

If a source is JS-rendered, paginated, or blocks static extraction:

1. Try normal search/fetch first.
2. Escalate to browser automation only if needed.
3. Prefer deterministic extraction.
4. Record when browser fallback was required.

See `references/SELENIUM_FALLBACK.md`.

---

## Current environment note

This repo supports Selenium/browser-assisted collection in principle, but actual execution depends on local runtime availability of browser tooling such as:
- Python Selenium package
- Chrome/Chromium
- ChromeDriver
- or an installed browser automation CLI

If those dependencies are missing, keep browser fallback documented and treat it as optional rather than blocking the rest of the research run.
