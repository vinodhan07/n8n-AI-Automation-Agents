# Ultimate Company Research (Webinar)

This n8n workflow automates the process of conducting due diligence and market research on companies. It aggregates data from Google Sheets, scrapes Trustpilot reviews and company websites, analyzes sentiment using OpenAI, and enriches the data using Google Search (SerpApi) before saving the results back to Google Sheets.

## Workflow Overview

The workflow performs the following steps:

1.  **Input Retrieval**: Fetches company data (specifically website URLs) from a Google Sheet named "Sheet1".
2.  **Trustpilot Scraping**: Uses the Firecrawl API (`v2/scrape`) to retrieve review data from Trustpilot based on the company's website.
3.  **Data Parsing**: A JavaScript Code node processes the raw markdown to extract the Company Name, TrustScore, Total Reviews, and individual review details (rating, title, content).
4.  **Review Analysis**: An OpenAI Chat Model (`gpt-4.1-mini`) generates a "Customer Review Summary," including overall feedback, product sentiment analysis, and key improvement areas.
5.  **Website Analysis**:
    * **Scraping**: Uses Jina AI to scrape the company's official website content.
    * **Extraction**: An AI Information Extractor node converts the website text into a structured JSON object containing Company Basics, Business Overview, Products/Services, Market Position, and Company Culture.
6.  **Enrichment**: A loop processes items to perform a Google Search via SerpApi to find LinkedIn profile details.
7.  **Output**: Appends the consolidated research data into a Google Sheet.

## Prerequisites

To run this workflow, you need credentials for the following services:

* **Google Sheets**: OAuth2 credentials to read and write data to your spreadsheets.
* **Firecrawl**: An API key to handle Trustpilot scraping.
* **OpenAI**: An API key to power the LLM nodes (Chat Model and Information Extractor).
* **Jina AI**: An Authorization Bearer token to scrape website content.
* **SerpApi**: An API key to perform Google searches for LinkedIn profiles.

## Data Structures

### Input (Google Sheets)
The workflow expects a Google Sheet with a column containing the company website URL. The specific sheet used in the configuration is "Sheet1".

### Output (Google Sheets)
The workflow appends a new row to the "Company Details" sheet with the following columns:
* `company_name`: Extracted from organic search results.
* `company_website`: Snippet from search results.
* `company_reviews`: The AI-generated summary of Trustpilot reviews.
* `company_business_profile`: The LinkedIn Profile URL.
* `company_linkedin_extracr`: A composite field containing the AI extraction text, key offerings, products/services, target audiences, unique values, and competitive advantages.
* `company_followers_on_linkedin`: Displayed link from search results.
* `company_about_us`: Snippet from search results.
* `company_industry`: Snippet from search results.
* `company_size`: Snippet from search results.
* `company_headquaters`: Extracted location data from the Website Analysis.
* `company_founded`: Extracted founding date from search related questions.

## AI Prompts

### Trustpilot Analyzer
The AI is prompted to output a structured summary starting with the company name, followed by:
* **Overall Company Feedback**: General sentiment highlighting positive and negative aspects.
* **Product Sentiment Analysis**: Sentiment breakdown for key products mentioned.
* **Key Improvement Areas**: Top 2-3 suggestions based on negative feedback.

### Information Extractor
The AI extracts a specific JSON schema from the website content, including:
* **Company Basics**: Name, industry, headquarters, founded date, website.
* **Business Overview**: Description, mission statement, key offerings.
* **Market Position**: Target audience, unique value proposition, competitive advantages.
* **Company Culture**: Values, work environment, team highlights.