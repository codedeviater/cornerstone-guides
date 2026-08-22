---
layout: default
title: "Study Guides"
permalink: /guides
---

<style>
  .subject-group { margin: 28px 0; }
  .subject-group h2 { font-size: 18px; margin: 0 0 10px; }
  .guide-link-row {
    display: flex; align-items: center; justify-content: space-between;
    padding: 14px 18px; border: 1px solid #e6e8eb; border-radius: 12px;
    margin-bottom: 8px; background: #fff; text-decoration: none; color: inherit;
  }
  .guide-link-row:hover { border-color: #2c3e50; }
  .guide-link-row .title { font-weight: 600; font-size: 14px; }
  .guide-link-row .meta { font-size: 12px; color: #6b7684; }
  #guides-empty, #guides-loading { text-align: center; padding: 40px 0; color: #6b7684; }
</style>

<div id="guides-loading">Loading guides…</div>
<div id="guides-empty" style="display:none;">No guides have been published yet. Check back soon.</div>
<div id="guides-list"></div>

<script>
(function () {
  const API_BASE = "https://cornerstone-guides-backend.vercel.app";

  fetch(`${API_BASE}/api/guides`)
    .then((res) => res.json())
    .then((guides) => {
      document.getElementById("guides-loading").style.display = "none";
      if (!Array.isArray(guides) || guides.length === 0) {
        document.getElementById("guides-empty").style.display = "block";
        return;
      }

      const groups = {};
      guides.forEach((g) => {
        const key = g.subject || "General";
        if (!groups[key]) groups[key] = [];
        groups[key].push(g);
      });

      const container = document.getElementById("guides-list");
      container.innerHTML = Object.keys(groups).sort().map((subject) => `
        <div class="subject-group">
          <h2>${subject}</h2>
          ${groups[subject].map((g) => `
            <a class="guide-link-row" href="/guides/${g.slug}">
              <div>
                <div class="title">${g.title}</div>
                <div class="meta">${g.section ? g.section + " • " : ""}Updated ${new Date(g.updated_at).toLocaleDateString()}</div>
              </div>
              <span>&rarr;</span>
            </a>
          `).join("")}
        </div>
      `).join("");
    })
    .catch(() => {
      document.getElementById("guides-loading").textContent = "Couldn't load guides right now.";
    });
})();
</script>
