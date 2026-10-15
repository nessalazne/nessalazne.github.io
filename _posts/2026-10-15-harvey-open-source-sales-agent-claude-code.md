---
layout: post
title: "Harvey: Open-Source Sales Agent for Claude Code"
description: "Harvey is an open-source sales agent that runs on a Claude Code subscription, profiles prospect websites, writes cold email, and waits for your approval."
author: ness
categories: [Claude Code, AI Automation]
tags: [cold outreach, sales automation, claude code skills, open source, agency tools]
image: assets/images/harvey-open-source-sales-agent-claude-code-header.jpg
featured: false
---

Harvey is an open-source sales agent that runs on a Claude Pro or Claude Max subscription instead of a per-token API bill. It finds local businesses, reads their websites, writes cold email that references something real on each site, and queues every message for your approval before anything goes out.

---

## Get the Free Guide

The Harvey Outreach Setup walks through installing the agent, training it on your own offer, and the exact commands to run a safe first campaign.

**[Get the free Harvey Outreach Setup →](https://hub.digicuratoragency.com/freebie?kw=outreach)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/hgn44aIO7Mo"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

Most cold outreach fails for one reason: the email is generic. A template that could go to any business in any city reads like a template, and prospects delete it in the same second they open it. Harvey, built by developer Ethan and hosted at [github.com/ethanplusai/harvey](https://github.com/ethanplusai/harvey), tries to fix that by making the research step mandatory instead of optional.

## What Is Harvey and How Does It Work?

Harvey is a Python command-line agent that chains five stages together: discover, profile, write, send, and handle replies. It runs on Claude Pro, Claude Max, or a ChatGPT subscription through the Claude Code or Codex CLI, so there's no OpenAI or Anthropic API bill stacking up per message the way most AI outreach tools charge.

The pipeline for a single prospect looks like this:

1. **Discover**: Harvey searches for local businesses matching the criteria you set (industry, location) using free or optional paid discovery providers like DataForSEO or Serper.
2. **Profile**: it visits the business's actual website and reads it, pulling out specific details: services offered, recent updates, tone, anything an email could reference honestly.
3. **Write**: the Writer agent drafts a three-email sequence (roughly 75, 75, and 40 words) using frameworks stored as plain Markdown files in `skills/`, such as AIDA, PAS, and BAB.
4. **Gate**: every email passes through `gate.py`, a deterministic pre-send check that rejects unrendered template tags, banned phrases, length violations, and non-deliverable addresses before a human ever sees it.
5. **Approve and send**: by default, `channels.email.require_approval` is `true` in `harvey.yaml`, so nothing leaves the queue until you review it in `harvey outbox` or the dashboard.

## Why Does the Flat Subscription Matter for Agencies?

It matters because per-message API costs eat directly into margin on volume outreach. A typical AI-powered outreach tool charges per API call for discovery, profiling, and writing, so every batch of 100 prospects adds a bill on top of whatever software fee you're already paying. Harvey routes its reasoning through the Claude Code or Codex CLI you already have a subscription for, so the agent's compute cost is the flat monthly fee, not a running meter. For agency owners and freelancers running outreach as part of client work, that's the difference between outreach that scales and outreach that gets throttled by budget before it gets throttled by results.

## What Do You Need Before Installing Harvey?

You need Python 3.11 or newer and an active Claude Pro or Claude Max subscription (or a ChatGPT subscription) with the matching CLI logged in on your machine. No Apollo, ZoomInfo, or other paid prospecting tool is required; Harvey's discovery step works with free providers out of the box and optional paid ones if you want broader coverage.

| Requirement | Why it's needed |
|---|---|
| Python 3.11+ | Harvey is a Python CLI application |
| Claude Pro/Max or ChatGPT subscription | Runs the agent's reasoning without per-token API billing |
| Mail provider credentials | Gmail, SMTP, or Instantly, set in `.env` |
| `.env` file | Holds credentials and provider keys |
| `harvey.yaml` | Sets persona, product, ICP, channels, and send limits |

## How Do You Run a Safe First Campaign?

You run a safe first campaign by training Harvey on your own offer, confirming its signal catalog, and letting discovery run with approval still turned on. The install sequence from the repo is:

```bash
git clone https://github.com/ethanplusai/harvey.git
cd harvey
python3.13 -m venv .venv && source .venv/bin/activate && pip install -e .
cp .env.example .env && $EDITOR .env
harvey train https://your-company.com
harvey signals --confirm free
harvey discover
```

`harvey train` reads your own website and writes `product_knowledge.md`, which the Writer agent later references so outgoing emails describe your offer accurately instead of generically. Leave `require_approval: true` in `harvey.yaml` for the first several batches, review everything in `harvey outbox`, and only flip it to `false` once you trust the gate and the copy it's producing.

For the deeper version of this, the free guide above covers the `.env` fields that trip people up, how to read the Writer's three-email sequence before approving it, and the kill switches (`harvey sending pause`, `max_daily_sends`, bounce-rate limits) worth setting before a real batch goes out. If you're also running outreach that leads with a rebuilt website instead of an email, see how that pairs with research-first prospecting in [Local Business Outreach: Claude Builds the Site First](https://blog.digicuratoragency.com/local-business-outreach-claude-website/).

## FAQ

### Does Harvey require an API key from Anthropic or OpenAI?
No. Harvey runs its reasoning through the Claude Code or Codex CLI tied to a Claude Pro/Max or ChatGPT subscription, so there's no separate per-token API bill for the agent itself. A mail provider (Gmail, SMTP, or Instantly) still needs its own credentials in `.env`.

### Can emails send automatically without my review?
Only if you set `channels.email.require_approval: false` in `harvey.yaml`. The default is `true`, meaning every email sits in `harvey outbox` until you approve it manually or run `harvey outbox --approve-all`.

### What stops Harvey from emailing the same business twice?
`state.py` keeps a SQLite record of every prospect and its stage, so already-contacted businesses are tracked and skipped on later discovery runs.

### Does Harvey need Apollo or ZoomInfo for prospecting?
No. Discovery works with free providers by default, with DataForSEO and Serper available as optional paid add-ons for broader coverage.

### What happens if a campaign gets too many bounces?
Harvey enforces a bounce-rate threshold and kills the campaign automatically once it's crossed, in addition to respecting `max_daily_sends` and quiet hours set in `harvey.yaml`.

## Try It With a Small Batch First

Personalization at volume is the actual promise here: cold email that references something real about each business, without a VA reading a hundred websites by hand and without templates that announce themselves as templates in the first sentence. Start with `harvey discover` on a narrow list, read every draft in `harvey outbox` before approving it, and widen the batch once the copy holds up.

Want the step-by-step setup, the `.env` fields that matter most, and the commands for a first safe run? [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about) for more systems like this one.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Does Harvey require an API key from Anthropic or OpenAI?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Harvey runs its reasoning through the Claude Code or Codex CLI tied to a Claude Pro/Max or ChatGPT subscription, so there's no separate per-token API bill for the agent itself. A mail provider (Gmail, SMTP, or Instantly) still needs its own credentials in .env." }
    },
    {
      "@type": "Question",
      "name": "Can emails send automatically without my review?",
      "acceptedAnswer": { "@type": "Answer", "text": "Only if you set channels.email.require_approval to false in harvey.yaml. The default is true, meaning every email sits in harvey outbox until you approve it manually or run harvey outbox --approve-all." }
    },
    {
      "@type": "Question",
      "name": "What stops Harvey from emailing the same business twice?",
      "acceptedAnswer": { "@type": "Answer", "text": "state.py keeps a SQLite record of every prospect and its stage, so already-contacted businesses are tracked and skipped on later discovery runs." }
    },
    {
      "@type": "Question",
      "name": "Does Harvey need Apollo or ZoomInfo for prospecting?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Discovery works with free providers by default, with DataForSEO and Serper available as optional paid add-ons for broader coverage." }
    },
    {
      "@type": "Question",
      "name": "What happens if a campaign gets too many bounces?",
      "acceptedAnswer": { "@type": "Answer", "text": "Harvey enforces a bounce-rate threshold and kills the campaign automatically once it's crossed, in addition to respecting max_daily_sends and quiet hours set in harvey.yaml." }
    }
  ]
}
</script>
