---
layout: default
title: "Credits"
permalink: /credits
---

<style>
  .credits-page {
    max-width: 920px;
    margin: 0 auto;
  }
  .credits-hero {
    position: relative;
    overflow: hidden;
    background: linear-gradient(135deg, #243746 0%, #2c3e50 55%, #3d566e 100%);
    color: #fff;
    border-radius: 22px;
    padding: 44px 42px;
    margin-bottom: 28px;
    box-shadow: 0 18px 40px rgba(31,44,56,0.14);
  }
  .credits-hero::after {
    content: "";
    position: absolute;
    width: 240px; height: 240px;
    right: -90px; top: -110px;
    border-radius: 50%;
    background: rgba(255,255,255,0.08);
  }
  .credits-eyebrow {
    margin: 0 0 8px;
    font-size: 12px; font-weight: 800; text-transform: uppercase;
    letter-spacing: 0.14em; opacity: 0.7;
  }
  .credits-hero h1 {
    position: relative; z-index: 1;
    margin: 0 0 12px; font-size: 34px; line-height: 1.15;
  }
  .credits-hero p {
    position: relative; z-index: 1;
    margin: 0; max-width: 650px;
    color: rgba(255,255,255,0.82); font-size: 15px; line-height: 1.7;
  }
  .credits-grid {
    display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 18px;
  }
  @media (max-width: 760px) {
    .credits-grid { grid-template-columns: 1fr; }
    .credits-hero { padding: 34px 28px; }
    .credits-hero h1 { font-size: 29px; }
  }
  .person-card {
    position: relative;
    background: #fff; border: 1px solid var(--line); border-radius: 18px;
    padding: 24px 22px; text-align: center;
    box-shadow: 0 8px 24px rgba(31,44,56,0.05);
    transition: transform 0.18s ease, box-shadow 0.18s ease;
  }
  .person-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 13px 28px rgba(31,44,56,0.09);
  }
  .person-avatar {
    width: 62px; height: 62px; margin: 0 auto 16px;
    display: flex; align-items: center; justify-content: center;
    border-radius: 18px; background: #eef1f4; color: var(--accent);
    font-size: 18px; font-weight: 800;
  }
  .person-card h2 { margin: 0 0 7px; font-size: 18px; }
  .person-role {
    display: inline-flex; align-items: center; justify-content: center;
    min-height: 28px; padding: 4px 10px; border-radius: 999px;
    background: #f2f4f7; color: var(--muted);
    font-size: 12px; font-weight: 700;
  }
  .credits-footer {
    text-align: center; color: var(--muted); font-size: 13px;
    margin: 26px 0 8px;
  }
</style>

<div class="credits-page">
  <section class="credits-hero">
    <p class="credits-eyebrow">Cornerstone Guides</p>
    <h1>The people behind the site</h1>
    <p>Cornerstone Guides is built and maintained by a small team focused on making school resources easier to find, learn from, and share.</p>
  </section>

  <section class="credits-grid" aria-label="Cornerstone Guides team">
    <article class="person-card">
      <div class="person-avatar" aria-hidden="true">AT</div>
      <h2>Aarsh Tripathi</h2>
      <span class="person-role">President</span>
    </article>

    <article class="person-card">
      <div class="person-avatar" aria-hidden="true">RY</div>
      <h2>Ryan Yin</h2>
      <span class="person-role">Vice President</span>
    </article>

    <article class="person-card">
      <div class="person-avatar" aria-hidden="true">WN</div>
      <h2>William Nguyen</h2>
      <span class="person-role">Coder-in-Chief</span>
    </article>

    <article class="person-card">
      <div class="person-avatar" aria-hidden="true">VB</div>
      <h2>Vedansh Bandil</h2>
      <span class="person-role">Archivist</span>
    </article>
  </section>

  <p class="credits-footer">Built with care by the Cornerstone Guides team.</p>
</div>
