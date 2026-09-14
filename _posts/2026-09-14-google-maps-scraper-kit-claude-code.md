---
layout: post
title: "Free Google Maps Scraper That Claude Code Runs For You"
description: "Google Maps Scraper Kit is a free, open-source tool that runs on your computer while Claude Code drives it, pulling local leads with contact info and socials."
author: ness
categories: [Claude Code, AI Automation]
tags: [google maps scraper, lead generation, claude code, local leads, agency tools]
image: assets/images/google-maps-scraper-kit-claude-code-header.jpg
featured: false
---

Google Maps Scraper Kit is a free, open-source tool that runs locally on your computer and lets Claude Code pull a clean list of local businesses, name, phone, email, website, and address, for any city and business type you name. It replaces paid lead databases that charge hundreds a month, with no subscription and no data cap.

---

## Get the Free Guide

Get the full walkthrough for setting up the scraper, connecting it to Claude Code, and running your first lead pull.

**[Get the free Google Maps Scraper Kit Guide →](https://hub.digicuratoragency.com/freebie?kw=scraper)**

---

<div style="max-width: 315px; margin: 2rem auto;">
  <div style="position: relative; padding-bottom: 177.78%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
      src="https://www.youtube.com/embed/P6RWiiakFqs"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen></iframe>
  </div>
</div>

## What Is Google Maps Scraper Kit?

Google Maps Scraper Kit is an open-source project built as a wrapper around `gosom/google-maps-scraper`, a scraper created by developer Georgios Komninos under the MIT license. The kit adds a one-command Docker setup, ready-to-run scripts, and a Claude skill so Claude Code knows how to call the scraper's API correctly. You run it entirely on your own machine, so there's no monthly fee and no vendor holding your data.

The scraper binds to `127.0.0.1` by default, meaning it only accepts connections from your own computer. It captures around 34 raw fields per business, but the kit strips out the noise, geo coordinates, internal IDs, hours, images, so what you get is a usable lead list: name, phone, email, website, category, address, rating, and review count.

An optional `--socials` flag also pulls each business's Instagram, Facebook, and LinkedIn by scanning its website directly. That step runs as plain code, HTTP requests plus regex matching, so it costs zero AI tokens no matter how many businesses you scrape.

## Why Not Just Ask an AI to Scrape Google Maps Directly?

Asking a chatbot to fetch `maps.google.com` on its own returns close to nothing, because Google Maps sits behind a consent wall and renders its listings with JavaScript. A general-purpose AI hitting that page directly gets blocked before it sees a single result. Google Maps Scraper Kit sidesteps this by running a dedicated scraping engine locally and letting Claude Code drive it through the engine's own API, which reliably returns dozens to hundreds of clean rows per search.

| Approach | Result |
|---|---|
| Chatbot fetches maps.google.com directly | Hits consent wall + JS rendering, near 0 structured results |
| Google Maps Scraper Kit + Claude Code | Dozens to hundreds of clean rows per query |

## How Do You Set It Up?

Setup takes about five minutes, most of it spent waiting for Docker to pull the scraper image the first time.

1. Install Docker Desktop, then confirm it's running with `docker ps`.
2. Clone the kit from GitHub and start the scraper with `docker compose up -d`. It runs at `http://localhost:8080`.
3. Confirm it's alive by running `curl http://localhost:8080/api/v1/jobs`, which should print an empty list or existing jobs.
4. Open the project folder in Claude Code and ask in plain English, for example "scrape coffee shops in Austin."

Claude Code checks the container is running, builds a job with the required `max_time`, `lat`, and `lon` fields, polls until the scrape finishes, downloads the results, and hands you a clean table. The kit also ships four slash commands, `/scrape`, `/scrape-batch`, `/scrape-setup`, and `/scrape-jobs`, if you'd rather type a direct command than a sentence.

## What Should You Watch Out For?

Google Maps Scraper Kit hits Google Maps for real, so over-using it can get your IP temporarily rate-limited. This isn't a bug, it's Google pushing back on a script hitting its servers repeatedly. The project's own guidance is to run one job at a time, start at a `depth` of 5, and only raise it if you need more results. Signs you've been throttled include jobs coming back `failed`, empty results, or far fewer rows than an identical search returned before. None of this bans your actual Google account, and the block usually clears within minutes to hours.

For larger or repeated scraping jobs, the scraper supports rotating proxies (`socks5`, `socks5h`, `http`, or `https`) passed in the job body, which cuts down on rate limiting. Since scraped phone numbers and emails count as personal data, treat the output as a list of leads to verify and reach out to, not a dataset to resell, and follow GDPR, CCPA, or CAN-SPAM rules for however you plan to contact people.

## Who Actually Benefits From This?

Agency owners and freelancers doing local outreach are the clearest fit, since this kind of contact data is normally sold through subscription tools that charge per month regardless of how many leads you pull. Running it yourself means the cost is just your own computer's electricity and a bit of patience while Docker sets up. For a broader look at using AI to land nearby clients, see [Get Local Business Clients Fast Using AI](https://blog.digicuratoragency.com/get-local-business-clients-ai/), and for another free scraping approach worth comparing, [Scrape Thousands of Free Leads With Claude Code](https://blog.digicuratoragency.com/scrape-free-leads-claude-scrapegraphai/) covers a different tool built on ScrapeGraphAI.

## FAQ

### Is Google Maps Scraper Kit really free?

Yes. It's open-source and runs on your own computer through Docker, with no subscription fee and no cap on how much data you pull.

### Do I need to know how to code to use it?

No. Once Docker Desktop is installed and the container is running, you can talk to Claude Code in plain English, such as "scrape gyms in Miami," and it handles the rest.

### Does this violate Google's terms of service?

Scraping Google Maps goes against Google's terms of service, so use it responsibly, keep jobs to a reasonable size, and follow data protection law for any contact information you collect.

### Can it scrape Instagram or TikTok too?

No. It's built specifically for Google Maps business listings and intentionally does not trigger for social media scraping requests.

### What happens if my IP gets rate-limited?

Jobs typically start returning `failed` status or unusually short result sets. Slow down, lower the `depth` setting, or add proxies for large or repeated jobs. Your Google account itself is not affected, and IP blocks usually clear within minutes to hours.

If you want to build more systems like this without stitching together docs and forum posts on your own, [Vibe Coding Mastery](https://hub.digicuratoragency.com/about) walks through exactly how these AI-driven setups fit together. Join the Vibe Coding Build →

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Is Google Maps Scraper Kit really free?",
      "acceptedAnswer": { "@type": "Answer", "text": "Yes. It's open-source and runs on your own computer through Docker, with no subscription fee and no cap on how much data you pull." }
    },
    {
      "@type": "Question",
      "name": "Do I need to know how to code to use it?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. Once Docker Desktop is installed and the container is running, you can talk to Claude Code in plain English, such as \"scrape gyms in Miami,\" and it handles the rest." }
    },
    {
      "@type": "Question",
      "name": "Does this violate Google's terms of service?",
      "acceptedAnswer": { "@type": "Answer", "text": "Scraping Google Maps goes against Google's terms of service, so use it responsibly, keep jobs to a reasonable size, and follow data protection law for any contact information you collect." }
    },
    {
      "@type": "Question",
      "name": "Can it scrape Instagram or TikTok too?",
      "acceptedAnswer": { "@type": "Answer", "text": "No. It's built specifically for Google Maps business listings and intentionally does not trigger for social media scraping requests." }
    },
    {
      "@type": "Question",
      "name": "What happens if my IP gets rate-limited?",
      "acceptedAnswer": { "@type": "Answer", "text": "Jobs typically start returning failed status or unusually short result sets. Slow down, lower the depth setting, or add proxies for large or repeated jobs. Your Google account itself is not affected, and IP blocks usually clear within minutes to hours." }
    }
  ]
}
</script>
