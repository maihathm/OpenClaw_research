# OpenClaw Research Base

A lightweight research workflow for OpenClaw to continuously track AI developments in one chosen domain, or collect practical blog posts / field tips with high signal.

## Goal

This repository is the working memory for OpenClaw research tasks.

It is designed for two recurring modes:

1. **Domain tracking**
   - Continuously update research on a specific AI domain
   - Example domains:
     - coding agents
     - AI security
     - multimodal evaluation
     - synthetic data
     - inference optimization
     - browser-use agents
     - long-context systems

2. **Tips / posts / blogs tracking**
   - Find practical posts, blogs, engineering notes, launch writeups, and implementation tips
   - Prefer concrete tactics, failure modes, benchmarks, architecture notes, and deployment lessons

---

## What counts as a good research item

A research item is valuable if it contains at least one of:

- a new model / framework / product / release
- a concrete architecture or workflow
- a benchmark or measurable result
- a practical implementation trick
- a failure mode or security lesson
- a comparison between tools / models / methods
- a deployment or operations insight
- code, config, or reproducible steps

Low-value items:

- generic hype
- vague AI trend summaries
- reposted news with no new detail
- SEO articles with no technical substance

---

## Research modes

### Mode A — Domain update

Use this mode when the user says things like:

- update research on AI coding agents
- find the latest work in browser-use agents
- summarize recent changes in agent security
- collect new launches in retrieval and RAG evals

Expected output:
- a dated summary
- a list of key items
- source links
- short takeaways
- what matters for OpenClaw
- suggested follow-up experiments or repo tasks

### Mode B — Tips / blogs / practical posts

Use this mode when the user says things like:

- find good blog posts with tips for agent prompting
- collect practical engineering posts on inference optimization
- gather field notes about sandboxing agents
- find implementation tricks for eval pipelines

Expected output:
- a curated list of posts
- 1–3 bullet takeaways per post
- “why this matters”
- whether the post is tactical, strategic, benchmark-focused, or operational

---

## Inputs

Every research run should start with the following fields:

- **domain**: the AI domain to track
- **intent**: `domain-update` or `tips-hunt`
- **time window**: e.g. last 7 days / 30 days / quarter
- **source preference**:
  - official docs
  - company engineering blogs
  - GitHub repos / release notes
  - research papers
  - practitioner blogs
  - social summaries only if they link to primary sources
- **depth**:
  - quick scan
  - normal
  - deep dive
- **output target**:
  - note
  - summary
  - weekly digest
  - source database update
  - experiment proposal

---

## Output format

Each run should create a markdown file in:

`research/<domain>/YYYY-MM-DD-<slug>.md`

Recommended structure:

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

### 2. <item>
- What happened
- Why it matters
- Evidence
- Link

## Practical takeaways
- Tactic 1
- Tactic 2
- Tactic 3

## Implications for OpenClaw
- What should be added to prompts
- What should be added to workflows
- What should be tested
- What should be watched

## Follow-up actions
- [ ] Add source to database
- [ ] Create experiment note
- [ ] Compare with previous item
- [ ] Write implementation draft