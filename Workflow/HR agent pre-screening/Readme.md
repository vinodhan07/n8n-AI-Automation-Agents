# HR Agent Pre-Screening Workflow (n8n)

This n8n workflow automates the recruitment pre-screening process. It monitors a Gmail inbox for job applications, analyzes attached CVs using AI, scores candidates against a specific job description, logs the results in Google Sheets, and sends an automated acknowledgement email to the candidate.

## 🚀 Features

* **Automated Email Parsing:** Monitors Gmail for incoming emails and uses AI to classify if the email is a legitimate job application.
* **Resume Handling:** Automatically uploads PDF attachments to Google Drive and extracts the text content for analysis.
* **AI Candidate Scoring:** Uses OpenAI (GPT-4o-mini) to analyze the candidate's profile against a defined "Business Development Representative" role. It scores the candidate (0-10) and provides a reasoning summary.
* **Structured Data Logging:** Parsed candidate data (Name, Email, Skills, Score) is formatted into JSON and appended to a Google Sheet.
* **Auto-Reply:** Sends a professional confirmation email back to the candidate.

## 📋 Prerequisites

To use this workflow, you need the following:

1.  **n8n:** An active instance of n8n.
2.  **OpenAI Account:** API Key with access to Chat models (default is configured for `gpt-4.1-mini` or `gpt-4o-mini`).
3.  **Google Cloud Project:** Configured with OAuth2 credentials for:
    * Gmail API
    * Google Drive API
    * Google Sheets API

## 🛠️ Setup & Configuration

### 1. Import Workflow
Import the provided JSON file into your n8n editor.

### 2. Configure Credentials
You must set up the following credentials in n8n:
* `OpenAi account`
* `Gmail account`
* `Google Drive account`
* `Google Sheets account`

### 3. Google Sheet Setup
Create a new Google Sheet. The workflow expects the following columns (headers) in `Sheet1`:
* `First Name`
* `Last Name`
* `Email`
* `Email Content`
* `Summary`
* `CV` (This will store the Google Drive Link)
* `Scoring`
* `Quick Read`

*Update the **Append row in sheet** node with your specific Spreadsheet ID.*

### 4. Google Drive Setup
* Ensure you have a specific folder created in Google Drive to store resumes.
* Update the **Upload file** node with the correct parent Folder ID.

### 5. Job Description (Customization)
The workflow is currently hardcoded for a **Business Development Representative (BDR)** role at "FIN AI".

To change the job description:
1.  Open the **AI Agent1** node.
2.  Edit the **Text** field.
3.  Replace the text under "The actual position being open is..." with your own job description and company details.

## 🔄 Workflow Logic

1.  **Gmail Trigger:** Checks inbox every minute.
2.  **Text Classifier:** Analyzes email body to determine if category is "Apply" or "Doesn't apply".
3.  **Filter (Switch):** Proceeds only if the email is classified as "Apply" AND contains an attachment.
4.  **File Operations:**
    * Uploads PDF to Google Drive.
    * Sets permission to "Anyone with link" (Reader) so the link is accessible.
    * Extracts text from the PDF.
5.  **AI Analysis:** The Agent reviews the extracted text against the Job Description prompt.
6.  **Structured Output:** Parser separates the AI response into fields (Fit Score, Experience, Technical Skills, etc.).
7.  **Database:** Appends the structured data to Google Sheets.
8.  **Reply:** Sends a "Thank you for applying" email to the sender.

## ⚠️ Troubleshooting

* **No Attachment Error:** If a candidate applies without a PDF, the `Switch1` node will stop the execution.
* **Auth Errors:** Ensure your Google OAuth scopes include `https://www.googleapis.com/auth/drive`, `https://www.googleapis.com/auth/spreadsheets`, and `https://www.googleapis.com/auth/gmail.modify`.