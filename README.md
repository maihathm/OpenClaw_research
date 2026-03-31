# OpenClaw Research

> Daily intelligence on the OpenClaw ecosystem — variants, patterns, operator lessons.

---

`Status: Active` · `Last scan: 2026-03-31 12:03 Asia/Saigon` · `Coverage: core + 7 tracked items`

## Current thesis

> The strongest signal still comes from **OpenClaw core behavior changes** and a small set of **practical operator variants**.
> Generic agent-framework noise matters less than routing, cron, execution, fallback, and orchestration patterns that change real usage.

---

## Top 3 signals

`#1` **OpenClaw core commits remain the highest-priority surface** — routing, cron, isolated execution, and security changes can alter workflow assumptions immediately.

`#2` **Operator-facing variants are where the best external signal is** — voice bridges, model/persona switching, regional search fallback, and rate-limit-aware orchestration are more actionable than broad launch hype.

`#3` **New repos should stay on watchlist first** — promote only when they show reproducibility, docs depth, or clear operator value.

---

## Variant watchlist

### Core signals
- [ ] `openclaw/openclaw` — watch for behavior-changing commits, release notes, routing semantics, and security defaults
- [ ] `TotzkePaul/OpenClawDiscordVC` — watch reliability, setup friction, and media decryption edge cases
- [ ] `frankekn/openclaw-model-switcher` — watch safe file swap/restore behavior and real profile usage

### Experimental
- [ ] `akhilc08/mission-control` — strong pause-resume idea, but still rough
- [ ] `z-imagine/openclaw-baidu-search` — useful fallback pattern, still early
- [ ] `Aston1690/vercel-sandbox` — interesting hosted browser wrapper, needs stronger production evidence
- [ ] `XingP14/clawlink` — adjacent coordination signal, still more watchlist than proven workflow value

---

## Confirmed operator lessons

- Tool-call, routing, and scheduler behavior changes in core OpenClaw deserve front-row attention.
- Practical operator patterns matter more than framework churn.
- The most reusable takeaway is usually the **pattern** behind a repo, not the repo itself.
- Watchlist status should be the default for new repos until they earn promotion.

---

## Useful repos

| Repo | Purpose | Current read |
|---|---|---|
| `openclaw/openclaw` | Core upstream | Top priority |
| `TotzkePaul/OpenClawDiscordVC` | OpenClaw-shaped voice integration | Hot / practical |
| `frankekn/openclaw-model-switcher` | Persona/bootstrap switching by model | Useful pattern |
| `akhilc08/mission-control` | Rate-limit-aware orchestration pattern | Worth extracting |
| `z-imagine/openclaw-baidu-search` | Regional search fallback plugin | Useful but early |
| `Aston1690/vercel-sandbox` | Hosted browser execution wrapper | Interesting |
| `XingP14/clawlink` | Multi-agent adjacent coordination signal | Watchlist |

---

## Latest scan

- `research/openclaw-agents/2026-03-31-midday-scan.md`

## Archive

Recent notes live under:
- `research/openclaw-agents/`

---

<details>
<summary>Workflow / maintenance / meta</summary>

### What this repo tracks
- OpenClaw core behavior changes
- OpenClaw-adjacent repos, plugins, and wrappers
- browser / automation / tooling patterns useful for agents
- deployment, debugging, rate-limit, and orchestration lessons
- durable patterns worth preserving beyond one daily scan

### Why this repo exists
Most agent-news streams are noisy.
This repo is meant to answer a narrower question:

> What changed in the OpenClaw / agent-tooling ecosystem that is actually worth an operator's attention?

### What gets updated after each crawl
Each crawl should do two things:
1. write a dated note under `research/openclaw-agents/YYYY-MM-DD-<slug>.md`
2. refresh the front page lightly when there is durable signal worth surfacing

### Stable vs dynamic README sections
**Dynamic — refresh after midday crawl**
- status strip
- current thesis
- top 3 signals
- variant watchlist
- latest scan

**Stable — update only when needed**
- confirmed operator lessons
- useful repos
- archive/meta/workflow notes

### Quick links
- `profiles/openclaw-agents.json`
- `references/SKILL.md`
- `references/CRAWL_PLAN.md`
- `references/AGENT_PROMPT.md`
- `references/FOCUS.md`
- `references/SELENIUM_FALLBACK.md`

### Repo map
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

### Browser fallback
If a source is JS-rendered, paginated, or blocks static extraction:
1. Try normal search/fetch first.
2. Escalate to browser automation only if needed.
3. Prefer deterministic extraction.
4. Record when browser fallback was required.

### Environment note
This repo supports Selenium/browser-assisted collection in principle, but actual execution depends on local availability of browser tooling such as Python Selenium, Chrome/Chromium, ChromeDriver, or an installed browser automation CLI.

</details>
