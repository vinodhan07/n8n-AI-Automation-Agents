# Ultimate Company Research (Multi-URL Support)

This n8n workflow automates the process of deep-diving into competitor analysis. It iterates through a list of companies provided in a Google Sheet, scrapes data from **Trustpilot**, **Official Websites**, and **LinkedIn**, uses AI to generate insights, and saves the consolidated report back to Google Sheets.

## 🚀 Features

* **Batch Processing:** Uses a loop to process multiple companies from a Google Sheet list.
* **Trustpilot Intelligence:** Scrapes reviews using Firecrawl, extracts data via custom JavaScript, and uses GPT-4o-mini to generate a sentiment summary (Overall feedback, Product sentiment, and Improvement areas).
* **Website Analysis:** Scrapes company websites using Jina AI and uses an LLM Information Extractor to structure unstructured text into categories like "Business Overview," "Market Position," and "Company Culture."
* **LinkedIn Enrichment:** Fetches firmographic data (Headquarters, Size, Followers, Tagline) using the Nubela/Proxycurl API.
* **Consolidated Reporting:** Appends a fully enriched row for each company into Google Sheets.

## 📋 Prerequisites

To run this workflow, you need an active n8n instance and credentials for the following services:

1.  **Google Sheets:** OAuth2 credentials to read inputs and write outputs.
2.  **Firecrawl API:** To scrape Trustpilot review pages.
3.  **OpenAI API:** To power the Sentiment Analysis and Information Extraction agents (`gpt-4o-mini`).
4.  **Jina AI:** To convert company websites into LLM-friendly text.
5.  **Nubela (Proxycurl) API:** To fetch LinkedIn company profile data.

## ⚙️ Workflow Logic

1.  **Input:** Reads the "Competitor List" from Google Sheets.
2.  **Loop:** Iterates through every row found in the input sheet.
3.  **Trustpilot Branch:**
    * Scrapes the Trustpilot URL.
    * Parses Markdown to extract specific ratings and review text.
    * Generates a "Customer Review Summary" using AI.
4.  **Website Branch:**
    * Scrapes the official website.
    * Extracts structured JSON (Mission, Target Audience, USP) using AI.
5.  **LinkedIn Branch:**
    * Fetches official metrics (Follower count, Founded year, HQ) using the LinkedIn URL.
6.  **Output:** merges all data points and appends a new row to the "Scrape Data" sheet.

## 🛠️ Google Sheets Setup

You need a Google Sheet with two tabs.

### Tab 1: Input (e.g., "Competitor List")
Must contain the following headers (case-sensitive based on your workflow mapping):
* `website` (e.g., `www.example.com`)
* `linkedin_profile_url` (e.g., `https://www.linkedin.com/company/example`)

### Tab 2: Output (e.g., "Scrape Data")
Ensure your sheet has headers matching the final node's configuration:
* `company_name`
* `company_website`
* `company_reviews` (AI Summary)
* `Company_business_profile` (AI Extracted Description & Offerings)
* `company_industry`
* `company_about_us` (LinkedIn Description)
* `company_size`
* `company_headquarters`
* `company_founded`
* `company_followers_on_linkedin`
* `company_linkedin_extract` (Tagline)

## 🧩 Node Breakdown

| Node Name | Function |
| :--- | :--- |
| **Competitor Data1** | Fetches the list of URLs to process. |
| **Trustpilot Review Scraping** | Uses Firecrawl to get the review page content. |
| **Extract Info** | Custom JavaScript that parses ratings, titles, and dates from the raw markdown. |
| **TrustPilot Review** | AI Agent that summarizes sentiment and identifies product pros/cons. |
| **Website Analyser** | AI Information Extractor that pulls structured data (Values, Culture, Pricing) from the website text. |
| **GetCompanyInfos** | Connects to Nubela to get LinkedIn data. |