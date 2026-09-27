---
layout: post
title: "Free AI Web Scraping: Agent Reach for Claude Code"
description: "Agent Reach is a free, open-source CLI that gives Claude Code and Codex real web access: LinkedIn, YouTube, Reddit and X, with no paid scraping API."
author: ness
categories: [Claude Code, AI Automation]
tags: [free ai web scraping, agent reach, claude code, open source tools, lead research]
image: assets/images/agent-reach-free-ai-web-scraping-claude-header.jpg
featured: false
---

Agent Reach is a free, open-source command line tool that gives an AI agent like Claude Code or OpenAI Codex real access to the web: LinkedIn profiles and job listings, YouTube transcripts, Reddit threads, Instagram profiles, X timelines and ordinary web pages. You install it once, run `agent-reach install`, and your agent reads those sites without a paid scraping API sitting in the middle. The project is MIT licensed and has passed 85,000 stars on GitHub as of September 2026.

That matters because most agent setups fake web access. They either guess from training data or burn credits on a scraping subscription that charges per request. Agent Reach wires your agent into the tools that already work for each site, then gets out of the way.

---

## Get the Free Guide

The guide has the install commands, the per-platform config steps, the prompts I run against it, and a fix table for the errors you will hit.

**[Get the free Agent Reach Setup Guide →](https://hub.digicuratoragency.com/freebie?kw=scrape)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/0pjxvwY1qQk"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is Agent Reach, and Why Is It Free?

Agent Reach is a single command line interface that bundles the existing open-source readers for a dozen or so platforms, so an AI agent can call one tool instead of eleven. It is published by GitHub user Panniantong under the MIT license, and the README describes its goal as giving agents internet access with zero API fees.

The reason it costs nothing is that it does not run a scraping service. There is no hosted proxy pool billing you per page. Each channel is handled by a program that already exists and already works: `yt-dlp` for YouTube transcripts, the GitHub `gh` CLI for repositories, `feedparser` for RSS, Jina Reader for plain web pages, and browser-session tools for the sites that need a login. Agent Reach installs them, stores the credentials you supply in `~/.agent-reach/config.yaml` with file permissions locked to 600, and gives your agent one consistent way to reach all of it.

Most channels work with no configuration at all. The ones that need you to be logged in are the ones you would expect: X, Reddit and XiaoHongShu.

## Which Sites Can Claude Code Actually Read?

Here is the channel list from the project README, with the tool doing the work behind each one, so you can see exactly where the data comes from.

| Platform | Backed by | Needs a login |
|---|---|---|
| Any web page | Jina Reader | No |
| YouTube transcripts | yt-dlp | No |
| RSS feeds | feedparser | No |
| GitHub | `gh` CLI | No (uses your existing `gh` auth) |
| Global search | Exa via mcporter | No |
| LinkedIn profiles and jobs | mcp-server-linkedin | No |
| X / Twitter | twitter-cli | Yes, cookie |
| Reddit | OpenCLI or rdt-cli | Yes |
| Facebook | OpenCLI with Chrome | Yes |
| Instagram | OpenCLI | Yes |
| Bilibili | bili-cli | No |
| XiaoHongShu | OpenCLI or xiaohongshu-mcp | Yes, cookie |
| Podcasts (Xiaoyuzhou) | Groq transcription | Free Groq API key |

The LinkedIn channel is the one people ask about first. It runs through `mcp-server-linkedin`, registered with `mcporter`, and covers profiles and job search. If you have been stitching together lead lists by hand, this is closer to what you wanted than any browser extension. It pairs well with the approach in [scraping free leads with Claude and ScrapeGraphAI](https://blog.digicuratoragency.com/scrape-free-leads-claude-scrapegraphai/), which handles arbitrary sites rather than named platforms.

## How Do You Install Agent Reach?

Installation is two commands, plus an approval step for anything that touches your system. `pipx` is the recommended path:

1. `pipx install https://github.com/Panniantong/agent-reach/archive/main.zip`
2. `agent-reach install --env=auto` runs a read-only dependency check and tells you what is missing.
3. `agent-reach install --env=auto --system` actually installs and configures, and it asks before changing anything.
4. `agent-reach doctor` reports the status of every channel, which is how you confirm the install worked.

If your Python came from Homebrew, or you hit a PEP 668 externally-managed-environment error, make a virtual environment first with `python3 -m venv ~/.agent-reach-venv`, activate it, then `pip install` the same archive URL.

Optional channels are opt-in rather than automatic. You add them by name:

```bash
agent-reach install --env=auto --system --channels=opencli,xiaohongshu
```

There is also `--dry-run` if you want to see the system changes before agreeing to them. I ran that first, and it is worth the extra thirty seconds.

The install doc is written to be handed to the agent rather than followed by hand, which is a pattern I like: you point Claude Code at `https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md` and let it do the sequencing. Same idea as the [four MCPs that make Claude genuinely useful](https://blog.digicuratoragency.com/4-mcps-make-claude-useful/), where the setup is the product.

## What Does This Replace in a Real Workflow?

For a small agency or a solo operator, Agent Reach absorbs a job that is usually split across three paid tools: competitor monitoring, prospect research, and content research.

- **Competitor research.** Ask your agent to pull a competitor's recent posts, their YouTube transcripts, and the threads where people complain about them, then summarise the pattern.
- **Prospecting.** LinkedIn job search plus profile reads gives you companies that are hiring for the thing you sell, which is the cleanest buying signal there is.
- **Content research.** YouTube transcripts and Reddit threads on one topic, in one pass, before you write anything.
- **Market monitoring.** `agent-reach watch` runs scheduled checks so you are not re-asking the same question every Monday.

The honest comparison is not "free versus expensive". It is "free and you maintain it" versus "paid and someone else maintains it". If you already run local tooling like the [Google Maps Scraper Kit](https://blog.digicuratoragency.com/google-maps-scraper-kit-claude-code/), maintaining one more CLI costs you almost nothing and you keep the data.

## What Are the Limits You Should Know About?

Cookie-based channels are the fragile part. X, Reddit and XiaoHongShu need you to export a session cookie, and those cookies expire, which means the channel goes quiet until you refresh it. The README is direct about the other risk: use throwaway accounts on login-required platforms, because scraping from your main account can get that account restricted.

Two more things worth knowing before you start. Instagram and Facebook run through OpenCLI, which needs a desktop Chrome session, so those two do not work on a headless server. And Agent Reach keeps everything inside `~/.agent-reach/`, with cloned tools in `~/.agent-reach/tools/`, so if an agent starts cloning repositories into your project folder, something has gone wrong and you should stop it.

## FAQ

### Is Agent Reach really free?

Yes. It is MIT licensed open source with no hosted service behind it, so there is nothing to subscribe to. The only paid piece is optional: podcast transcription uses a Groq API key, and Groq has a free tier.

### Does Agent Reach work with ChatGPT and Codex, or only Claude Code?

It works with any agent that can run shell commands, which includes Claude Code and OpenAI Codex. It is a command line tool, so the agent calls it the same way it would call `git`.

### Can it scrape LinkedIn without getting my account banned?

LinkedIn access goes through `mcp-server-linkedin` and covers profiles and job search. The project recommends using a throwaway account for any login-required platform, and that advice applies here. Reading at human pace is much safer than bulk pulls.

### What do I do when a channel stops working?

Run `agent-reach doctor`. It checks every channel and reports which one is broken, and the usual answer for a login-based channel is that the cookie expired and needs re-exporting with `agent-reach configure`.

### Where does Agent Reach store my credentials?

In `~/.agent-reach/config.yaml`, on your own machine, with permissions set to 600 so only your user can read the file. Nothing is sent to a third-party server.

## Give Your Agent Real Web Access

Free AI web scraping stopped being a contradiction the moment someone bundled the working open-source readers into one CLI. Install Agent Reach, run `agent-reach doctor`, pick the two or three channels you will actually use, and your agent can research the internet instead of guessing about it. Start with the channels that need no login, because those work in the first ten minutes.

If you want to build the rest of the system around it, the research loop, the lead list, the content pipeline, that is what we do inside [Vibe Coding Mastery](https://hub.digicuratoragency.com/about).

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is Agent Reach really free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. It is MIT licensed open source with no hosted service behind it, so there is nothing to subscribe to. The only paid piece is optional: podcast transcription uses a Groq API key, and Groq has a free tier." }
    },
    {
      "@type": "Question",
      "name": "Does Agent Reach work with ChatGPT and Codex, or only Claude Code?",
      "acceptedAnswer": { "@type": "Answer", "text": "It works with any agent that can run shell commands, which includes Claude Code and OpenAI Codex. It is a command line tool, so the agent calls it the same way it would call git." }
    },
    {
      "@type": "Question",
      "name": "Can it scrape LinkedIn without getting my account banned?",
      "acceptedAnswer": { "@type": "Answer", "text": "LinkedIn access goes through mcp-server-linkedin and covers profiles and job search. The project recommends using a throwaway account for any login-required platform, and that advice applies here. Reading at human pace is much safer than bulk pulls." }
    },
    {
      "@type": "Question",
      "name": "What do I do when a channel stops working?",
      "acceptedAnswer": { "@type": "Answer", "text": "Run agent-reach doctor. It checks every channel and reports which one is broken, and the usual answer for a login-based channel is that the cookie expired and needs re-exporting with agent-reach configure." }
    },
    {
      "@type": "Question",
      "name": "Where does Agent Reach store my credentials?",
      "acceptedAnswer": { "@type": "Answer", "text": "In ~/.agent-reach/config.yaml, on your own machine, with permissions set to 600 so only your user can read the file. Nothing is sent to a third-party server." }
    }
  ]
}
</script>
