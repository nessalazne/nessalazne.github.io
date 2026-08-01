---
layout: post
title: "45+ Free Claude Skills for Every Business Department"
description: "Claude Skills give solo founders a free staff — 45+ marketing, social, design, finance, and legal skill packs you can install and customize today."
author: ness
categories: [Claude Code, AI Automation]
tags: [claude skills, ai automation, solopreneur, free ai tools, claude code]
image: assets/images/free-claude-skills-by-department-header.jpg
featured: false
---

Claude Skills are free markdown files that hand Claude specialized instructions for one job — marketing, social media, design, finance, or legal — so a general AI agent starts acting like a department specialist. As of July 2026, community and Anthropic-maintained skill packs cover 45 marketing skills, 17 social media skills, two design packs, eight finance skills, and nine legal skills, and every one of them installs into Claude Code for zero dollars. If you're running a business solo, stacking these is the closest thing to hiring a full staff without touching payroll.

---

## Get the Free Guide

Get the full download list — every repo, every starter skill, and exactly how to customize each one for your business.

**[Get the free Claude Skills Directory →](https://hub.digicuratoragency.com/freebie?kw=skills)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/Fkwh11OoJZE"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is a Claude Skill, Exactly?

A Claude Skill is a folder containing a `SKILL.md` file plus any supporting scripts or reference docs — instructions Claude reads before it works on a specific type of task. Unlike a one-off prompt you retype every session, a skill is a permanent installation: drop the folder into `~/.claude/skills/` for personal use, or into a project's own `.claude/skills/` folder to scope it to that codebase, and Claude Code picks it up automatically. The folder name becomes the command you type to invoke it, and some packs — like Anthropic's finance and legal plugins — use a namespaced format such as `/finance:financial-statements`.

## Which Free Claude Skill Packs Cover Every Department?

Five skill packs, most maintained by third-party creators and two built by Anthropic itself, cover the departments a solo business actually needs:

| Department | Skills | Source | Best Starter Skill |
|---|---|---|---|
| Marketing | 45 | `coreyhaines31/marketingskills` | `copywriting` |
| Social Media | 17 | `charlie947/social-media-skills` | `voice-builder` |
| Design | 2 packs | Community (UI/UX + general taste) | Brand-token setup |
| Finance | 8 | Anthropic `knowledge-work-plugins` | `financial-statements` |
| Legal | 9 | Anthropic `knowledge-work-plugins` | `review-contract` |

Marketing's pack alone spans ad-creative variations, conversion-rate-optimization analysis, and full copywriting for landing pages and email. The social pack's `voice-builder` skill interviews you about your brand and writes reference files that every other skill in the pack reads from — run that one first. Finance and legal both ship from Anthropic directly, so they're built to the same maintenance standard as Claude Code itself.

## How Do You Install and Customize a Claude Skill?

Installing a skill takes three steps: copy the skill folder into your `~/.claude/skills/` directory (or your project's `.claude/skills/`), note the folder name — that's your command — and then open the `SKILL.md` file to see what it expects from you. That third step is the one people skip, and it's the one that matters most.

Each department needs a different kind of customization:

- **Marketing:** brand voice, pricing, and customer profiles
- **Social Media:** hook style, platform format, and preferred video length
- **Design:** brand tokens — hex codes, fonts, spacing, and corner-radius values
- **Finance:** your chart of accounts, fiscal calendar, and reporting format
- **Legal:** your jurisdiction and a contract playbook of accepted, negotiable, and rejected terms

You don't have to write any of this by hand. Open Claude Code, point it at the `SKILL.md` file, and describe your business — Claude can draft the customization for you while you act as editor rather than author.

## Why Do Most People Never Get Value From Free Skills?

Most people download a skill pack, run it once out of the box, and conclude it's "generic." An uncustomized skill behaves exactly like a new hire on day one — technically capable, but blind to your brand voice, your numbers, and your risk tolerance. The gap between a skill that feels generic and one that feels like it's read every document in your business is almost always five or ten minutes of customization, not a better skill pack.

For the full download list and a customization checklist per department, [grab the free guide](https://hub.digicuratoragency.com/freebie?kw=skills).

## Where Do You Find These Skill Packs?

All five packs referenced here are public GitHub repositories, which means you can inspect exactly what a skill does before you install it:

1. **Marketing** — `coreyhaines31/marketingskills`
2. **Social Media** — `charlie947/social-media-skills`
3. **Design** — community UI/UX and taste-focused packs (search "claude skills design" on GitHub for current forks)
4. **Finance** — `anthropics/knowledge-work-plugins`
5. **Legal** — `anthropics/knowledge-work-plugins`

Because Finance and Legal come straight from Anthropic, they're the two packs most likely to stay current as Claude Code's skill format evolves. For the community packs, check the repo's last commit date before installing — an actively maintained pack gets bug fixes and new skills; an abandoned one just accumulates stale instructions.

If you're new to Claude Code entirely, start with [5 Claude Code Skills Every Creator Needs Right Now](https://blog.digicuratoragency.com/5-skills-for-creators-claude-code/) before working through department-specific packs, and see [5 Claude Code Skills You Can Use in a Real Project Right Now](https://blog.digicuratoragency.com/claude-code-5-skills-project/) for a hands-on install walkthrough.

## FAQ

### What is a Claude Skill?

A Claude Skill is a folder — usually just a `SKILL.md` file plus optional scripts — that gives Claude specialized instructions and knowledge for one type of task. It installs once and stays active every time you invoke it, unlike a prompt you'd retype each session.

### Are Claude Skills really free?

Yes. The packs referenced in this guide — marketing, social media, design, finance, and legal — are all free, open-source repositories on GitHub, including the two built directly by Anthropic.

### Do I need to know how to code to use Claude Skills?

No. Installing a skill is copying a folder into `~/.claude/skills/`. Customizing one is mostly plain-English editing of a markdown file, and you can have Claude Code do that editing for you if you describe your business.

### How do I customize a Claude Skill for my business?

Open the skill's `SKILL.md` file and fill in the specifics it asks for — brand voice for marketing, hook style for social, brand tokens for design, your chart of accounts for finance, your jurisdiction for legal. Claude Code can draft this customization interactively if you'd rather talk it through than write it yourself.

### Where can I find more Claude Skills?

Beyond the five packs in this guide, search GitHub for "claude skills" plus your department or niche — new packs ship regularly, and Anthropic's own `knowledge-work-plugins` repository is a good source to watch for official additions.

---

Free skill packs get you the raw capability; a system that installs, customizes, and actually runs them is what turns that capability into hours back in your week. If you want help building that system end to end, [join the Vibe Coding Build →](https://hub.digicuratoragency.com/about) — that's exactly what we do inside Vibe Coding Mastery.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is a Claude Skill?",
      "acceptedAnswer": { "@type": "Answer", "text": "A Claude Skill is a folder — usually just a SKILL.md file plus optional scripts — that gives Claude specialized instructions and knowledge for one type of task. It installs once and stays active every time you invoke it, unlike a prompt you'd retype each session." }
    },
    {
      "@type": "Question",
      "name": "Are Claude Skills really free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. The packs referenced in this guide — marketing, social media, design, finance, and legal — are all free, open-source repositories on GitHub, including the two built directly by Anthropic." }
    },
    {
      "@type": "Question",
      "name": "Do I need to know how to code to use Claude Skills?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Installing a skill is copying a folder into ~/.claude/skills/. Customizing one is mostly plain-English editing of a markdown file, and you can have Claude Code do that editing for you if you describe your business." }
    },
    {
      "@type": "Question",
      "name": "How do I customize a Claude Skill for my business?",
      "acceptedAnswer": { "@type": "Answer", "text": "Open the skill's SKILL.md file and fill in the specifics it asks for — brand voice for marketing, hook style for social, brand tokens for design, your chart of accounts for finance, your jurisdiction for legal. Claude Code can draft this customization interactively if you'd rather talk it through than write it yourself." }
    },
    {
      "@type": "Question",
      "name": "Where can I find more Claude Skills?",
      "acceptedAnswer": { "@type": "Answer", "text": "Beyond the five packs in this guide, search GitHub for \"claude skills\" plus your department or niche — new packs ship regularly, and Anthropic's own knowledge-work-plugins repository is a good source to watch for official additions." }
    }
  ]
}
</script>
