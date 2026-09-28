---
layout: post
title: "Claude Instagram Agent Skill: 16 Free Skills for Instagram"
description: "The Claude Instagram Agent Skill runs your Instagram account with 16 free skills for captions, comments, replies, and a virality skill that clones Reels."
author: ness
categories: [Claude Code, AI Automation]
tags: [claude skills, instagram agent skill, instagram automation, content strategy, claude code]
image: assets/images/claude-instagram-agent-skill-header.jpg
featured: false
---

The Claude Instagram Agent Skill is a free, MIT licensed pack of 16 Claude Skills that writes your Reel scripts, captions, comments, and replies, plans your week, and finds what is already working in your niche, all inside Claude Code. Fifteen of the sixteen skills only write copy for you to review. The sixteenth, `/ig-publish`, is the only one that touches your account, and it posts through Blotato only after you type the word publish.

---

## Get the Free Guide

The full setup walkthrough: where the skill folder goes, the voice profile every skill reads, the API keys two of the skills need, and the commands worth running first.

**[Get the free Instagram Agent Skill Setup Playbook →](https://hub.digicuratoragency.com/freebie?kw=agent)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/jJCscA_06jw"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Does the Claude Instagram Agent Skill Actually Do?

Each of the 16 skills owns one job on an Instagram account, and you call it by name like a slash command inside Claude Code. There is no dashboard and no subscription.

| Command | What it does |
|---|---|
| `/ig-reel` | Writes Reel scripts with three hook options scored from 26 formulas |
| `/ig-caption` | Writes captions with a preview of the 125-character feed cutoff |
| `/ig-carousel` | Designs swipeable posts, cover image and slide copy, 2 to 10 slides |
| `/ig-story` | Plans a daily story sequence with sticker placement and a DM funnel |
| `/ig-profile` | Scores a profile against a 12-part rubric and suggests fixes |
| `/ig-plan` | Builds a weekly content and engagement schedule |
| `/ig-human` | Strips invisible characters and stock phrases, scores authenticity |
| `/ig-comment` | Writes comments for other accounts' posts |
| `/ig-reply` | Sorts and drafts replies to incoming comments by type |
| `/ig-dm` | Drafts DM sequences, opening message and follow-ups |
| `/ig-repurpose` | Turns one video or podcast into a week of Reels and carousels |
| `/ig-audit` | Reviews posted content ranked by performance outlier |
| `/ig-viral` | Finds top-performing Reels in a niche and scores why they worked |
| `/ig-insights` | Pulls hashtag and profile data through Apify for the swipe file |
| `/ig-hashtags` | Picks three to five hashtags, sized niche to broad, with a reason each |
| `/ig-publish` | Posts or schedules through Blotato after you type publish |

Every skill reads one shared file, `templates/voice.md`, so the sixteen drafts sound like the same account instead of like sixteen different writers. Voice matters more here than on text platforms, since a Reel script has to be spoken out loud, not just read.

## How Does the Virality Skill Turn Top Reels Into Your Voice?

`/ig-viral` finds the Reels already outperforming their own account, then rewrites the idea behind them in your voice rather than copying the video. It runs on `swipe.py`, which ranks content by performance multiple over that account's own median instead of raw view count, the same logic behind [the outlier score used to explain why copying viral videos usually fails](https://blog.digicuratoragency.com/outlier-score-why-your-videos-flop/). A video is worth studying because it beat its own channel's normal, not because the number looks big next to yours.

The skill runs at human speed on purpose. The README is direct that no automated scraping happens; `/ig-insights` reads hashtag and profile data through Apify's public actors instead, and it never logs into or touches your account.

Hook scoring inside `/ig-reel` comes with the same honesty about its limits. It was measured at an AUC of 0.56 for separating hits from misses, which the pack describes plainly: nothing that reads text can tell you which of two decent hooks will actually travel. A low score is a reason to look twice. A high score isn't a promise.

## How Do You Install the Claude Instagram Agent Skill?

There are three ways to get the skill folder into Claude Code, all documented in the repo at [github.com/nessalazne/instagram-agent-skill](https://github.com/nessalazne/instagram-agent-skill):

1. **Paste the repo URL into Claude** and ask it to install the skill, then confirm `/ig-reel` works.
2. **Clone it manually** and copy the skill folders into your skills directory:
   ```bash
   git clone https://github.com/nessalazne/instagram-agent-skill.git
   cp -r instagram-agent-skill/skills/ig-* ~/.claude/skills/
   ```
3. **Install it as a plugin**:
   ```
   /plugin marketplace add nessalazne/instagram-agent-skill
   /plugin install instagram-agent
   ```

A fourth option pastes a single skill's `SKILL.md` into a chat as a one-off mode, but that drops the Python tools each skill leans on, which is most of the point.

Copy `templates/voice.md` to `~/.claude/instagram/voice.md` and fill it in, or hand Claude three of your own Reels and let it extract your voice from those. Every one of the 16 skills reads that file before drafting anything, so a blank profile gives generic output across the board.

Two skills need keys. Create `~/.claude/instagram/.env` with `BLOTATO_API_KEY` and `BLOTATO_ACCOUNT_INSTAGRAM` before `/ig-publish` can post anything, and add `APIFY_TOKEN` to the same file before `/ig-insights` can pull hashtag or profile data. The other 14 skills need neither.

## What Are the Limits Worth Knowing Before You Trust It?

The pack states its own limits instead of selling past them, which is worth reading before you build a habit around it.

- **Nothing posts until you say the word.** `/ig-publish` requires explicit confirmation; every other skill only produces a copy-ready draft.
- **The formula classifier names 49% of real hooks.** The rest get abstained from rather than forced into a label that doesn't fit.
- **The hashtag cap moved from 30 to 5 in December 2025.** The README flags that platform numbers like this go stale, so check the live limit before assuming the old ceiling still applies.
- **Captions enforce a hard limit.** `caption.py` lints against Instagram's 2,200-character cap and a five-hashtag maximum, and carousels are checked against a 2 to 10 slide range.
- **Invisible-character detection is not watermark detection.** `/ig-human` strips zero-width spaces and other format characters and scores authenticity across five checks, but the README is clear that this isn't a claim about defeating a cryptographic watermarking scheme.

## Who Is This For?

This fits a creator or a solo agency owner already running an Instagram account who is losing time to the work around each Reel, the caption, the comment replies, the DM follow-ups, rather than the Reel itself. It slots next to the same author's [Claude YouTube Agent Skill](https://blog.digicuratoragency.com/claude-youtube-agent-skill/) and [Claude LinkedIn Agent Skill](https://blog.digicuratoragency.com/claude-linkedin-agent-skill/), and it fits the broader list of [free Claude Skills worth installing by department](https://blog.digicuratoragency.com/free-claude-skills-by-department/) if this is the first one you're adding.

## FAQ

### Is the Claude Instagram Agent Skill free?
Yes. The pack is MIT licensed, so you can use it, change it, or redistribute it without paying anything.

### Does it post to Instagram automatically?
No. Fifteen of the sixteen skills only produce a draft for you to review. `/ig-publish` is the one skill that reaches your account, and it posts or schedules through Blotato only after you type the word publish.

### Do I need an API key to use it?
Only for two skills. `/ig-publish` needs a Blotato API key and account ID, and `/ig-insights` needs an Apify token. The other 14 skills, including `/ig-reel`, `/ig-caption`, and `/ig-viral`, run without any key.

### How does the virality skill find what's working?
`/ig-viral` runs `swipe.py`, which ranks Reels by how far they beat their own account's median rather than by raw view count, then breaks down why the top ones worked before turning the idea into an original script in your voice.

### What's the biggest limit to know before relying on it?
The hook scorer's AUC of 0.56 means it separates clearly bad hooks from good ones well, but it can't reliably pick a winner between two decent options. Treat a high score as a pass, not a guarantee.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is the Claude Instagram Agent Skill free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. The pack is MIT licensed, so you can use it, change it, or redistribute it without paying anything." }
    },
    {
      "@type": "Question",
      "name": "Does it post to Instagram automatically?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Fifteen of the sixteen skills only produce a draft for you to review. /ig-publish is the one skill that reaches your account, and it posts or schedules through Blotato only after you type the word publish." }
    },
    {
      "@type": "Question",
      "name": "Do I need an API key to use it?",
      "acceptedAnswer": { "@type": "Answer", "text": "Only for two skills. /ig-publish needs a Blotato API key and account ID, and /ig-insights needs an Apify token. The other 14 skills, including /ig-reel, /ig-caption, and /ig-viral, run without any key." }
    },
    {
      "@type": "Question",
      "name": "How does the virality skill find what's working?",
      "acceptedAnswer": { "@type": "Answer", "text": "/ig-viral runs swipe.py, which ranks Reels by how far they beat their own account's median rather than by raw view count, then breaks down why the top ones worked before turning the idea into an original script in your voice." }
    },
    {
      "@type": "Question",
      "name": "What's the biggest limit to know before relying on it?",
      "acceptedAnswer": { "@type": "Answer", "text": "The hook scorer's AUC of 0.56 means it separates clearly bad hooks from good ones well, but it can't reliably pick a winner between two decent options. Treat a high score as a pass, not a guarantee." }
    }
  ]
}
</script>

Install the pack, fill in `voice.md`, and run `/ig-viral` on your niche before writing your next script. Seeing which Reels actually beat their own account's normal changes what you make next more than another hook generator will. [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about)
