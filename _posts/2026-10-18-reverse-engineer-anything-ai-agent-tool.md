---
layout: post
title: "REA: Reverse Engineer Any App Feature With AI"
description: "REA is an open-source MCP server that lets Claude Code study any app feature with no source code and rebuild a working version in one session."
author: ness
categories: [Claude Code, AI Automation]
tags: [rea, reverse engineering, claude code, mcp server, open source tools]
image: assets/images/reverse-engineer-anything-ai-agent-tool-header.jpg
featured: false
---

REA, short for Reverse Engineer Anything, is an open-source MCP server that lets Claude Code and other AI agents study an app feature with no source code and build a working version of it. You point the agent at the feature, it inspects the binary, JavaScript, or network traffic, and it hands back notes, evidence, and working code.

---

## Get the Free Guide

I put together the full setup playbook, every command and prompt I use with REA, in one PDF.

**[Get the free REA Setup Playbook →](https://hub.digicuratoragency.com/freebie?kw=decode)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/2m_ElxKSVA4"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

Builders have always copied what works. What changed is speed. A dev team used to spend months tracing how a feature worked before they could rebuild it. An agent running REA does the same tracing in a single session, because it can read the binary and the runtime behavior directly instead of guessing from the outside.

## What Does REA Actually Do?

REA connects your AI agent to a set of analysis tools that inspect code, binaries, and runtime behavior on your own machine, nothing is sent to a remote service. It was built to analyze a wide range of formats: native binaries (ELF, PE, Mach-O), JavaScript and Electron applications, .NET assemblies, Android APKs, websites and network captures, firmware images, SQLite databases, Go and Rust binaries, and WASM artifacts.

Once it's connected, the agent can:

- Investigate how a feature behaves with no access to its source code
- Trace the path from high-level behavior down to the actual binary instructions
- Generate pseudocode and assembly analysis of what it finds
- Map how different modules and files relate to each other
- Return its findings with the evidence attached, not just a guess

That last point matters. The agent doesn't just say "this is how it probably works." It shows you the trace it followed to get there.

## How Do You Set Up REA in Claude Code?

Setup is one command, because REA ships its own installer. Run this from your terminal:

```bash
npx rea-agents setup
```

That registers REA as an MCP server with your coding agent and installs its workflow instructions. The installer supports Claude Code, Codex, Cursor, Gemini CLI, and Grok Build, so it detects whichever one you're running.

If you'd rather have the CLI installed globally instead of calling it through `npx` each time:

```bash
npm install --global rea-agents
```

And to pull the latest version later:

```bash
rea update
```

| Requirement | Version |
|---|---|
| Node.js | 22.x (≥22.19), 24.x (≥24.11), or 26+ |
| npm | Any current version |
| Linux only | A `procps`-compatible `ps` for process checks |
| Optional | Hopper, Ghidra, IDA, or another decompiler for native binary work |

The optional decompilers are only needed if you're analyzing native binaries. For JavaScript apps, websites, or Electron apps, REA's built-in tools handle the whole trace on their own.

## What Do You Actually Say to the Agent?

Once REA is registered, you talk to your agent the same way you always do, you just point it at a feature instead of a file. The project's own example is a good template:

> Understand how search works in the Notes app, show me the evidence, and build a similar feature for my project.

The agent then picks the right analysis tool for the target. For a JavaScript or Electron app, it can run REA's own analyzer directly from the terminal:

```bash
npx -y rea-agents@latest analyze-javascript-application /absolute/path/to/app --json
```

That returns structured JSON the agent reads back in, which is why the whole workflow stays inside your normal Claude Code session instead of bouncing you out to a separate decompiler GUI.

## Where Does This Actually Help a Solo Builder?

The practical case for a solo builder is catching up on features fast. If a competitor's app has a smooth onboarding flow, a clever search ranking, or a sync mechanism you can't figure out from the outside, REA gives your agent a way to study the actual implementation instead of you reverse-engineering it by hand through screen recordings and guesswork.

It's the same instinct behind [recreating a viral video's structure with AI](https://blog.digicuratoragency.com/reverse-engineer-viral-videos-ai/): you're not copying the content, you're studying the mechanism so you can build your own version faster. REA just moves that instinct from video structure to software structure.

If you're already running a Claude Code setup with other MCP servers and skills installed, REA slots in the same way [Agent Reach gives Claude Code live web access](https://blog.digicuratoragency.com/agent-reach-free-ai-web-scraping-claude/): one more capability your agent can reach for mid-session, no separate app to tab into.

## FAQ

### Does REA need the source code of the app I'm studying?

No. REA is built specifically for cases where you don't have source code. It analyzes the compiled binary, the JavaScript bundle, or the running network traffic directly.

### Which AI coding agents does REA work with?

The setup installer supports Claude Code, Codex, Cursor, Gemini CLI, and Grok Build. It detects your agent and installs the right configuration automatically.

### Is REA free and open source?

Yes. REA is released under the MIT license. Some optional third-party decompilers it can call into, like IDA, Hopper, or JEB, require their own separate licenses if you choose to use them.

### What happens to the code and binaries I analyze?

REA's analysis tools run locally on your machine. Nothing is sent to a remote server as part of the tracing process.

### Can REA analyze a whole website, not just an app?

Yes. Websites and network captures are listed among its supported analysis targets, alongside native binaries, Android APKs, and several other formats.

## Ready to Build With This?

REA is one more tool in the growing kit of things a Claude Code agent can reach for without you writing a single line of analysis code yourself. If you want the full command list, the exact setup steps, and the fix table for the errors people actually hit, grab the playbook above. And if you want to go deeper on running an AI agent system like this day to day, [join the Vibe Coding Build →](https://hub.digicuratoragency.com/about).

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Does REA need the source code of the app I'm studying?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. REA is built specifically for cases where you don't have source code. It analyzes the compiled binary, the JavaScript bundle, or the running network traffic directly." }
    },
    {
      "@type": "Question",
      "name": "Which AI coding agents does REA work with?",
      "acceptedAnswer": { "@type": "Answer", "text": "The setup installer supports Claude Code, Codex, Cursor, Gemini CLI, and Grok Build. It detects your agent and installs the right configuration automatically." }
    },
    {
      "@type": "Question",
      "name": "Is REA free and open source?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. REA is released under the MIT license. Some optional third-party decompilers it can call into, like IDA, Hopper, or JEB, require their own separate licenses if you choose to use them." }
    },
    {
      "@type": "Question",
      "name": "What happens to the code and binaries I analyze?",
      "acceptedAnswer": { "@type": "Answer", "text": "REA's analysis tools run locally on your machine. Nothing is sent to a remote server as part of the tracing process." }
    },
    {
      "@type": "Question",
      "name": "Can REA analyze a whole website, not just an app?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. Websites and network captures are listed among its supported analysis targets, alongside native binaries, Android APKs, and several other formats." }
    }
  ]
}
</script>
