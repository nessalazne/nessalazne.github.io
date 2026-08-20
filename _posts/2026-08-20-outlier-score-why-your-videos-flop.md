---
layout: post
title: "The Outlier Score: Why Copying Viral Videos Fails"
description: "Raw views lie. The outlier score divides a video's views by its channel's 90-day average, so you copy real breakouts instead of expensive-looking flops."
author: ness
categories: [Claude Code, AI Automation]
tags: [outlier score, content research, viral videos, youtube strategy, claude code]
image: assets/images/outlier-score-why-your-videos-flop-header.jpg
featured: true
---

Raw view counts lie, and copying them is why your videos flop. The outlier score fixes it with one division: take any video's views and divide by that channel's own average over the last ninety days. Two times or better means the video broke out, one and a half times is strong, and anything below that is noise you should ignore — no AI, no tool, no subscription required.

---

## Get the Remix Prompt

The remix prompt from this video, plus the rest of the skills library, is free inside the community.

**[Grab the remix prompt and skills →](https://hub.digicuratoragency.com/welcome)**

---

<div style="max-width: 720px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/kWo3zvUKgW4"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is an Outlier Score?

An outlier score is a video's views divided by the average views of that same channel over the previous ninety days. It measures a video against its own channel instead of against the internet, which is the only comparison that tells you anything.

Run the numbers and the ranking inverts completely:

| Video | Views | Channel 90-day average | Outlier score | Verdict |
|---|---|---|---|---|
| Big channel upload | 100,000 | 400,000 | **0.25×** | Flop |
| Small channel upload | 20,000 | 5,000 | **4.0×** | Breakout |

A hundred thousand views on a two-million-subscriber channel is a flop. Twenty thousand on a small channel can be the biggest thing that person has ever made. From the outside, the big number looks like the lesson — and it is the one you would have copied.

Read the scale like this:

- **2.0× or higher** — it broke out. Study this one.
- **1.5× to 2.0×** — strong. Worth a look.
- **Below 1.5×** — ordinary for that channel. Ignore it.

The smartest part of this entire system is division. You can do it in your head in about ten seconds, and it costs nothing.

## Why Does Copying a Winning Video Still Fail?

Because you copied the topic, and the topic is not what worked. The structure underneath it is what worked.

You watched something take off, you took the subject, you made your own version, and it went nowhere. Then you decided their audience must just be different from yours. They were not different. You lifted the visible layer and left the mechanism behind — the order the ideas arrive in, where the tension sits, what gets withheld and for how long.

Topics are the easiest thing to see and the least transferable thing to steal.

## How Do You Extract the Structure Instead of the Topic?

You hand a model the winning video and your own brand, and you demand the answer back in a fixed shape rather than asking for "a similar video."

The remix prompt names every part in advance. Seven hook steps, in order:

1. Pattern interrupt
2. Mirror the viewer
3. Reveal the opportunity
4. Expose the gap
5. Promise transformation
6. Authority
7. Clean transition

Then four to five named body sections. No negotiation, no improvising. Fixed slots stop the model wandering off and writing you a nice introduction instead of a hook.

The prompt also carries your brand profile, so the output arrives in your voice rather than a neutral one — that is [the brand clarity prompt](https://blog.digicuratoragency.com/brand-clarity-prompt-fix-generic-ai-writing/) doing silent work inside this one. Build the profile first and every prompt after it gets better for free.

## What Is the One Line Worth Stealing?

**Preserve every specific.** If the source names eight tools, name all eight.

That single instruction is what stops a real video degrading into vague advice. Models compress by default: given a concrete example, they will happily return "use the right tools for your workflow" and consider the job done. Specificity is the thing that made the original worth studying, and it is the first thing lost without an explicit rule protecting it.

If you only steal one line from the whole prompt, steal that one.

## How Do You Actually Start This Week?

Do it by hand before you automate anything. Pick three channels you already watch, take their recent uploads, and divide each video's views by that channel's ninety-day average. Ten minutes, and you will have your winner.

Then run the remix prompt on it and see what comes back. Once the manual loop works, automating it is straightforward — the same principle applies to any content workflow, which is how [automatic content repurposing](https://blog.digicuratoragency.com/repurpose-content-automatically-video-blog-freebie/) gets built.

## FAQ

### Why ninety days instead of a channel's lifetime average?

Ninety days reflects where the channel is now. A lifetime average is dragged down by early uploads from before the audience existed, which inflates every recent video's score and makes ordinary uploads look like breakouts.

### What outlier score counts as a real breakout?

Two times the channel's own average or better. One and a half is strong and worth a look. Below that, the video performed normally for that channel and there is no lesson in it.

### Can I calculate an outlier score without a tool?

Yes. It is one division you can do in your head: views divided by that channel's recent average. Doing it manually on three channels takes about ten minutes and teaches you more than a dashboard will.

### Does the outlier score work on TikTok and Instagram?

The arithmetic works anywhere you can see per-post view counts and estimate an account's recent average. The harder part is data access, not the maths — some platforms make the recent average awkward to gather.

## Stop Copying Flops

Raw views are a lie, and the outlier score is the ten-second fix. Divide a video's views by its channel's ninety-day average, ignore anything under 1.5×, and study only what actually broke out. Then copy the structure rather than the topic, and make the prompt preserve every specific so it stays useful.

That is one division and one prompt, done by hand. Inside GrowthOS, Niche Pulse is system number two: it watches five channels for you, runs the division on every upload every day, and your brand profile from system one is already inside the prompt before you click anything. [Get GrowthOS →](https://builds.digicuratoragency.com/growth-os/) and stop doing the watching yourself.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Why ninety days instead of a channel's lifetime average?",
      "acceptedAnswer": { "@type": "Answer", "text": "Ninety days reflects where the channel is now. A lifetime average is dragged down by early uploads from before the audience existed, which inflates every recent video's score and makes ordinary uploads look like breakouts." }
    },
    {
      "@type": "Question",
      "name": "What outlier score counts as a real breakout?",
      "acceptedAnswer": { "@type": "Answer", "text": "Two times the channel's own average or better. One and a half is strong and worth a look. Below that, the video performed normally for that channel and there is no lesson in it." }
    },
    {
      "@type": "Question",
      "name": "Can I calculate an outlier score without a tool?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. It is one division you can do in your head: views divided by that channel's recent average. Doing it manually on three channels takes about ten minutes and teaches you more than a dashboard will." }
    },
    {
      "@type": "Question",
      "name": "Does the outlier score work on TikTok and Instagram?",
      "acceptedAnswer": { "@type": "Answer", "text": "The arithmetic works anywhere you can see per-post view counts and estimate an account's recent average. The harder part is data access, not the maths — some platforms make the recent average awkward to gather." }
    }
  ]
}
</script>
