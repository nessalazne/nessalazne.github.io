---
layout: post
title: "Claude Fable 5.1 System Prompt Leak: What 275K Chars Reveal"
description: "Anthropic's full Claude Fable 5.1 system prompt is on public GitHub. Here is what the 275K-character file contains and how to study its tool rules."
author: ness
categories: [Claude Code, AI Automation]
tags: [claude fable, system prompt, prompt engineering, anthropic, claude code]
image: assets/images/claude-fable-5-1-system-prompt-leak-header.jpg
featured: false
---

The full Claude Fable 5.1 system prompt leaked in September 2026 and is sitting in a public GitHub repository right now. It runs past 275,000 characters and roughly 8,000 lines, and it holds the exact instructions Anthropic uses to control how Claude thinks, plans, picks tools, and finishes work. If you build AI systems into your workflow, it is the clearest look you will get at how a frontier lab writes a prompt.

---

## Get the Free Guide

The guide walks you through cloning the repo, reading the file in Claude Code without blowing your context, and the exact prompts I use to pull out the tool-definition pattern so you can reuse it in your own skills.

**[Get the free Claude Fable 5.1 System Prompt Study Guide →](https://hub.digicuratoragency.com/freebie?kw=fable)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/eYMr_RycHxk"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Exactly Leaked From Claude Fable 5.1?

The leak is the complete system prompt for Claude Fable 5.1 on claude.ai, including every tool definition, published in the [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) repository on September 1, 2026. The file lives at `Anthropic/claude-fable-5.1.md`, and the same repo added the Claude Code version of the Fable 5.1 prompt the same day and a headless Claude Code variant on September 5, 2026.

This is not a screenshot pieced together from a forum. The repo keeps verbatim captures of ChatGPT, Gemini, Grok, Perplexity, Codex and most other major assistants, and it was the source for a Washington Post interactive on hidden AI rules in May 2026. The Anthropic folder alone holds prompts for Claude Opus 5, Claude Sonnet 5, Claude Science, Claude in Chrome, Claude for Excel and the older Fable 5 file, which I covered in July in [the first Fable 5 system prompt leak](https://blog.digicuratoragency.com/fable-5-leaked-system-prompt/).

The video quotes the size at over 275,000 characters. When I pulled the raw file on September 12, 2026 it measured about 413,000 characters across 7,810 lines, so the exact count depends on when it was captured. Either way, it is longer than most novellas.

## How Is the Prompt Structured?

The prompt is organised into named top-level sections, and the section names alone tell you what Anthropic thinks a model needs to be told. As of the September 12, 2026 copy, the top-level headings are:

| Section | What it covers |
|---|---|
| `claude_behavior` | Product info, refusal handling, tone and formatting, user wellbeing, evenhandedness, knowledge cutoff |
| `memory_filesystem` | What gets remembered, the file format, where it goes, when to write |
| `persistent_storage_for_artifacts` | The storage API artifacts can use, with usage examples and limits |
| `mcp_app_suggestions` | When to suggest a connector and when to call a third-party tool directly |
| `computer_use` | Skills, file handling rules, producing outputs, when to build an artifact |
| `request_evaluation_checklist` | A four-step decision tree run before any visual output |
| `search_instructions` | When to search, how to phrase queries, copyright limits |
| `Tools` | 97 tool definitions, from `bash_tool` to Gmail, Google Calendar and Google Drive connectors |
| `anthropic_api_in_artifacts` | How artifacts call the Claude API, structured outputs, error handling |

The behavioural sections read like an engineering spec rather than a personality note. A few concrete rules from the file: Claude avoids the words "genuinely", "honestly" and "straightforward" because they come off as disingenuous; it never uses bullet points when declining a task; and after its last tool call in a turn it must state the actual answer, because "a sign-off alone, such as 'Done.', is not a reply."

## How Does Anthropic Define a Tool?

Every one of the 97 tools follows the same three-part pattern: a name, a plain-language description of when to use it and when not to, and a JSON schema with typed parameters and a `required` list. That pattern is the most reusable thing in the whole file for anyone writing Claude Code skills or agent tool sets.

Take `bash_tool`. The description is one line: "Run a bash command in the container." The schema has two required fields, `command` and `description`, and the `description` field is defined as "Why I'm running this command." Anthropic forces the model to justify every shell command as part of the call itself.

`create_file` goes further. Its parameter titles say "ALWAYS PROVIDE THIS PARAMETER FIRST" on the description, "SECOND" on the path and "LAST" on the file text, so the model states why it is creating the file before it writes the content. `web_fetch` carries a restriction most people never see: it can only fetch URLs that already appeared in the conversation, so a URL recalled from training gets rejected.

If you want the compressed version of this for your own skills, my [Prompt Master Claude skill post](https://blog.digicuratoragency.com/prompt-master-claude-skill/) covers how I package rules like these so they load once instead of every turn.

## What Can You Actually Learn From It?

The practical value is in the decision rules, because they show how Anthropic sequences choices instead of leaving them to vibes. Three examples worth copying into your own systems:

1. **Ordered checklists that stop at the first match.** The `request_evaluation_checklist` runs Step 0 (does this need a visual at all?), then Step 1 (is a connected MCP tool a fit?), then Step 2 (did the person ask for a file?), then Step 3 (use the inline visualizer). The model is told not to narrate which branch it took.
2. **Search discipline with numbers.** Queries should be one to six words. Simple factual questions get exactly one search. Copyright limits are hard-coded: 15 or more words quoted from a single source is a violation and each source gets one quote maximum.
3. **Memory handled by a background pass.** The prompt tells Claude not to file memories mid-conversation. A separate pass re-reads the finished exchange and files what is durable, unless the user explicitly asks it to remember or forget something in the turn.

If you read my post on [why Fable 5.1 gets cheaper at scale](https://blog.digicuratoragency.com/claude-fable-5-1-cheaper-at-scale/), this file is the instruction layer underneath the behaviour I described there. Reading the source is different from guessing at it.

## FAQ

### Where is the leaked Claude Fable 5.1 system prompt?

It is in the public GitHub repository asgeirtj/system_prompts_leaks, in the file Anthropic/claude-fable-5.1.md, added on September 1, 2026. The repo also holds the Claude Code and headless Claude Code prompts for Fable 5.1.

### How long is the Claude Fable 5.1 system prompt?

The video quotes over 275,000 characters and around 8,000 lines. The raw file pulled on September 12, 2026 measures about 413,000 characters across 7,810 lines, including 97 tool definitions.

### Is it legal to read a leaked system prompt?

The repository is public and outlets like The Washington Post have built stories on it, so reading and studying it is common practice. Reusing it verbatim in a commercial product is a judgement call to make with your own advisor.

### Can I use the leaked prompt in Claude Code?

Yes, as study material. Clone the repo, open Claude Code in the folder, and ask it to extract the tool-definition pattern or the decision checklists into a SKILL.md you control. The free guide above has the exact prompts.

### Does the leak apply to the Claude API or only claude.ai?

The file is the claude.ai system prompt for web, desktop and mobile. The API ships with no default system prompt, and Claude Code has its own prompt, which the same repo also holds.

## Conclusion

The Claude Fable 5.1 system prompt leak is the best free prompt engineering textbook available in September 2026: named sections, ordered decision rules, and 97 tool definitions that all follow one repeatable pattern. Grab the free guide above for the clone steps and the study prompts. If you want to build full agent systems with rules like these, [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about).

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Where is the leaked Claude Fable 5.1 system prompt?",
      "acceptedAnswer": { "@type": "Answer", "text": "It is in the public GitHub repository asgeirtj/system_prompts_leaks, in the file Anthropic/claude-fable-5.1.md, added on September 1, 2026. The repo also holds the Claude Code and headless Claude Code prompts for Fable 5.1." }
    },
    {
      "@type": "Question",
      "name": "How long is the Claude Fable 5.1 system prompt?",
      "acceptedAnswer": { "@type": "Answer", "text": "The video quotes over 275,000 characters and around 8,000 lines. The raw file pulled on September 12, 2026 measures about 413,000 characters across 7,810 lines, including 97 tool definitions." }
    },
    {
      "@type": "Question",
      "name": "Is it legal to read a leaked system prompt?",
      "acceptedAnswer": { "@type": "Answer", "text": "The repository is public and outlets like The Washington Post have built stories on it, so reading and studying it is common practice. Reusing it verbatim in a commercial product is a judgement call to make with your own advisor." }
    },
    {
      "@type": "Question",
      "name": "Can I use the leaked prompt in Claude Code?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes, as study material. Clone the repo, open Claude Code in the folder, and ask it to extract the tool-definition pattern or the decision checklists into a SKILL.md you control. The free guide above has the exact prompts." }
    },
    {
      "@type": "Question",
      "name": "Does the leak apply to the Claude API or only claude.ai?",
      "acceptedAnswer": { "@type": "Answer", "text": "The file is the claude.ai system prompt for web, desktop and mobile. The API ships with no default system prompt, and Claude Code has its own prompt, which the same repo also holds." }
    }
  ]
}
</script>
