---
layout: post
title: "How to Create AI Carousel Videos with Claude Code, Higgsfield & Kie.ai (+ Clone Any $1M App)"
author: nessa
categories: [Claude Code, Antigravity, AI Automation]
image: assets/images/claude-code-carousel-video-higgsfield-kieai-header.jpg
featured: false
---

You've seen the AI-generated carousel videos blowing up on Instagram and TikTok — cinematic B-roll, smooth motion, polished talking-head intros. Most creators assume that takes a production team. It doesn't. With Claude Code connected to Higgsfield MCP or Kie.ai, you can generate broadcast-quality video clips in seconds — directly from your terminal, no switching apps.

And if you've ever looked at a $1M App Store app and thought "I could never build that" — this post covers the exact Claude Code prompts to reverse-engineer and scaffold one from screenshots.

{% include youtube.html id="k0_DwTsTCBM" %}

---

## Get the Free Guide

The full step-by-step prompt cheat sheet — Higgsfield MCP setup, Kie.ai workflow, and the two power prompts for cloning any App Store app.

**[Get the free Carousel Video Creator + App Builder Prompt Guide →](https://guides.digicuratoragency.com/guides/claude-code-carousel-video-higgsfield-kieai)**

---

## What Is Higgsfield MCP and Why It Changes Everything

Higgsfield is an AI video generation platform — think cinematic AI clips, image-to-video, and motion effects. On its own it's impressive. But connected to Claude Code via MCP (Model Context Protocol), it becomes a tool you control with a single line of text from inside your workflow.

No dashboard. No tab-switching. No copy-paste. You describe what you want, Claude calls Higgsfield, and the video lands in your output folder.

To set it up:
1. Open Claude Code settings (or Anthropic Console)
2. Add the Higgsfield MCP server: `higgsfield.ai/mcp`
3. Restart Claude Code — the Higgsfield tools appear automatically in your available toolset

Once connected, try this prompt to generate a carousel intro clip:

> *"Use Higgsfield to generate a cinematic talking-head carousel intro: dark studio background, purple rim lighting, camera slowly pushing in, duration 5 seconds."*

For B-roll:

> *"Create a B-roll clip: aerial cityscape at night, neon reflections on wet pavement, slow pan, 6 seconds."*

You can chain these into full carousel sequences inside one Claude Code session.

## Kie.ai — The Cheaper Alternative That Still Delivers

If Higgsfield's pricing doesn't fit your volume, Kie.ai (available at redpandaai.co) is the go-to alternative for creators who need consistent output without blowing the budget. Same quality AI video generation, lower cost per clip.

The integration with Claude Code is lightweight:

1. Grab your API key from the Kie.ai dashboard
2. Add `KIE_API_KEY` to your `.env` file
3. In Claude Code, use the built-in upload tool: `upload_file(Path("video.mp4"))` — it returns a public URL instantly

From there, that URL works anywhere in your content workflow: Blotato scheduling, social repurposing, wherever you post.

Image-to-video prompts that convert well:

> *"Animate this product photo with a subtle zoom and lens flare — 3 seconds, seamless loop."*

> *"Turn this screenshot into a parallax video: foreground moves faster than background, 4 seconds."*

The free guide includes the full prompt list for both tools. **[Grab it here →](https://guides.digicuratoragency.com/guides/claude-code-carousel-video-higgsfield-kieai)**

## How to Reverse-Engineer Any $1M App Store App with Claude Code

Here's where it gets wild. You don't need a dev team or a $500K budget to build an app that competes with the best in your niche. You need Claude Code, a set of screenshots, and two prompts.

**Step 1 — Pick your target.** Open the App Store, search your niche, and sort by Top Charts. You're looking for an app with 4.5+ stars and 10K+ reviews. That review count is proof the market exists. That's your blueprint.

**Step 2 — Screenshot everything.** Capture the full user journey: onboarding screens, main dashboard, key feature screens, settings, and the paywall or pricing screen. Drop them all into one folder on your desktop.

**Step 3 — Paste into Claude Code and use the reverse-engineering prompt:**

> *"I'm going to paste screenshots of [App Name]. Analyze the complete feature set, UI/UX patterns, user flows, monetization model, and core value proposition. Then give me: (1) a ranked list of the 5 most important features to clone first, (2) the recommended tech stack, (3) a project folder structure, and (4) the first file to create."*

Claude will map the app's entire architecture from those screenshots. It identifies patterns, infers the data model, and suggests a build order based on dependency logic — not random guessing.

**Step 4 — Build it with this follow-up prompt:**

> *"Based on your analysis, scaffold the full project. Use [the tech stack Claude recommended]. Create the complete folder structure, install dependencies, and build [Feature 1] first with full styling matching the app's visual style."*

**Step 5 — Iterate screen by screen.** After each feature is built, paste the next screenshot and say:

> *"Now build this screen exactly as shown. Match the layout, spacing, and interactions."*

Pro tip before you start: Add a `CLAUDE.md` file to your project with your brand colors, font stack, and preferred component library. Claude will use them consistently across every screen — no re-prompting needed.

## What to Do With Your Clips After You Generate Them

Once you have the AI video clips, the rest of the carousel creation workflow is fast:

- Drop clips into **Captions.app** or **CapCut** for captions and transitions
- Use **Blotato** (or Claude Code's Blotato MCP) to schedule the carousel across Instagram, TikTok, and YouTube Shorts in one pass
- Repurpose the same clips into a B-roll library for future content — AI-generated B-roll stays evergreen

If you're using Claude Code for content automation already, this slots directly into your existing workflow. The Higgsfield or Kie.ai output becomes just another asset your system handles.

## Start With the Prompt Guide

The fastest way to start is with the free cheat sheet — it has the exact MCP setup steps, the Kie.ai integration, and both power prompts for app reverse-engineering, formatted for quick reference.

**[Download the free Carousel Video Creator + App Builder Prompt Guide →](https://guides.digicuratoragency.com/guides/claude-code-carousel-video-higgsfield-kieai)**

If you're ready to go deeper into building full AI content systems with Claude Code, the [Vibe Coding Mastery](https://builds.digicuratoragency.com/) community covers the full stack — skills, automations, and weekly live builds.
