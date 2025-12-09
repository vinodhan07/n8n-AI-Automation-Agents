# Intelligent Lead Capture & Engagement System

This n8n workflow automates the process of capturing leads from Slack notifications (typically from website visitor identification tools like RB2B), enriching their data, generating personalized outreach via AI, and routing them to the appropriate channel (Email or LinkedIn) based on data availability and validity.

## 🚀 Features

* **Slack Parsing:** Automatically parses raw text from Slack messages to extract Name, Company, Email, and LinkedIn URLs.
* **Data Enrichment:** Uses **Dropcontact** to enrich prospect data and find missing contact information.
* **AI Content Generation:** Uses **OpenAI (GPT-4o-mini)** to write a highly personalized, non-salesy cold email (<50 words) referencing the prospect's company and website visit.
* **Smart Routing:**
    * **Email Path:** If an email is found, it is verified using **Reoon**. If valid, the AI-generated email is sent via **Gmail**.
    * **LinkedIn Path:** If no email is found (or the email is invalid), the lead is automatically added to a **HeyReach** LinkedIn campaign for manual/automated connection requests.

## 📋 Prerequisites

To use this workflow, you need the following accounts and credentials configured in n8n:

1.  **n8n** (Self-hosted or Cloud)
2.  **Slack** (Connected to the channel receiving lead alerts)
3.  **Dropcontact** (API Key for enrichment)
4.  **OpenAI** (API Key for GPT-4o-mini)
5.  **Reoon** (API Key for email verification)
6.  **Gmail** (OAuth2 credentials for sending emails)
7.  **HeyReach** (API Key for LinkedIn automation)

## 🛠️ Setup & Configuration

### 1. Credentials
Ensure the following credentials are setup in your n8n instance:
* `Slack account`
* `Dropcontact account`
* `OpenAi account`
* `Gmail account`

### 2. Node Configuration

#### **Slack Trigger**
* Ensure the **Channel ID** (`C0A1LMSG3V3`) is updated to match the channel where your lead alerts are posted.

#### **Reoon Email Verifier (HTTP Request)**
* **Node Name:** `Gmail Messages` (This node is actually an HTTP Request to Reoon).
* **Action:** You must replace the hardcoded API key in the URL parameter (`key=veFL...`) with your own Reoon API key.

#### **HeyReach (LinkedIn Automation)**
* **Node Name:** `HTTPS Request`
* **Headers:** Update the `X-API-KEY` with your own HeyReach API key.
* **JSON Body:** Update the `campaignId` (`115122`) and `linkedInAccountId` (`71043`) to match your specific HeyReach campaign settings.

### 3. AI Customization
* Open the **AI Agent** node.
* The current prompt is set to sign off as "Vinodhan, Student, KIOT". Update the system prompt and user prompt to reflect your own name and job title.

## 🔄 Workflow Logic

1.  **Trigger:** Workflow starts when a new message is posted in the specified Slack channel.
2.  **Parse:** A Code node extracts `Name`, `Company`, `Email`, and `LinkedIn` using Regex.
3.  **Enrich:** Data is sent to **Dropcontact** to fill in missing details.
4.  **Draft:** **OpenAI** writes a personalized subject line and body.
5.  **Decision 1 (Email Exists?):**
    * **Yes:** Proceed to verification.
    * **No:** Send lead to **HeyReach** (LinkedIn).
6.  **Verification:** The email is checked via **Reoon** (API).
7.  **Decision 2 (Email Valid?):**
    * **Valid:** Send email via **Gmail**.
    * **Invalid/Risky:** Send lead to **HeyReach** (LinkedIn).

## ⚠️ Important Security Note
The provided JSON contains hardcoded API keys in the HTTP Request nodes (Reoon and HeyReach). **Immediately replace these with your own keys and consider using n8n credentials or environment variables for better security.**