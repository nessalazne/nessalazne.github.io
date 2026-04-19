---
layout: post
title: "How to Use Claude Code Routines to Automate Your Workflows"
author: nessa
categories: [Claude Code, AI Automation, Vibe Coding]
image: assets/images/claude-code-routines-header.jpg
featured: false
---

Most people use Claude Code for one-off tasks — ask a question, get an answer, close the tab. Claude Code Routines are something completely different. They're always-on, trigger-based workflows that run automatically, read context from your repos and tools, and take action without you having to start a session.

If you've ever wanted to automate bug triage, code reviews, or deploy verification without writing a custom script — this is how you do it.

{% include youtube-short.html id="tjGxhwjYaXk" %}

---

## What Are Claude Code Routines?

A Claude Code Routine is a saved prompt + trigger combination that Claude executes automatically. You write the prompt once — describing what to check, what counts as important, and what to do about it — and Claude handles the rest on the schedule or trigger you set.

Unlike a regular automation tool (n8n, Zapier, cron), a routine doesn't just run fixed steps. It **reads context and reasons about what it finds**. That's the key difference. A cron job runs the same command every night. A routine reads your issues, understands what just happened in your codebase, decides what's worth flagging, and posts a meaningful summary to Slack.

Routines are available on **Pro, Max, Team, and Enterprise** plans. Get started at [claude.ai/code/routines](https://claude.ai/code/routines).

> **Note:** If you were using `/schedule` tasks before — those have been automatically converted to routines. No migration needed.

---

## The 3 Trigger Types

Every routine needs at least one trigger. You can combine multiple triggers on the same routine — the same prompt, multiple entry points.

### Trigger 1: Scheduled

Set a cadence — hourly, nightly, weekly — and Claude runs your prompt on that schedule automatically. This is best for recurring tasks that need to happen even when you're not at your desk.

**Example use cases:**
- Nightly bug triage — read new issues, label by code area, assign owners, post a Slack summary
- Weekly docs drift check — scan merged PRs and flag any documentation that references old behavior
- Monday morning PR cleanup — find stale PRs and notify authors

### Trigger 2: API

Every routine gets its own HTTP endpoint and bearer token. Send a POST request from anywhere — your deploy pipeline, n8n, Zapier, a monitoring alert — and Claude executes the prompt with your optional context included.

**Example use cases:**
- Deploy verification — CD pipeline calls the routine after each deploy, Claude runs smoke checks and posts go/no-go to Slack
- Alert triage — monitoring tool detects an error, sends the alert body, Claude correlates with recent commits and opens a draft PR with a proposed fix
- Customer feedback pipeline — feedback comes in, Claude determines bug vs. feature request and creates the issue in Linear

### Trigger 3: GitHub Events

Subscribe a routine to fire automatically on GitHub repository events: pull requests, pushes, issues, releases, check runs, and more. For PRs, Claude opens one session per PR and continues responding as reviewers comment or CI updates — you don't re-trigger it manually.

**Example use cases:**
- Automated code review — triggers on every PR open, leaves inline comments for security and performance issues
- Release notes generation — triggers on release published, reads all merged PRs and writes human-readable notes to CHANGELOG.md
- Docs update on merge — Anthropic uses this internally: every merge to the release branch fires a routine to synthesize and update documentation

---

## How to Create Your First Routine

**Option 1 — Through the browser:**
Go to [claude.ai/code/routines](https://claude.ai/code/routines) → click "New Routine" → give it a clear name → write your prompt → choose the model → link your repos and connectors → add one or more triggers. It's live immediately.

**Option 2 — Through the CLI:**
Type `/schedule` in Claude Code, provide a description, and it registers the routine. You can also use `/schedule` to list and modify existing routines.

---

## Writing Prompts That Actually Work

Each routine run is stateless — the prompt carries the entire job specification. There's no memory between runs unless you explicitly write state to a file in your repo.

Every reliable routine prompt answers these five questions:

1. **What to check** — be specific. "Read issues opened since the last run" beats "check for new issues"
2. **What counts as important** — define your criteria clearly so Claude makes consistent decisions
3. **What to do about it** — describe the exact actions: open a PR, post to Slack, create an issue
4. **When to stop or escalate** — "If the fix requires changes to more than 3 files, don't attempt a PR — post to Slack asking for human review instead"
5. **What to do on failure** — "If you can't access the repo, post an error to #routines-errors with the routine name and failure reason"

**Pro tip:** Test your prompt manually in a regular Claude Code session 3–5 times before converting it to a routine. Once it produces reliable results, then automate it.

---

## 3 Routines Worth Building First

Don't try to automate everything at once. Start with the one that saves you the most repetitive time.

**1. Nightly Bug Triage**
Trigger: Scheduled, every weeknight at 11pm. Reads all issues opened since the last run, labels them by area of code, assigns owners based on your CODEOWNERS file, flags regressions by cross-referencing recent PRs, and posts a summary to Slack. Your team walks in to a groomed board every morning.

**2. Automated Code Review**
Trigger: GitHub event, `pull_request.opened`. Reads the diff, applies your review checklist, leaves inline comments for security and performance issues, and adds a summary comment. Human reviewers focus on architecture and design — not mechanical catches.

**3. Deploy Verification**
Trigger: API, called by your CD pipeline after each deploy. Runs smoke checks against the new build, scans error logs for regressions, and posts a go/no-go to your release Slack channel before the deploy window closes.

---

## Start Automating Today

Claude Code Routines are the difference between using Claude reactively and building a system that works while you sleep. Pick one workflow, write the prompt, set the trigger, and check the output tomorrow morning.

Grab the free **Claude Code Routines Cheat Sheet** — a 2-page PDF covering all 3 trigger types, the 5-element prompt formula, and the top workflows to build first.

[Download the free guide →](/assets/pdfs/claude-routines-freebie.pdf)

Want more Claude automation systems like this? Join [AI Social Hub](https://digicuratoragency.com/aisocialhub_freeplan) — free access to templates, workflows, and the full Claude Code toolkit.
