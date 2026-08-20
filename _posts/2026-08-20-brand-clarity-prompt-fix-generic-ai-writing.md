---
layout: post
title: "Brand Clarity Prompt: Fix Generic AI Writing"
description: "Generic AI writing is a missing-context problem, not a prompting problem. This brand clarity prompt turns six answers into a profile every tool can read."
author: ness
categories: [Claude Code, AI Automation]
tags: [brand clarity prompt, ai brand voice, content pillars, claude code, brand profile]
image: assets/images/brand-clarity-prompt-fix-generic-ai-writing-header.jpg
featured: true
---

Generic AI writing is not a prompting problem. It is a missing-context problem: the tool hands everyone the same voice because it has no idea who you are. A brand clarity prompt fixes that by turning six honest answers about your business into a structured brand profile — positioning, tagline, archetype, a real tone-of-voice guide, five content pillars with twenty-five topics, and your actual hex codes — that every AI tool you touch can read before it writes a single word.

---

## Get the Master Prompt

The full six-question master prompt from this video, plus the rest of the skills library, is free inside the community.

**[Grab the master prompt and skills →](https://hub.digicuratoragency.com/welcome)**

---

<div style="max-width: 720px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/RyycyiRoFT8"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## Why Does Every AI Tool Sound the Same?

Every AI writing tool produces the same voice because it is working with the same information about you: none. You paste in your idea, you get back something technically correct and completely forgettable, and you cannot work out why, because your prompt was fine.

Your prompt probably *was* fine. The model simply had nothing specific to be specific about, so it fell back on the average of everything it has ever read. That average is what "generic" actually is. No amount of clever phrasing fixes a context gap — you have to close the gap.

## What Are the Six Questions in a Brand Clarity Prompt?

The prompt asks six questions, and four of them are the Ikigai square:

1. **What do you love?**
2. **What are you good at?**
3. **What is the world getting wrong?**
4. **What would someone actually pay you for?**

Most branding exercises stop right there, and that is exactly why they produce something that sounds nice and describes nobody. So the prompt adds two more:

5. **Who specifically are you building for?** Not "everyone" — a person.
6. **What makes your approach different** from the other thousand people doing this?

Those last two are what stop the output being interchangeable. Questions one to four describe a category. Questions five and six describe you.

## What Should the Prompt Return?

The prompt does not ask for "a brand profile" — it specifies the exact JSON structure it wants back, with every field named. That shape is the real lesson, and it is worth stealing even if you never use this particular prompt.

The profile it returns includes:

| Field | What it gives you |
|---|---|
| Positioning | One sentence on who you help and how |
| Tagline | A line you can actually put on a site |
| Archetype | The brand character your voice ladders up to |
| Tone of voice | Sentence length, how you open, what you never say |
| Content pillars | Five pillars, five topics each — twenty-five topics |
| Colours | Real hex codes, not colour names |
| Clarity score | How usable your answers actually were |
| Gaps | Where your answers were too thin to build on |

"Five pillars, five topics each, no negotiation" gets you a usable content calendar. "Give me some content ideas" gets you a paragraph of encouragement. Same model, different instruction. If you are new to directing AI this precisely, [Claude Code for non-developers](https://blog.digicuratoragency.com/claude-code-for-non-developers/) covers the mindset shift.

## Which Two Rules Do the Most Work?

Two lines in the prompt carry most of the weight, and both are about constraint rather than creativity.

**The banned-words list.** Every model defaults to *empower*, *unlock* and *elevate*. Ban them explicitly and the model has to reach for something that means an actual thing. Skip this and you end up sounding like a LinkedIn post no matter how good your answers were.

**The `gaps` section.** This gives the model permission to tell you your answers were thin, instead of inventing confidence you have not earned. Most prompts implicitly demand a polished result, so the model fabricates certainty to comply. A named `gaps` field makes honesty the compliant answer. If you only steal one thing from this prompt, steal that.

## Where Should Your Brand Profile Live?

A brand profile only works if something reads it automatically, before it writes. This is the part people get backwards.

This is not a branding worksheet. If the answer ends up in a PDF, you will never open it again and nothing changes. It has to sit somewhere your content engine reaches for by default — a file your AI tool loads with every session, a project instruction, or a database row that every other system queries. The same logic applies to any reusable instruction set, which is why [building Claude skills by department](https://blog.digicuratoragency.com/free-claude-skills-by-department/) works the way it does: the context lives with the tool, not in a folder you mean to check.

Run the prompt properly once, with real answers rather than placeholders, and every AI tool you touch afterwards gets better the moment that profile exists.

## FAQ

### Do I need Claude Code to run a brand clarity prompt?

No. The prompt is just text — paste it into whatever AI chat tool you already use and it works. Claude Code matters when you want the profile stored somewhere your other systems read from automatically.

### How long does the brand clarity prompt take to run?

Answering the six questions honestly takes about twenty minutes. The prompt itself returns the full profile in one pass. The slow part is you, not the model, and rushing the answers is what produces a low clarity score.

### Why does the prompt ask for JSON instead of a written report?

A named structure forces the model to fill every field rather than writing around the ones it finds hard. It also means the output can be read by another program later, instead of only by you.

### What if my answers are vague?

That is what the `gaps` section is for. The model tells you which answers were too thin to build on, and you rerun those. A profile built on vague answers produces vague content, so it is better to be told early.

## One Prompt, Then Everything Downstream

Generic AI writing is a context problem, and a brand clarity prompt is the cheapest fix available. Six honest answers produce a profile with your positioning, tagline, archetype, tone of voice, twenty-five content topics and real hex codes — and every tool that reads it stops sounding like everyone else.

The prompt gives you a document, and a document works. But you will be pasting it into every prompt by hand, forever. Inside GrowthOS, Brand Clarity is system number one, and the other fourteen systems read from it automatically before they generate anything. [Get GrowthOS →](https://builds.digicuratoragency.com/growth-os/) and own the whole stack instead of renting it.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Do I need Claude Code to run a brand clarity prompt?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. The prompt is just text — paste it into whatever AI chat tool you already use and it works. Claude Code matters when you want the profile stored somewhere your other systems read from automatically." }
    },
    {
      "@type": "Question",
      "name": "How long does the brand clarity prompt take to run?",
      "acceptedAnswer": { "@type": "Answer", "text": "Answering the six questions honestly takes about twenty minutes. The prompt itself returns the full profile in one pass. The slow part is you, not the model, and rushing the answers is what produces a low clarity score." }
    },
    {
      "@type": "Question",
      "name": "Why does the prompt ask for JSON instead of a written report?",
      "acceptedAnswer": { "@type": "Answer", "text": "A named structure forces the model to fill every field rather than writing around the ones it finds hard. It also means the output can be read by another program later, instead of only by you." }
    },
    {
      "@type": "Question",
      "name": "What if my answers are vague?",
      "acceptedAnswer": { "@type": "Answer", "text": "That is what the gaps section is for. The model tells you which answers were too thin to build on, and you rerun those. A profile built on vague answers produces vague content, so it is better to be told early." }
    }
  ]
}
</script>
