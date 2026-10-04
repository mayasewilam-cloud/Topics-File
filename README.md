# 🎓 Graduation Project Topic Registration Portal (GitHub Pages)

Welcome to the **MSA Faculty of Biotechnology Graduation Project Topic Registration Portal**.

This directory (`/docs`) is designed for deployment via **GitHub Pages** to provide a single, fast, mobile-friendly link for students to register and update their graduation project topics.

---

## 🏛️ System Architecture

```text
┌────────────────────────────────────────────────────────┐
│   Public Student Form (GitHub Pages /docs/index.html)   │
│   • Instant ID / Name Search (217 Enrolled Students)    │
│   • Committee Allocation Details (Venue & Supervisors)  │
│   • Live Topic Quality Validator & Phone Enforcer       │
└──────────────────────────┬─────────────────────────────┘
                           │
                           │ HTTPS POST (Webhook)
                           ▼
┌────────────────────────────────────────────────────────┐
│     Google Sheets Web App (Apps Script Deployment)     │
│     • Code.gs & TopicsSystem.gs                         │
│     • Updates 'Topics File' (Highlight in Yellow #FFFF00)│
│     • Updates 'Students' Backing Database Tab           │
│     • Live =COUNTIF Table for Internal Supervisors      │
└──────────────────────────┬─────────────────────────────┘
                           │
                 Two-Way Sync (Push / Pull)
                           │
                           ▼
┌────────────────────────────────────────────────────────┐
│    Faculty & Admin Command Center (Private Local UI)    │
│    • http://127.0.0.1:5000/admin (Passcode Protected)  │
│    • "📥 Pull from Google Sheet" (Import Submissions)   │
│    • "🔄 Push to Google Sheet" (Dispatches Cohort)      │
│    • Allocation & Attendance Discrepancy Audits         │
│    • Official Formatted Excel (.xlsx) Downloads        │
└────────────────────────────────────────────────────────┘
```

---

## 🚀 How to Enable the Student Link on GitHub Pages

1. **Commit and Push:**
   Ensure the `docs/` folder (containing `index.html` and `static/`) is pushed to your GitHub repository.
2. **Open Repository Settings:**
   - In your repository, click **Settings** (top right gear icon).
   - In the left sidebar, click **Pages**.
3. **Configure Build and Deployment:**
   - **Source:** *Deploy from a branch*.
   - **Branch:** Select `main` (or `master`).
   - **Folder:** Select `/docs`.
   - Click **Save**.
4. **Your Public Student Link:**
   Within 1–2 minutes, GitHub will display your live public URL:
   ```text
   https://<your-username>.github.io/<repository-name>/
   ```
5. **Share with Students:**
   Share this URL with enrolled students. They can access it on any phone, tablet, or desktop browser.

---

## 🔒 Privacy & Security Design

- **Zero Confidential Exposure:** Only the student registration interface is located in this directory. Administrative passwords, email distribution scripts, attendance logs, and full database exports remain securely on the private faculty server.
- **Direct Cloud Webhook:** Student submissions are sent directly to the Google Apps Script Webhook, writing directly into the official Google Sheet without requiring the faculty member's computer to be powered on 24/7.
- **Two-Way Reconciliation:** Whenever the faculty member opens the command center, clicking **"📥 Pull from Google Sheet"** reconciles all online student submissions into the local database with zero data loss.

---

## 📂 Directory Contents

- [`index.html`](index.html): The standalone, responsive student topic submission form.
- [`static/`](static/): Local offline-ready Tailwind CSS and official MSA branding images (`msa_logo.png`, `biotech_seal.jpg`).
- [`STUDENT_GUIDE.md`](STUDENT_GUIDE.md): Student user guide and submission rules.
- [`FACULTY_SETUP_GUIDE.md`](FACULTY_SETUP_GUIDE.md): Complete setup and synchronization manual for coordinators.
