# ⚙️ Setup Guide — Auto-LinkedIn-Job-Tracker-N8N

Follow every step in order. Do not skip any step.

> 💡 **Before you start:** Use the **same Gmail account** for Google Drive, Google Sheets, and Gemini API. This makes setup much easier — no extra tokens or API keys needed for Google services.

**Estimated time: 30–45 minutes**

---

## 📸 Screenshots Folder

All screenshots are inside the `screenshots/` folder.
Each step below tells you exactly which screenshot to refer to.

```
screenshots/
├── 01_workflow_overview.png         ← Full n8n workflow canvas
├── 02_google_drive_node.png         ← Download file node setup
├── 03_filter_tab.png                ← Google Sheets Filter tab columns
├── 04_sheets_node.png               ← Get row(s) in sheet node setup
├── 05_botfather_create_bot.png      ← Creating bot in BotFather
├── 06_userinfobot_chatid.png        ← Getting Chat ID from @userinfobot
├── 07_telegram_node.png             ← Telegram node with Chat ID field
└── 08_telegram_job_alerts.png       ← Real job alerts received on Telegram
```

---

## 📋 Overview — What You Will Set Up

| Step | Task |
|------|------|
| 1 | Import workflow into n8n |
| 2 | Set up Google Drive — upload resume |
| 3 | Set up Google Sheets — upload and fill filter sheet |
| 4 | Get Google Gemini API Key |
| 5 | Set up Telegram Bot and get Chat ID |
| 6 | Connect everything inside n8n nodes |
| 7 | Test the workflow manually |
| 8 | Activate — runs every day at 5PM automatically |

---

## STEP 1 — Import Workflow into n8n

### 1.1 Open n8n
1. Go to [app.n8n.cloud](https://app.n8n.cloud) and log in
2. If you don't have an account → Sign up free (14 day trial)

### 1.2 Create a New Workflow
1. On the left sidebar → click **"+"** or **"New Workflow"**
2. An empty canvas will open

### 1.3 Import the JSON File
1. Click the **"..."** three dots menu at the top right of the canvas
2. Click **"Import from File"**
3. Select the file `Auto-LinkedIn-Job-Tracker-N8N.json` from your computer
4. All nodes will appear on the canvas automatically

### 1.4 Rename the Workflow
1. Click on **"My workflow"** text at the top
2. Rename it to: `Auto-LinkedIn-Job-Tracker-N8N`
3. Click **Save**

📸 See screenshot: `screenshots/01_workflow_overview.png`

After import your canvas should show two rows of connected nodes exactly like the screenshot.

---

## STEP 2 — Google Drive Setup (Your Resume PDF)

> ✅ No API key needed. Just sign in with Google — takes 1 minute.

### 2.1 Upload Your Resume to Google Drive
1. Open [drive.google.com](https://drive.google.com) in your browser
2. Make sure you are signed in with your Gmail account
3. Click **"+ New"** button (top left)
4. Click **"File upload"**
5. Select your **resume PDF** from your computer
6. Wait for the upload to finish
7. Remember the exact file name — you will select it inside n8n

### 2.2 Open the Download File Node in n8n
1. Go back to your n8n workflow
2. Click on the **"Download file"** node (second node from left in Row 1)
3. The node settings panel opens on the right side

### 2.3 Connect Google Drive Credential
1. Click the **"Credential to connect with"** dropdown
2. Click **"+ Create new credential"**
3. A popup appears — click **"Sign in with Google"**
4. Your Google account list appears — select your Gmail account
5. Click **"Allow"** to give n8n access
6. Credential is saved automatically ✅
7. The dropdown now shows **"Google Drive account"**

### 2.4 Configure the Node Settings
Set these fields exactly:
```
Resource:  File
Operation: Download
File:      From list → [click and select your resume PDF]
```

### 2.5 Select Your Resume File
1. Click the **File** field
2. Click **"From list"** in the dropdown
3. Click the **"..."** three dots icon → click **"Open"**
4. Your Google Drive files appear
5. Click on your resume PDF to select it
6. The file name appears in the field ✅

### 2.6 Test This Node
1. Click **"Execute step"** button at the top right of the node panel
2. The node should turn **green** ✅
3. If it turns red → re-check your credential and file selection

📸 See screenshot: `screenshots/02_google_drive_node.png`

The node should look exactly like the screenshot — showing your resume PDF name in the File field.

---

## STEP 3 — Google Sheets Setup

> ✅ Same Gmail account as Google Drive. No extra token needed — just sign in.

### 3.1 Upload the Google Sheet
1. Go to [sheets.google.com](https://sheets.google.com)
2. Click **"+"** to create a new blank spreadsheet
3. Click **File → Import**
4. Click **"Upload"** tab → select `google_sheet.xlsx` from your computer
5. Select **"Replace spreadsheet"** → click **"Import data"**
6. Your sheet now has 2 tabs at the bottom — **Filter** and **Result** ✅

### 3.2 Fill in the Filter Tab
1. Click the **"Filter"** tab at the bottom of the sheet
2. Fill in Row 2 with your job search preferences:

| Column | What to Enter | Your Example |
|--------|--------------|--------------|
| **A — Keyword** | Job title you want | `Data Scientist` |
| **B — Location** | City or country | `New York` |
| **C — Experience Level** | Your level | `Mid-Senior level` |
| **D — Remote** | Work preference | `Remote` or `Hybrid` |
| **E — Job Type** | Employment type | `Full-time` |

> ✅ You can select multiple values for Experience Level, Remote, and Job Type using the dropdown tags in each cell

> ✅ Leave the **Result** tab completely empty — the workflow fills it automatically every time it runs

📸 See screenshot: `screenshots/03_filter_tab.png`

Your Filter tab should look exactly like the screenshot — with your values filled in Row 2.

### 3.3 Connect Google Sheets in n8n — Get Row(s) Node
1. In your workflow → click the **"Get row(s) in sheet"** node (4th node in Row 1)
2. Click **"Credential to connect with"** dropdown
3. Click **"+ Create new credential"**
4. Click **"Sign in with Google"** → select same Gmail account → Allow
5. Credential saved ✅
6. Click the **Document** field → **"From list"** → select your Google Sheet
7. Click the **Sheet** field → **"From list"** → select **"Filter"**

📸 See screenshot: `screenshots/04_sheets_node.png`

The node should look exactly like the screenshot — showing your sheet name in Document and Filter in Sheet field.

### 3.4 Connect Google Sheets — Append or Update Node
1. Click the **"Append or update row in sheet"** node (second to last in Row 2)
2. Click **"Credential to connect with"** dropdown
3. Select the **same Google Sheets credential** you just created
4. Click the **Document** field → **"From list"** → select your Google Sheet
5. Click the **Sheet** field → **"From list"** → select **"Result"**
6. This node saves every job result automatically ✅

---

## STEP 4 — Google Gemini API Key

### 4.1 Create Your Gemini API Key
1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in with your **same Gmail account**
3. Click **"Get API Key"** on the left sidebar
4. Click **"+ Create API key"** button
5. A dropdown appears — select your Google project
6. Click **"Create API key in existing project"**
7. Your API key appears on screen — looks like: `AIzaSy...`
8. Click **"Copy"** button immediately
9. Save it somewhere safe — you cannot see it again after closing

> ⚠️ Never share this key with anyone or push it to GitHub

### 4.2 Add Gemini Credential in n8n
1. In your workflow → click the **"Google Gemini Chat Model"** node
   (round node at the bottom, connected to AI Agent)
2. Click **"Credential to connect with"** dropdown
3. Click **"+ Create new credential"**
4. Select **"Google Gemini(PaLM) API"**
5. In the **API Key** field → paste your key from Step 4.1
6. Click **"Save"** ✅

---

## STEP 5 — Telegram Bot Setup ⭐ Most Important Step

This step has 3 parts:
- **Part A** — Create your bot using BotFather and get Bot Token
- **Part B** — Get your personal Chat ID using @userinfobot
- **Part C** — Connect both inside n8n

---

### PART A — Create Bot and Get Token via BotFather

1. Open **Telegram** on your phone or desktop
2. In the search bar → type **@BotFather**
3. Click on **BotFather** — it has a blue verified tick ✅
4. Click **"Start"** button at the bottom
5. Type `/newbot` and press Send

6. BotFather replies: **"What name do you want for your bot?"**
   - This is the display name — type anything you like
   - Example: `My Job Alert`
   - Press Send

7. BotFather replies: **"Choose a username for your bot"**
   - Username MUST end with the word `bot`
   - Example: `myjobtracker_bot` or `harsha_jobs_bot`
   - If it says **"Sorry, this username is already taken"** → try a different name
   - Keep trying until it accepts ✅

8. BotFather sends a success message with your **Bot Token**:
```
Done! Congratulations on your new bot.

Use this token to access the HTTP API:
1234567890:AAFxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

Keep your token secure and store it safely.
```

9. **Copy your Bot Token** — the long string after the colon
10. Save it somewhere safe — you need it in Part C

📸 See screenshot: `screenshots/05_botfather_create_bot.png`

Your conversation with BotFather should look exactly like the screenshot.

---

### PART B — Get Your Chat ID via @userinfobot

1. In Telegram search bar → type **@userinfobot**
2. Click on **userinfobot** (445,000+ monthly users — green icon)
3. Click **"Start"**
4. The bot instantly replies with your information:

```
Id: 987654321
First: John
Last: Doe
Lang: en
Registered: Check Date
```

5. **Copy the number** next to **"Id:"** — this is your **Chat ID** ✅

> ✅ That's it! One click and you have your Chat ID. No URL or API call needed.

📸 See screenshot: `screenshots/06_userinfobot_chatid.png`

Your @userinfobot reply should look exactly like the screenshot — with your Chat ID highlighted at the top.

---

### PART C — Connect Telegram in n8n

**Add Bot Token as Credential:**
1. In your workflow → click the **"Send a text message"** node (last node in Row 2)
2. Click **"Credential to connect with"** dropdown
3. Click **"+ Create new credential"**
4. Select **"Telegram API"**
5. In the **"Access Token"** field → paste your **Bot Token** from Part A
6. Click **"Save"** ✅

**Add Your Chat ID:**
1. Still inside the **"Send a text message"** node
2. Find the **"Chat ID"** field
3. Delete the existing placeholder value completely
4. Type or paste your **Chat ID** from Part B
5. Do NOT add any spaces or extra characters

The Text field below Chat ID should already contain:
```
Title: {{ $('Modify Job Attributes').item.json.title }}
Company: {{ $('Modify Job Attributes').item.json.company }}
Location: {{ $('Modify Job Attributes').item.json.location }}
Job Score: {{ $json.score }}
Apply: {{ $('Modify Job Attributes').item.json.applyLink }}
```
> ✅ Do NOT change this text — it is already configured correctly

📸 See screenshot: `screenshots/07_telegram_node.png`

Your Telegram node should look exactly like the screenshot — with your Chat ID in the field.

**Activate Your Bot:**
1. Open Telegram
2. Search for your bot username → example: `@myjobtracker_bot`
3. Click on your bot
4. Click **"Start"**
5. Send any message → type `hi` and press Send

> ⚠️ This is mandatory — if you do not send a message to your bot first, Telegram will block the workflow from sending you alerts

---

## STEP 6 — Final Checklist

Go through every item before testing. Do not skip any:

- [ ] Workflow JSON imported into n8n ✅
- [ ] **Download file** node → Google Drive credential connected ✅
- [ ] **Download file** node → Your resume PDF selected from list ✅
- [ ] **Get row(s) in sheet** node → Google Sheets credential connected ✅
- [ ] **Get row(s) in sheet** node → Filter tab selected ✅
- [ ] **Append or update row in sheet** node → same credential connected ✅
- [ ] **Append or update row in sheet** node → Result tab selected ✅
- [ ] **Google Gemini Chat Model** node → Gemini API key added ✅
- [ ] **Send a text message** node → Telegram Bot Token added ✅
- [ ] **Send a text message** node → Your personal Chat ID replaced ✅
- [ ] Filter tab in Google Sheet → all 5 columns filled with your preferences ✅
- [ ] You clicked Start and sent at least one message to your Telegram bot ✅

---

## STEP 7 — Test the Workflow Manually

Do this right now — do not wait for 5PM:

1. In n8n → look at the bottom center of the screen
2. Click the orange **"Execute Workflow"** button
3. The workflow starts running — watch each node carefully
4. Each node that runs successfully turns **green** ✅
5. If any node turns **red** → click on it → read the error message → fix it using the table below
6. Wait for the full workflow to finish — it takes a few minutes because of the 10 second wait between each job

**After execution check two things:**

**Check 1 — Telegram:**
Open your Telegram bot chat — you should see job alert messages arriving like this:
```
Title: Senior Data Scientist
Company: Capital One
Location: New York, NY
Job Score: 85
Apply: https://www.linkedin.com/jobs/view/...
```

**Check 2 — Google Sheet:**
Open your Google Sheet → click the **Result** tab → you should see rows of jobs with scores, titles, companies, locations, and apply links filled in automatically

📸 See screenshot: `screenshots/08_telegram_job_alerts.png`

Your Telegram should look exactly like the screenshot — multiple job alerts with real scores and apply links.

---

## STEP 8 — Activate the Workflow

Once the manual test is successful:

1. In n8n → look at the top right of the canvas
2. Toggle the **"Active"** switch to **ON** (it turns green)
3. The workflow is now fully automated ✅
4. It will run **every day at 5PM** without you doing anything
5. Jobs with score **≥ 50** → sent directly to your Telegram
6. All jobs regardless of score → saved to Google Sheet Result tab

> 💡 You can change the time by clicking the **Schedule Trigger** node → change the hour value

---

## 🔧 Common Issues and Fixes

| Problem | Cause | Fix |
|---------|-------|-----|
| Google Drive node turns red | Credential expired or not connected | Click node → re-connect credential → sign in again |
| Google Sheets node turns red | Wrong sheet or tab selected | Make sure Filter and Result tabs exist → re-select them |
| No Telegram message received | Chat ID wrong or bot not started | Double check Chat ID → make sure you sent a message to your bot |
| Gemini API error | Wrong API key | Re-copy key from aistudio.google.com → paste again with no spaces |
| LinkedIn returns no results | Keywords too specific or location wrong | Change keywords in Filter tab → try broader search |
| Result tab stays empty | Filter tab not filled correctly | Check all 5 columns in Filter tab have values |
| Bot token invalid | Token copied incorrectly | Go to @BotFather → /mybots → select your bot → copy token again |
| Workflow runs but score is always 0 | AI Agent not connected to Gemini | Check Gemini credential is selected in the Chat Model node |

---

> 🎉 **You are done!** The workflow now runs every day at 5PM, searches LinkedIn for matching jobs, scores each one against your resume using AI, and sends the best matches directly to your Telegram.
>
> 💼 Built by **Harshavardhan Reddy**
> - LinkedIn: [linkedin.com/in/harshareddy0001](https://linkedin.com/in/harshareddy0001)
> - Portfolio: [harsha-porfolio.netlify.app](https://harsha-porfolio.netlify.app)
