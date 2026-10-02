---
layout: post
title: "Cut AI Token Costs 70% With Jev and Claude"
description: "Jev classifies data in under a second for $0.042 per million input tokens. Here is how pairing it with Claude cut token costs by 70% across 12 prompts."
author: ness
categories: [AI Automation, Claude Code]
tags: [cut ai token costs, jev model, typesafe ai, classification model, claude code]
image: assets/images/jev-cut-ai-token-costs-70-percent-header.jpg
featured: false
---

Most of the AI work running inside a small business is classification, and a full language model is the wrong tool for it. Jev, a model from TypeSafe built by ChatGPT co-inventor Diogo Almeida, answers typed questions in 70 to 500 milliseconds at $0.042 per million input tokens, with output tokens unmetered. In one test, routing work through Jev first cut token costs by 70% across 12 prompts, and nine of those tasks never needed the expensive model at all.

That gap is the whole point. You are paying frontier prices to decide whether an email is an invoice or a pitch. Jev makes that decision for a fraction of a cent, and hands Claude only the jobs that actually need thinking.

---

## Get the Free Guide

The full two-model setup: the install command, the API key step, the exact Python router that gates on confidence, the prompts I run, and a fix table for when it breaks.

**[Get the free Jev + Claude Router Playbook →](https://hub.digicuratoragency.com/freebie?kw=jev)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/wE3pynNiF1g"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is Jev and Why Is It So Cheap?

Jev is a classification model that returns a typed answer plus a confidence number instead of a paragraph of text. TypeSafe launched it on 15 September 2026 and calls the category a System One model, the fast reflex half of the pair, with a reasoning model like Claude playing the slow deliberate half.

You give it a state, which can be a support message, a JSON record, or a list of items, and a set of questions you defined in advance. It answers every question in parallel inside the answer space you specified. There are three question types as of October 2026:

| Type | What it returns | Good for |
|---|---|---|
| `Choice` | One option from your list, plus a probability per option | Routing, tagging, category sorting |
| `Score` | A level from a rubric you wrote, plus a probability per level | Urgency, lead quality, sentiment strength |
| `Noul` | A single probability from 0 to 1 for a yes/no statement | Flags, filters, guardrails |

It is cheap because it never generates text. Input runs at $0.042 per million tokens and output is free, which TypeSafe puts at roughly 1/48th the input cost of a GPT-5.6-class model. Latency lands between 70 and 500 milliseconds against the 3 to 30 seconds a frontier model takes on the same call. Because the answer is constrained to the schema you wrote, it cannot hallucinate a category that does not exist or return a broken JSON shape.

## Which of Your Tasks Are Actually Classification Jobs?

The test is simple: if you already know every possible answer before you send the request, it is a classification job and it does not need a language model. Most of the AI spend in a creator or agency workflow sits in this bucket.

| Task | Classification or reasoning | Who should run it |
|---|---|---|
| Sorting inbound email into invoice, brand deal, phishing, spam | Classification | Jev |
| Triaging a support ticket to billing, technical, or sales | Classification | Jev |
| Scoring a lead 1 to 5 against your ICP | Classification | Jev |
| Flagging churn risk on an account note | Classification | Jev |
| Filtering YouTube comments worth replying to | Classification | Jev |
| Writing the reply to that comment | Reasoning | Claude |
| Summarising a 40 minute call | Reasoning | Claude |
| Drafting the brand deal response | Reasoning | Claude |

One published test processed 1,000 emails through Jev in about 6 seconds for $0.09, where a GPT-5.6-class model took about 5 minutes and $0.62. Across a batch of workflows the same test pushed close to 20,000 requests for under a dollar. If you have been watching your bill climb, this pairs well with the [four Claude Code plugins that cut token usage in half](https://blog.digicuratoragency.com/four-claude-code-plugins-cut-token-usage/) and the case for [cheaper models at scale](https://blog.digicuratoragency.com/claude-fable-5-1-cheaper-at-scale/).

## How Do You Pair Jev With Claude?

The pattern is confidence-gated routing: Jev decides first, and only the uncertain cases reach Claude. Every `Choice` and `Score` answer comes back with a confidence field derived from the shape of the probability distribution, so a flat spread reads as genuine uncertainty rather than the model's opinion of itself.

1. **Install the SDK.** `pip install typesafe-sdk`, then set `TYPESAFE_API_KEY` in your shell profile.
2. **Write the questions once.** A `Choice` for the route, a `Score` for urgency, a `Noul` for anything you want to gate on.
3. **Send the state.** One call answers all of your questions in parallel, under half a second.
4. **Gate on confidence.** Act automatically above 0.85. Hand anything between 0.6 and 0.85 to Claude for a slower look. Below 0.6, put it in front of a human.
5. **Let Claude do the writing.** It only ever sees the cases that earned the cost.

Nine of the 12 prompts in the test never crossed the threshold where Claude was needed, which is where the 70% saving came from. The architecture is the same brain-and-harness split covered in [how AI agents actually work](https://blog.digicuratoragency.com/ai-agents-llm-brain-harness-system/): a cheap fast layer handling the decisions, an expensive layer handling the judgement.

As of October 2026 you can reach Jev three ways: direct through `console.typesafe.ai`, through OpenRouter as `jev-latest` or `jev-1.13`, or through the Vercel AI Gateway as `typesafe-ai/jev`. Direct signups were paused shortly after launch, so the gateways are the reliable door. TypeSafe gives $5 of free credit, which is around 120 million tokens.

## What Jev Cannot Do

Jev has hard limits, and hitting one is the most common reason a first build goes wrong. It cannot generate text, so there is no summary, no reply, no explanation. It does not do arithmetic or counting reliably, and it cannot compare dates as ordered values, so "is this newer than that" belongs in your own code. The context ceiling is 64,000 tokens for state and questions combined, with 32,000 per individual question, and a `Choice` question caps at 255 options.

Treat those as the routing rules rather than flaws. Anything open-ended goes to Claude. Anything with a known answer space goes to Jev.

## FAQ

### What is Jev?

Jev is a classification model from TypeSafe that returns a typed answer and a confidence score instead of text. It was built by Diogo Almeida, a co-inventor of ChatGPT at OpenAI, and launched on 15 September 2026.

### How much does Jev cost?

Input is $0.042 per million tokens and output is unmetered, which TypeSafe puts at roughly 1/48th the input cost of a GPT-5.6-class model. A single classification lands near $0.0004. New accounts get $5 of free credit, about 120 million tokens.

### Does Jev replace Claude?

No. Jev cannot write, summarise, or explain anything. It handles the fast decisions and Claude handles the thinking, which is why the two models together cost less than one model doing everything.

### Can Jev hallucinate?

Not in the usual sense. The answer is constrained to the schema you defined, so it cannot invent a category you did not list or return a malformed shape. It can still be wrong, which is what the confidence score is for.

### How do I get a Jev API key?

Direct signups at `console.typesafe.ai` were paused shortly after the September 2026 launch. The dependable route is OpenRouter or the Vercel AI Gateway, where Jev is available without a TypeSafe account.

## Start With One Workflow

Pick the task you run most often where you already know every possible answer. Email sorting is usually the one. Move that single decision to Jev, gate it at 0.85, and leave everything else on Claude. You will see the cost difference on the first batch of a few hundred items.

Two models beat one. The cheap one decides, the expensive one thinks, and you stop paying frontier prices to label an invoice. If you want to build the full router with me and the rest of the systems around it, [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about).

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is Jev?",
      "acceptedAnswer": { "@type": "Answer", "text": "Jev is a classification model from TypeSafe that returns a typed answer and a confidence score instead of text. It was built by Diogo Almeida, a co-inventor of ChatGPT at OpenAI, and launched on 15 September 2026." }
    },
    {
      "@type": "Question",
      "name": "How much does Jev cost?",
      "acceptedAnswer": { "@type": "Answer", "text": "Input is $0.042 per million tokens and output is unmetered, which TypeSafe puts at roughly 1/48th the input cost of a GPT-5.6-class model. A single classification lands near $0.0004. New accounts get $5 of free credit, about 120 million tokens." }
    },
    {
      "@type": "Question",
      "name": "Does Jev replace Claude?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Jev cannot write, summarise, or explain anything. It handles the fast decisions and Claude handles the thinking, which is why the two models together cost less than one model doing everything." }
    },
    {
      "@type": "Question",
      "name": "Can Jev hallucinate?",
      "acceptedAnswer": { "@type": "Answer", "text": "Not in the usual sense. The answer is constrained to the schema you defined, so it cannot invent a category you did not list or return a malformed shape. It can still be wrong, which is what the confidence score is for." }
    },
    {
      "@type": "Question",
      "name": "How do I get a Jev API key?",
      "acceptedAnswer": { "@type": "Answer", "text": "Direct signups at console.typesafe.ai were paused shortly after the September 2026 launch. The dependable route is OpenRouter or the Vercel AI Gateway, where Jev is available without a TypeSafe account." }
    }
  ]
}
</script>
