# Company Technology Stack Scraper

This n8n workflow automates the process of identifying the technology stack (CMS, Hosting, Analytics, etc.) used by companies. It reads a list of domains from Google Sheets, scrapes their public technology profile using Jina AI (via BuiltWith), uses Google Gemini to categorize the technologies, and updates the Google Sheet with the results.

## 🚀 Features

* **Batch Processing:** Reads company domains row-by-row from Google Sheets.
* **Tech Scraping:** Uses the **Jina AI Reader API** to fetch technology profiles from `builtwith.com`.
* **AI Analysis:** Utilizes **Google Gemini (PaLM)** to analyze the raw scraped data and filter out noise.
* **Structured Categorization:** Automatically categorizes tech into:
    * Hosting & Servers
    * CMS & Content Management
    * Analysis & Tracking Tools
    * Security & Performance
    * Other Technologies
* **Data Enrichment:** Updates the original Google Sheet row with the discovered data.

## 📋 Prerequisites

To use this workflow, you need:

1.  **n8n:** An active instance.
2.  **Google Cloud Platform:** OAuth2 credentials for the **Google Sheets API**.
3.  **Google Gemini (PaLM):** An API Key for the **Google Gemini Chat Model**.
4.  **Jina AI:** An API Key for the Reader API (used in the HTTP Request node).

## 🛠️ Setup & Configuration

### 1. Google Sheet Preparation
Create a Google Sheet with the following headers in Row 1:
* `Company Domain` (Input column, e.g., `n8n.io`)
* `Hosting & Servers`
* `CMS & Content Management`
* `Analysis & Tracking Tools`
* `Security & Preferences`
* `other Technologies`

*Note: The column headers must match exactly for the final Google Sheets node to map the data correctly.*

### 2. Credential Setup
Ensure the following credentials are configured in n8n:
* `Google Sheets account`
* `Google Gemini(PaLM) Api account`

### 3. Node Configuration

#### **Google Sheets (Read)**
* Select your spreadsheet and sheet.
* Ensure it reads the `Company Domain` column.

#### **Tech Technologies Sourcing (HTTP Request)**
* **Important:** This node currently contains a hardcoded Jina AI Bearer token.
* Go to the **Headers** section of this node.
* Replace the `Authorization` value with your own API key: `Bearer YOUR_JINA_API_KEY`.

#### **Google Sheets1 (Write)**
* Select the same spreadsheet used in the first step.
* The node is set to **Update** rows based on the `Company Domain` match.

## 🔄 Workflow Logic

1.  **Trigger:** Manual trigger (click "Test Workflow").
2.  **Read:** Fetches the list of domains from the connected Google Sheet.
3.  **Loop:** Iterates through the domains one by one.
4.  **Scrape:** Sends the domain to `https://s.jina.ai//builtwith.com/...` to get the tech stack text.
5.  **AI Process:** Sends the raw text to **Google Gemini** with a prompt to extract and categorize specific technologies.
6.  **Parse:** A Structured Output Parser ensures the AI returns clean JSON.
7.  **Save:** The structured data is written back to the Google Sheet columns corresponding to that domain.