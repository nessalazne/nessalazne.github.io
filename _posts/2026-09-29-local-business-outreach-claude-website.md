---
layout: post
title: "Local Business Outreach: Claude Builds the Site First"
description: "Local business outreach that gets replies: Claude finds dated websites, builds a free replacement, hosts a preview, and sends it through their own form."
author: ness
categories: [Claude Code, AI Automation]
tags: [local business outreach, claude code skills, lead generation, agency clients, ai automation]
image: assets/images/local-business-outreach-claude-website-header.jpg
featured: false
---

Cold outreach to local businesses fails because it asks for attention before it gives anything. A Claude Code skill called `local-business-revamp` reverses the order: it finds local businesses whose websites look dated, builds each one a replacement from a prepared template, deploys that replacement to a public preview link, and submits the link through the business's own contact form. The owner opens their inbox and finds a finished website instead of a pitch.

The open-source version of this system is on GitHub as `albertshiney/websitegenerator`. It runs as a Claude Code or OpenAI Codex skill, keeps a SQLite ledger so the same business never gets contacted twice, and ships with a local dashboard that shows every prospect as it moves through the pipeline.

---

## Get the Free Guide

The Website-First Outreach Setup walks through installing the skill, the seven fields that change per business, the exact generator command, and the failure modes that waste a batch.

**[Get the free Website-First Outreach Setup →](https://hub.digicuratoragency.com/freebie?kw=site)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/ghuBTM289EY"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## How does the local business outreach system work?

You give the skill an industry, a city, and a number of websites, and it carries each prospect through eight stages without asking you to fill anything in. The default batch is five businesses, and the skill accepts anywhere from 1 to 100, processing larger runs in waves of up to five parallel workers.

Here is the path a single prospect takes:

1. **Discover.** Claude searches the industry and city and opens each business's actual website to confirm the name and service area.
2. **Qualify.** The page gets screened for visual weakness: fixed-width layouts, illegible type, tiny navigation, stretched images, broken mobile.
3. **Check the form.** The contact page is screened for a real enquiry form with a message field and a submit button. No usable form means the job routes to manual handoff.
4. **Collect facts.** Business name, public phone, email, and publicly listed address come off the business's own site.
5. **Generate.** A prepared template gets the business's details and a theme colour pulled from its existing branding.
6. **Deploy.** The static site goes to its own isolated Vercel project.
7. **Verify.** The preview URL gets opened in a logged-out context to confirm it loads for a stranger.
8. **Contact.** One submission of a fixed message through the business's original form, then the result goes in the ledger.

Step 7 is the one people skip. A preview that only loads for you is worthless, and a dead link in an outreach message is worse than no message at all.

## What does Claude actually build for each business?

Only seven values change per business, which is what makes the batch fast. The rest of the site, the copy, the layout, and the stock photography stay exactly as the template ships them.

| Field | What it holds |
|---|---|
| `name` | The verified business name |
| `phone` | A public phone number in international format |
| `email` | A public email address |
| `street` | Publicly listed street address |
| `city` | City or service area |
| `zip` | Postal code |
| `theme_color` | Six-digit hex taken from the business's own branding |

The generator is a single command:

```bash
./website --theme-color "#2563eb" --name "Business Name" \
  --phone "+44 20 7946 0958" --email "hello@business.com"
```

That writes a deployable folder under `runs/quick/`, and the generation step takes roughly 30 seconds. Discovery, deployment, and outreach are separate and much slower, so a batch of five is an afternoon, not a minute. Either a phone or an email is required, and the generator rejects a business with neither.

## Why does qualifying on looks beat qualifying on age?

The skill qualifies purely on what the site looks like, and it specifically forbids using copyright years, publication dates, or domain age as signals. That rule exists because those signals lie in both directions. A plumber who updated their footer last week can still be running a 2011 layout, and a site with a stale copyright line can be perfectly readable on a phone.

So the qualification evidence is a desktop view, a narrow-viewport view, and at least two written findings. Those findings stay internal. They never appear in the message, because opening with "I noticed your site isn't responsive" turns a gift into a critique.

If you want the list side of this rather than the build side, the [free Google Maps scraper kit that Claude Code runs for you](https://blog.digicuratoragency.com/google-maps-scraper-kit-claude-code/) pulls name, phone, email, and website for a city and business type, and [Agent Reach for free AI web scraping](https://blog.digicuratoragency.com/agent-reach-free-ai-web-scraping-claude/) gives the agent real access to the pages it needs to read.

## What does the message actually say?

The outreach message is fixed. Same wording every time, with only the preview URL and the business name changing:

> Hey!
>
> Your website is decent, but looks a little old. I made an updated one.
>
> You can take a look here: [preview URL]
>
> The website is totally free, you just pay for hosting.

No SEO claims, no flattery, no rewritten opening per prospect. Spun messages are how a system like this turns into spam.

The ledger enforces one submit per business. Before the form is sent, `contact-begin` atomically reserves the attempt, which rejects duplicates, unverified previews, and failed QA. After the click, `contact-finish` records what was observed. There are no retries and no falling back to email or SMS.

## What does it cost to run?

The repository is free and open source, as of September 2026. You supply a Firecrawl API key for page screening and a Vercel account for hosting previews. Python 3 runs the generator, and Node and npm are only needed if you edit the master template.

| Piece | What it does | What you provide |
|---|---|---|
| The skill | Runs the whole pipeline | Claude Code or Codex |
| Firecrawl | Screens homepages and contact pages | API key in `.env` |
| Vercel | Hosts one isolated preview per prospect | Account login |
| SQLite ledger | Deduplicates and reserves submissions | Nothing, it ships with the repo |

The real cost is the build, and the template absorbs it once instead of per prospect. For a slower manual version of the same idea, the [full system for getting local business clients with AI](https://blog.digicuratoragency.com/get-local-business-clients-ai/) covers the list, the targets, and a sheet CRM.

## FAQ

### Do I need to know how to code to run this?

No. You clone the repository, tell Claude Code where the skill folder is, and ask for a batch with an industry and a city. The skill runs the commands itself. You do need to install Python 3 and log in to Vercel once.

### Is building someone a website and sending it unsolicited legal?

It is ordinary business-to-business outreach through a form the business published for enquiries, so in most places it sits alongside any other cold contact. The skill respects visible no-solicitation notices, leaves CAPTCHA challenges alone, and never sends a second message to the same business. Check the rules in your own country before running a large batch.

### How many businesses can it handle at once?

Batches default to five and accept up to 100. Larger runs are processed in waves of up to five parallel workers, with one coordinator holding the ledger so two workers never claim the same prospect.

### What happens if a business has no contact form?

The site still gets built, deployed, and verified, then the job moves to manual handoff with the message and the verified contact details prepared for you. It is never silently skipped.

### Can I use a template other than the electrician one?

The repository ships with one prepared template. Adding another means building it in `templates/`, registering it in `settings.json`, and keeping the same seven personalization fields so the generator can fill it.

## Give something before you ask for something

The reason this local business outreach works has little to do with Claude. A finished product answers the only question a business owner has, which is whether you can do the thing. A preview link answers it in four seconds, and a cold email asks them to take it on faith. Build the system once and the only variable left is how many cities you point it at.

Want to build systems like this with a group doing the same? [Join the Vibe Coding Build →](https://hub.digicuratoragency.com/about)

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Do I need to know how to code to run this?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. You clone the repository, tell Claude Code where the skill folder is, and ask for a batch with an industry and a city. The skill runs the commands itself. You do need to install Python 3 and log in to Vercel once." }
    },
    {
      "@type": "Question",
      "name": "Is building someone a website and sending it unsolicited legal?",
      "acceptedAnswer": { "@type": "Answer", "text": "It is ordinary business-to-business outreach through a form the business published for enquiries, so in most places it sits alongside any other cold contact. The skill respects visible no-solicitation notices, leaves CAPTCHA challenges alone, and never sends a second message to the same business. Check the rules in your own country before running a large batch." }
    },
    {
      "@type": "Question",
      "name": "How many businesses can it handle at once?",
      "acceptedAnswer": { "@type": "Answer", "text": "Batches default to five and accept up to 100. Larger runs are processed in waves of up to five parallel workers, with one coordinator holding the ledger so two workers never claim the same prospect." }
    },
    {
      "@type": "Question",
      "name": "What happens if a business has no contact form?",
      "acceptedAnswer": { "@type": "Answer", "text": "The site still gets built, deployed, and verified, then the job moves to manual handoff with the message and the verified contact details prepared for you. It is never silently skipped." }
    },
    {
      "@type": "Question",
      "name": "Can I use a template other than the electrician one?",
      "acceptedAnswer": { "@type": "Answer", "text": "The repository ships with one prepared template. Adding another means building it in templates/, registering it in settings.json, and keeping the same seven personalization fields so the generator can fill it." }
    }
  ]
}
</script>
