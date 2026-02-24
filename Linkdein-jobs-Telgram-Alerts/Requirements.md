# ✅ Requirements — LinkedIn Job Hunter

Before you start the setup, make sure you have everything listed here ready. This saves you from getting stuck halfway through.

---

## 1. Accounts You Need

| Account | Free? | Link |
|---------|-------|------|
| **n8n** | ✅ Free trial | [app.n8n.cloud](https://app.n8n.cloud) |
| **Google Account** | ✅ Free | [google.com](https://google.com) |
| **Telegram Account** | ✅ Free | [telegram.org](https://telegram.org) |
| **LinkedIn Account** | ✅ Free | [linkedin.com](https://linkedin.com) |
| **Google AI Studio** | ✅ Free | [aistudio.google.com](https://aistudio.google.com) |

---

## 2. Things to Prepare Before Setup

### 📄 Your Resume
- Must be in **PDF format**
- Upload it to **Google Drive**
- Note the file name — you'll select it inside n8n

### 📊 Google Sheet
- Download and upload `google_sheet.xlsx` to **Google Sheets**
- It has 2 tabs — **Filter** and **Result**
- You will fill in the Filter tab with your job search preferences

### 📱 Telegram
- You need a **Telegram Bot** — created via BotFather
- You need your **Telegram Chat ID** — explained in `setup_guide.md`

---

## 3. API Keys & Credentials You Need

| Credential | Where to Get It |
|-----------|----------------|
| **Google Gemini API Key** | [aistudio.google.com](https://aistudio.google.com) → Get API Key |
| **Google Drive OAuth2** | Google Cloud Console → OAuth2 credentials |
| **Google Sheets OAuth2** | Same OAuth2 credentials as Google Drive |
| **Telegram Bot Token** | Telegram → @BotFather → /newbot |
| **Telegram Chat ID** | Telegram → @userinfobot or via BotFather flow |

---

## 4. Technical Requirements

| Requirement | Details |
|-------------|---------|
| **n8n version** | 1.0 or higher recommended |
| **Resume format** | PDF only |
| **Google Sheet** | Must have Filter tab and Result tab |
| **Score threshold** | Default is 50 — you can change it |
| **Run schedule** | Default is 5PM daily — you can change it |

---

## 5. What You Do NOT Need

- ❌ No coding skills required
- ❌ No LinkedIn Premium
- ❌ No paid API keys (all free tier works)
- ❌ No server or hosting

---

> Once you have everything above ready, go to [`setup_guide.md`](setup_guide.md) to start the setup.
