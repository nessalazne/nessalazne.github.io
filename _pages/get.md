---
layout: page
title: Get Your Free Guide
permalink: /get/
---

<div class="keyword-lookup-wrapper">

  <div class="keyword-lookup-hero">
    <p class="keyword-lookup-sub">Type the keyword from the video below</p>
    <form id="keywordForm" onsubmit="lookupKeyword(event)">
      <div class="keyword-input-row">
        <input
          type="text"
          id="keywordInput"
          class="keyword-input"
          placeholder="e.g. EDIT"
          autocomplete="off"
          autocorrect="off"
          autocapitalize="off"
          spellcheck="false"
        />
        <button type="submit" class="keyword-btn">Get It →</button>
      </div>
    </form>
  </div>

  <div id="keywordResults"></div>

</div>

<style>
.keyword-lookup-wrapper {
  max-width: 620px;
  margin: 2rem auto 3rem;
}
.keyword-lookup-hero {
  text-align: center;
  padding: 2.5rem 1.5rem 2rem;
  background: #f8fffe;
  border: 1px solid #d4f0e5;
  border-radius: 10px;
  margin-bottom: 1.5rem;
}
.keyword-lookup-sub {
  font-size: 1.05rem;
  color: #555;
  margin-bottom: 1.25rem;
}
.keyword-input-row {
  display: flex;
  gap: 0.5rem;
  justify-content: center;
  flex-wrap: wrap;
}
.keyword-input {
  flex: 1;
  min-width: 200px;
  max-width: 320px;
  padding: 0.6rem 1rem;
  font-size: 1.1rem;
  border: 2px solid #1a5d1a;
  border-radius: 6px;
  outline: none;
  letter-spacing: 0.04em;
  font-weight: 600;
  color: #222;
}
.keyword-input:focus {
  border-color: #123d12;
  box-shadow: 0 0 0 3px rgba(26,93,26,0.15);
}
.keyword-btn {
  padding: 0.6rem 1.4rem;
  background: #1a5d1a;
  color: #fff;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  transition: background 0.2s;
  white-space: nowrap;
}
.keyword-btn:hover {
  background: #123d12;
}

/* Result cards */
.keyword-results-label {
  font-size: 0.85rem;
  color: #888;
  text-align: center;
  margin-bottom: 0.75rem;
}
.keyword-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 1.1rem 1.25rem;
  border: 1px solid #d4f0e5;
  border-left: 4px solid #1a5d1a;
  border-radius: 8px;
  margin-bottom: 0.75rem;
  background: #fff;
  flex-wrap: wrap;
}
.keyword-card-info {
  flex: 1;
  min-width: 200px;
}
.keyword-card-title {
  font-weight: 700;
  font-size: 1rem;
  color: #222;
  margin-bottom: 0.2rem;
}
.keyword-card-desc {
  font-size: 0.88rem;
  color: #666;
  margin: 0;
}
.keyword-card-btn {
  display: inline-block;
  padding: 0.5rem 1.1rem;
  background: #1a5d1a;
  color: #fff !important;
  border-radius: 6px;
  font-size: 0.9rem;
  font-weight: 700;
  text-decoration: none !important;
  white-space: nowrap;
  transition: background 0.2s;
}
.keyword-card-btn:hover {
  background: #123d12;
  color: #fff !important;
}
.keyword-card-actions {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.5rem;
}
.keyword-card-post-link {
  font-size: 0.82rem;
  color: #1a5d1a !important;
  text-decoration: none !important;
  text-align: right;
  white-space: nowrap;
}
.keyword-card-post-link:hover {
  text-decoration: underline !important;
  color: #123d12 !important;
}

/* Not found */
.keyword-not-found {
  text-align: center;
  padding: 1.5rem;
  background: #fff8f8;
  border: 1px solid #f5c6c6;
  border-radius: 8px;
  color: #c0392b;
  font-size: 0.95rem;
}
.keyword-not-found strong {
  display: block;
  font-size: 1rem;
  margin-bottom: 0.25rem;
}
</style>

<script>
var GUIDES = {
  "vox": [
    {
      title: "The Vox Animation Playbook",
      desc: "The Complete 10-State Engine for Free Documentary Paper-Collage Videos",
      url: "https://hub.digicuratoragency.com/freebie?kw=vox",
      post: "https://blog.digicuratoragency.com/vox-style-animations-free-ai/"
    }
  ],
  "hyperframes": [
    {
      title: "The HyperFrames Playbook",
      desc: "Your Free Guide to Building Animated Explainer Videos Inside Claude",
      url: "https://hub.digicuratoragency.com/freebie?kw=hyperframes",
      post: "https://blog.digicuratoragency.com/hyperframes-free-animated-explainer-videos-claude/"
    }
  ],
  "design": [
    {
      title: "The AI App Design Playbook",
      desc: "Your System for Turning a Generic AI App Into One Users Open Daily",
      url: "https://hub.digicuratoragency.com/freebie?kw=design",
      post: "https://blog.digicuratoragency.com/ai-app-design-conversion-system/"
    }
  ],
  "repurpose": [
    {
      title: "The Content Repurposing Playbook",
      desc: "Turn One Video Into a Video, Blog Post, and Lead Magnet in Minutes",
      url: "https://hub.digicuratoragency.com/freebie?kw=repurpose",
      post: "https://blog.digicuratoragency.com/repurpose-content-automatically-video-blog-freebie/"
    }
  ],
  "director": [
    {
      title: "The Vibe Directing Playbook",
      desc: "Your Step-by-Step Guide to Building Full AI Films From One Sentence",
      url: "https://hub.digicuratoragency.com/freebie?kw=director",
      post: "https://blog.digicuratoragency.com/vibe-directing-openart-director-ai-video/"
    }
  ],
  "apps": [
    {
      title: "The Niche App Playbook",
      desc: "Your 3-Phase Guide to Turning a Free Tool's Gap Into a Focused App People Pay For",
      url: "https://hub.digicuratoragency.com/freebie?kw=apps",
      post: "https://blog.digicuratoragency.com/simple-niche-apps-40k-month/"
    }
  ],
  "builder": [
    {
      title: "The Full-App Builder Playbook",
      desc: "The 4-step system to build a deployable app with Claude Code \u2014 auth, payments and dashboard, no developers needed.",
      url: "https://hub.digicuratoragency.com/freebie?kw=builder",
      post: "https://blog.digicuratoragency.com/build-full-app-claude-code/"
    }
  ],
  "app": [
    {
      title: "The Zero-Code App Launch Playbook",
      desc: "Your 5-step playbook to go from idea to a live app in hours with Claude Code and Railway \u2014 no dev team, no code.",
      url: "https://hub.digicuratoragency.com/freebie?kw=app",
      post: "https://blog.digicuratoragency.com/claude-code-railway-live-app/"
    },
    {
      title: "The Reverse-Engineer Playbook",
      desc: "Turn a proven app's bad reviews into your build plan \u2014 worked on a real meal tracker",
      url: "https://hub.digicuratoragency.com/freebie?kw=app",
      post: "https://blog.digicuratoragency.com/reverse-engineer-app-claude-code/"
    }
  ],
  "receipt": [
    {
      title: "The Boring App Build Playbook",
      desc: "The screenshot prompt that makes Claude Code reverse-engineer a proven App Store app, the PRD it returns, and the phased build prompt — worked through on a $80K/month receipt tracker.",
      url: "https://hub.digicuratoragency.com/freebie?kw=receipt",
      post: "https://blog.digicuratoragency.com/boring-apps-receipt-tracker-claude-code/"
    }
  ],
  "prompts": [
    {
      title: "How to Actually Prompt Fable 5",
      desc: "Anthropic's field guide to Fable 5 — effort levels, the verification prompt that stops it faking progress, and the memory + sub-agent setups that make it reliable on long runs.",
      url: "https://guides.digicuratoragency.com/guides/fable-5-prompting-guide",
      post: "https://blog.digicuratoragency.com/fable-5-prompting-guide/"
    }
  ],
  "prompt": [
    {
      title: "How to Actually Prompt Fable 5",
      desc: "Anthropic's field guide to Fable 5 — effort levels, the verification prompt that stops it faking progress, and the memory + sub-agent setups that make it reliable on long runs.",
      url: "https://guides.digicuratoragency.com/guides/fable-5-prompting-guide",
      post: "https://blog.digicuratoragency.com/fable-5-prompting-guide/"
    }
  ],
  "niche": [
    {
      title: "The Trending Niche Finder",
      desc: "The exact Claude Code research prompt and 5-signal scoring framework to find trending, low-competition content niches in minutes — no guessing.",
      url: "https://guides.digicuratoragency.com/guides/ai-find-trending-content-niches",
      post: "https://blog.digicuratoragency.com/ai-find-trending-content-niches/"
    }
  ],
  "spy": [
    {
      title: "The Trending Niche Finder",
      desc: "The exact Claude Code research prompt and 5-signal scoring framework to find trending, low-competition content niches in minutes — no guessing.",
      url: "https://guides.digicuratoragency.com/guides/ai-find-trending-content-niches",
      post: "https://blog.digicuratoragency.com/ai-find-trending-content-niches/"
    }
  ],
  "fable": [
    {
      title: "Fable vs Opus: The 4 App-Build Test Prompts",
      desc: "The exact 4 prompts used to test Claude Fable 5 against Opus — one per app (quiz app, booking app, landing page, simulation game) so you can run the same head-to-head yourself.",
      url: "https://guides.digicuratoragency.com/guides/claude-fable-vs-opus",
      post: "https://blog.digicuratoragency.com/claude-fable-vs-opus/"
    },
    {
      title: "Fable 5's Leaked System Prompt, Decoded",
      desc: "The full 120,000-character Fable 5 system prompt leak, where to read it, and how to inject its reasoning structure into a cheaper open-source model.",
      url: "https://blog.digicuratoragency.com/fable-5-leaked-system-prompt/"
    },
    {
      title: "The Chef's Kitchen Loop for Claude Code",
      desc: "The 3-tier model system — head chef, sous chef, line cooks — plus the exact executor sub-agent and loop setup to stop burning your best Claude model on grunt work.",
      url: "https://guides.digicuratoragency.com/guides/chefs-kitchen-loop-claude-code",
      post: "https://blog.digicuratoragency.com/chefs-kitchen-loop-claude-code/"
    }
  ],
  "edit": [
    {
      title: "Claude Design → Video Cheat Sheet",
      desc: "Turn Claude-generated designs into polished short-form video with the Hyperframes workflow.",
      url: "https://guides.digicuratoragency.com/guides/claude-design-hyperframes",
      post: "https://blog.digicuratoragency.com/claude-design-to-video-hyperframes/"
    }
  ],
  "research": [
    {
      title: "Claude + NotebookLM Research Guide",
      desc: "A step-by-step setup guide for pairing Claude Code with NotebookLM for deep research workflows.",
      url: "https://guides.digicuratoragency.com/guides/claude-notebooklm-research",
      post: "https://blog.digicuratoragency.com/claude-code-notebooklm-research/"
    }
  ],
  "routine": [
    {
      title: "Claude Code Routines Cheat Sheet",
      desc: "2-page PDF covering all 3 trigger types, the 5-element prompt formula, and the top workflows to build first.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-routines",
      post: "https://blog.digicuratoragency.com/claude-code-routines-automate-workflows/"
    }
  ],
  "blueprint": [
    {
      title: "Claude Code Folder Setup Guide",
      desc: "3-page PDF with the full folder structure diagram and a checklist to get your project configured in under 20 minutes.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-folder-setup",
      post: "https://blog.digicuratoragency.com/claude-code-folder-setup/"
    }
  ],
  "activate": [
    {
      title: "Claude Code 4-File System Cheat Sheet",
      desc: "The exact 4 files that activate Claude's full context — a quick-reference guide for your Claude Code setup.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-setup-4-file-system",
      post: "https://blog.digicuratoragency.com/claude-code-setup-4-file-system/"
    }
  ],
  "claude": [
    {
      title: "Claude Code Beginner's Playbook",
      desc: "Your No-Code Guide to Building Real Apps With Claude Code",
      url: "https://hub.digicuratoragency.com/freebie?kw=claude",
      post: "https://blog.digicuratoragency.com/claude-code-for-non-developers/"
    },
    {
      title: "Claude 101: Beginner's Cheat Sheet",
      desc: "A quick-reference PDF with the 3-part prompt formula, 5 essential Claude commands, and the top 3 workflows to set up first.",
      url: "https://guides.digicuratoragency.com/guides/claude-101-beginners-guide",
      post: "https://blog.digicuratoragency.com/claude-101-beginners-guide/"
    }
  ],
  "extension": [
    {
      title: "Chrome Extension Content Automation Setup Guide",
      desc: "Step-by-step PDF showing how to install the extension, connect your accounts, and automate posting to every platform in under 20 minutes.",
      url: "https://guides.digicuratoragency.com/guides/chrome-extension-content-automation",
      post: "https://blog.digicuratoragency.com/chrome-extension-content-automation/"
    }
  ],
  "build": [
    {
      title: "The Weekend App Playbook",
      desc: "Your 3-Phase Guide to Shipping a Monetizable App Prototype in One Weekend",
      url: "https://hub.digicuratoragency.com/freebie?kw=build",
      post: "https://blog.digicuratoragency.com/build-app-prototype-weekend-no-coding/"
    },
    {
      title: "The App Idea Research Prompt Guide",
      desc: "Screenshot Any App, Get a Full Business Case: The Claude Reverse-Engineering Prompt + a Worked Example",
      url: "https://hub.digicuratoragency.com/freebie?kw=build",
      post: "https://blog.digicuratoragency.com/app-idea-research-claude/"
    },
    {
      title: "Claude Code 4 Tips Cheat Sheet",
      desc: "A 1-page quick-reference guide covering the 4 Claude Code tips that shift it from a chatbot into a full agentic workflow system — CLAUDE.md, Skills, Sub-agents, and Hooks.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-4-tips",
      post: "https://blog.digicuratoragency.com/claude-code-4-tips/"
    },
    {
      title: "Build a $1M App With Claude Code — Prompt Guide",
      desc: "Two power prompts for reverse-engineering any top App Store app from screenshots and building your own version with Claude Code — no dev team needed.",
      url: "https://guides.digicuratoragency.com/guides/build-1m-app-claude-code",
      post: "https://blog.digicuratoragency.com/build-1m-app-claude-code/"
    }
  ],
  "remotion": [
    {
      title: "Remotion + Claude Code Setup Guide",
      desc: "A 5-phase setup guide for building animated videos with Remotion inside Claude Code and Antigravity IDE — no video editor needed.",
      url: "https://guides.digicuratoragency.com/guides/remotion-claude-code-video-creator",
      post: "https://blog.digicuratoragency.com/remotion-claude-code-video-creator/"
    }
  ],
  "clone": [
    {
      title: "The Website Cloning Playbook",
      desc: "Clone any page with Claude + Ditto MCP, then make it yours in 4 steps",
      url: "https://hub.digicuratoragency.com/freebie?kw=clone",
      post: "https://blog.digicuratoragency.com/clone-any-website-claude-ditto-mcp/"
    },
    {
      title: "Clone Any $800K App in 15 Minutes",
      desc: "A 4-phase cheat sheet for cloning any SaaS app using Claude Code — no dev team, no coding background, and no $800K budget required.",
      url: "https://guides.digicuratoragency.com/guides/clone-800k-app-claude-code",
      post: "https://blog.digicuratoragency.com/clone-800k-app-claude-code/"
    }
  ],
  "codes": [
    {
      title: "5 Must-Have Claude Code Skills for Creators",
      desc: "The 5 open-source Claude Code skills and AI tools that automate your content workflow — with direct links to install each one today.",
      url: "https://guides.digicuratoragency.com/guides/5-skills-for-creators-claude-code",
      post: "https://blog.digicuratoragency.com/5-skills-for-creators-claude-code/"
    }
  ],
  "carousel": [
    {
      title: "Carousel Video Creator + App Builder Prompt Guide",
      desc: "The exact prompts for generating AI carousel videos with Higgsfield MCP or Kie.ai — plus the two-prompt system for reverse-engineering any $1M App Store app with Claude Code.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-carousel-video-higgsfield-kieai",
      post: "https://blog.digicuratoragency.com/claude-code-carousel-video-higgsfield-kieai/"
    }
  ],
  "wiggum": [
    {
      title: "Chief Wiggum Goal Execution System",
      desc: "Paste-ready /goal and Mission Control skill blocks for Claude Code — the two-layer AI goal execution system that actually ships your goals.",
      url: "https://guides.digicuratoragency.com/guides/chief-wiggum-ai-goal-executor",
      post: "https://blog.digicuratoragency.com/chief-wiggum-ai-goal-executor/"
    }
  ],
  "skill": [
    {
      title: "5 Claude Code Skills — Real Project Setup Guide",
      desc: "The 5-skill stack that automates your entire content workflow — with step-by-step instructions for each skill and the exact sequence to run them in a real project.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-5-skills-project",
      post: "https://blog.digicuratoragency.com/claude-code-5-skills-project/"
    }
  ],
  "growthos": [
    {
      title: "Beat Context Rot: The Claude Code Handoff Method",
      desc: "The six-section handoff.md template and copy-paste prompt that stop Claude Code sessions from getting dumber the longer they run.",
      url: "https://guides.digicuratoragency.com/guides/beat-context-rot-claude-code-handoff",
      post: "https://blog.digicuratoragency.com/beat-context-rot-claude-code-handoff/"
    }
  ],
  "subagent": [
    {
      title: "Beat Context Rot: The Claude Code Handoff Method",
      desc: "The six-section handoff.md template and copy-paste prompt that stop Claude Code sessions from getting dumber the longer they run.",
      url: "https://guides.digicuratoragency.com/guides/beat-context-rot-claude-code-handoff",
      post: "https://blog.digicuratoragency.com/beat-context-rot-claude-code-handoff/"
    }
  ],
  "sub agent": [
    {
      title: "Beat Context Rot: The Claude Code Handoff Method",
      desc: "The six-section handoff.md template and copy-paste prompt that stop Claude Code sessions from getting dumber the longer they run.",
      url: "https://guides.digicuratoragency.com/guides/beat-context-rot-claude-code-handoff",
      post: "https://blog.digicuratoragency.com/beat-context-rot-claude-code-handoff/"
    }
  ],
  "cms": [
    {
      title: "Claude Code CMS Dashboard Playbook",
      desc: "A practical build checklist, data model, safety rules, and Claude Code prompt for adding a client-safe CMS to AI-built websites.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-cms-dashboard",
      post: "https://blog.digicuratoragency.com/claude-code-cms-dashboard/"
    }
  ],
  "studio": [
    {
      title: "The Malleable Software Playbook",
      desc: "A step-by-step playbook for auditing your current software stack and building flexible AI business systems you own — with Claude Code prompts included.",
      url: "https://guides.digicuratoragency.com/guides/malleable-software-ai-business",
      post: "https://blog.digicuratoragency.com/malleable-software-ai-business/"
    }
  ],
  "commands": [
    {
      title: "Claude Code Slash Commands Cheat Sheet",
      desc: "All 12 must-know Claude Code slash commands — the 7 from the video plus 5 more builder commands — with what each does, when to use it, and a pro tip.",
      url: "https://guides.digicuratoragency.com/guides/claude-code-slash-commands",
      post: "https://blog.digicuratoragency.com/claude-code-slash-commands/"
    },
    {
      title: "Claude Slash Commands Cheat Sheet",
      desc: "10 built-in Claude Code slash commands — 6 from the video plus 4 essential builder commands — with what each does, when to use it, and pro tips.",
      url: "https://guides.digicuratoragency.com/guides/claude-slash-commands-guide",
      post: "https://blog.digicuratoragency.com/claude-slash-commands-guide/"
    }
  ]
};

function lookupKeyword(e) {
  e.preventDefault();
  var raw = document.getElementById('keywordInput').value.trim();
  var key = raw.toLowerCase();
  var resultsEl = document.getElementById('keywordResults');

  if (!key) {
    resultsEl.innerHTML = '';
    return;
  }

  var matches = GUIDES[key];

  if (!matches || matches.length === 0) {
    resultsEl.innerHTML =
      '<div class="keyword-not-found">' +
        '<strong>Keyword not found.</strong>' +
        'Double-check the word from the video — keywords are not case-sensitive.' +
      '</div>';
    return;
  }

  var label = matches.length > 1
    ? '<p class="keyword-results-label">' + matches.length + ' guides found for <strong>' + raw.toUpperCase() + '</strong></p>'
    : '<p class="keyword-results-label">Here\'s your free guide for <strong>' + raw.toUpperCase() + '</strong></p>';

  var cards = matches.map(function(g) {
    var postLink = g.post
      ? '<a href="' + g.post + '" class="keyword-card-post-link">Read the blog post →</a>'
      : '';
    return (
      '<div class="keyword-card">' +
        '<div class="keyword-card-info">' +
          '<div class="keyword-card-title">' + g.title + '</div>' +
          '<p class="keyword-card-desc">' + g.desc + '</p>' +
        '</div>' +
        '<div class="keyword-card-actions">' +
          '<a href="' + g.url + '" target="_blank" rel="noopener" class="keyword-card-btn">Get the Free Guide →</a>' +
          postLink +
        '</div>' +
      '</div>'
    );
  }).join('');

  resultsEl.innerHTML = label + cards;
  resultsEl.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
}
</script>
