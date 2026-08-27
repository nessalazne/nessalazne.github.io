---
layout: page
title: Follow Ness Alazne
permalink: /follow/
---

{% assign author = site.authors[site.author] %}

<div class="follow-wrapper">

  <div class="follow-hero">
    {% if author.avatar %}
    <img class="follow-avatar" src="{{ site.baseurl }}/{{ author.avatar }}" alt="{{ author.display_name }}">
    {% endif %}
    <h2 class="follow-name">{{ author.display_name }}</h2>
    <p class="follow-bio">{{ author.description }}</p>
    <p class="follow-prompt">Pick your platform. I post something new on all of them.</p>
  </div>

  <div class="follow-list">
    {% for s in site.socials %}
    <a class="follow-card" href="{{ s.url }}" target="_blank" rel="noopener" style="--brand: {{ s.color }};">
      <span class="follow-icon">
        <svg viewBox="0 0 24 24" width="26" height="26" fill="currentColor" aria-hidden="true" focusable="false">
        {% case s.icon %}
          {% when 'youtube' %}
          <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
          {% when 'instagram' %}
          <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
          {% when 'tiktok' %}
          <path d="M12.525.02c1.31-.02 2.61-.01 3.91-.02.08 1.53.63 3.09 1.75 4.17 1.12 1.11 2.7 1.62 4.24 1.79v4.03c-1.44-.05-2.89-.35-4.2-.97-.57-.26-1.1-.59-1.62-.93-.01 2.92.01 5.84-.02 8.75-.08 1.4-.54 2.79-1.35 3.94-1.31 1.92-3.58 3.17-5.91 3.21-1.43.08-2.86-.31-4.08-1.03-2.02-1.19-3.44-3.37-3.65-5.71-.02-.5-.03-1-.01-1.49.18-1.9 1.12-3.72 2.58-4.96 1.66-1.44 3.98-2.13 6.15-1.72.02 1.48-.04 2.96-.04 4.44-.99-.32-2.15-.23-3.02.37-.63.41-1.11 1.04-1.36 1.75-.21.51-.15 1.07-.14 1.61.24 1.64 1.82 3.02 3.5 2.87 1.12-.01 2.19-.66 2.77-1.61.19-.33.4-.67.41-1.06.1-1.79.06-3.57.07-5.36.01-4.03-.01-8.05.02-12.07z"/>
          {% when 'linkedin' %}
          <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
          {% when 'substack' %}
          <path d="M22.539 8.242H1.46V5.406h21.08v2.836zM1.46 10.812V24L12 18.11 22.54 24V10.812H1.46zM22.54 0H1.46v2.836h21.08V0z"/>
          {% when 'facebook' %}
          <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
        {% endcase %}
        </svg>
      </span>
      <span class="follow-text">
        <span class="follow-platform">{{ s.name }}</span>
        <span class="follow-handle">{{ s.handle }}</span>
        <span class="follow-blurb">{{ s.blurb }}</span>
      </span>
      <span class="follow-chevron" aria-hidden="true">&rarr;</span>
    </a>
    {% endfor %}
  </div>

  <p class="follow-footnote">
    Or grab a free guide <a href="{{ site.baseurl }}/get/">over here &rarr;</a>
  </p>

</div>

<style>
.follow-wrapper {
  max-width: 620px;
  margin: 2rem auto 3rem;
}
.follow-hero {
  text-align: center;
  padding: 2.25rem 1.5rem 1.75rem;
  background: #f8fffe;
  border: 1px solid #d4f0e5;
  border-radius: 10px;
  margin-bottom: 1.5rem;
}
.follow-avatar {
  width: 84px;
  height: 84px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid #fff;
  box-shadow: 0 2px 10px rgba(0,0,0,0.12);
  margin-bottom: 0.9rem;
}
.follow-name {
  font-size: 1.5rem;
  font-weight: 700;
  color: #111;
  margin: 0 0 0.4rem;
}
.follow-bio {
  font-size: 1rem;
  color: #555;
  margin: 0 auto 0.9rem;
  max-width: 26rem;
  line-height: 1.5;
}
.follow-prompt {
  font-size: 0.95rem;
  color: #00ab6b;
  font-weight: 600;
  margin: 0;
}
.follow-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}
.follow-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.9rem 1.1rem;
  min-height: 72px;
  background: #fff;
  border: 1px solid #e6e6e6;
  border-radius: 10px;
  text-decoration: none;
  transition: transform 0.15s ease, box-shadow 0.15s ease, border-color 0.15s ease;
}
.follow-card:hover,
.follow-card:focus {
  transform: translateY(-2px);
  border-color: var(--brand);
  box-shadow: 0 6px 18px rgba(0,0,0,0.09);
  text-decoration: none;
}
.follow-icon {
  flex: 0 0 48px;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  color: var(--brand);
  background: color-mix(in srgb, var(--brand) 10%, #fff);
  transition: background 0.15s ease, color 0.15s ease;
}
/* Fallback tint for browsers without color-mix() */
@supports not (background: color-mix(in srgb, red 10%, white)) {
  .follow-icon { background: #f4f4f4; }
}
.follow-card:hover .follow-icon,
.follow-card:focus .follow-icon {
  background: var(--brand);
  color: #fff;
}
.follow-text {
  flex: 1 1 auto;
  min-width: 0;
  display: flex;
  flex-direction: column;
  line-height: 1.35;
}
.follow-platform {
  font-size: 1.05rem;
  font-weight: 700;
  color: #111;
}
.follow-handle {
  font-size: 0.85rem;
  color: var(--brand);
  font-weight: 600;
}
.follow-blurb {
  font-size: 0.88rem;
  color: #666;
  margin-top: 0.15rem;
}
.follow-chevron {
  flex: 0 0 auto;
  font-size: 1.2rem;
  color: #bbb;
  transition: color 0.15s ease, transform 0.15s ease;
}
.follow-card:hover .follow-chevron,
.follow-card:focus .follow-chevron {
  color: var(--brand);
  transform: translateX(3px);
}
.follow-footnote {
  text-align: center;
  margin-top: 1.75rem;
  font-size: 0.95rem;
  color: #777;
}
.follow-footnote a {
  color: #00ab6b;
  font-weight: 600;
}
@media (max-width: 480px) {
  .follow-card { padding: 0.8rem 0.85rem; gap: 0.8rem; }
  .follow-icon { flex-basis: 44px; width: 44px; height: 44px; border-radius: 10px; }
  .follow-blurb { display: none; }
  .follow-avatar { width: 72px; height: 72px; }
}
</style>
