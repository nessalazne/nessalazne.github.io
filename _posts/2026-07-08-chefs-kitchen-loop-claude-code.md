---
layout: post
title: "The Chef's Kitchen Loop: Stop Burning Your Best Claude Model on Grunt Work"
author: nessa
categories: [Claude Code, Fable 5, AI Automation]
image: assets/images/chefs-kitchen-loop-claude-code-header.jpg
featured: false
---

Everyone's blowing through their Fable 5 limits — Claude's best model — and burning through them fast. Here's the fix: your best model is too powerful to waste on grunt work, so stop making it the executor. In this post you'll learn the 3-tier Claude Code sub-agent workflow that turns your top model into the head chef instead of the line cook, plus the exact setup to run it as a self-correcting loop.

---

## Get the Free Guide

Want the paste-ready version — the exact sub-agent config, the loop wiring, and the watch-outs before you trust it with real work? That's all in the free **Chef's Kitchen Loop for Claude Code** playbook.

**[Get the free Chef's Kitchen Loop Playbook →](https://guides.digicuratoragency.com/guides/chefs-kitchen-loop-claude-code)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/uTDeIJiZ14A"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## Stop Making Your Best Model the Executor

Here's the mistake almost everyone makes with Claude Code: they point their most expensive, most capable model at every single task — the plan, the boilerplate, the renames, the tests, all of it. Then they're confused when they burn through their Fable 5 usage in a single afternoon.

Your best model's real value isn't typing out code — it's judgment. So instead of using it as the executor, run your Claude Code setup like a real kitchen: the head chef designs the menu and tastes the final plate. The line cooks handle the prep. Nobody hands the head chef a cutting board full of onions.

## The Three Kitchen Tiers

This is the core of the Claude Code sub-agent workflow — three tiers, three jobs:

- **Head Chef (Opus 4.8):** Designs the menu — writes the plan, the spec, and the acceptance criteria. Then tastes every plate by reviewing the final result against that spec.
- **Sous Chef (Fable 5):** Does the skilled cooking — the actual implementation and heavy building, once the plan is set.
- **Line Cooks (Sonnet / Haiku):** Handle the prep work — boilerplate, refactors, renames, tests, and repetitive edits that don't need premium judgment.

The rule: your most expensive judgment goes at the two ends — plan and review. The cheap tokens do the middle.

It's worth being clear on *why* this actually saves you anything. Sub-agents draw from the same usage meter as your main session — they aren't a separate free budget. The savings come from not spending premium-model tokens on work a cheaper model handles just as well. Fewer expensive tokens spent on prep means your top-tier capacity lasts across far more real work.

## Setting Up the Executor Sub-Agent

For the full setup, [grab the free guide](https://guides.digicuratoragency.com/guides/chefs-kitchen-loop-claude-code) — but here's the shape of it:

1. **Create a sub-agent** whose only job is execution.
2. **Point it at the cheaper model** — Sonnet for skilled work, Haiku for pure prep.
3. **Give it the plan as input.** It never plans, it only builds against the spec your head chef wrote.
4. **Route the review back to your top model.** It checks the output against the acceptance criteria before anything ships.

That last step matters more than it sounds. Without a real reviewer checking real criteria, you're just hoping the cheaper model got it right.

## Closing the Loop

Once the executor and reviewer roles are wired up, the next move is to stop babysitting it manually and let the system run itself:

- **Define the goal and criteria up front.** "Done" means it passes *these* checks — not "the model stopped talking."
- **Loop until criteria are met.** Wire a check-and-retry so the executor keeps working, hands back to the reviewer, and only exits when the plate passes the taste test.
- **Schedule it.** Once the loop is trustworthy, set it to run on its own — batch overnight, on a trigger, or on a cadence.

Plan with your best. Build with your cheapest. Judge with your best. That's the whole system in one line.

## Before You Rely On This System

Three things to confirm before you hand this loop real work:

- **Confirm the loop/goal mechanism in your current Claude Code version.** Name the real command or custom slash command you're using — don't assume a built-in exists.
- **Watch the reviewer's standards.** A weak acceptance spec means the loop "passes" garbage. The criteria are the whole game.
- **Check your own usage first before quoting a multiplier.** Mechanics change, and you want your numbers to hold up.

## Wrapping Up

If you're blowing through your Fable 5 limits, the fix isn't a bigger budget — it's a better org chart. Put your best model at the two ends (plan and review), route the actual building to a cheaper sub-agent, and close the loop so it keeps working until the output actually passes your bar. That's how you get Claude's best judgment on every task without paying premium rates for prep work.

Grab the [free Chef's Kitchen Loop Playbook](https://guides.digicuratoragency.com/guides/chefs-kitchen-loop-claude-code) for the paste-ready executor sub-agent config and loop wiring, then start rebuilding your workflow around it.

And if you want to go further and build a full AI system you actually own — not just a smarter prompt — come [Join the Vibe Coding Build →](https://builds.digicuratoragency.com/) inside Vibe Coding Mastery.
