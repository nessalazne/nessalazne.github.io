---
layout: post
title: "How to Create Videos with Remotion in Claude Code (Antigravity IDE)"
author: ness
categories: [Claude Code, Antigravity, AI Automation]
image: assets/images/remotion-claude-code-video-creator-header.jpg
featured: false
---

What if you could build a video — complete with animations, captions, and transitions — without touching a video editor? That's exactly what's possible when you pair Remotion with Claude Code in the Antigravity IDE. In this post, I'll show you how it works and how to get started fast.

{% include youtube-short.html id="OuCM6m5YQxE" %}

---

## Get the Free Guide

Want the step-by-step setup checklist for Remotion in Claude Code? I've put the full workflow into a quick-reference PDF you can follow right now.

**[Get the free Remotion + Claude Code Setup Guide →](https://guides.digicuratoragency.com/guides/remotion-claude-code-video-creator)**

---

## What Is Remotion?

Remotion is a framework that lets you build videos using React. Instead of dragging clips on a timeline, you write components — and the video renders from your code. Every frame is a React render. Every animation is a function. That means your videos are version-controlled, reusable, and completely scriptable.

For creators and entrepreneurs, this is a game-changer: you can build video templates once and regenerate them on demand — different captions, different clips, different styles — all from a single codebase.

## Why Claude Code + Antigravity?

Claude Code (running inside Antigravity IDE) is an agentic AI that can write, edit, and execute code in your project. When you point it at a Remotion project, it can:

- Build new video compositions from a description
- Add captions, overlays, and animated text
- Adjust timing, colors, and transitions based on your instructions
- Render the final MP4 using Remotion's CLI

You describe what you want. Claude builds it. You render it. The whole flow — from idea to exported video — can happen in under 10 minutes.

## How to Set Up Remotion in Claude Code

Here's the core setup flow:

**1. Create your Remotion project**

In your terminal, run:

```bash
npx create-video@latest
```

Choose the blank template and give your project a name. This scaffolds the full Remotion setup with a sample composition.

**2. Open the project in Antigravity IDE**

Open Antigravity, point it at your new Remotion folder. Claude Code will scan the project structure and understand the composition setup automatically.

**3. Tell Claude what video to build**

From the Claude Code chat inside Antigravity, describe your video:

> "Add animated captions to this video that fade in with each subtitle line. Use white text, 56px, centered at the bottom of the frame."

Claude writes the component, imports it into your composition, and updates the timeline.

**4. Preview and render**

Run the Remotion preview server:

```bash
npx remotion preview
```

Check it in the browser. Once it looks right, render to MP4:

```bash
npx remotion render MyComposition out/video.mp4
```

That's it. Your animated video is ready to post.

## The Real Power: Skills

Once you've done this once, you can save the entire workflow as a Claude Code skill. A skill is a reusable instruction file that tells Claude Code how to handle a specific task — in this case, generating a Remotion video from a given script and template.

With a skill in place, you don't set anything up manually again. You just run the skill with your new content, and Claude generates the video.

For the full checklist — including the CLAUDE.md setup, folder structure, and skill file template — grab the free guide below.

## What You Can Build

Here's what creators are already using Remotion + Claude Code to produce:

- **Auto-captioned short-form videos** — drop in a transcript, get a captioned reel
- **Animated data visualizations** — render charts and stats as video for reports or social
- **Branded intro/outro templates** — generate platform-specific clips with your logo and colors baked in
- **Batch video generation** — feed a list of topics and render 10 videos at once

The common thread: once it's built as a skill, it runs itself.

## Conclusion

Remotion + Claude Code is one of the most underrated combos in the creator stack right now. You get the flexibility of a fully coded video system with the speed of an AI agent doing the heavy lifting. If you're already using Antigravity IDE, adding Remotion to your skill library is a natural next step.

Grab the free setup guide to get your first Remotion composition running inside Claude Code today — and when you're ready to go further, check out the [YouTube Repurposer system](https://builds.digicuratoragency.com/youtube-repurposer/) for automating your entire video-to-content pipeline.

**[Get the free Remotion + Claude Code Setup Guide →](https://guides.digicuratoragency.com/guides/remotion-claude-code-video-creator)**
