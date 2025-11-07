🤖 n8n AI Automation Agents

A complete suite of AI-powered automation workflows built with n8n.

This repository contains a collection of smart, production-ready n8n JSON workflows — integrating OpenAI, Gemini, Google APIs, Telegram, Webhooks, and HTTP tools to automate tasks across email, calendar, content, and communication.

📂 Included Workflows
1. 🧑‍💻 Developer Workflow Builder

File: n8n_Developer_Agent.json
Automatically generates new n8n workflows from natural language prompts.

Uses GPT-4.1 & Claude via OpenRouter

Connects to n8n API and Google Drive

Ideal for developers building automations with AI

2. ✉️ Smart Email Generator

File: n8n.json
Reads data from Google Sheets, drafts personalized Gmail messages.

GPT-4.1-mini model

Personality-based tone control

Fully integrated with Gmail & Sheets

3. 😂 Joke Agent (with HTTP Tool)

File: Joke agent (with HTTP tool).json
AI joke generator using Gemini and JokeAPI.

Integrates external APIs dynamically

Chat-based humor engine with memory

4. 💞 Lovable Excuse Generator

Files: Lovable_and_N8N.json, Lovable and N8N.json
Webhook-driven funny or realistic excuse generator.

Uses GPT-4o-mini

Perfect example of n8n + OpenAI integration

5. 🔎 R&D Research Agent

File: R&D.json
Web-connected research workflow with SerpAPI and LLM reasoning.

Searches live data

Summarizes and verifies facts with GPT and Gemini

Ideal for knowledge workflows

6. 📅 AI Event Scheduling Assistant (Telegram + GCal)

File: SCHEDULING THE EVENT.json
Conversational scheduling through Telegram.

Reads and edits Google Calendar

Understands natural language dates

Ideal for personal assistant bots

7. 📣 Social Media Content Creator

File: social media ai.json
Turns blog URLs into ready-to-post social media content.

Extracts facts, generates captions, and AI images

Logs output in Google Sheets

8. 🎤 Voice Assistant Agent (Telegram + GCal)

File: Voice assistant agent (with Telegram and Gcal).json
A fully functional voice-enabled personal AI assistant.

Handles both text and voice messages in Telegram

Integrates with Google Calendar

Powered by GPT-4.1-mini

Automatically transcribes voice → responds naturally

9. 🌐 Webhook Request Automation

File: WEBHOOK REQUEST.json
Automates API call chains with wait timers and Telegram triggers.

Uses HTTP requests with Bearer auth

Integrates with BrowserAct API

Demonstrates complex HTTP orchestration in n8n

🧩 Tech Stack

n8n (v1.80+ recommended)

OpenAI / Gemini / Claude APIs

Google Calendar, Gmail, Sheets, Drive

Telegram Bot API

SerpAPI, BrowserAct API

Webhooks & HTTP Request nodes

🚀 How to Use

Clone the repository:

git clone https://github.com/vinodhan07/n8n-AI-Automation-Agents.git


Open n8n → click Import Workflow

Select a .json file

Add required credentials

Execute and enjoy your automation!

⚙️ Required Credentials

OpenAI / Gemini API Keys

Google Cloud (Sheets, Gmail, Calendar)

Telegram Bot API Token

SerpAPI Key (for R&D)

BrowserAct Key (for Webhook Request flow)

👨‍💻 Author

Created by Vinodhan V A

✨ Passionate about AI-powered workflow automation using n8n + LLMs

📜 License

MIT License © 2025 [Vinodhan V A]

⭐ Star this repository if you find it useful!
