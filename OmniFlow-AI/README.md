<p align="center">
  <h1 align="center">OmniFlow AI</h1>
  <p align="center"><b>Autonomous Multi-Agent Orchestration & Enterprise Automation Engine</b></p>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/OmniFlow_AI-Autonomous_Orchestrator-000000?style=for-the-badge&logo=ai&logoColor=white" alt="OmniFlow AI">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/n8n-Workflow_Automation-000000?style=flat-square&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/LangChain-AI_Framework-000000?style=flat-square&logo=langchain&logoColor=white" alt="LangChain">
  <img src="https://img.shields.io/badge/OpenAI-GPT--4o_/_Whisper-000000?style=flat-square&logo=openai&logoColor=white" alt="OpenAI">
  <img src="https://img.shields.io/badge/Google_Gemini-Reasoning_Engine-000000?style=flat-square&logo=googlegemini&logoColor=white" alt="Google Gemini">
  <img src="https://img.shields.io/badge/Perplexity_AI-Web_Intelligence-000000?style=flat-square&logo=perplexity&logoColor=white" alt="Perplexity AI">
  <img src="https://img.shields.io/badge/Qdrant-Vector_Database-000000?style=flat-square&logo=qdrant&logoColor=white" alt="Qdrant">
  <img src="https://img.shields.io/badge/PostgreSQL-Chat_Memory-000000?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Gmail-Email_Automation-000000?style=flat-square&logo=gmail&logoColor=white" alt="Gmail">
  <img src="https://img.shields.io/badge/Google_Drive-Cloud_Storage-000000?style=flat-square&logo=googledrive&logoColor=white" alt="Google Drive">
  <img src="https://img.shields.io/badge/Google_Calendar-Scheduling-000000?style=flat-square&logo=googlecalendar&logoColor=white" alt="Google Calendar">
  <img src="https://img.shields.io/badge/Google_Sheets-Data_Management-000000?style=flat-square&logo=googlesheets&logoColor=white" alt="Google Sheets">
  <img src="https://img.shields.io/badge/Google_Docs-Documentation-000000?style=flat-square&logo=googledocs&logoColor=white" alt="Google Docs">
  <img src="https://img.shields.io/badge/Google_Slides-Presentations-000000?style=flat-square&logo=googleslides&logoColor=white" alt="Google Slides">
</p>

---

## 📑 Project Overview

**OmniFlow AI** is a professional-grade, autonomous multi-agent system designed for enterprise-level automation. Engineered using the **n8n** framework, it implements a highly-scalable "OpenClaw" orchestration pattern that consolidates fragmented business tools into a single, intelligent interface.

The system acts as an **Autonomous Executive**, capable of interpreting multi-modal inputs (Voice, Text, Vision) and executing complex, cross-platform workflows. By sitting at the intersection of LLM reasoning and professional toolsets, OmniFlow AI automates the "thinking" as well as the "doing," making it a powerful asset for modern AI-driven operations.

---

## 🏗️ Technical Architecture

The following diagram illustrates the high-level architecture of the OmniFlow AI system, featuring a black-and-white professional theme.

```mermaid
graph TD
    %% Global B&W Styling
    classDef mainNode fill:#000,stroke:#fff,stroke-width:2px,color:#fff
    classDef subNode fill:#fff,stroke:#000,stroke-width:1px,color:#000
    classDef container fill:#f5f5f5,stroke:#000,stroke-dasharray: 5 5

    %% Entry Points
    User((<b>User</b>)) -- "Multi-modal Input" --> Gateway[<b>Telegram Gateway</b>]
    
    subgraph "Preprocessing & Validation"
        Gateway --> Auth{<b>Security Check</b>}
        Auth -- "Authorized" --> Logic[<b>Input Normalization</b>]
        Logic --> Transcribe[<b>Whisper (Voice)</b>]
        Logic --> Vision[<b>GPT-4o (Vision)</b>]
    end

    %% Core Orchestration
    subgraph "Agentic Core"
        Transcribe --> Orchestrator["<b>🧠 OmniFlow Orchestrator</b><br/>Autonomous Planner"]
        Vision --> Orchestrator
        Orchestrator <--> Memory[(<b>Persistent Memory</b><br/>PostgreSQL)]
    end

    %% Specialized Toolsets
    subgraph "Execution Layer (Pipelines)"
        Orchestrator --> GSuite["<b>G-Suite Pipeline</b><br/>Gmail, Drive, Sheets, Docs"]
        Orchestrator --> Intelligence["<b>Research Pipeline</b><br/>Perplexity, ScrapeGraph"]
        Orchestrator --> Knowledge["<b>Knowledge Pipeline</b><br/>Qdrant (RAG), Cohere"]
        Orchestrator --> Creative["<b>Media Pipeline</b><br/>Grok Image/Video"]
    end

    %% Feedback Loop
    GSuite --> Orchestrator
    Intelligence --> Orchestrator
    Knowledge --> Orchestrator
    Creative --> Orchestrator

    %% Output
    Orchestrator --> Response[<b>Final Synthesis</b>]
    Response --> User

    %% Apply Styles
    class Gateway,Orchestrator,Response mainNode
    class Auth,Logic,Transcribe,Vision,GSuite,Intelligence,Knowledge,Creative subNode
```

---

## ⚙️ Core Pipelines

The OmniFlow AI architecture is built around several "High-Throughput Pipelines" that handle specific enterprise tasks:

### 1. **G-Suite Workflow Pipeline**
*   **Purpose**: Complete automation of the Google Workspace ecosystem.
*   **Mechanism**: Uses **Model Context Protocol (MCP)** to bridge n8n with G-Suite APIs.
*   **Capabilities**: Automated draft generation, intelligent calendar conflict resolution, and dynamic documentation synthesis.

### 2. **Cognitive Research Pipeline**
*   **Purpose**: Real-time information gathering and data extraction.
*   **Mechanism**: Chained execution between **Perplexity AI** (for broad search) and **ScrapeGraph AI** (for structured scraping).
*   **Capabilities**: Competitor analysis reports, market trend extraction, and cited source consolidation.

### 3. **RAG & Knowledge Pipeline**
*   **Purpose**: Context-aware retrieval of private enterprise data.
*   **Mechanism**: High-speed vector search via **Qdrant** with **Cohere Reranking** for maximum relevance.
*   **Capabilities**: Private policy querying, internal document search, and personal knowledge base interaction.

### 4. **Multi-modal Input Pipeline**
*   **Purpose**: Seamless handling of diverse communication types.
*   **Mechanism**: Parallel processing of **Whisper** (Audio) and **GPT-4o/Gemini** (Vision/Text).
*   **Capabilities**: Hands-free voice operation, visual document analysis, and complex OCR-based triggers.

---

## 🛠️ Technology Stack

| Stack | Technologies |
| :--- | :--- |
| **Frameworks** | n8n, LangChain |
| **Intelligence** | GPT-4o, Gemini 1.5 Pro, Whisper, Cohere |
| **Databases** | PostgreSQL (History), Qdrant (Vector) |
| **Integrations** | Gmail, Drive, Calendar, Sheets, Docs, Slides, Telegram |
| **Research** | Perplexity AI, ScrapeGraph AI |
| **Media** | Grok (xAI) |

---

## 💼 Deployment & Configuration

1.  **Workflow Import**: Import the production-ready `OmniFlow_AI.json` into n8n.
2.  **Auth Configuration**: Set your authorized `USER_ID` and Telegram credentials.
3.  **MCP Server Setup**: Connect your MCP servers for Google Workspace endpoints.
4.  **Credential Management**: Securely store API keys for OpenAI, Google, and Perplexity within n8n.

---

## 📄 License
This system is provided under the **MIT License**. It is designed as a template for professional-grade autonomous agent deployments.

---
<p align="center">
  <b>Developed for Professional Portfolio Use | n8n Multi-Agent System v1.0</b>
</p>
