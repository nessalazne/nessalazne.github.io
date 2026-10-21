---
layout: post
title: "Claude Sub-Agents: Run 100 in Parallel, Stop Re-Prompting"
description: "Claude Code sub-agents each get their own context window. Here is the setup that fans one task across 100 agents in parallel and surfaces the best output."
author: ness
categories: [Claude Code, AI Automation]
tags: [claude sub-agents, claude code, parallel agents, ai automation, agent orchestration]
image: assets/images/claude-100-sub-agents-parallel-setup-header.jpg
featured: false
---

Claude Code sub-agents are separate agent instances that the main Claude session spawns to work on a slice of your task, each with its own context window and its own tool access. Because the orchestrator can launch many of them from a single turn, you can fan one problem out across dozens or even a hundred agents, have each one attack a different angle, then have Claude compare what came back and surface the strongest result. That is the whole trick behind killing the re-prompting loop: instead of asking once, reading a mediocre answer, and asking again, you ask once and get a hundred attempts graded for you.

Most people never touch this. They prompt Claude, get a first draft, nudge it, get a slightly different draft, nudge it again, and burn forty minutes arriving at something a parallel fan-out would have handed them in one pass.

---

## Get the Free Guide

The guide walks through the sub-agent files, the fan-out prompt, and the setup steps for both Claude Code and Codex, with the exact commands I run.

**[Get the free 100 Sub-Agent Setup for Claude Code →](https://hub.digicuratoragency.com/freebie?kw=agents)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/S2qw35hUJ3g"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is a Claude Code Sub-Agent?

A sub-agent is a defined agent persona that Claude Code can delegate work to, and the thing that makes it useful is isolation: it runs in a fresh context window and reports a summary back instead of dumping its whole transcript into your main thread. You write one as a markdown file with YAML front matter, drop it in a folder, and Claude can call it.

A minimal sub-agent file looks like this:

```markdown
---
name: hook-critic
description: Judges a short-form video hook on the first three seconds only.
tools: Read, Grep
model: sonnet
---

You judge hooks. Score the first three seconds out of 10,
name the single weakest word, and rewrite the hook twice.
Return only the score, the weak word, and the two rewrites.
```

Two folders matter, as of October 2026:

| Location | Scope | Use it for |
|---|---|---|
| `~/.claude/agents/` | Every project on your machine | Reusable critics, researchers, writers |
| `.claude/agents/` | The current project only | Agents that know this codebase or client |
| `AGENTS.md` + project folder | Codex and other harnesses | Pointing a second tool at the same personas |

The folder name and the `name:` field have to match what you reference in your prompt, which is where most first attempts quietly fail.

## How Does the 100 Sub-Agent Fan-Out Actually Work?

The fan-out works because the orchestrator treats sub-agent calls as independent jobs it can issue together, so one instruction becomes many simultaneous runs instead of one sequential chain. There are three moving parts:

1. **The split.** Claude decides how to slice the task. One hundred agents writing the same hook is waste. One hundred agents each writing a hook for a different audience, angle, emotion, or length is coverage.
2. **The run.** Each agent works alone in its own context. It cannot see the others, which is the point: no groupthink, no drift toward the first answer.
3. **The merge.** Every agent returns a short structured result. Claude scores them against criteria you set in the original prompt and hands you a ranked shortlist with the reasoning.

The prompt that triggers it is plain English. Something like: *"Spawn 40 sub-agents. Each one writes a cold email opener for a different buyer objection. Score all 40 on specificity and send me the top five with why each won."*

## What Does Almost Everyone Get Wrong?

The mistake is asking for a number of agents without giving each one a different job, which produces a hundred near-identical answers and a hundred times the token bill. Parallelism buys you diversity, nothing else. If the slices are the same, the outputs will be too.

Two more things worth knowing before you run this on real work:

- **The agents run bounded, not literally all at once.** Claude Code issues a batch, waits, then issues the next. A hundred-agent run finishes in waves, so expect minutes rather than seconds.
- **Cost scales with the count.** Each sub-agent is its own context window being filled and read. Ten agents cost roughly ten times one agent. If you are watching your plan, the [two claude.md rules that stop Claude from burning your usage limit](https://blog.digicuratoragency.com/claude-opus-5-5-usage-limits-claude-md-config/) are worth reading first.

Set the scoring criteria in the same prompt that launches the fan-out. If you add them afterwards, Claude grades on whatever it inferred, and you are back to re-prompting.

## When Is This Worth Running?

Fan-outs pay off on tasks with many valid answers and one best answer, and they waste money on tasks with exactly one correct answer. A migration script does not need a hundred opinions. A positioning line does.

Good fits:

- Hooks, headlines, subject lines, ad angles, names
- Research sweeps where each agent takes a different source or competitor
- Code review from several specialist angles at once, security, performance, readability
- Pricing or offer variants scored against one customer profile

Poor fits: anything deterministic, anything that writes to the same file, and anything where you have not defined "best" yet.

If you want the mechanics underneath all of this, the breakdown of [how an AI agent's LLM brain and harness split the work](https://blog.digicuratoragency.com/ai-agents-llm-brain-harness-system/) explains why isolated context windows behave so differently from one long chat. And if you would rather manage many agent sessions from a single window, [Orca is a free agent manager for Claude Code and Codex](https://blog.digicuratoragency.com/orca-free-ai-agent-manager-claude-codex/).

## FAQ

### How many sub-agents can Claude Code actually run?

You can ask for any number, and Claude Code will work through them in batches rather than firing all of them at the same instant. A request for 100 completes in waves, so the practical limit is your patience and your token budget, not a hard cap in the prompt.

### Do sub-agents share my main conversation?

No. Each sub-agent starts with a fresh context window and only receives the instructions the orchestrator passes it. It returns a summary, which is why a hundred-agent run does not flood your main session.

### Where do I save a sub-agent file?

Put reusable agents in `~/.claude/agents/` and project-specific ones in `.claude/agents/`. The file is markdown with YAML front matter, and the `name:` field is what you reference when you ask Claude to use it.

### Does this work in Codex too?

Yes, with a different wiring. You keep the same agent persona files in your project and point to them from an `AGENTS.md` file so Codex knows they exist. The fan-out prompt itself is identical.

### Will 100 agents give me a better answer than one?

Only if each agent has a genuinely different assignment and you told Claude how to score the results. Identical instructions produce identical output at a hundred times the cost.

## Start With Ten, Not a Hundred

Write one sub-agent file, ask Claude to spawn ten copies of the task across ten different angles, and read the ranked shortlist. You will know inside one run whether your slices were real or whether you just paid for ten versions of the same sentence. Then scale the count.

Want the full system behind this, plus the rest of the agent setups I run every day? [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about)

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How many sub-agents can Claude Code actually run?",
      "acceptedAnswer": { "@type": "Answer", "text": "You can ask for any number, and Claude Code will work through them in batches rather than firing all of them at the same instant. A request for 100 completes in waves, so the practical limit is your patience and your token budget, not a hard cap in the prompt." }
    },
    {
      "@type": "Question",
      "name": "Do sub-agents share my main conversation?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Each sub-agent starts with a fresh context window and only receives the instructions the orchestrator passes it. It returns a summary, which is why a hundred-agent run does not flood your main session." }
    },
    {
      "@type": "Question",
      "name": "Where do I save a sub-agent file?",
      "acceptedAnswer": { "@type": "Answer", "text": "Put reusable agents in ~/.claude/agents/ and project-specific ones in .claude/agents/. The file is markdown with YAML front matter, and the name: field is what you reference when you ask Claude to use it." }
    },
    {
      "@type": "Question",
      "name": "Does this work in Codex too?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes, with a different wiring. You keep the same agent persona files in your project and point to them from an AGENTS.md file so Codex knows they exist. The fan-out prompt itself is identical." }
    },
    {
      "@type": "Question",
      "name": "Will 100 agents give me a better answer than one?",
      "acceptedAnswer": { "@type": "Answer", "text": "Only if each agent has a genuinely different assignment and you told Claude how to score the results. Identical instructions produce identical output at a hundred times the cost." }
    }
  ]
}
</script>
