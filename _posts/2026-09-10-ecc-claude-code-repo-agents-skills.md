---
layout: post
title: "ECC: The Claude Code Repo With 256K GitHub Stars"
description: "ECC installs 68 agents, 291 skills, and 94 commands into Claude Code with one free command. Here is what it does and how to set it up safely."
author: ness
categories: [Claude Code, AI Automation]
tags: [ecc, claude code, ai agents, claude skills, free tools]
image: assets/images/ecc-claude-code-repo-agents-skills-header.jpg
featured: false
---

ECC is a free, MIT-licensed repository that installs a complete engineering system into Claude Code with a single command. As of September 2026 it carries roughly 256,000 stars on GitHub and ships 68 specialized agents, 291 skills, and 94 commands. It was built by Affaan Mustafa, who won an Anthropic hackathon with Zenith Chat, placing first out of more than 100 entrants.

When I filmed the video below, the repo was at 240,000 stars with 64 agents, 261 skills, and 84 commands. It has grown since. That pace is part of the story: one maintainer shipping weekly across seven coding agents.

---

## Get the Free Guide

The guide has the install command, where every file lands on your machine, the setup order for Claude Code and Codex, and a fix table for the errors that hit most people on their first run.

**[Get the free ECC Install Guide →](https://hub.digicuratoragency.com/freebie?kw=claude)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/th3pP3ktyfA"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is ECC and Who Built It?

ECC is what its author calls an agent harness operating system: a coordinated engineering process that your coding agent follows instead of you re-explaining it in every prompt. The repo describes the loop in one line, `plan -> test -> implement -> review -> verify -> remember -> improve`, and installs the pieces that make each step happen.

Affaan Mustafa (@affaan-m on GitHub) maintains it. He is based in New York, has around 10,600 GitHub followers, and co-founded Itô Markets. His Anthropic hackathon win with Zenith Chat came with $15,000 in credits. His other public projects include AgentShield, an agent security scanner that ships inside ECC, and JARVIS, an OSINT platform.

The license is MIT and the open-source repo is free forever. There is a paid hosted GitHub App (ECC Pro) for private repos starting at $19 per seat per month, which is what funds the weekly release cadence. You never have to touch it to use the repo.

## What Do You Actually Get?

The counts sound abstract until you see the split. Here is what the repo lists as of September 2026:

| Included | Count | What it covers |
|---|---|---|
| Agents | 68 | Planning, review, build repair, security, architecture, domain work |
| Skills | 291 | TDD, research, security, docs, frontend, data, ML, operations |
| Commands | 94 | Slash entry points while ECC moves to a skills-first surface |
| Hooks and memory | Runtime | Enforcement, session summaries, continuous learning, context controls |
| Rules | Selective | Always-loaded standards you pick per language or project |
| AgentShield | Included | Scans prompts, hooks, MCP config, permissions, secrets, agent files |

Skills are the main surface now. Commands still work and are maintained, but new workflows land in `skills/` first. If you have already installed [free Claude Skills by department](https://blog.digicuratoragency.com/free-claude-skills-by-department/), ECC is the same idea scaled to an engineering team rather than a marketing one.

## How Do You Install ECC in One Command?

One command runs a guided wizard that inventories your existing setup before it writes anything. From your project directory:

```bash
npx ecc-universal@2.2.1 setup
```

That is the recommended path for Claude Code. Three things to know before you run it:

1. **You need Node.js 18 or newer**, plus Git and Claude Code CLI v2.1.0 or later on your `PATH`. Check with `claude --version`.
2. **The wizard asks you to pick a scope**: `user`, `project`, or `local`. Rerun the same command later to update ECC, change scope, or change the hook profile.
3. **Rules are not distributed by the plugin.** Claude Code plugins cannot carry them, so you clone the repo and copy the packs you want into `~/.claude/rules/ecc/`.

If you would rather use Claude Code's own plugin commands, run these two inside Claude Code:

```text
/plugin marketplace add https://github.com/affaan-m/ECC
/plugin install ecc@ecc
```

For more than one coding agent in one flow, `npx ecc-universal@2.2.1 install --guided` handles Claude Code, Codex, and Kimi Code together. Codex also has its own native path with `codex plugin marketplace add affaan-m/ECC`.

## What Is the One Mistake Almost Everyone Makes?

Do not stack two install methods into the same harness. Installing the Claude Code plugin and then running `./install.sh --profile full` on top of it is the single most common failure in the repo's own troubleshooting notes. You get duplicate skills, duplicate commands, and hooks that fire twice.

Installing ECC once into several different harnesses is fine. Installing it twice into one harness is what breaks. If you already did it, remove the plugin, run `npx ecc-universal@2.2.1 uninstall --dry-run` from the project directory that holds the install state, delete the rule folders you copied by hand, then reinstall using one path only.

## Is 291 Skills Too Much for Your Context Window?

Skills load on demand, so the catalog size is not the thing that eats your context. What eats it is model choice and thinking budget, and the repo publishes settings for both. Its recommended `~/.claude/settings.json` block:

```json
{
  "model": "sonnet",
  "env": {
    "MAX_THINKING_TOKENS": "10000",
    "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "50",
    "CLAUDE_CODE_SUBAGENT_MODEL": "haiku"
  }
}
```

The repo puts the model switch at roughly a 60% cost reduction and the thinking-token cap at around 70% less hidden thinking cost per request, with Opus reserved for deep architectural work. That pairs well with the [Claude Code plugins that cut token usage](https://blog.digicuratoragency.com/four-claude-code-plugins-cut-token-usage/) I covered earlier, and with the [MCP servers worth installing](https://blog.digicuratoragency.com/4-mcps-make-claude-useful/) once your agent has a process to follow.

For a solopreneur or a small agency, the practical read is simple. You get a planner, a code reviewer, a build fixer, a security reviewer, and language specialists that were already wired to hand work to each other. That is a research, build, and review crew running from day one, with no hires and no monthly fee.

## FAQ

### Is ECC free?

Yes. The GitHub repository is MIT-licensed and free forever. ECC Pro is a separate hosted GitHub App for private repos, priced from $19 per seat per month as of September 2026, and it is optional.

### Does ECC work with anything other than Claude Code?

It works best with Claude Code, has a supported Codex path, and provides capability-limited adapters for Cursor, OpenCode, Gemini, Zed, GitHub Copilot, Antigravity, and Qwen. Check the repo's platform support matrix before assuming the same features everywhere.

### What do I run first after installing?

Start with the workflow you need rather than the whole catalog. For a new feature, run `/ecc:plan "describe the feature"` and then the `tdd-workflow` skill. For a review, run `/code-review`.

### Why does the plugin identifier not match the repo name?

ECC has three public identifiers on purpose: the GitHub repo is `affaan-m/ECC`, the Claude marketplace plugin is `ecc@ecc`, and the npm package is `ecc-universal`. The short plugin name keeps tool names and slash-command namespaces inside strict validators.

### How do I check what is installed?

Run `/plugin list ecc@ecc` inside Claude Code, or `npx ecc-universal@2.2.1 list-installed` followed by `doctor` from your project directory.

## The Takeaway

One command turns Claude Code from a coding assistant into a coordinated team with a plan step, a test step, a review step, and a memory. ECC is free, the numbers behind it are public, and the only real trap is installing it twice into the same harness.

Grab the free guide above for the install order and the fix table. If you want the full builds behind systems like this, [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about).

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is ECC free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. The GitHub repository is MIT-licensed and free forever. ECC Pro is a separate hosted GitHub App for private repos, priced from $19 per seat per month as of September 2026, and it is optional." }
    },
    {
      "@type": "Question",
      "name": "Does ECC work with anything other than Claude Code?",
      "acceptedAnswer": { "@type": "Answer", "text": "It works best with Claude Code, has a supported Codex path, and provides capability-limited adapters for Cursor, OpenCode, Gemini, Zed, GitHub Copilot, Antigravity, and Qwen. Check the repo's platform support matrix before assuming the same features everywhere." }
    },
    {
      "@type": "Question",
      "name": "What do I run first after installing?",
      "acceptedAnswer": { "@type": "Answer", "text": "Start with the workflow you need rather than the whole catalog. For a new feature, run /ecc:plan \"describe the feature\" and then the tdd-workflow skill. For a review, run /code-review." }
    },
    {
      "@type": "Question",
      "name": "Why does the plugin identifier not match the repo name?",
      "acceptedAnswer": { "@type": "Answer", "text": "ECC has three public identifiers on purpose: the GitHub repo is affaan-m/ECC, the Claude marketplace plugin is ecc@ecc, and the npm package is ecc-universal. The short plugin name keeps tool names and slash-command namespaces inside strict validators." }
    },
    {
      "@type": "Question",
      "name": "How do I check what is installed?",
      "acceptedAnswer": { "@type": "Answer", "text": "Run /plugin list ecc@ecc inside Claude Code, or npx ecc-universal@2.2.1 list-installed followed by doctor from your project directory." }
    }
  ]
}
</script>
