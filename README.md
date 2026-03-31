# OpenClaw Research Base

> Curated signal for the **OpenClaw ecosystem**: core changes, useful variants, operator workflows, and practical implementation patterns.

<p align="center">
  <b>Hot updates first.</b> • <b>Operator value over hype.</b> • <b>Curated, not exhaustive.</b>
</p>

---

> [!IMPORTANT]
> **Current thesis:** the strongest signal still comes from **OpenClaw core behavior changes + practical operator variants**, not generic agent-framework noise.

## Hot right now

- **Highest-priority source:** `openclaw/openclaw` core commits affecting routing, cron, isolated execution, or security behavior.
- **Most actionable patterns:** voice bridges, model/persona switching, regional search fallback, and rate-limit-aware orchestration.
- **Current filter rule:** new repos stay on **watchlist** until they show reproducibility, docs depth, or clear operator value.

---

## Top things to know

### 1. Core OpenClaw changes matter more than ecosystem chatter
If upstream changes routing, cron, session flow, or security defaults, it can change real workflow assumptions immediately.

### 2. Small practical variants are often more useful than big “new framework” launches
The best external signal lately has come from operator-facing ideas: wrappers, fallbacks, orchestration tricks, and integrations.

### 3. This repo is a curated radar, not a news dump
The goal is not completeness. The goal is to stay **decision-useful**.

---

## Hot variants / useful repos

| Project / Variant | Why it matters | Status |
|---|---|---|
| `openclaw/openclaw` | Primary source for behavior-changing commits and safe-default changes | **Top priority** |
| `TotzkePaul/OpenClawDiscordVC` | Concrete OpenClaw-shaped Discord voice pipeline with practical debug detail | **Hot / practical** |
| `frankekn/openclaw-model-switcher` | Model switching as persona/bootstrap/workspace switching | **Useful pattern** |
| `akhilc08/mission-control` | Strong pause-resume pattern for rate-limit-aware agent workflows | **Worth extracting** |
| `z-imagine/openclaw-baidu-search` | Regional search plugin with API + scraper fallback design | **Useful but early** |
| `Aston1690/vercel-sandbox` | Hosted browser execution wrapper using Vercel microVM flow | **Interesting** |
| `XingP14/clawlink` | Multi-agent adjacent, but still more watchlist than proven workflow value | **Watchlist** |

### Confidence guide
- **Top priority** = monitor closely
- **Hot / practical** = directly worth trying or learning from
- **Useful pattern** = the idea matters even if the repo is early
- **Watchlist** = interesting, but not yet promoted

---

## Latest scan

- **Latest note:** `research/openclaw-agents/2026-03-31-midday-scan.md`
- **Last front-page refresh:** 2026-03-31
- **Best next click:** open the latest scan note, then return here for the short watchlist view.

---

## Important rolling notes

### OpenClaw core commit flow deserves front-row attention
Recent changes around Telegram routing, cron isolated retry behavior, detached execution, and SSRF hardening had direct operator impact.

### Practical operator patterns matter more than framework churn
The best recent external signal has come from operator-facing patterns such as model-aware switching, fallback plugins, hosted browser wrappers, and voice bridges.

### New repos should earn promotion
A repo being new is not enough. It should show reproducibility, docs depth, practical value, or a reusable pattern before moving beyond watchlist status.

### Extract patterns, not just headlines
The most reusable takeaway is often the underlying pattern: fallback design, resume logic, routing/session handling, packaging strategy, or workflow improvement.

---

## What this repo tracks

This repo focuses on:
- OpenClaw core behavior changes
- OpenClaw-adjacent repos, plugins, and wrappers
- browser / automation / tooling patterns useful for agents
- deployment, debugging, rate-limit, and orchestration lessons
- durable patterns worth preserving beyond one daily scan

---

## Why this repo exists

Most agent-news streams are noisy.
This repo is meant to answer a narrower question:

> **What changed in the OpenClaw / agent-tooling ecosystem that is actually worth an operator's attention?**

That means prioritizing:
- behavior-changing core updates
- useful variants / plugins
- practical workflows worth copying
- deployment / debugging / orchestration lessons
- durable patterns, not just headlines

---

## Quick links

- **Profile:** `profiles/openclaw-agents.json`
- **Workflow guide:** `references/SKILL.md`
- **Crawl plan:** `references/CRAWL_PLAN.md`
- **Prompt template:** `references/AGENT_PROMPT.md`
- **Focus surface:** `references/FOCUS.md`

---

## What gets updated after each crawl

Each crawl should do two things:

### 1. Write a dated research note
Save a note under:
- `research/openclaw-agents/YYYY-MM-DD-<slug>.md`

### 2. Refresh the front page lightly
Update this README when there is durable front-page signal, especially:
- a new repo / variant worth adding
- a meaningful status change for an existing watch item
- an operator takeaway worth preserving
- a core OpenClaw change that alters the short landscape summary

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
