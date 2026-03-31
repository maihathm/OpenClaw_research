---
name: ai-research-base
description: >
  Automated domain-specific AI research and practical tips/blog hunting workflow
  for OpenClaw. Use when the user asks to continuously track one AI domain,
  collect practical blog posts or engineering notes, build a living research
  repo, generate daily or weekly digests, update a research knowledge base, or
  monitor launches, benchmarks, repos, release notes, security lessons, evals,
  browser-use tools, coding agents, OpenClaw-related tooling, new repo variants,
  forks, or new usage patterns. Also use when a source requires browser
  automation fallback after normal search/fetch is insufficient.
---

# AI Research Base Skill

## Purpose

Run a repeatable research workflow that turns scattered AI updates into dated,
structured notes with source links, short analysis, and follow-up actions.

The default OpenClaw profile should behave like an ecosystem radar focused on:
- new repos
- meaningful forks or technical variants
- new ways to use tools in practice
- release / docs / issue changes that alter operator behavior

## Quick Start

1. Read `profiles/openclaw-agents.json`.
2. Read `references/CRAWL_PLAN.md`.
3. Read `references/FOCUS.md` when you need the exact radar surface.
4. Use `references/AGENT_PROMPT.md` when you need a reusable prompt shell.
5. Save every run to `research/<profile-or-domain>/YYYY-MM-DD-<slug>.md`.

## Core Workflow

### 1. Define scope

Capture these inputs before searching:
- domain
- intent: `domain-update`, `tips-hunt`, `repo-radar`, or `usage-radar`
- time window
- depth: quick scan / normal / deep dive
- output target: note / digest / experiment proposal / workflow update

### 2. Search in source order

Prefer this order unless the task says otherwise:
1. official docs and release notes
2. GitHub repos, changelogs, issues, PRs, and discussions
3. company engineering blogs
4. research papers and benchmarks
5. practitioner blogs with concrete evidence
6. social discovery only if it points to stronger sources

### 3. Filter hard

Keep items only if they contain at least one of:
- a new repo or variant
- a release or architecture change
- a concrete workflow or implementation trick
- a benchmark or measurable result
- a practical debugging or deployment lesson
- a failure mode, security lesson, or operational insight
- code, config, or reproducible steps

Reject:
- generic hype
- thin rewrites of primary sources
- vague trend posts
- SEO content with no technical substance

### 4. Write durable notes

For each accepted item, record:
- what happened
- why it matters
- the evidence/source
- practical takeaway
- implication for OpenClaw or the tracked domain

Also review `README.md` after each run and make a small front-page refresh when warranted.

Refresh these sections when the signal justifies it:
- `Latest update`
- `Important rolling notes`
- `OpenClaw variants / useful repos watch table`

Use README only for durable, front-page signal. Keep transient detail in the dated research note.

### 5. Compare with prior runs

Avoid repeating unchanged items unless there is a real new angle:
- new release
- benchmark update
- deployment lesson
- repo movement
- newly discovered code or docs
- a new usage pattern worth trying

## Browser Automation Fallback

Only escalate to browser automation when normal fetch/search is insufficient.

Use browser fallback for:
- JS-heavy pages hiding the real content
- infinite scroll or delayed rendering
- pages where meaningful text only appears after interaction
- docs sites that require UI navigation to reveal the real details

Rules:
1. Prefer static fetch first.
2. If browser automation is required, use a deterministic workflow.
3. Record that browser fallback was needed.
4. If Selenium/browser tooling is unavailable locally, note the limitation and continue with reachable sources.
5. Do not let browser fallback block the entire research run.

See `references/SELENIUM_FALLBACK.md`.

## Output Format

Create one markdown note per run:

```md
# <Run title>

## Scope
- Domain:
- Intent:
- Time window:
- Research date:

## Executive summary
- ...

## Key findings
### 1. <item>
- What happened
- Why it matters
- Evidence
- Link

## Practical takeaways
- ...

## Implications for OpenClaw
- ...

## Follow-up actions
- [ ] ...
```
