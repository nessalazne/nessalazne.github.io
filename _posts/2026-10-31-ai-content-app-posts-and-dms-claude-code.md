---
layout: post
title: "AI Content App That Posts and DMs for You (Claude Code)"
description: "Build an AI content app with Claude Code and Antigravity that writes your script and captions for nine platforms. No coding needed, free starter prompt."
author: ness
categories: [Claude Code, AI Automation]
tags: [ai content app, claude code, content engine, antigravity, instagram dm automation]
image: assets/images/ai-content-app-posts-and-dms-claude-code-header.jpg
featured: true
---

You can build an AI content app with Claude Code without writing any code. It is a Chrome extension that takes a viral reel, a blog post or a plain idea and turns it into a short video script in your own brand voice, with a caption for each platform. The full version goes further: it makes the video, posts it to 11 accounts across 9 platforms and sends an automatic DM when someone comments your keyword on Instagram or Facebook. This post walks through the starter version, the one you can build yourself.

---

## Get the Master Prompt

The free starter prompt from this video is the exact prompt that builds the Chrome extension, the local server and the Airtable log in one run.

**[Get the starter prompt →](https://hub.digicuratoragency.com/claim?kw=starterkit)**

---

<div style="max-width: 720px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/chgMF6rEZ_I?start=37"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Does the AI Content App Actually Do?

The app turns one source into a posted short video in a few minutes, a job that used to take days. The post you want to remake has to be open in your browser tab: a blog post, an Instagram reel, a TikTok, a YouTube Short or a long YouTube video. With no post, you type an idea into the box and the idea becomes the video.

In the demo, I pick a HeyGen avatar, open one of my best Instagram reels about LinkedIn and hit generate. The app reads the reel, keeps the hook that already works and rewrites the script for my audience with a call to action of its own. Then it stops so I can check the script before anything is spent on the voice or the video. After I approve, the full version writes a caption for every platform, makes the voiceover in my cloned voice, makes the talking head, posts everywhere and turns on the Instagram and Facebook DM automations.

My Facebook business page was dead for more than three years. After I started posting educational reels from this tool consistently, the last 28 days showed over 680,000 views (up 473%) and over 6,000 new follows (up 836%). These are numbers from my own accounts, so treat them as one example, not a promise.

## What Do You Need Before You Build?

You need three free or cheap accounts and one paid plan, and Claude Code is the only paid requirement. Prices are as of October 2026.

| Tool | Role | Cost |
|---|---|---|
| Antigravity | The IDE where you build and see every file | Free for individuals |
| Claude plan with Claude Code | The builder | Pro is $20 a month ($17 on the yearly plan), Max starts at $100 |
| OpenRouter | One key for Claude and hundreds of other models | Pay as you go, a script plus nine captions costs a few cents |
| Airtable | Saves each script and its captions | Free plan: 1,000 records per base |

Two things confuse almost everyone. The Claude desktop app has three modes (Chat, Cowork and Code), and Code is the one you want. And this project has two extensions: the Claude Code extension lives inside Antigravity and does the building, while the Chrome extension is the app you are building.

## How Do You Build the Starter Version?

The starter build takes five steps, and Claude does the coding.

1. **Install Antigravity** from antigravity.google and close its built-in agent panel, because you are adding Claude Code instead.
2. **Add Claude Code.** Search "Claude Code" in Extensions, install the official one from Anthropic and sign in. No API key is needed here.
3. **Pick a mode and a model.** If you are new, start in Plan mode, then Manual, then Edit automatically once you trust it. Use the strongest model you have for the first build, such as Fable 5.1 or Opus 5.5, and Sonnet 5.5 for small fixes.
4. **Make a new empty folder** and open it in Antigravity. Empty matters because Claude builds everything from nothing.
5. **Paste the [starter prompt](https://hub.digicuratoragency.com/claim?kw=starterkit)** and let it run.

In the video I use bypass permissions, which skips every question. I only do that because I wrote the prompt myself and the folder is empty. Do not use it on your own projects. For more on the project memory file the build creates, see [this post on claude.md rules](https://blog.digicuratoragency.com/claude-opus-5-5-usage-limits-claude-md-config/).

## What Does the Starter Prompt Build?

The prompt builds a Chrome extension, a small server on your computer and a project memory file called `CLAUDE.md`. You type an idea into the extension, and the server sends it to Claude together with your brand voice. Claude writes a 50-second script with a hook, the value and a call to action with a comment keyword. You can edit the script, then it writes captions for nine platforms, each with a copy button.

Two parts of the prompt do most of the work. The brand file describes how you talk and who you talk to, and Claude reads it for every script. The caption rules set a length limit per platform, so a Bluesky caption never gets cut off. The last line of the prompt is "Ask no questions, build everything." Without it, Claude stops every few minutes to check in.

## How Do You Set Up the .env File and API Keys?

A `.env` file is a private vault for your keys, and an API key is just a password that lets your app use a service. Set it up in five steps:

1. **OpenRouter:** add $10 in credits, create a key named "content engine starter" with a spending limit, and copy it right away because you only see it once.
2. **Airtable base:** create a table called `posts` with the fields `idea`, `script`, `keyword` and `captions`.
3. **Airtable token:** create a personal access token with data records read and write, limited to this one base.
4. **Base ID:** copy the part of your base's web address that starts with `app`.
5. **Rename the file** from `.env.example` to `.env`. People miss this one all the time, and the app only reads the file called `.env`.

Then describe your voice in the brand file in plain English. Mine says short sentences, talk straight to the viewer, no hype words.

## What Happens When Something Breaks?

You paste the error into Claude Code and ask it to fix it. In the demo, saving to Airtable fails with "Unknown field name". I copy the error, paste it in and Claude Code finds and fixes the mismatch. On the next try the idea, script, keyword and every caption show up in Airtable. That loop of build, test and iterate is the whole vibe coding workflow.

## How Is the Starter Different From the Full Content Engine?

The starter gives you the words, and the full Content Engine turns them into a posted video. The full version also reads any link, makes the voiceover and the talking head, posts to 11 accounts and runs the Instagram and Facebook comment-to-DM automation. It will not post the same video twice if a run times out, it picks up from the step that failed, and it spends nothing on the voice or video until you approve the script.

For posting, the full app uses Blotato or Zernio. Zernio is free for your first two accounts and $6 per account after that, and the DM automation works on those free accounts too. Blotato is $29 a month, so it gets cheaper past six accounts.

## FAQ

### Do I need to know how to code to build this?

No. Claude Code writes the extension and the server from the starter prompt. Your jobs are to install the tools, paste in your keys and fix errors by pasting them back into Claude Code.

### How much does the starter version cost to run?

Antigravity is free for individuals and Airtable has a free plan. Claude Code needs a paid Claude plan, starting at $20 a month as of October 2026. OpenRouter credits start at $10, and one script plus nine captions costs a few cents.

### What is the difference between the Chrome extension and the Claude Code extension?

The Claude Code extension lives inside Antigravity and does the building. The Chrome extension is the app you are building, and it lives in your browser where you type an idea and get a script.

## Build the Starter, Then Decide on the Full App

The starter version is real and it proves the idea: one prompt, a few keys and you have a Chrome extension that writes scripts and captions in your voice. If you want the posted video and the DM automation already working, the full app has the hard parts worked out. It comes with the complete source code, an Airtable base with every field the extension needs, a setup walkthrough and help when you get stuck. [Meet Content Engine →](https://builds.digicuratoragency.com/content-engine/)

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Do I need to know how to code to build this?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Claude Code writes the extension and the server from the starter prompt. Your jobs are to install the tools, paste in your keys and fix errors by pasting them back into Claude Code." }
    },
    {
      "@type": "Question",
      "name": "How much does the starter version cost to run?",
      "acceptedAnswer": { "@type": "Answer", "text": "Antigravity is free for individuals and Airtable has a free plan. Claude Code needs a paid Claude plan, starting at $20 a month as of October 2026. OpenRouter credits start at $10, and one script plus nine captions costs a few cents." }
    },
    {
      "@type": "Question",
      "name": "What is the difference between the Chrome extension and the Claude Code extension?",
      "acceptedAnswer": { "@type": "Answer", "text": "The Claude Code extension lives inside Antigravity and does the building. The Chrome extension is the app you are building, and it lives in your browser where you type an idea and get a script." }
    }
  ]
}
</script>
