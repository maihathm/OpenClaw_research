# OpenClaw Research Base

A living research repo for OpenClaw to continuously track one AI domain, collect high-signal practical posts, and turn raw updates into reusable notes.

## What this repo is for

This repo is the working memory for recurring research tasks such as:

1. **Domain tracking**
   - track a narrow AI domain over time
   - examples: coding agents, browser-use agents, AI security, evals, inference optimization, long-context systems

2. **Tips / blog / field-note hunting**
   - collect practical posts with implementation details
   - prefer engineering notes, release writeups, benchmark breakdowns, architecture decisions, operational lessons, and failure modes

## Design principles

- **Signal over noise**: ignore generic hype and SEO sludge
- **Primary-source first**: official docs, repos, release notes, engineering blogs, papers
- **Practical bias**: focus on tactics, measurable results, benchmarks, code, workflows, and lessons learned
- **Living archive**: every run should leave behind a dated note that can be reviewed later
- **Browser fallback when needed**: prefer normal fetch/search first; escalate to browser automation only when a source is JS-heavy or blocks static extraction

## Default workflow

This repo now ships with:

- `SKILL.md` — reusable research skill for domain updates and tips hunts
- `profiles/openclaw-agents.json` — default profile for OpenClaw / agent-tooling research
- `references/AGENT_PROMPT.md` — reusable prompt templates
- `references/CRAWL_PLAN.md` — source priority, cadence, and run design
- `references/sources.json` — machine-readable source and query list
- `references/SELENIUM_FALLBACK.md` — when and how to use browser automation

## Recommended output layout

```text
OpenClaw_research/
├── README.md
├── SKILL.md
├── profiles/
│   └── openclaw-agents.json
├── references/
│   ├── AGENT_PROMPT.md
│   ├── CRAWL_PLAN.md
│   ├── SELENIUM_FALLBACK.md
│   └── sources.json
└── research/
    └── openclaw-agents/
        └── YYYY-MM-DD-<slug>.md
```

## Output contract

Each research run should create a markdown file at:

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
3–8 bullets.

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

## Default profile

The default profile bundled here is:

- **`openclaw-agents`**
  - OpenClaw ecosystem
  - agent tooling
  - browser automation for agents
  - evals / guardrails / ops
  - practical engineering posts and implementation tips

You can add more profiles later for other domains.

## Cadence suggestion

A good default daily rhythm is:

- **12:00 Asia/Saigon** — quick scan for fresh launches, releases, posts, and urgent updates
- **23:00 Asia/Saigon** — broader end-of-day digest with takeaways and follow-up actions

## Browser fallback

If a source is JS-rendered, paginated, or blocks static extraction:

1. Try normal search/fetch first
2. Escalate to browser automation only if needed
3. Prefer deterministic extraction
4. Record when browser fallback was required

See `references/SELENIUM_FALLBACK.md`.

## Current environment note

This repo supports Selenium/browser-assisted collection in principle, but actual execution depends on local runtime availability of browser tooling such as:

- Python Selenium package
- Chrome/Chromium
- ChromeDriver
- or an installed browser automation CLI

If those dependencies are missing, keep the browser fallback documented and treat it as optional rather than blocking the rest of the research run.
