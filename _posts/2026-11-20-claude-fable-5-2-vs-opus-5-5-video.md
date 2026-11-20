---
layout: post
title: "Claude Fable 5.2 vs Opus 5.5: Same Prompt, One Video"
description: "I gave Claude Fable 5.2 and Claude Opus 5.5 the same short video prompt. See what changed between the two builds and how to run the head-to-head yourself."
author: ness
categories: [Claude Code, AI Automation]
tags: [claude fable 5.2, claude opus 5.5, ai video, claude code, content engine]
image: assets/images/claude-fable-5-2-vs-opus-5-5-video-header.jpg
featured: false
---

Claude Fable 5.2 and Claude Opus 5.5 do not build the same short video from the same prompt, even when the brief is identical down to the last character. I sent both models the exact prompt my Content Engine Chrome extension generates, let each one build a vertical short, and put the two results next to each other. Both finished. Both looked like my brand. The two files were still clearly different videos, which is the whole reason the test is worth running before you commit a model to your content pipeline.

---

## Get the Free Guide

The guide has the full same-prompt test kit: the brief template, the judging rubric I score both videos against, and the setup for running it in Claude Code or Codex.

**[Get the free Same-Prompt Model Test Kit →](https://hub.digicuratoragency.com/freebie?kw=fable)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/BY6igihDvts"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Happens When Two Claude Models Get the Same Video Prompt?

Both models shipped a watchable vertical short, and neither file could stand in for the other. A model swap in a content pipeline is not a quality dial you turn up or down. It changes the editorial choices the model makes inside the gaps your prompt left open, and every prompt leaves gaps.

The brief itself came from Content Engine, the Chrome extension I use to turn a link or an idea into a finished short. It sends the same instructions no matter which model sits behind it, so the prompt was a controlled variable and the model was the only thing I changed. As of November 2026, Anthropic ships several Claude models behind the same Claude Code command line, so switching between Fable 5.2 and Opus 5.5 is one setting, not a rebuild.

I did not declare a winner in the video and I am not going to declare one here. I put both cuts up and asked people which they preferred, because "better" for a short video means whichever one your audience watches to the end. For the software version of this test, I ran [the same head-to-head on four real app builds](https://blog.digicuratoragency.com/claude-fable-vs-opus/) earlier this year.

## Why Build the Video in Code Instead of Image Generation?

Every frame in both videos was rendered from code, with no image generation model anywhere in the pipeline. The model writes the animation, the timing and the layout as a program, and the renderer turns that program into an MP4. Nothing gets diffused into existence.

That choice matters more than it sounds:

- **No per-image or per-second credits.** You pay for the model thinking, and the rendering runs on your own machine.
- **On-screen text stays spelled correctly.** Image models still mangle words at small sizes. A code renderer draws the string you gave it.
- **Edits are one-line edits.** Wrong colour, wrong timing, wrong scene order, you change the line and re-render instead of rolling the dice on a new generation.
- **Reruns are repeatable.** The same code produces the same frames, which is what made this comparison fair in the first place.

I use the same approach for [animated reels rendered entirely in code](https://blog.digicuratoragency.com/claude-skill-unlimited-animated-reels/), and the economics are the reason it stuck.

## Which Video Styles Can One Prompt Build?

The same prompt can produce three different shapes of short, and the model you pick does not change which shapes are available to you.

| Style | What you supply | Who it suits |
|---|---|---|
| Avatar explainer | A script and a HeyGen avatar | You want a talking head without filming one |
| Split A-roll and B-roll | Your own raw recording | You already film yourself and want animated B-roll above your head |
| Fully faceless | A link or a plain idea | You do not want to appear on camera at all |

Pick the style first. Swapping styles halfway through changes the brief, and a changed brief means your model comparison is measuring two things at once.

## How Do You Run the Same-Prompt Test Yourself?

Run it as six steps, in a fresh session per model, so no context from the first build leaks into the second.

1. **Write the brief once** and save it to a file. Topic, duration, style, voice, caption rules, the CTA. Every detail you care about goes in writing, because anything you leave out is exactly where the two models will differ.
2. **Open Claude Code and set the model to Fable 5.2.** Paste the brief verbatim. Add nothing, answer no questions with extra guidance.
3. **Render and save the output** as `fable.mp4`. Note how many follow-up prompts it took to get something postable.
4. **Start a brand new session and set the model to Opus 5.5.** Paste the identical brief. Resist the urge to improve it now that you know what the first build got wrong.
5. **Render and save the output** as `opus.mp4`, and note the follow-up count again.
6. **Watch both muted first, then with sound.** Muted shows you whether the visuals carry the story, which is how most people on Instagram and TikTok will see it.

## What Should You Compare in the Two Videos?

Score both videos on the same six things rather than trusting your gut after one viewing.

| What to check | Why it matters |
|---|---|
| The first two seconds | If the hook does not land, nothing after it gets watched |
| Scene count and pacing | Too few scenes feels static, too many feels frantic |
| Caption timing against the voiceover | Captions that drift out of sync read as sloppy instantly |
| Word count versus the brief | A model that quietly runs long will blow your duration limit |
| Invented facts | Check that no number or claim appears on screen that your script never said |
| Follow-up prompts needed | A build that took one prompt beats a slightly nicer build that took nine |

The last row is the one people skip and the one that decides which model you keep. A pipeline you run three times a week lives or dies on how often you have to step in, the same lesson I took from building [an AI content app that writes scripts and captions for nine platforms](https://blog.digicuratoragency.com/ai-content-app-posts-and-dms-claude-code/).

## FAQ

### Is Claude Fable 5.2 better than Claude Opus 5.5 for video?

Neither model won this test outright, which is why I put both cuts to my audience instead of announcing a result. Run the same brief through both on your own topic and judge by watch time, because the better model for short video is the one your viewers finish.

### Will the same prompt give me the same video twice?

Not from the model, no. The model writes new code each run, so two runs of the same brief produce two slightly different programs. The render step is repeatable, so once the code exists, re-rendering it gives you identical frames.

### Do I need an image generation model to make a short video?

No. Both videos in this test were built entirely from code, with no image generation anywhere in the pipeline, which is why there were no per-image credits to spend.

### Can I switch models halfway through a build?

You can, but it ruins the comparison. Mid-build switching mixes two models' choices into one output, so run each model in its own fresh session when you are testing them against each other.

### How long does one of these video builds take?

The model work is the slow part and the render is the fast part. In my pipeline a finished short comes out in under three minutes end to end, and the comparison itself takes about as long as watching both videos twice.

## Build Your Own Short in Under Three Minutes

The point of a same-prompt test is to stop guessing which model to trust with your content and start measuring it. Write the brief once, run it through Fable 5.2 and Opus 5.5 in separate sessions, score both on the hook, the pacing, the caption sync and the number of follow-ups, then keep the one that needs you least.

If you want the pipeline that sent the prompt in this test, that is Content Engine. Paste any link or idea and get a published video in under 3 minutes, with DM automation armed to capture leads. [Meet Content Engine →](https://builds.digicuratoragency.com/content-engine/)

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is Claude Fable 5.2 better than Claude Opus 5.5 for video?",
      "acceptedAnswer": { "@type": "Answer", "text": "Neither model won this test outright, which is why I put both cuts to my audience instead of announcing a result. Run the same brief through both on your own topic and judge by watch time, because the better model for short video is the one your viewers finish." }
    },
    {
      "@type": "Question",
      "name": "Will the same prompt give me the same video twice?",
      "acceptedAnswer": { "@type": "Answer", "text": "Not from the model, no. The model writes new code each run, so two runs of the same brief produce two slightly different programs. The render step is repeatable, so once the code exists, re-rendering it gives you identical frames." }
    },
    {
      "@type": "Question",
      "name": "Do I need an image generation model to make a short video?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Both videos in this test were built entirely from code, with no image generation anywhere in the pipeline, which is why there were no per-image credits to spend." }
    },
    {
      "@type": "Question",
      "name": "Can I switch models halfway through a build?",
      "acceptedAnswer": { "@type": "Answer", "text": "You can, but it ruins the comparison. Mid-build switching mixes two models' choices into one output, so run each model in its own fresh session when you are testing them against each other." }
    },
    {
      "@type": "Question",
      "name": "How long does one of these video builds take?",
      "acceptedAnswer": { "@type": "Answer", "text": "The model work is the slow part and the render is the fast part. In my pipeline a finished short comes out in under three minutes end to end, and the comparison itself takes about as long as watching both videos twice." }
    }
  ]
}
</script>
