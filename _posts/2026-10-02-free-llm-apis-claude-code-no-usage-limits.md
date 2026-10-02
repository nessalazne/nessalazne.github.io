---
layout: post
title: "Free LLM APIs: Keep Claude Code Running at Zero Cost"
description: "16 providers with permanent free LLM API tiers, the gateway setup that keeps Claude Code running when your limit hits, and what Anthropic does not support."
author: ness
categories: [Claude Code, AI Automation]
tags: [free llm apis, claude code, llm gateway, anthropic base url, usage limits]
image: assets/images/free-llm-apis-claude-code-no-usage-limits-header.jpg
featured: false
---

Awesome Free LLM APIs is a GitHub list of 16 providers that give away permanent free API access to text models, and as of October 2026 it has more than 9,000 stars. Every endpoint on the list is OpenAI SDK-compatible, so anything that speaks the OpenAI API can call them, including a gateway sitting in front of Claude Code. Set up a fallback chain and the moment one model refuses you, the same conversation gets re-sent to the next free model and your session keeps moving.

The headline number from the video is roughly 7 billion free tokens a month across 600-plus models. That figure is the sum of every tier added together. Below are the per-provider numbers you can actually check, plus the exact Claude Code configuration, and the one limitation Anthropic states in writing.

---

## Get the Free Guide

The guide has the full provider table, the `settings.json` block, the curl test, and the error-to-fix table for when the gateway misbehaves.

**[Get the free Free LLM API Playbook →](https://hub.digicuratoragency.com/freebie?kw=free)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/T5kekZT-wNs"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is Awesome Free LLM APIs?

Awesome Free LLM APIs is a curated directory, not a program you install. The repository, maintained by mnfst at [github.com/mnfst/awesome-free-llm-apis](https://github.com/mnfst/awesome-free-llm-apis), lists every LLM API with a **permanent** free tier for text inference, along with its base URL, its model names, and its rate limits. Trial credits and time-limited promos are explicitly excluded, which is what makes the list usable for a workflow you run every day.

It splits into two groups. Provider APIs are run by the companies that train the models: Google Gemini, Mistral AI, Cohere, Z AI (Zhipu AI), and Aion Labs. Inference providers are third-party platforms hosting open-weight models: Groq, OpenRouter, Cloudflare Workers AI, NVIDIA NIM, Hugging Face, Kilo Code, LLM7.io, ModelScope, Ollama Cloud, OVHcloud AI Endpoints, and SiliconFlow.

Two of those sixteen need no API key at all. OVHcloud AI Endpoints serves 20-plus open-weight models anonymously at 2 requests per minute per IP. LLM7.io answers anonymous requests to its `turbo` models, and a free token from token.llm7.io raises the ceiling without changing which models you reach.

## How Much Free Usage Do You Actually Get?

The useful tiers are the ones with daily request ceilings in the thousands rather than monthly call counts in the hundreds. Here is what the repository lists as of October 2026:

| Provider | Free tier | Notable models |
|---|---|---|
| NVIDIA NIM | 40 RPM, 10,000 requests/day **per model**, 100+ models | `nvidia/nemotron-3-ultra-550b-a55b`, `openai/gpt-oss-120b` |
| Cloudflare Workers AI | 10,000 Neurons/day shared, 75+ models | `@cf/meta/llama-3.3-70b-instruct-fp8-fast`, `@cf/openai/gpt-oss-120b` |
| Google Gemini | No credit card, 15 RPM and 1,500 requests/day on Flash tiers | Gemini 3.7 Flash, Gemini 2.5 Pro, Gemma 4 31B |
| Kilo Code | 200 requests/hour per IP, no key required | `kilo-auto/free`, `nvidia/nemotron-3-ultra-550b-a55b:free` |
| Groq | 30 RPM, 1,000 requests/day on most models | `openai/gpt-oss-120b`, `qwen/qwen3.6-27b` |
| Mistral AI | $10/month in API credits, free mode on by default | Mistral Large 3, Codestral, Ministral 3 14B |
| LLM7.io | 1,000,000 tokens per 24 hours with a free token | `gpt-oss:20b`, `minimax-m2.7` |
| OpenRouter | 17 free models at 50 requests/day each | `openai/gpt-oss-20b:free`, `cohere/north-mini-code:free` |

NVIDIA NIM is the standout because the 10,000 requests per day applies per model rather than per account, across more than 100 models. Cloudflare's 10,000 Neurons are shared across all Workers AI usage and reset daily at 00:00 UTC, and going over fails the request instead of billing you.

Read the footnotes before you commit to one. Mistral's free mode may use your prompts to train its models unless you opt out. Cohere's trial key is non-commercial only. Kilo Code warns that its auto-router may send requests to providers that log prompts and outputs. If you are routing client work through any of these, that matters more than the rate limit does.

## How Do You Point Claude Code at a Free Model?

Claude Code reaches a different endpoint through two environment variables: `ANTHROPIC_BASE_URL` for the address and `ANTHROPIC_AUTH_TOKEN` for the credential. Put them in the `env` block of `~/.claude/settings.json` so they apply everywhere, including background agents:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://your-gateway.example.com",
    "ANTHROPIC_AUTH_TOKEN": "sk-gateway-key"
  }
}
```

The gap people miss is in the middle. The providers on the list are OpenAI SDK-compatible, and Claude Code speaks the Anthropic Messages format, so something has to translate between them. That something is an LLM gateway: a small proxy that accepts `POST /v1/messages`, rewrites it into an OpenAI-format chat completion, calls the free provider, and converts the answer back.

Four steps get you running:

1. **Collect the free keys.** Start with Google Gemini, Groq, and NVIDIA NIM. Each is a signup with no credit card.
2. **Stand up a gateway** that exposes an Anthropic-format `/v1/messages` endpoint and holds your provider keys server-side.
3. **Export the two variables**, then prove the path works before opening Claude Code:

   ```bash
   curl -sS -w '\n%{http_code}\n' -X POST "$ANTHROPIC_BASE_URL/v1/messages" \
     -H "Authorization: Bearer $ANTHROPIC_AUTH_TOKEN" \
     -H "anthropic-version: 2023-06-01" \
     -H "content-type: application/json" \
     -d '{"model": "claude-sonnet-4-6", "max_tokens": 1, "messages": [{"role": "user", "content": "."}]}'
   ```

   A response starting with `{"id":"msg_` means the URL and credential both work. A `401` means your credential is in the wrong header, so switch to `ANTHROPIC_API_KEY`.
4. **Run `claude` from the same shell and check `/status`.** An `Anthropic base URL` line showing your gateway, plus an `Auth token` line naming the variable you set, confirms the session is routed.

To get the free model names into the `/model` picker, set `CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY=1`. Claude Code queries the gateway for its catalog at startup and adds whatever it returns.

## What Makes a Model Switch Keep Your Context?

A fallback chain carries context because it re-sends the whole conversation, not a summary. OpenRouter documents two mechanisms for this: [model fallbacks](https://openrouter.ai/docs/guides/routing/model-fallbacks), which chain models in priority order, and the Free Models Router at `openrouter/free`, which picks from the free pool for you. Kilo Code's `kilo-auto/free` router does the same across its pool.

When the first model returns a rate-limit error, the router forwards the identical message array to the next one. The new model receives every turn that came before it, so nothing is lost and nothing has to be re-explained. The handoff note described in the video is a line you add yourself, at the top of your system prompt or in `CLAUDE.md`, telling the incoming model which model it replaced and where the work stopped. That part is configuration, not a feature of the list.

For keeping your paid Claude usage from running out in the first place, the [claude.md rules that stop Claude Opus 5.5 from burning your usage limit](https://blog.digicuratoragency.com/claude-opus-5-5-usage-limits-claude-md-config/) solve the same problem from the other direction, and these [four Claude Code plugins that cut token usage in half](https://blog.digicuratoragency.com/four-claude-code-plugins-cut-token-usage/) include one that reroutes to free providers automatically.

## What Does Anthropic Not Support Here?

Anthropic's own documentation states the limit plainly: it "doesn't endorse, maintain, or audit third-party gateway products, and doesn't support routing Claude Code to non-Claude models through any gateway." The configuration works, and nothing stops you, but a broken session on a free Nemotron model is yours to debug.

Three other things change the moment you set a gateway credential:

- **Your subscription stops applying.** While `ANTHROPIC_AUTH_TOKEN` or an `apiKeyHelper` is active, requests carry that credential instead of your claude.ai login, and the subscription's usage limits do not apply to them. Your login stays saved and unused.
- **Remote Control and voice dictation switch off.** Both need a claude.ai identity, and Remote Control is also disabled while `ANTHROPIC_BASE_URL` points at a non-Anthropic host.
- **Smaller context windows bite.** If the gateway enforces a lower limit than the model's native window and rewrites the error, Claude Code will not recognise it as a too-long error and will not compact on its own. Run `/compact` to recover, and set `CLAUDE_CODE_AUTO_COMPACT_WINDOW` to the gateway's limit to avoid it.

The sensible pattern is a split. Keep Claude on the work that needs Claude, and send the bulk jobs, the classification, and the first-draft passes to a free tier. That is the same logic behind [cutting AI token costs by 70% with Jev](https://blog.digicuratoragency.com/jev-cut-ai-token-costs-70-percent/): match the model to the job instead of running everything through the most expensive one.

## FAQ

### Is Awesome Free LLM APIs a tool I install?

No. It is a GitHub directory of providers with permanent free tiers, listing each one's base URL, models, and rate limits. You use it to pick providers and collect keys, then wire them up yourself.

### Do I need a credit card for any of these?

Most entries state no credit card required, including Google Gemini, Groq, Mistral AI, Cohere, Z AI, and Cloudflare Workers AI. OVHcloud AI Endpoints and LLM7.io go further and answer anonymous requests with no signup and no key.

### Can Claude Code call these endpoints directly?

Not directly. The providers are OpenAI SDK-compatible and Claude Code sends the Anthropic Messages format, so an LLM gateway has to translate between the two. Claude Code reaches that gateway through `ANTHROPIC_BASE_URL` and `ANTHROPIC_AUTH_TOKEN`.

### Does my Claude subscription still count while a gateway is set?

No. While a gateway credential variable or an `apiKeyHelper` is active, requests carry that credential in place of your claude.ai subscription login, and the subscription's usage limits do not apply to those requests.

### Will the free providers train on my prompts?

Some will. Mistral's free mode may use inputs and outputs for training unless you opt out, Google may use free-tier prompts to improve products outside the EEA, Switzerland and the UK, and Kilo Code warns that its auto-router may route to providers that log prompts. Check the footnote for any provider before sending client data.

## Where to Take This Next

Sixteen providers with permanent free LLM API tiers is enough to keep a Claude Code workflow running past any single limit, as long as you accept the trade: an unsupported routing path, a gateway you maintain, and data terms that vary provider by provider. Start with the three keys that take two minutes each, put a gateway in front of them, and route only the work that does not need your best model.

If you want the whole system rather than one piece of it, come build with us. [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about)

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is Awesome Free LLM APIs a tool I install?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. It is a GitHub directory of providers with permanent free tiers, listing each one's base URL, models, and rate limits. You use it to pick providers and collect keys, then wire them up yourself." }
    },
    {
      "@type": "Question",
      "name": "Do I need a credit card for any of these?",
      "acceptedAnswer": { "@type": "Answer", "text": "Most entries state no credit card required, including Google Gemini, Groq, Mistral AI, Cohere, Z AI, and Cloudflare Workers AI. OVHcloud AI Endpoints and LLM7.io go further and answer anonymous requests with no signup and no key." }
    },
    {
      "@type": "Question",
      "name": "Can Claude Code call these endpoints directly?",
      "acceptedAnswer": { "@type": "Answer", "text": "Not directly. The providers are OpenAI SDK-compatible and Claude Code sends the Anthropic Messages format, so an LLM gateway has to translate between the two. Claude Code reaches that gateway through ANTHROPIC_BASE_URL and ANTHROPIC_AUTH_TOKEN." }
    },
    {
      "@type": "Question",
      "name": "Does my Claude subscription still count while a gateway is set?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. While a gateway credential variable or an apiKeyHelper is active, requests carry that credential in place of your claude.ai subscription login, and the subscription's usage limits do not apply to those requests." }
    },
    {
      "@type": "Question",
      "name": "Will the free providers train on my prompts?",
      "acceptedAnswer": { "@type": "Answer", "text": "Some will. Mistral's free mode may use inputs and outputs for training unless you opt out, Google may use free-tier prompts to improve products outside the EEA, Switzerland and the UK, and Kilo Code warns that its auto-router may route to providers that log prompts. Check the footnote for any provider before sending client data." }
    }
  ]
}
</script>
