# OpenClaw Research Crawl Plan

## Objective

Maintain a living, high-signal research archive for OpenClaw-adjacent agent tooling.

The daily workflow should emphasize three things:
- **new repos** worth knowing about
- **new variants / forks / technical branches** that materially differ
- **new ways of using tools**: practical workflows, implementation tricks, debugging notes, and deployment patterns

## Daily Cadence

### Midday run — ecosystem radar
Purpose:
- catch fresh launches, releases, repo movement, new variants, and high-velocity implementation posts
- produce a concise alert-style digest

Suggested scope:
- last 18 hours
- 3-6 strongest new items
- prioritize real newness over completeness

### Night run — usage and implication digest
Purpose:
- produce a broader end-of-day digest
- include what changed, why it matters, and how it changes usage or operating practice

Suggested scope:
- last 12-24 hours depending on signal density
- 4-8 items max
- include at least some operator-facing takeaways when available

## Source Priority

### Tier 1 — Primary / highest signal
- official OpenClaw docs and GitHub
- release notes and changelogs
- issues / PRs / discussions with behavioral impact
- official repos for adjacent tools (browser automation, evals, agent runtimes)

### Tier 2 — High-value secondary
- company engineering blogs
- benchmark writeups
- implementation repos
- technical issue threads with concrete evidence

### Tier 3 — Practical field notes
- practitioner blogs
- high-quality tutorials
- migration notes
- debugging or deployment writeups

## What to keep

Keep an item if it contains one or more of:
- a genuinely new repo
- a meaningful new variant or fork
- a release / changelog / architecture change
- a practical workflow improvement
- a reproducible implementation tip
- a bug or failure mode that changes how operators should use the tool
- a new docs pattern or tutorial with real tactical value

Reject:
- generic AI news
- thin summaries of launch posts
- hype without technical substance
- unchanged projects being re-mentioned without a new angle

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

Each run should also review `README.md` and make a small front-page refresh when warranted.

Update `README.md` when there is:
- a new repo or variant worth adding to the watch table
- a meaningful status change for an existing watch item
- a durable operator takeaway worth preserving in `Important rolling notes`
- a core OpenClaw change that materially changes the short landscape summary

Keep README edits curated and small. Use README for durable signal, not for dumping all daily findings.

## Browser Fallback Policy

Escalate to Selenium or another browser automation method only when:
- meaningful content is hidden behind JS rendering
- interaction is required to expose details
- normal fetch/search misses the important text

If browser tooling is missing locally, note the limitation and continue with accessible sources.
