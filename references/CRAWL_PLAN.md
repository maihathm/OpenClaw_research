# OpenClaw Research Crawl Plan

## Objective

Maintain a living, high-signal research archive for one AI domain at a time,
with a default focus on OpenClaw-adjacent agent tooling and practical field
notes.

## Default Cadence

### Midday run — 12:00 Asia/Saigon
Purpose:
- catch fresh launches, releases, changelog updates, and high-velocity posts
- produce a concise alert-style digest

Suggested scope:
- last 18 hours
- 3-6 strongest new items
- emphasize what changed since the prior run

### Night run — 23:00 Asia/Saigon
Purpose:
- broader end-of-day digest
- include practical takeaways, implications, and follow-up actions

Suggested scope:
- last 12-24 hours, depending on signal density
- 4-8 items max
- favor completeness over speed, but keep it concise

## Source Priority

### Tier 1 — Primary / highest signal
- official docs
- GitHub repos
- release notes
- changelogs
- vendor or project engineering blogs

### Tier 2 — High-value secondary
- benchmark writeups
- research papers
- implementation repos related to the topic
- technical issue threads with concrete evidence

### Tier 3 — Curated practitioner sources
- strong independent engineering blogs
- detailed postmortems
- field notes from reputable builders

### Tier 4 — Social discovery only
Use only to discover links to stronger sources. Do not treat social summaries as final evidence unless they point to primary materials.

## Item Selection Rules

Keep an item if it has one or more of:
- measurable benchmark or result
- concrete system design or workflow
- implementation trick or failure mode
- code or config detail
- release / version / changelog movement
- deployment, eval, or security lesson

Reject:
- generic AI trend summaries
- recycled launch posts with no new facts
- listicles with no technical detail
- vague opinion pieces

## Deduping Rules

Do not repeat yesterday's story unless there is a true update:
- new version
- new benchmark
- new docs or implementation detail
- new code repo or commit activity
- new failure mode or correction

## Repo Update Rules

Each run should leave behind a dated markdown note under:

`research/<profile-or-domain>/YYYY-MM-DD-<slug>.md`

Each note should include:
- scope
- executive summary
- key findings with links
- practical takeaways
- implications for OpenClaw
- follow-up actions

## Browser Fallback Policy

Escalate to Selenium or another browser automation method only when:
- content is hidden behind JS rendering
- interaction is required to expose meaningful content
- normal fetch/search misses critical text

If browser tooling is missing locally, document the limitation and continue the run with accessible sources.
