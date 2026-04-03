# OpenClaw Research

> Daily intelligence on the OpenClaw ecosystem — variants, patterns, operator lessons.

---

`Status: Active` · `Last scan: 2026-04-03 12:01 Asia/Saigon` · `Coverage: core + 11 tracked items`

## Current thesis

> The strongest signal is again **upstream OpenClaw behavior change**, but the more durable secondary signal is now **small, inspectable operational components** rather than broad agent wrappers.
> Config-surface moves, task/scheduler semantics, privacy-at-the-edge plugins, lightweight routing skills, and more operable cross-agent runtime layers matter more than generic launch noise.

---

## Top 3 signals

`#1` **OpenClaw `v2026.4.2` is a real operator release** — config ownership moved for `x_search` and Firecrawl-backed `web_fetch`, Task Flow was restored as a more durable substrate, and host exec defaults shifted in a more aggressive direction.

`#2` **Fresh upstream issues already make `v2026.4.2` worth watching carefully** — one report flags duplicate cron startup catch-up runs, another reports lost async tool results in replies.

`#3` **The best ecosystem signal is now concrete packaging, not generic agent launches** — `woclaw` added a more usable CLI/dashboard layer, while `data-guard` and `models-triage` package privacy and routing as small OpenClaw-ready components.

---

## Variant watchlist

### Core signals
- [ ] `openclaw/openclaw` — watch for behavior-changing releases, routing semantics, `/tasks` evolution, search/provider changes, and approval/task-control fixes
- [ ] `TotzkePaul/OpenClawDiscordVC` — watch reliability, setup friction, and media decryption edge cases
- [ ] `frankekn/openclaw-model-switcher` — watch safe file swap/restore behavior and real profile usage
- [ ] `vercel-labs/agent-browser` — watch daemon reliability, provider compatibility, and practical fallback fit for OpenClaw browser workflows

### Experimental
- [ ] `akhilc08/mission-control` — strong pause-resume idea, but still rough
- [ ] `z-imagine/openclaw-baidu-search` — useful fallback pattern, still early
- [ ] `Aston1690/vercel-sandbox` — interesting hosted browser wrapper, needs stronger production evidence
- [ ] `XingP14/woclaw` — increasingly interesting now that it has CLI/dashboard ergonomics in addition to multi-runtime packaging, but still needs stronger operator proof
- [ ] `AliNek09/openclaw-google-trends` — thin skill repo; watch whether it develops beyond a one-off packaged data source
- [ ] `sealofyou/hackathon-copilot` — skill-suite + CLI bridge pattern; still useful, but no fresh midday movement
- [ ] `AlanSong2077/openclaw-plugins-data-guard` — promising privacy-at-the-edge plugin; watch for real install reports and maintainability
- [ ] `xaspx/models-triage` — lightweight routing-skill pattern; watch whether it becomes reusable cost-control infrastructure

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

- `research/openclaw-agents/2026-04-03-midday-scan.md`

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
