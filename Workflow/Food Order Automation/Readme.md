# 📦 Telegram Food Order Automation (n8n)

An end-to-end **Telegram-based food order automation** built using **n8n**, designed to handle unstructured user messages and convert them into clean, validated order data stored in **Google Sheets**, with instant confirmation sent back to users.

This workflow removes manual order handling and ensures accuracy, consistency, and scalability.

---

## 🚀 Features

- 📩 Real-time Telegram order intake
- 🧠 Regex-based intelligent message parsing
- ✅ Order validation with user feedback
- ⏰ Automatic meal type detection (time-based)
- 📊 Structured storage in Google Sheets
- 📁 Excel-compatible order formatting
- 🔔 Automated Telegram order confirmation
- 🔄 Production-ready, fault-tolerant workflow

---

## 🛠 Tech Stack

- **n8n** – Workflow automation
- **Telegram Bot API** – Order intake & confirmation
- **JavaScript (Code Node)** – Parsing & business logic
- **Google Sheets API** – Persistent storage
- **Regex-based NLP logic** – Free-text interpretation

---

## 📐 Workflow Overview

Telegram Message
↓
Workflow Configuration
↓
Parse Order Message (Regex Logic)
↓
Validate Order Data
├── Invalid → Send Format Help
└── Valid
↓
Format Order Data
↓
Prepare Order Row
↓
Aggregate Orders
↓
Append to Google Sheet
↓
Send Order Confirmation


---

## 🧠 Parsed Order Fields

| Field | Description |
|------|------------|
| Customer Name | Extracted from flexible text formats |
| Dish Name | Supports dish / order / item keywords |
| Quantity | Supports qty, x2, 2 plates, etc. |
| Meal Type | Auto-detected from system time |
| Date | ISO format (YYYY-MM-DD) |
| Time | HH:MM:SS |
| Chat ID | Used for Telegram replies |

---

## 🕒 Meal Type Logic

| Time Range | Meal Type |
|-----------|-----------|
| 06:00 – 09:59 | Breakfast |
| 11:00 – 14:59 | Lunch |
| 19:00 – 21:59 | Dinner |
| 22:00 – 05:59 | Midnight Dinner |
| Others | Other |

---

## 📋 Recommended Order Format

Name: John Doe
Dish: Chicken Biryani
Quantity: 2


### Supported Flexible Inputs

- `John - Biryani x2`
- `Order: Dosa`
- `2 plates idli`

---

## ❌ Invalid Order Handling

- Detects missing or incorrect fields
- Sends a friendly format guide to the user
- Prevents incomplete or dirty data storage

---

## 📊 Google Sheets Output

Each order is appended as a new row with:

- Date
- Time
- Meal Type
- Customer Name
- Dish Name
- Quantity

This structure supports filtering, analytics, and reporting.

---

## 🔐 Reliability & Best Practices

- OAuth-based Google authentication
- No hardcoded credentials
- Default fallbacks for missing values
- Time-based logic handled server-side
- Safe execution flow with validation checks

---

## 📈 Scalability & Extensions

This workflow can be extended to support:
- Billing & price calculation
- Admin dashboards
- Multiple vendors or menus
- WhatsApp or Webhook-based intake
- LLM-powered intent extraction
- Database storage (Postgres / MongoDB)

---

## 📌 Applicable Use Cases

- Food order management
- HR candidate intake
- Service request logging
- Event registrations
- Internal operations automation

---

## 👨‍💻 Author
**Vinodhan V A**  
Automation Engineer | n8n | AI Agents  
GitHub: https://github.com/vinodhan07
Designed as a **production-ready automation workflow** using n8n, Telegram, and Google integrations.
