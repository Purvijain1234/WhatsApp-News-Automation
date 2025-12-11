# WhatsApp News Automation

**Automated daily news summaries delivered to WhatsApp using n8n, AI, and Twilio.**

---

## Workflow

<img width="1477" height="343" alt="Image" src="https://github.com/user-attachments/assets/c919d3f1-5f66-4ec0-b1d6-9d86e9aeb9a7" />

## Project Overview

This project automates a pipeline that collects news (India, World, Tech) from news APIs, processes and combines article content in n8n, uses an AI model to generate a concise daily summary, and delivers the summary to a WhatsApp number via the Twilio WhatsApp API.

It demonstrates end-to-end automation, API integrations, lightweight data processing, and AI-powered summarization.

---

## Features

* Fetches news from multiple APIs (India / World / Tech categories).
* Cleans and combines article text.
* Uses an AI model to generate a concise, readable summary.
* Sends summary automatically to WhatsApp using Twilio.
* Scheduleable in n8n (daily or custom cron).
* Logging and basic error handling.

---

## Tech Stack

* **n8n** — workflow automation and orchestration
* **AI model** — any compatible text summarization model or API (OpenAI, Google, local LLM) integrated via HTTP or n8n node
* **Twilio** — WhatsApp API for delivery
* **News APIs** — (e.g., NewsAPI, GNews, custom RSS endpoints) — replaceable

---

## Architecture 

1. Scheduled trigger in n8n (cron) starts the workflow.
2. Fetch news from configured APIs (separate nodes for India/World/Tech).
3. Parse and normalize results; extract relevant text and metadata.
4. Combine and clean article texts (de-duplication, trimming).
5. Send combined text to AI summarization node.
6. Receive summary and format message.
7. Send message to WhatsApp via Twilio node.
8. Log success/failure and optionally save summaries to a datastore.

---

## Prerequisites

* n8n (cloud or self-hosted)
* Twilio account with WhatsApp sandbox or approved WhatsApp sender
* API key(s) for chosen news provider(s)
* AI model API key or access (OpenAI, Google, Ollama, etc.)

---

## 🧑‍💻 Getting Started

1. Clone the repository
```bash
git clone https://github.com/Purvijain1234/WhatsApp-News-Automation.git
```

2. Set up n8n
- Install n8n locally or use n8n Cloud.
- Follow the official guide: https://docs.n8n.io/hosting/installation/

3. Import Workflow(s)
- Use n8n’s workflow import feature to add the news automation workflows from the /workflows/ folder.
- Workflows include:
  - News API fetch (India / World / Tech)
  - AI summarization flow
  - WhatsApp message delivery (Twilio)

4. Configure Credentials
- Set up credentials and data source connections within n8n.
- Add the following credentials:
  - News API Key
  - AI Model API Key (OpenAI / Gemini / etc.)
  - Twilio WhatsApp Credentials:
    - Account SID
    - Auth Token
    - WhatsApp From + To numbers

5. Customize Templates
- Modify:
  - News categories or keywords
  - AI summary prompt
  - WhatsApp message format
- These can be edited inside the Function and AI nodes.

6. Run the Workflow
- Trigger manually or create a scheduled automation.
- OR set a Cron schedule to automatically receive daily summarized news on WhatsApp.

---


### Example prompt (for summarization)

```
You are an assistant that writes a concise 5-7 sentence summary of the following news items. Keep it neutral, accurate, and include the most important facts and one-sentence call-to-action to read more.

```

---

## Contributing

Contributions, suggestions, and bug reports are welcome. Open a GitHub issue or submit a pull request with clear description and reproduction steps.

---

## License

This project is released under the MIT License. See `LICENSE` for details.

---

## Contact

Project owner: Purvi Jain
LinkedIn: [https://www.linkedin.com/in/purvi-jain-315683326](https://www.linkedin.com/in/purvi-jain-315683326)

---
