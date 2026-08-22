---
layout: default
title: "Apply"
permalink: /apply
---

<style>
  .apply-gate { max-width: 420px; margin: 60px auto; text-align: center; }
  .apply-gate h1 { font-size: 20px; margin-bottom: 6px; }
  .apply-gate p { color: #6b7684; font-size: 14px; margin-bottom: 20px; }
  .apply-gate button { padding: 10px 22px; border-radius: 999px; border: none; font-weight: 600; font-size: 14px; cursor: pointer; background: #2c3e50; color: #fff; }
  .apply-gate button:hover { background: #1f2c38; }

  .my-applications { background: #fff; border: 1px solid #e6e8eb; border-radius: 14px; padding: 18px 20px; margin-bottom: 26px; }
  .my-applications h2 { font-size: 15px; margin: 0 0 12px; }
  .app-row { display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid #e6e8eb; font-size: 13px; }
  .app-row:last-child { border-bottom: none; }
  .app-row .meta { color: #6b7684; font-size: 12px; }
  .app-row .app-actions { display: flex; align-items: center; gap: 8px; }
  .msg-btn { background: none; border: 1px solid #d0d7de; border-radius: 999px; padding: 4px 10px; font-size: 11px; cursor: pointer; }

  .msg-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.4); align-items: center; justify-content: center; z-index: 50; }
  .msg-overlay.open { display: flex; }
  .msg-modal { background: #fff; border-radius: 10px; width: 420px; max-width: 92vw; max-height: 80vh; display: flex; flex-direction: column; padding: 16px; }
  .msg-modal h2 { margin: 0 0 10px; font-size: 16px; }
  .msg-list { flex: 1; overflow-y: auto; border: 1px solid #eee; border-radius: 6px; padding: 10px; margin-bottom: 10px; }
  .msg-row { margin-bottom: 10px; font-size: 13px; }
  .msg-row .who { font-weight: 700; font-size: 11px; text-transform: uppercase; color: #666; }
  .msg-row.admin .who { color: #2c3e50; }
  .msg-row.applicant .who { color: #9a6700; }
  .msg-row .when { color: #999; font-size: 11px; margin-left: 6px; }
  .msg-row .body { margin-top: 2px; white-space: pre-wrap; }
  .msg-compose { display: flex; gap: 8px; }
  .msg-compose textarea { flex: 1; padding: 8px; font-size: 13px; resize: vertical; min-height: 44px; }
  .msg-close { margin-top: 10px; align-self: flex-end; background: #eee; border: none; padding: 6px 12px; border-radius: 6px; cursor: pointer; }
  .status-pill { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.03em; padding: 3px 10px; border-radius: 999px; }
  .status-pill[data-status="new"] { background: #eef1f4; color: #57606a; }
  .status-pill[data-status="accepted"] { background: #dafbe1; color: #1a7f37; }
  .status-pill[data-status="rejected"] { background: #fbe8e6; color: #b3261e; }
  .status-pill[data-status="reviewing"] { background: #fff8c5; color: #9a6700; }
  #my-apps-empty { color: #6b7684; font-size: 13px; }

  .signed-in-as { font-size: 12px; color: #6b7684; margin-bottom: 18px; }
</style>

<div id="apply-signed-out" class="apply-gate" style="display:none;">
  <h1>Sign in to apply</h1>
  <p>You need to be signed in to submit an application — this lets us confirm who you are and lets you check your status later.</p>
  <button id="apply-signin-btn">Sign in</button>
</div>

<div id="apply-already-staff" class="apply-gate" style="display:none;">
  <h1>You're already staff</h1>
  <p>Your account is already on the staff list, so there's nothing to apply for.</p>
</div>

<div id="apply-signed-in" style="display:none;">

<div class="my-applications">
  <h2>Your applications</h2>
  <div id="my-apps-list"></div>
  <div id="my-apps-empty" style="display:none;">You haven't submitted an application yet.</div>
</div>

<div class="msg-overlay" id="msg-overlay">
  <div class="msg-modal">
    <h2 id="msg-modal-title">Messages</h2>
    <div class="msg-list" id="msg-list"></div>
    <div class="msg-compose">
      <textarea id="msg-compose-input" placeholder="Write a message..."></textarea>
      <button id="msg-send-btn">Send</button>
    </div>
    <button class="msg-close" id="msg-close-btn">Close</button>
  </div>
</div>

<h1>Apply to Join TJSG</h1>
<p class="signed-in-as" id="signed-in-as"></p>

<form id="apply-form">

<h2>Section A</h2>
<p>This section will take details of your application.</p>

<p>
  <label for="apply-email">Email *</label><br>
  <input type="text" id="apply-email" name="email" readonly>
</p>
<p>
  <label for="apply-name">Name *</label><br>
  <input type="text" id="apply-name" name="name" required>
</p>
<p>
  <label for="apply-student-id">Student ID *</label><br>
  <input type="text" id="apply-student-id" name="studentId" required>
</p>

<h2>Section B</h2>
<p>This section will get to know you.</p>

<p>Why do you want to join tjsg? *</p>
<p>
  <input type="checkbox" id="reason-archive" value="I want to contribute to Archive faster">
  <label for="reason-archive">I want to contribute to Archive faster</label><br>
  <input type="checkbox" id="reason-guides" value="I want to add to the guides">
  <label for="reason-guides">I want to add to the guides</label><br>
  <input type="checkbox" id="reason-design" value="I want to improve the site design">
  <label for="reason-design">I want to improve the site design</label><br>
  <input type="checkbox" id="reason-code" value="I want to code for tjsg">
  <label for="reason-code">I want to code for tjsg (please follow the instructions of the next question)</label><br>
  <input type="checkbox" id="reason-other">
  <label for="reason-other">Other:</label>
  <input type="text" id="reason-other-text">
</p>

<div id="coding-experience-wrap" style="display:none;">
  <p>How experienced are you with coding? (1-5)<br>
  <em>Do not answer if you did not choose "I want to code for tjsg"</em></p>
  <input type="number" id="coding-experience" min="1" max="5">
</div>

<button type="submit">Submit Application</button>
<p id="apply-status"></p>

</form>

</div>

<script>
const API_BASE = "https://cornerstone-guides-backend.vercel.app";

async function authedFetch(path, opts = {}) {
  const headers = Object.assign({ "Content-Type": "application/json" }, opts.headers || {});
  if (window.clerkToken) headers["Authorization"] = `Bearer ${window.clerkToken}`;
  const res = await fetch(`${API_BASE}${path}`, Object.assign({}, opts, { headers }));
  if (!res.ok) {
    const body = await res.json().catch(() => ({}));
    throw new Error(body.error || `${path} -> ${res.status}`);
  }
  return res.json();
}

window.addEventListener("clerk-ready", async (e) => {
  const signedOutView = document.getElementById("apply-signed-out");
  const signedInView = document.getElementById("apply-signed-in");
  const alreadyStaffView = document.getElementById("apply-already-staff");
  if (e.detail.user) {
    const user = e.detail.user;
    const email = user.primaryEmailAddress?.emailAddress || "";

    // Staff shouldn't see the application form at all, not just the nav link.
    let isStaff = false;
    try {
      const staff = await authedFetch("/api/staff");
      isStaff = Array.isArray(staff) && user.username && staff.includes(user.username.toLowerCase());
    } catch (err) {
      isStaff = false;
    }

    if (isStaff) {
      signedOutView.style.display = "none";
      signedInView.style.display = "none";
      alreadyStaffView.style.display = "block";
      return;
    }

    alreadyStaffView.style.display = "none";
    signedOutView.style.display = "none";
    signedInView.style.display = "block";
    document.getElementById("apply-email").value = email;
    document.getElementById("signed-in-as").textContent = `Applying as ${user.username || email}`;
    loadMyApplications();
  } else {
    alreadyStaffView.style.display = "none";
    signedOutView.style.display = "block";
    signedInView.style.display = "none";
  }
});

document.getElementById("apply-signin-btn").addEventListener("click", () => {
  if (window.clerk) window.clerk.openSignIn();
});

async function loadMyApplications() {
  const list = document.getElementById("my-apps-list");
  const empty = document.getElementById("my-apps-empty");
  list.innerHTML = "";
  empty.style.display = "none";
  try {
    const apps = await authedFetch("/api/my/applications");
    if (!apps.length) {
      empty.style.display = "block";
      return;
    }
    list.innerHTML = apps.map(a => `
      <div class="app-row">
        <span>
          Submitted ${new Date(a.submitted_at).toLocaleDateString(undefined, { year: "numeric", month: "long", day: "numeric" })}
          <span class="meta">· ${a.name}</span>
        </span>
        <span class="app-actions">
          <button class="msg-btn" data-id="${a.id}">Messages</button>
          <span class="status-pill" data-status="${a.status}">${a.status}</span>
        </span>
      </div>
    `).join("");
    document.querySelectorAll(".msg-btn").forEach(function (btn) {
      btn.addEventListener("click", function () { openMessages(btn.dataset.id); });
    });
  } catch (err) {
    empty.textContent = "Couldn't load your applications.";
    empty.style.display = "block";
  }
}

let activeApplicationId = null;

async function openMessages(applicationId) {
  activeApplicationId = applicationId;
  document.getElementById("msg-compose-input").value = "";
  document.getElementById("msg-overlay").classList.add("open");
  await loadMessages();
}

async function loadMessages() {
  const list = document.getElementById("msg-list");
  list.innerHTML = "Loading...";
  try {
    const messages = await authedFetch(`/api/my/applications/${activeApplicationId}/messages`);
    if (!messages.length) {
      list.innerHTML = "<div style='color:#999; font-size:13px;'>No messages yet.</div>";
      return;
    }
    list.innerHTML = messages.map(function (m) {
      const who = m.sender === "applicant" ? "You" : "Staff";
      return `
        <div class="msg-row ${m.sender}">
          <span class="who">${who}</span><span class="when">${new Date(m.created_at).toLocaleString()}</span>
          <div class="body"></div>
        </div>
      `;
    }).join("");
    const bodies = list.querySelectorAll(".msg-row .body");
    messages.forEach(function (m, i) { bodies[i].textContent = m.body; });
    list.scrollTop = list.scrollHeight;
  } catch (err) {
    list.innerHTML = "<div style='color:#b3261e;'>Failed to load messages.</div>";
  }
}

document.getElementById("msg-send-btn").addEventListener("click", async function () {
  const input = document.getElementById("msg-compose-input");
  const body = input.value.trim();
  if (!body || !activeApplicationId) return;
  try {
    await authedFetch(`/api/my/applications/${activeApplicationId}/messages`, {
      method: "POST",
      body: JSON.stringify({ body })
    });
    input.value = "";
    loadMessages();
  } catch (err) {
    // no-op; the message box just won't clear if it failed
  }
});

document.getElementById("msg-close-btn").addEventListener("click", function () {
  document.getElementById("msg-overlay").classList.remove("open");
  activeApplicationId = null;
});

document.getElementById("reason-code").addEventListener("change", function () {
  document.getElementById("coding-experience-wrap").style.display = this.checked ? "block" : "none";
});

document.getElementById("apply-form").addEventListener("submit", async function (e) {
  e.preventDefault();
  const status = document.getElementById("apply-status");
  status.textContent = "Submitting...";

  const reasons = [];
  document.querySelectorAll('#apply-form input[type="checkbox"][value]').forEach(function (cb) {
    if (cb.checked) reasons.push(cb.value);
  });

  const payload = {
    name: document.getElementById("apply-name").value,
    studentId: document.getElementById("apply-student-id").value,
    username: window.clerkUser ? (window.clerkUser.username || null) : null,
    reasons: reasons,
    otherReason: document.getElementById("reason-other").checked
      ? document.getElementById("reason-other-text").value
      : null,
    codingExperience: document.getElementById("reason-code").checked
      ? Number(document.getElementById("coding-experience").value) || null
      : null
  };

  try {
    await authedFetch("/api/apply", { method: "POST", body: JSON.stringify(payload) });
    status.textContent = "Application submitted. Thank you! You can check its status above.";
    e.target.reset();
    document.getElementById("apply-email").value = window.clerkUser?.primaryEmailAddress?.emailAddress || "";
    document.getElementById("coding-experience-wrap").style.display = "none";
    loadMyApplications();
  } catch (err) {
    status.textContent = err.message || "Something went wrong. Please try again.";
  }
});
</script>
