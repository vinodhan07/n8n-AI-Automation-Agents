# LinkedIn Job Scraping & Lead Enrichment Automation (n8n)

This repository contains an advanced **n8n automation workflow** that scrapes LinkedIn job listings, enriches company and decision-maker data, finds and verifies emails, generates personalized icebreakers using AI, and pushes qualified leads into Google Sheets and outreach platforms.

The workflow is designed for **lead generation, recruitment sourcing, and outbound sales automation** with minimal manual effort.

---

## 🚀 Key Features

- 🔍 Scrapes LinkedIn job listings using **Apify**
- 🏢 Filters companies based on employee count
- 🧹 Removes duplicate companies automatically
- 👤 Identifies HR / decision makers
- 📧 Finds professional emails using multiple enrichment tools
- ✅ Verifies emails to ensure deliverability
- 🌐 Scrapes company websites for contextual data
- 🤖 Generates AI-based personalized icebreakers (OpenAI)
- 📊 Stores clean leads in **Google Sheets**
- 📬 (Optional) Pushes leads to outreach tools like **Smartlead** and **HeyReach**

---

## 🧠 Workflow Overview

### High-Level Flow

1. Manual Trigger  
2. LinkedIn Job Scraping (Apify)  
3. Company Size Filtering  
4. Duplicate Removal  
5. Company Name Cleanup  
6. Decision Maker Discovery  
7. Email Discovery  
8. Email Verification  
9. Company Website Scraping  
10. AI Icebreaker Generation  
11. Google Sheets Lead Storage  
12. Outreach Tool Integration (Optional)

---

## 🛠️ Tech Stack & Services Used

| Tool / Service | Purpose |
|---------------|---------|
| n8n | Workflow automation |
| Apify | LinkedIn job scraping |
| Anymailfinder / Prospeo | Email discovery |
| Reoon | Email verification |
| OpenAI (GPT-4 / GPT-4.1) | Icebreaker generation |
| Google Sheets | Lead storage |
| Smartlead | Email outreach (optional) |
| HeyReach | LinkedIn campaign automation (optional) |

---

## 📂 Files in This Repository

```
.
├── Linkedin Job Scraping.json
├── README.md
```

---

## ⚙️ Setup Instructions

### 1️⃣ Import Workflow into n8n

1. Open your **n8n dashboard**
2. Go to **Workflows → Import**
3. Upload `Linkedin Job Scraping.json`
4. Save the workflow

---

### 2️⃣ Configure Required Credentials

You must add the following credentials in n8n:

- Apify API Token  
- OpenAI API Key  
- Email Finder API (Anymailfinder / Prospeo)  
- Email Verification API (Reoon)  
- Google Sheets OAuth  
- Smartlead API (optional)  
- HeyReach API (optional)

⚠️ Never commit real API keys to GitHub.

---

## 🤖 AI Icebreaker Logic

The OpenAI node generates short, natural first-line compliments based on the company website.

Rules:
- Under 15 words  
- Conversational tone  
- Based on real website content  
- No generic phrases  

---

## 📤 Outreach Integrations (Optional)

- **Smartlead** – Email campaigns  
- **HeyReach** – LinkedIn campaigns  

Nodes are disabled by default.

---

## ⚠️ Legal Notice

This project is for educational and internal automation purposes only.  
Ensure compliance with LinkedIn ToS, GDPR, and local data protection laws.

---

## 👨‍💻 Author

**Vinodhan V A**  
Automation Engineer | n8n | AI Agents  

GitHub: https://github.com/vinodhan07

---

⭐ Star the repo if you find it useful!
