# 🎓 Graduation Project Topics System · Faculty & Coordinator Manual

This guide walks faculty coordinators through the setup, maintenance, and two-way synchronization of the Graduation Project Topics System.

---

## 📋 System Overview

The Topics System links three environments seamlessly:
1. **Student Form (Public GitHub Pages):** Hosted via `/docs/index.html`. Students search their name/ID and submit topics with mandatory phone validation.
2. **Official Google Sheet (Cloud Hub):** Hosted in Google Drive. Formatted with official navy headers (`#1C4587`), merged venue/supervisor blocks, and yellow topic highlights (`#FFFF00`).
3. **Faculty Command Center (Local / Private):** Hosted at `http://127.0.0.1:5000/admin` (passcode: `gradteam`). Provides full auditing, Excel generation, and internal supervisor email roster dispatch.

---

## 🛠️ Step 1: Setting Up Google Sheets & Apps Script

1. Open your official **Graduation Project Topics** Google Sheet.
2. Click **Extensions → Apps Script**.
3. In the Apps Script project:
   - Paste the code from [`TopicsSystem.gs`](../TopicsSystem.gs) into `TopicsSystem.gs`.
   - Paste the code from [`Code.gs`](../Code.gs) into `Code.gs`.
4. Click **Save** (disk icon or `Ctrl + S`).
5. Click **Deploy → Manage deployments**:
   - Click the pencil icon (**Edit**).
   - Set **Execute as:** `Me (<your-email>)`.
   - Set **Who has access:** `Anyone`.
   - Set **Version:** `New version`.
   - Click **Deploy**.
6. Copy the resulting **Web App URL** (e.g. `https://script.google.com/macros/s/.../exec`).

---

## 🔄 Step 2: Configuring Webhooks

- In [`docs/index.html`](index.html), line 195:
  ```javascript
  const GOOGLE_SCRIPT_WEBAPP_URL = "https://script.google.com/macros/s/<YOUR_DEPLOYMENT_ID>/exec";
  ```
- In the local Faculty Dashboard at `http://127.0.0.1:5000/admin`:
  - Click **⚙️ Google Sheet Configuration**.
  - Paste the Web App URL into Box #2 (**Google Apps Script Web App URL**).
  - Click **Save & Test Link**.

---

## 📊 Step 3: Google Sheets Custom Menu

When you open the Google Sheet, a custom menu appears:
```text
🎓 Graduation Projects
├── 📊 Create / Update Topics File
├── 🛡️ Run Allocation & Attendance Verification
└── 🔍 Scan Topic Quality Audits
```

- **Create / Update Topics File:**
  - Reads students from the uploaded Allocation sheet, the synced `Students` sheet, or `INITIAL_STUDENTS`.
  - Scans and **preserves all existing student topics** before refreshing.
  - Merges Venues, Fields, and External Supervisor cohorts.
  - Highlights rows with submitted topics in **Yellow (`#FFFF00`)**.
  - Re-calculates live `=COUNTIF` totals in the **Internal Supervisor Count** tab.

---

## 📥 Step 4: Uploading New Semester Allocation Reports

When a new semester begins or an updated Allocation Report is released:
1. Open the local dashboard: `http://127.0.0.1:5000/admin`.
2. Scroll to the **📥 Upload Allocation Report** card.
3. Select the `.xlsx` file (e.g., `Allocation_System_3.xlsx`) and click **Process Allocation Report & Refresh Topics**.
4. The system will:
   - Dynamically identify headers across rows 1–10.
   - Forward-fill merged cells for Venues, Supervisors, and Fields.
   - Extract all enrolled students and update the local database.
   - Preserve all student topic submissions already recorded.
   - Automatically generate and download the official 4-sheet Topics Excel workbook (`Grad_Topics_File_Export_...xlsx`).
5. Click **🔄 Push to Google Sheet** to update the online sheet instantly.

---

## 🔄 Step 5: Two-Way Synchronization

| Action | Button on Dashboard | Description |
| :--- | :--- | :--- |
| **Pull from Google Sheet** | `📥 Pull from Google Sheet` | Fetches student topic submissions entered online and saves them into the local database. |
| **Push to Google Sheet** | `🔄 Push to Google Sheet` | Sends all local records, committee allocations, and audit flags directly to the Google Sheet. |

---

## 📧 Step 6: Internal Supervisor Roster Dispatch

1. Click **📧 Send Internal Supervisor Rosters** in the dashboard.
2. An interactive modal displays each internal supervisor with their assigned student cohort.
3. Verify the official Supervision Guidelines document link.
4. Click **Dispatch Rosters** to send official emails to supervisors.
