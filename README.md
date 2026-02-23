# 🤖 Editor-in-Chief: Multi-Agent Content Factory

An autonomous AI orchestration system built in n8n that transforms any article URL into a multi-platform social media campaign using **Groq (Llama 3.3 & 3.1)**.



## 🧠 System Architecture
This project implements a **Hierarchical Orchestration** pattern:
* **Master Agent:** Uses `Llama-3.3-70b` for high-level reasoning and tool delegation.
* **Researcher Specialist:** Uses `Llama-3.1-8b` for cost-effective, high-speed data extraction and token management.
* **Social Strategist Specialist:** Uses `Llama-3.1-8b` for creative copywriting and platform-specific formatting.

## 🌟 Key Technical Features
- **Token Shielding:** Custom JavaScript logic strips HTML and trims text to 2,000 characters, preventing the common "40k Token Crash".
- **Modular Tooling:** Specialists are built as separate sub-workflows, allowing for easy updates and independent testing.
- **Context Management:** Implements **Simple Memory** with a limited window to keep the Master Agent focused and within TPM limits.

## 🚀 Installation & Setup

### 1. Prerequisites
You will need:
- An **n8n** instance (Self-hosted or Cloud).
- A **Groq API Key** (Free tier supported).
- **SerpAPI Key** (For the search capabilities).

### 2. Import Instructions
1.  **Import Specialists First:** Import `researcher_specialist.json` and `strategist_specialist.json`. Save both.
2.  **Import Master Agent:** Import `master_editor_agent.json`.
3.  **Relink Tools:** Open the AI Agent node in the Master Agent, click on the **Call n8n Workflow** tools, and select the specialists you just imported from the dropdown.
4.  **Enable AI Mapping:** Ensure the `url` and `hooks` input fields are set to **"Let the model define this parameter"**.

## 📊 Performance Data
- **Input Limit:** Handles articles up to 50k+ tokens via preprocessing.
- **Output:** ~200 tokens for social posts, staying well within Groq's 12K TPM free tier.
- **Execution Time:** ~10-15 seconds for a full campaign.
