---
layout: post
title: "5 Claude Code Plugins You Need to Install Right Now"
description: "Five free Claude Code plugins, Claude Code Setup, OmniRoute, Find Skills, Strix, and Agent Reach, that auto-configure your project, add free tokens, and add security testing."
author: ness
categories: [Claude Code, AI Automation]
tags: [claude code plugins, omniroute, strix, agent reach, claude code setup]
image: assets/images/5-claude-code-plugins-install-right-now-header.jpg
featured: false
---

Five plugins cover four problems most Claude Code users hit every week: a cluttered setup, hitting a usage limit mid-task, not knowing which skill to install, and needing a security check or a scrape without paying for an API. Claude Code Setup, OmniRoute, Find Skills, Strix, and Agent Reach fix all four, and every one of them is free to install.

---

## Get the Free Guide

Get the exact install commands, config files, and setup steps for all five plugins in one PDF.

**[Get the free 5 Claude Code Plugins Guide →](https://hub.digicuratoragency.com/freebie?kw=plugins)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/6ukFw6vtNSg"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Does Claude Code Setup Do?

Claude Code Setup is an official Anthropic plugin that scans your codebase and recommends the MCP servers, skills, hooks, subagents, and slash commands that actually fit your project, then tells you what to remove. It's a read-only analysis tool, so it doesn't touch your files, it just reports back.

Instead of hand-picking automations from a list you've never used, you open Claude Code in your project and ask it directly:

- "recommend automations for this project"
- "help me set up Claude Code"
- "what hooks should I use?"

The plugin checks your stack against categories like MCP servers (context7 for docs, Playwright for frontend testing), skills (Plan agent, frontend-design), hooks (auto-format, auto-lint, block sensitive files), subagents (security review, performance review), and slash commands (/test, /pr-review, /explain), then surfaces the top one or two picks per category. It's built by Isabella He at Anthropic and lives in the official `anthropics/claude-plugins-official` repo.

## How Does OmniRoute Give You 1.6 Billion Free Tokens?

OmniRoute is an open-source AI gateway that routes your requests across more than 300 AI providers, so when Claude hits its usage limit, OmniRoute switches to the next available model instead of stopping your work. It catalogs roughly 1.47 billion free tokens a month across 34 recurring pools and 52 permanently free providers, which is where the "up to 1.6 billion" figure in the video comes from.

You install it as a local server, and it exposes an OpenAI-compatible endpoint at `http://localhost:20128/v1`. Point your tools at that endpoint and pick the `auto` model, and OmniRoute picks a provider for you based on real-time health, quota, latency, and cost. It has three self-healing layers, circuit breakers, connection cooldowns, and per-model lockouts, so a dead provider doesn't stall your session.

| Feature | What it does |
|---|---|
| Free tier | ~1.47B tokens/month across 34 pools + 52 free providers |
| Providers | 300+, including OpenAI, Anthropic, Gemini, Grok, DeepSeek, Llama, Mistral |
| Routing strategies | 19, from simple priority order to cost optimization |
| Token compression | RTK and Caveman engines cut usage 15% to 95% |
| Platforms | npm, Docker, desktop app, PWA, Android via Termux |

Setup is one command:

```bash
npm install -g omniroute
omniroute serve
```

No configuration is required to start, and custom provider "combos" can be set up later from the dashboard or through JSON config in `~/.omniroute/`.

## How Does Find Skills Search 100,000 Skills for You?

Find Skills is a plugin that takes what you're building and searches a marketplace of skills to install the right ones automatically, instead of you scrolling through a list yourself. It runs on the Skills CLI (`npx skills`), a package manager built specifically for agent skills.

The plugin activates when you ask something like "find a skill for X" or "how do I do X," then runs a search behind the scenes:

```bash
npx skills find [query] [--owner <owner>]
```

Once it finds a match, it installs with:

```bash
npx skills add <owner/repo@skill>
```

Add `-g -y` for a global install with no confirmation prompt. Before recommending anything, the plugin is meant to check install counts, favoring options with 1,000-plus installs, prioritize official sources, and weigh GitHub stars, so you're not installing something nobody has tested.

## What Does Strix Actually Attack on Your App?

Strix is an open-source, autonomous security testing platform that acts as a penetration tester against your own application, covering the OWASP Top 10, injection attacks, broken access control, authentication bypass, cross-site scripting, and infrastructure misconfigurations. It runs a multi-agent system: one set of agents does reconnaissance, another looks for vulnerabilities, and a third validates each finding with a working proof of concept before it reports it, which cuts down on false positives.

It needs Docker running and an API key from a supported LLM provider (OpenAI, Anthropic, Google, and others). Install and configure it like this:

```bash
curl -sSL https://strix.ai/install | bash
export STRIX_LLM="openrouter/z-ai/glm-5.3"
export LLM_API_KEY="your-api-key"
```

Then point it at a local codebase or a live URL:

```bash
strix --target ./app-directory
strix --target https://your-app.com
strix view
```

Results land in `strix_runs/<run-name>`, and `strix view` opens the dashboard.

## How Does Agent Reach Scrape Without API Keys?

Agent Reach is an open-source CLI that lets AI agents read and extract data from LinkedIn, Instagram, X, Reddit, and other platforms without paid APIs, using browser-based methods and open tools instead of official developer keys. It reads general web pages through Jina Reader, pulls YouTube transcripts with yt-dlp, searches X with twitter-cli, and reaches Reddit, Facebook, and Instagram through browser-login methods, alongside support for Bilibili, XiaoHongShu, GitHub (via the official `gh` CLI), RSS feeds, and Exa for semantic search.

Credentials stay local in `~/.agent-reach/config.yaml`, and if one data source fails, it automatically routes to a working alternative. A `agent-reach doctor` command reports which channels are working and which still need setup. It requires Python 3.10+, Node.js for some of the underlying tools, and an optional ~$1/month proxy only if you're running it on a server instead of a local machine.

If you want a deeper walkthrough of pairing Claude Code with a scraping tool, [Scrape Thousands of Free Leads With Claude Code](https://blog.digicuratoragency.com/scrape-free-leads-claude-scrapegraphai/) covers the ScrapeGraphAI setup in full.

## FAQ

### Are these five Claude Code plugins free?

Yes. Claude Code Setup, Find Skills, and Strix are open-source and free to run. OmniRoute's free tier covers roughly 1.47 billion tokens a month across its free provider pools. Agent Reach is free locally, with an optional ~$1/month proxy only for server deployments.

### Do I need an API key for Strix?

Yes, Strix needs an API key from a supported LLM provider such as OpenAI, Anthropic, or Google, set as the `LLM_API_KEY` environment variable, plus Docker running locally.

### Does OmniRoute replace my existing Anthropic API key?

No. OmniRoute sits in front of your requests and routes them across providers, including Anthropic, so you keep using your existing keys where you have them while OmniRoute adds fallback options when a provider hits a limit.

### Can Agent Reach scrape Instagram and LinkedIn without an official API?

Yes. Agent Reach reaches Instagram, LinkedIn, Reddit, and Facebook through browser-based login methods rather than each platform's paid developer API, storing credentials locally in `~/.agent-reach/config.yaml`.

### Where do I find more Claude Code plugins like these?

Two related roundups cover different plugin sets: [4 Claude Code Plugins That Cut Token Usage in Half](https://blog.digicuratoragency.com/four-claude-code-plugins-cut-token-usage/) and [4 Free Claude Plugins That Fix Generic AI Output](https://blog.digicuratoragency.com/four-free-claude-plugins-fix-generic-ai-output/).

If you want the full install walkthrough for all five plugins from this post in one place, [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about) for step-by-step Claude Code systems every week.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Are these five Claude Code plugins free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. Claude Code Setup, Find Skills, and Strix are open-source and free to run. OmniRoute's free tier covers roughly 1.47 billion tokens a month across its free provider pools. Agent Reach is free locally, with an optional ~$1/month proxy only for server deployments." }
    },
    {
      "@type": "Question",
      "name": "Do I need an API key for Strix?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes, Strix needs an API key from a supported LLM provider such as OpenAI, Anthropic, or Google, set as the LLM_API_KEY environment variable, plus Docker running locally." }
    },
    {
      "@type": "Question",
      "name": "Does OmniRoute replace my existing Anthropic API key?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. OmniRoute sits in front of your requests and routes them across providers, including Anthropic, so you keep using your existing keys where you have them while OmniRoute adds fallback options when a provider hits a limit." }
    },
    {
      "@type": "Question",
      "name": "Can Agent Reach scrape Instagram and LinkedIn without an official API?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. Agent Reach reaches Instagram, LinkedIn, Reddit, and Facebook through browser-based login methods rather than each platform's paid developer API, storing credentials locally in ~/.agent-reach/config.yaml." }
    },
    {
      "@type": "Question",
      "name": "Where do I find more Claude Code plugins like these?",
      "acceptedAnswer": { "@type": "Answer", "text": "Two related roundups cover different plugin sets: 4 Claude Code Plugins That Cut Token Usage in Half and 4 Free Claude Plugins That Fix Generic AI Output." }
    }
  ]
}
</script>
