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
