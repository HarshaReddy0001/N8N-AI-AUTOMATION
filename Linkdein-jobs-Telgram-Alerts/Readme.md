# 🤖 LinkedIn Job Hunter — AI-Powered Resume Matching + Telegram Alerts

An intelligent, fully automated LinkedIn job search workflow built with **n8n**, **Google Gemini**, and **Telegram**. Runs every day at 5PM — scrapes LinkedIn jobs, compares each job description against your resume using AI, scores the match from 0–100, generates a custom cover letter, and sends only the best matches straight to your Telegram.

**No more manually scrolling LinkedIn. Let AI do the work.**

![Workflow Screenshot](workflow_screenshot.png)

---

## ✨ What It Does

| Feature | Description |
|---------|-------------|
| ⏰ **Fully Automated** | Runs every day at 5PM — zero manual effort |
| 📄 **Reads Your Resume** | Downloads your PDF resume from Google Drive |
| 🔍 **Searches LinkedIn** | Builds a custom LinkedIn search URL from your filters |
| 🤖 **AI Resume Matching** | Gemini compares your resume vs every job description |
| 📊 **Scores 0–100** | 0 = no match, 100 = perfect match |
| ✉️ **Writes Cover Letter** | Generates a custom cover letter for each job automatically |
| 📋 **Saves to Google Sheets** | All jobs + scores + cover letters saved automatically |
| 📱 **Telegram Alerts** | Only jobs scoring ≥ 50 sent to your Telegram instantly |

---

## 🏗️ Architecture

```
⏰ Schedule Trigger (5PM daily)
        │
        ▼
📁 Download Resume PDF ──► 📝 Extract Text from PDF
                                      │
        ┌─────────────────────────────┘
        ▼
📊 Read Filter Settings (Google Sheets)
        │
        ▼
🔗 Build LinkedIn Search URL
        │
        ▼
🌐 Fetch LinkedIn Job Results (HTTP)
        │
        ▼
🔗 Extract All Job Links
        │
        ▼
✂️ Split Into Individual Jobs
        │
        ▼
🔁 Loop Over Each Job
        │
    ⏳ Wait 10 sec (anti-block)
        │
    🌐 Fetch Individual Job Page
        │
    📋 Parse Job Details (title, company, location, description, apply link)
        │
    🤖 AI Agent (Gemini)
        ├── Scores resume vs job → 0 to 100
        └── Writes custom cover letter
        │
    💾 Save to Google Sheets (all jobs)
        │
    🔢 Score Filter (≥ 50 only)
        │
        ▼
📱 Send Telegram Alert
   (Title, Company, Location, Score, Apply Link)
```

---

## 📱 Telegram Alert Example

When a job scores ≥ 50, you receive this on Telegram instantly:

```
Title: Senior Data Scientist
Company: Capital One
Location: New York, NY (Remote)
Job Score: 87
Apply: https://linkedin.com/jobs/view/...
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** | Workflow automation |
| **Google Gemini** | AI resume scoring + cover letter generation |
| **Google Drive** | Resume PDF storage |
| **Google Sheets** | Filter config + job results storage |
| **Telegram Bot** | Job alert notifications |
| **LinkedIn** | Job data source (via HTTP scraping) |

---

## 📂 Folder Structure

```
linkedin-job-hunter-n8n/
│
├── README.md                   ← This file
├── setup_guide.md              ← Complete setup instructions
├── ai_prompt.md                ← Gemini scoring + cover letter prompt
├── workflow.json               ← Import directly into n8n
├── google_sheet_template.xlsx  ← Ready-made Filter + Result tabs
└── workflow_screenshot.png     ← n8n workflow screenshot
```

---

## ⚡ Quick Start

1. Import `workflow.json` into n8n
2. Upload your resume PDF to Google Drive
3. Set up Google Sheets with the template
4. Add credentials — Gemini, Google Drive, Google Sheets, Telegram
5. Set your search filters in the Google Sheet
6. Activate the workflow — runs at 5PM daily

For detailed steps → see [`setup_guide.md`](setup_guide.md)

---

## 🔧 Customization

| What to Change | Where |
|---------------|-------|
| Run time (default: 5PM) | Schedule Trigger node |
| Job search keywords | Google Sheets → Filter tab |
| Location / Remote / Job type | Google Sheets → Filter tab |
| Minimum score threshold (default: 50) | Score Filter node |
| AI scoring logic | AI Agent node → System Message |

---

## 📊 Google Sheets Structure

**Filter Tab** — your search settings:

| Column | Example |
|--------|---------|
| keywords | Data Scientist |
| location | New York |
| remote | true |
| jobType | fulltime |
| easyApply | true |

**Result Tab** — auto-filled by workflow:

| Column | Description |
|--------|-------------|
| title | Job title |
| company | Company name |
| location | Job location |
| score | AI match score (0-100) |
| coverLetter | AI generated cover letter |
| applyLink | Direct apply URL |
| date | Date found |

---

## ⚠️ Important Notes

- This workflow **scrapes LinkedIn** via HTTP — LinkedIn may block if run too frequently. The 10-second wait between fetches helps avoid this.
- Your **resume PDF must be in Google Drive** and linked in the Download File node.
- The **Telegram Chat ID** is required — see [`setup_guide.md`](setup_guide.md) for exactly how to get it.
- Gemini **free tier** has rate limits — if processing many jobs, consider upgrading.

---

## 👤 Author

**Harshavardhan Reddy**
- 🌐 Portfolio: [harsha-porfolio.netlify.app](https://harsha-porfolio.netlify.app)
- 💼 LinkedIn: [linkedin.com/in/harshareddy0001](https://linkedin.com/in/harshareddy0001)
- 🐙 GitHub: [github.com/HarshaReddy0001](https://github.com/HarshaReddy0001)

---

> Built with n8n + Google Gemini. Fully automated. Zero manual job hunting. ⚡
