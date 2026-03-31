# OpenClaw Research Base

> A curated, high-signal research hub for the **OpenClaw ecosystem**, adjacent agent tooling, practical operator workflows, and meaningful implementation variants.

<p align="center">
  <b>Track what changed.</b> • <b>Keep what matters.</b> • <b>Ignore the hype.</b>
</p>

---

## Why this repo exists

Most agent-news streams are noisy.
This repo is meant to answer a narrower, more useful question:

> **What changed in the OpenClaw / agent-tooling ecosystem that is actually worth an operator's attention?**

This means prioritizing:
- **behavior-changing core updates**
- **useful new repos / variants / plugins**
- **practical workflows worth copying**
- **deployment / debugging / orchestration lessons**
- **durable patterns**, not just headlines

---

## Snapshot

> [!IMPORTANT]
> **Current thesis:** the strongest signal is still coming from **OpenClaw core changes + practical operator variants**, not from generic “new agent framework” noise.

### What is hot right now

- **OpenClaw core commits** are still the highest-priority source when they affect routing, cron, isolated execution, or security behavior.
- **Voice bridges, model/persona switching, regional search fallback, and rate-limit-aware orchestration** are currently more actionable than broad launch hype.
- **New repos should stay on watchlist status first** until they prove setup depth, reproducibility, or operator value.

### Fastest way to understand this repo

1. Read **this README** for the front-page view.
2. Check the **hot variants table** below.
3. Open the **latest dated scan note**.
4. Dive into `references/` only if you want the workflow details.

---

## Quick links

- **Latest scan:** `research/openclaw-agents/2026-03-31-midday-scan.md`
- **Profile:** `profiles/openclaw-agents.json`
- **Workflow guide:** `references/SKILL.md`
- **Crawl plan:** `references/CRAWL_PLAN.md`
- **Prompt template:** `references/AGENT_PROMPT.md`
- **Focus surface:** `references/FOCUS.md`

---

## What to look at first

### If you are a reader
Start here:
- **Snapshot**
- **Why this matters now**
- **Hot variants / useful repos**
- **Latest scan**

### If you are maintaining the repo
Start here:
- `references/SKILL.md`
- `references/CRAWL_PLAN.md`
- `references/AGENT_PROMPT.md`

---

## Why this matters now

> [!TIP]
> The best signal in this space is often **not** a giant new framework.
> It is usually a smaller, more transferable pattern:
> a routing fix, a safer fallback, a better orchestration trick, a deployable wrapper, or a tool-usage pattern that clearly improves operator workflow.

### Current high-value patterns

- **Core runtime / routing / cron behavior changes**
- **Model-aware persona or bootstrap switching**
- **Search fallback patterns for constrained regions/providers**
- **Hosted browser execution wrappers**
- **Pause / resume patterns for usage- or rate-limit-aware agent work**
- **Voice integrations shaped around OpenClaw workflows**

---

## Hot variants / useful repos

> [!NOTE]
> This table is intentionally curated. Fewer rows, higher signal.

| Project / Variant | Type | Highlight | Status | What to watch |
|---|---|---|---|---|
| `openclaw/openclaw` | Core upstream | The main source of behavior-changing commits: routing, cron/session/runtime flow, security hardening | **Top priority** | release notes, execution model changes, routing semantics, security defaults |
| `TotzkePaul/OpenClawDiscordVC` | Voice integration | Concrete OpenClaw-shaped Discord voice pipeline with useful debugging detail | **Hot / practical** | reliability, setup friction, media decryption edge cases, voice quality |
| `frankekn/openclaw-model-switcher` | Plugin / workflow variant | Treats model switching as persona/bootstrap/workspace switching | **Useful pattern** | safe file swap/restore behavior, real profile usage |
| `akhilc08/mission-control` | Ops / orchestration pattern | Rough repo, but a strong pause-resume pattern for rate-limit-aware agent workflows | **Worth extracting** | whether the pattern becomes cleaner and more OpenClaw-native |
| `z-imagine/openclaw-baidu-search` | Search plugin | Regional search coverage with API + scraper fallback pattern | **Useful but early** | install stability, anti-bot robustness, query quality |
| `Aston1690/vercel-sandbox` | Deployment wrapper | Packs `agent-browser` + Chrome into a Vercel microVM flow | **Interesting** | production caveats, latency/cost tradeoffs |
| `XingP14/clawlink` | Coordination / multi-agent adjacent | Potentially relevant, but current signal is still more roadmap/docs than proven operator value | **Watchlist** | implementation depth, interop usefulness, behavior-changing updates |

### How to read the table

- **Top priority** = monitor closely; likely to affect workflow assumptions.
- **Hot / practical** = directly interesting for near-term usage or experimentation.
- **Useful pattern** = maybe not mature, but the underlying idea is reusable.
- **Watchlist** = worth tracking, but not yet strong enough to promote.

---

## Important rolling notes

> [!IMPORTANT]
> Keep this section short, durable, and opinionated.

### 1. OpenClaw core commit flow deserves front-row attention
Recent changes around Telegram routing, cron isolated retry behavior, detached execution, and SSRF hardening had direct operator impact.

**Why this matters:**
- routing changes can affect message continuity and delivery semantics
- cron / isolated execution changes can alter scheduled workflow behavior
- security hardening changes may affect network behavior and safe defaults

### 2. Practical operator patterns matter more than framework churn
The best recent external signal has come from operator-facing patterns, not generic “agent ecosystem” noise.

Examples:
- model-aware persona switching
- regional search fallback
- hosted browser wrappers
- rate-limit-aware orchestration
- OpenClaw-shaped voice bridges

### 3. New repos should earn promotion
A repo being new is not enough.

Promote it only when there is evidence of:
- real docs depth
- reproducible setup
- concrete operator value
- meaningful updates over time
- a pattern that transfers beyond one demo

### 4. Extract patterns, not just headlines
For many repos, the most valuable takeaway is the reusable idea behind them:
- fallback design
- resume logic
- routing/session handling
- packaging strategy
- operator-facing workflow improvements

---

## What gets updated after each crawl

Each crawl should do two things:

### 1. Write a dated research note
Save a note under:
- `research/openclaw-agents/YYYY-MM-DD-<slug>.md`

### 2. Refresh the front page lightly
Update this README only when there is durable front-page signal, especially:
- a new repo / variant worth adding
- a meaningful status change for an existing watch item
- an operator takeaway worth preserving
- a core OpenClaw change that changes the short landscape summary

> [!WARNING]
> Do **not** turn the README into a dump of daily findings.
> Put transient detail in the dated note.
> Keep the front page curated.

---

## Repo map

```text
OpenClaw_research/
├── README.md
├── profiles/
│   └── openclaw-agents.json
├── references/
│   ├── SKILL.md
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

## Reader-first design rules for this README

This front page should help a first-time GitHub visitor answer four questions fast:

1. **What is this repo tracking?**
2. **Why should I care?**
3. **What is hot right now?**
4. **Where should I click next?**

If a section does not help answer one of those, it should move lower or be shortened.

---

## Research principles

- **Signal over noise**
- **Primary-source first**
- **Practical bias**
- **Pattern extraction over hype**
- **Living archive with front-page memory**
- **Browser fallback only when needed**

---

## Browser fallback

If a source is JS-rendered, paginated, or blocks static extraction:

1. Try normal search/fetch first.
2. Escalate to browser automation only if needed.
3. Prefer deterministic extraction.
4. Record when browser fallback was required.

See `references/SELENIUM_FALLBACK.md`.

---

## Environment note

This repo supports Selenium/browser-assisted collection in principle, but actual execution depends on local availability of browser tooling such as:
- Python Selenium package
- Chrome/Chromium
- ChromeDriver
- or an installed browser automation CLI

If those dependencies are missing, keep browser fallback documented and treat it as optional rather than blocking the rest of the research run.
