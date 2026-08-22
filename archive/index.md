---
layout: default
title: "Archive"
permalink: /archive
---

<style>
  .archive-signed-out { font-size: 14px; color: #6b7684; }
  .arc-section { margin-bottom: 34px; }
  .arc-section h2 { font-size: 16px; margin: 0 0 4px; }
  .arc-section .arc-sub { font-size: 12px; color: #6b7684; margin-bottom: 14px; }

  .arc-upload-card {
    background: #fff; border: 1px solid #e6e8eb; border-radius: 14px; padding: 18px;
    display: flex; flex-direction: column; gap: 12px; max-width: 480px;
  }
  .arc-field label { display: block; font-size: 12px; font-weight: 600; margin-bottom: 5px; }
  .arc-field input[type=text], .arc-field input[type=file] {
    width: 100%; padding: 9px 10px; border: 1px solid #e6e8eb; border-radius: 8px; font-size: 13px; box-sizing: border-box;
  }
  .arc-class-picker { position: relative; }
  .arc-class-pill {
    border: 1px solid #e6e8eb; border-radius: 8px; padding: 9px 10px; font-size: 13px;
    display: flex; justify-content: space-between; cursor: pointer; background: #fff;
  }
  .arc-class-dropdown {
    display: none; position: absolute; top: calc(100% + 4px); left: 0; right: 0; z-index: 10;
    background: #fff; border: 1px solid #e6e8eb; border-radius: 10px; box-shadow: 0 10px 30px rgba(0,0,0,0.08);
    max-height: 220px; overflow-y: auto; padding: 6px;
  }
  .arc-class-dropdown.open { display: block; }
  .arc-class-dropdown input { width: 100%; padding: 7px 8px; border: 1px solid #e6e8eb; border-radius: 6px; font-size: 12px; margin-bottom: 6px; box-sizing: border-box; }
  .arc-class-dropdown div[data-value] { padding: 7px 8px; font-size: 13px; border-radius: 6px; cursor: pointer; }
  .arc-class-dropdown div[data-value]:hover { background: #f3f4f6; }

  .arc-upload-status { font-size: 12px; }
  .arc-upload-status.ok { color: #1a7f37; }
  .arc-upload-status.err { color: #c0362c; }

  .arc-filter-row { display: flex; align-items: center; gap: 10px; margin-bottom: 14px; }
  .arc-filter-row select { padding: 7px 10px; border: 1px solid #e6e8eb; border-radius: 8px; font-size: 13px; }

  .arc-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 14px; }
  .arc-item {
    background: #fff; border: 1px solid #e6e8eb; border-radius: 12px; padding: 14px;
    display: flex; flex-direction: column; gap: 6px; cursor: pointer;
  }
  .arc-item:hover { border-color: #cfd4da; }
  .arc-item .arc-tag {
    align-self: flex-start; background: #eef1f4; color: #2c3e50; border-radius: 999px;
    padding: 3px 9px; font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.04em;
  }
  .arc-item .arc-title { font-size: 14px; font-weight: 600; }
  .arc-item .arc-meta { font-size: 11px; color: #6b7684; }

  .arc-list { display: flex; flex-direction: column; gap: 10px; }
  .arc-row {
    background: #fff; border: 1px solid #e6e8eb; border-radius: 12px; padding: 12px 14px;
    display: flex; align-items: center; justify-content: space-between; gap: 12px; flex-wrap: wrap;
  }
  .arc-row-main { display: flex; flex-direction: column; gap: 3px; }
  .arc-row-title { font-size: 13px; font-weight: 600; }
  .arc-row-meta { font-size: 11px; color: #6b7684; }
  .arc-badge { font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.04em; padding: 3px 9px; border-radius: 999px; }
  .arc-badge.pending { background: #fff4d6; color: #8a6300; }
  .arc-badge.approved { background: #d9f2e3; color: #1a7f37; }
  .arc-badge.rejected { background: #fbdcd8; color: #c0362c; }
  .arc-row-actions { display: flex; align-items: center; gap: 8px; }
  .arc-row-actions button, .arc-row-actions select {
    padding: 6px 12px; border-radius: 999px; border: 1px solid #e6e8eb; background: #fff; font-size: 12px; cursor: pointer; font-weight: 600;
  }
  .arc-row-actions button.primary { background: #2c3e50; color: #fff; border-color: #2c3e50; }
  .arc-row-actions button.danger { color: #c0362c; border-color: #f3c9c4; }
  .arc-empty { font-size: 13px; color: #6b7684; }
</style>

<div id="archive-signed-out" class="archive-signed-out">Sign in to upload, browse, and track archive uploads.</div>

<div id="archive-app" style="display:none;">

  <div class="arc-section">
    <h2>Upload</h2>
    <div class="arc-sub" id="arc-upload-sub">Pick a class if you know it — staff can tag it later if you leave it blank.</div>
    <div class="arc-upload-card">
      <div class="arc-field">
        <label>Title</label>
        <input type="text" id="arc-upload-title" placeholder="e.g. Unit 4 review sheet" />
      </div>
      <div class="arc-field">
        <label>Class (optional)</label>
        <div class="arc-class-picker" id="arc-class-picker">
          <div class="arc-class-pill" id="arc-class-pill"><span id="arc-class-pill-text">Select a class…</span><span>▾</span></div>
          <div class="arc-class-dropdown" id="arc-class-dropdown">
            <input type="text" id="arc-class-search" placeholder="Search classes…" />
            <div id="arc-class-options"></div>
          </div>
        </div>
      </div>
      <div class="arc-field">
        <label>File</label>
        <input type="file" id="arc-upload-file" />
      </div>
      <div class="arc-field">
        <button class="btn primary" id="arc-upload-btn" type="button">Upload</button>
        <div class="arc-upload-status" id="arc-upload-status"></div>
      </div>
    </div>
  </div>

  <div class="arc-section" id="arc-pending-section" style="display:none;">
    <h2>Pending review <span class="staff-star">★</span></h2>
    <div class="arc-sub">Approve (optionally set a class) or reject each upload.</div>
    <div class="arc-list" id="arc-pending-list"><div class="arc-empty">Loading…</div></div>
  </div>

  <div class="arc-section">
    <h2>My uploads</h2>
    <div class="arc-sub">Track the status of what you've submitted.</div>
    <div class="arc-list" id="arc-mine-list"><div class="arc-empty">Loading…</div></div>
  </div>

  <div class="arc-section">
    <h2>Browse the archive</h2>
    <div class="arc-sub">Approved uploads from everyone.</div>
    <div class="arc-filter-row">
      <select id="arc-browse-filter"><option value="">All classes</option></select>
    </div>
    <div class="arc-grid" id="arc-browse-grid"><div class="arc-empty">Loading…</div></div>
  </div>

</div>

<script>
const ARCHIVE_API_BASE = "https://cornerstone-guides-backend.vercel.app";
let arcClasses = [];
let arcSelectedClassId = "";
let arcIsStaff = false;

async function arcAuthedFetch(path, opts = {}) {
  const headers = Object.assign({ "Content-Type": "application/json" }, opts.headers || {});
  if (window.clerkToken) headers["Authorization"] = `Bearer ${window.clerkToken}`;
  const res = await fetch(`${ARCHIVE_API_BASE}${path}`, Object.assign({}, opts, { headers }));
  if (!res.ok) {
    const body = await res.json().catch(() => ({}));
    throw new Error(body.error || `${path} -> ${res.status}`);
  }
  return res.json();
}

function fileToBase64(file) {
  return new Promise((resolve, reject) => {
    const r = new FileReader();
    r.onload = () => resolve(r.result.split(",")[1]);
    r.onerror = () => reject(new Error("Couldn't read file"));
    r.readAsDataURL(file);
  });
}

window.addEventListener("clerk-ready", async (e) => {
  if (!e.detail.user) {
    document.getElementById("archive-signed-out").style.display = "block";
    document.getElementById("archive-app").style.display = "none";
    return;
  }
  document.getElementById("archive-signed-out").style.display = "none";
  document.getElementById("archive-app").style.display = "block";

  await loadArcClasses();
  await checkArcStaff(e.detail.user.username);
  loadArcMine();
  loadArcBrowse();
  if (arcIsStaff) {
    document.getElementById("arc-pending-section").style.display = "block";
    loadArcPending();
  }
});

async function checkArcStaff(username) {
  arcIsStaff = false;
  if (!username) return;
  try {
    const staff = await arcAuthedFetch("/api/staff");
    arcIsStaff = staff.includes(username.toLowerCase());
  } catch (err) { /* not fatal */ }
}

async function loadArcClasses() {
  try {
    arcClasses = await arcAuthedFetch("/api/classes");
  } catch (err) {
    arcClasses = [];
  }
  renderArcClassOptions(arcClasses);
  const filter = document.getElementById("arc-browse-filter");
  arcClasses.forEach(c => {
    const opt = document.createElement("option");
    opt.value = c.id; opt.textContent = c.name;
    filter.appendChild(opt);
  });
  filter.addEventListener("change", () => loadArcBrowse(filter.value));
}

function renderArcClassOptions(list) {
  const container = document.getElementById("arc-class-options");
  if (!list.length) { container.innerHTML = `<div style="opacity:0.6;">No classes found</div>`; return; }
  container.innerHTML = list.map(c => `<div data-value="${c.id}">${c.name}</div>`).join("");
}

document.getElementById("arc-class-pill").addEventListener("click", () => {
  document.getElementById("arc-class-dropdown").classList.toggle("open");
});
document.getElementById("arc-class-dropdown").addEventListener("click", (e) => {
  if (e.target.dataset.value) {
    arcSelectedClassId = e.target.dataset.value;
    document.getElementById("arc-class-pill-text").textContent = e.target.textContent;
    document.getElementById("arc-class-dropdown").classList.remove("open");
  }
});
document.getElementById("arc-class-search").addEventListener("input", (e) => {
  const q = e.target.value.trim().toLowerCase();
  renderArcClassOptions(!q ? arcClasses : arcClasses.filter(c => c.name.toLowerCase().includes(q)));
});
document.addEventListener("click", (e) => {
  const picker = document.getElementById("arc-class-picker");
  if (picker && !picker.contains(e.target)) document.getElementById("arc-class-dropdown").classList.remove("open");
});

document.getElementById("arc-upload-btn").addEventListener("click", async () => {
  const title = document.getElementById("arc-upload-title").value.trim();
  const fileInput = document.getElementById("arc-upload-file");
  const status = document.getElementById("arc-upload-status");
  const file = fileInput.files[0];
  if (!title || !file) {
    status.className = "arc-upload-status err";
    status.textContent = "A title and a file are both required.";
    return;
  }
  if (file.size > 2 * 1024 * 1024) {
    status.className = "arc-upload-status err";
    status.textContent = "That file is too big — keep uploads under 2MB.";
    return;
  }
  status.className = "arc-upload-status";
  status.textContent = "Uploading…";
  try {
    const fileData = await fileToBase64(file);
    const item = await arcAuthedFetch("/api/archive", {
      method: "POST",
      body: JSON.stringify({
        title, filename: file.name, mimeType: file.type, fileData,
        classId: arcSelectedClassId || null
      })
    });
    status.className = "arc-upload-status ok";
    status.textContent = item.status === "approved"
      ? "Uploaded and live in the archive."
      : "Uploaded — pending staff approval.";
    document.getElementById("arc-upload-title").value = "";
    fileInput.value = "";
    arcSelectedClassId = "";
    document.getElementById("arc-class-pill-text").textContent = "Select a class…";
    loadArcMine();
    if (item.status === "approved") loadArcBrowse(document.getElementById("arc-browse-filter").value);
  } catch (err) {
    status.className = "arc-upload-status err";
    status.textContent = err.message || "Upload failed.";
  }
});

function arcClassName(id) {
  const c = arcClasses.find(c => String(c.id) === String(id));
  return c ? c.name : null;
}

async function loadArcMine() {
  const list = document.getElementById("arc-mine-list");
  try {
    const items = await arcAuthedFetch("/api/archive/mine");
    if (!items.length) { list.innerHTML = `<div class="arc-empty">You haven't uploaded anything yet.</div>`; return; }
    list.innerHTML = items.map(item => `
      <div class="arc-row" id="mine-item-${item.id}">
        <div class="arc-row-main">
          <div class="arc-row-title">${item.title}</div>
          <div class="arc-row-meta">${arcClassName(item.class_id) || "No class tagged"} · uploaded ${new Date(item.uploaded_at).toLocaleDateString()}${item.status === "rejected" && item.rejection_reason ? ` · "${item.rejection_reason}"` : ""}</div>
        </div>
        <div class="arc-row-actions">
          <span class="arc-badge ${item.status}">${item.status}</span>
          ${item.status !== "approved" ? `<button class="danger" data-delete-id="${item.id}">Remove</button>` : ""}
        </div>
      </div>
    `).join("");
    list.querySelectorAll("[data-delete-id]").forEach(btn => {
      btn.addEventListener("click", async () => {
        try {
          await arcAuthedFetch(`/api/archive/${btn.dataset.deleteId}`, { method: "DELETE" });
          loadArcMine();
        } catch (err) { console.error(err); }
      });
    });
  } catch (err) {
    list.innerHTML = `<div class="arc-empty">Couldn't load your uploads.</div>`;
  }
}

async function loadArcPending() {
  const list = document.getElementById("arc-pending-list");
  try {
    const items = await arcAuthedFetch("/api/archive/pending");
    if (!items.length) { list.innerHTML = `<div class="arc-empty">Nothing waiting on review.</div>`; return; }
    list.innerHTML = items.map(item => `
      <div class="arc-row" id="pending-item-${item.id}">
        <div class="arc-row-main">
          <div class="arc-row-title">${item.title}</div>
          <div class="arc-row-meta">by ${item.uploader_username || "a student"} · uploaded ${new Date(item.uploaded_at).toLocaleDateString()}</div>
        </div>
        <div class="arc-row-actions">
          <select id="pending-class-${item.id}">
            <option value="">${arcClassName(item.class_id) || "No class"}</option>
            ${arcClasses.map(c => `<option value="${c.id}">${c.name}</option>`).join("")}
          </select>
          <button class="primary" data-approve-id="${item.id}">Approve</button>
          <button class="danger" data-reject-id="${item.id}">Reject</button>
        </div>
      </div>
    `).join("");
    list.querySelectorAll("[data-approve-id]").forEach(btn => {
      btn.addEventListener("click", async () => {
        const id = btn.dataset.approveId;
        const classId = document.getElementById(`pending-class-${id}`).value;
        try {
          await arcAuthedFetch(`/api/archive/${id}/review`, {
            method: "PATCH",
            body: JSON.stringify({ status: "approved", classId: classId || null })
          });
          loadArcPending();
          loadArcBrowse(document.getElementById("arc-browse-filter").value);
        } catch (err) { console.error(err); }
      });
    });
    list.querySelectorAll("[data-reject-id]").forEach(btn => {
      btn.addEventListener("click", async () => {
        const id = btn.dataset.rejectId;
        const reason = window.prompt("Reason (optional, shown to the uploader):", "") || "";
        try {
          await arcAuthedFetch(`/api/archive/${id}/review`, {
            method: "PATCH",
            body: JSON.stringify({ status: "rejected", rejectionReason: reason })
          });
          loadArcPending();
        } catch (err) { console.error(err); }
      });
    });
  } catch (err) {
    list.innerHTML = `<div class="arc-empty">Couldn't load the review queue.</div>`;
  }
}

async function loadArcBrowse(classId) {
  const grid = document.getElementById("arc-browse-grid");
  try {
    const items = await arcAuthedFetch(`/api/archive${classId ? `?classId=${classId}` : ""}`);
    if (!items.length) { grid.innerHTML = `<div class="arc-empty">No approved uploads yet.</div>`; return; }
    grid.innerHTML = items.map(item => `
      <div class="arc-item" id="item-${item.id}" data-open-id="${item.id}">
        <span class="arc-tag">${arcClassName(item.class_id) || "Untagged"}</span>
        <div class="arc-title">${item.title}</div>
        <div class="arc-meta">by ${item.uploader_username || "a student"} · ${new Date(item.uploaded_at).toLocaleDateString()}</div>
      </div>
    `).join("");
    grid.querySelectorAll("[data-open-id]").forEach(el => {
      el.addEventListener("click", () => openArcItem(el.dataset.openId));
    });
  } catch (err) {
    grid.innerHTML = `<div class="arc-empty">Couldn't load the archive.</div>`;
  }
}

async function openArcItem(id) {
  try {
    const item = await arcAuthedFetch(`/api/archive/${id}`);
    const byteChars = atob(item.file_data);
    const bytes = new Uint8Array(byteChars.length);
    for (let i = 0; i < byteChars.length; i++) bytes[i] = byteChars.charCodeAt(i);
    const blob = new Blob([bytes], { type: item.mime_type || "application/octet-stream" });
    const url = URL.createObjectURL(blob);
    window.open(url, "_blank");
  } catch (err) {
    console.error(err);
    alert("Couldn't open that file.");
  }
}
</script>
