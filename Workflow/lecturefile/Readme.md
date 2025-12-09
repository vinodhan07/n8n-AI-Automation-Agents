# Ultimate Company Research Workflow (n8n)

This n8n workflow automates the process of deep-diving into company research. It aggregates data from **Trustpilot**, **Official Websites**, and **LinkedIn**, uses AI to analyze sentiment and extract structured data, and compiles a comprehensive report into a Google Sheet.

## 🚀 Features

* **Trustpilot Analysis:** Scrapes reviews using Firecrawl, parses them via code, and uses GPT-4o-mini to generate a sentiment summary (Pros, Cons, and Product feedback).
* **Website Intelligence:** Scrapes the target company's website using Jina AI and uses an AI Information Extractor to structure data into categories like "Business Overview," "Market Position," and "Company Culture."
* **LinkedIn Enrichment:** Fetches official company metrics (Followers, Headquarters, Founding Year) using Proxycurl/Nubela.
* **Centralized Reporting:** Reads input from and writes final analysis back to Google Sheets.

---

## 📋 Prerequisites

To run this workflow, you need an active n8n instance and API keys for the following services:

1. **OpenAI:** For the LLM agents (`gpt-4o-mini`).
2. **Google Cloud Platform:** OAuth2 credentials for Google Sheets.
3. **Firecrawl:** For scraping Trustpilot pages.
4. **Jina AI:** For converting website HTML to LLM-ready text.
5. **Nubela (Proxycurl):** For scraping LinkedIn company profiles.

---

## ⚙️ Workflow Logic

1. **Trigger:** Manual start (or can be scheduled).
2. **Input:** Reads a row from Google Sheets containing the company `website` and `linkedin_profile_url`.
3. **Parallel Processing:**
   * **Path A (Reputation):** Scrapes Trustpilot → Clean Data via Code → AI summarizes reviews.
   * **Path B (Content):** Scrapes Company Website → AI extracts structured JSON (Mission, Products, Culture).
4. **Enrichment:** Uses the LinkedIn URL to fetch firmographic data (Locations, Follower counts).
5. **Output:** Updates the Google Sheet with a combined profile.

---

## 🛠️ Google Sheets Setup

You need a Google Sheet with two tabs.

### Tab 1: "Company List" (Input)
Create a sheet with the following columns (headers):
* `website` (e.g., `zomato.com`)
* `linkedin_profile_url` (e.g., `https://www.linkedin.com/company/zomato/`)

### Tab 2: "Scrape Data" (Output)
The workflow will append data here. Ensure you have headers corresponding to the output mapping, or let n8n define them:
* `company_name`
* `company_website`
* `company_reviews` (The AI summary)
* `Company_business_profile` (Structured data)
* `company_followers_on_linkedin`
* `company_headquarters`
* `company_founded`

---

## 📥 Installation Steps

1. **Import:** Download the `lecturefile.json` and import it into your n8n workflows.
2. **Credentials:**
   * Open the workflow nodes.
   * Double-click the **Google Sheets** node and select your Google OAuth credential.
   * Double-click **Trustpilot Review** (HTTP Request) and add your Firecrawl API key.
   * Double-click **OpenAI Chat Model** and add your OpenAI API key.
   * Double-click **HTTP Request** (Jina AI) and add your Jina API key in the Authorization header.
   * Double-click **GetCompanyInfos** and add your Nubela/Proxycurl API key.
3. **Configure Sheet:** Update the `Document ID` and `Sheet Name` in the **Google Sheets** nodes to match your specific spreadsheet.
4. **Test:** Click "Test Workflow" to run a single execution based on the first row of your sheet.

---

## 🧩 Key Nodes Explained

| Node Name | Function |
| :--- | :--- |
| **Trustpilot Review** | Uses Firecrawl to get markdown content of the review page. |
| **Code** | Custom JavaScript to parse raw markdown, extracting specific star ratings and review text using Regex. |
| **Trustpilot Review Analyser** | LangChain node that prompts the LLM to create a "Customer Review Summary" identifying key improvement areas. |
| **Website Analysis** | LangChain Information Extractor that converts raw website text into a strict JSON schema (e.g., `company_culture`, `market_position`). |