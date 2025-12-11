# n8n AI News Summarizer

**Automated daily news summaries delivered to WhatsApp using n8n, AI, and Twilio.**

---

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
* (Optional) Small helper service or functions (Node.js) for advanced processing

---

## Architecture (High-level)

1. Scheduled trigger in n8n (cron) starts the workflow.
2. Fetch news from configured APIs (separate nodes for India/World/Tech).
3. Parse and normalize results; extract relevant text and metadata.
4. Combine and clean article texts (de-duplication, trimming).
5. Send combined text to AI summarization node.
6. Receive summary and format message.
7. Send message to WhatsApp via Twilio node.
8. Log success/failure and optionally save summaries to a datastore.

---

## Setup & Installation

### Prerequisites

* Node.js (if self-hosting any helper service)
* n8n (cloud or self-hosted)
* Twilio account with WhatsApp sandbox or approved WhatsApp sender
* API key(s) for chosen news provider(s)
* AI model API key or access (OpenAI, Google, Ollama, etc.)

### Environment Variables

Create a `.env` file (if using local helper service) and add:

```
NEWS_API_KEY=your_news_api_key
AI_API_KEY=your_ai_api_key
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_WHATSAPP_FROM=whatsapp:+1415XXXXXXX   # Twilio sandbox or number
WHATSAPP_TO=whatsapp:+91YYYYYYYYYY         # Recipient number
```

> Note: In n8n you can store credentials in the Credentials manager instead of `.env`.

---

## n8n Workflow (recommended nodes)

A suggested simplified workflow layout:

1. **Cron** (trigger) — schedule daily run
2. **HTTP Request** — fetch India news API
3. **HTTP Request** — fetch World news API
4. **HTTP Request** — fetch Tech news API
5. **Function / Code** — normalize & extract article text
6. **SplitInBatches** or **Merge** — combine texts into a single payload
7. **AI / HTTP Request** — call summarization API with prompt (system + user prompt)
8. **Function** — format the summary message (add date, source list)
9. **Twilio** (or HTTP Request to Twilio) — send WhatsApp message
10. **IF** / **Error handling** — capture failures and log/notify

### Example prompt (for summarization)

```
You are an assistant that writes a concise 5-7 sentence summary of the following news items. Keep it neutral, accurate, and include the most important facts and one-sentence call-to-action to read more.

[INSERT COMBINED ARTICLES HERE]
```

---

## Twilio WhatsApp Setup

1. Sign up for Twilio and activate the WhatsApp sandbox (or a production WhatsApp sender).
2. Note your `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`.
3. Configure the `From` WhatsApp number (Twilio will provide `whatsapp:+1415...` for sandbox).
4. Add the recipient to the sandbox by sending the required join message from the recipient's WhatsApp.
5. In n8n, configure Twilio credentials and use the Twilio node to send the message.

---

## How to Run (Quick)

1. Import the provided n8n workflow JSON into your n8n instance.
2. Add credentials for News API, AI provider, and Twilio in n8n Credentials.
3. Configure schedule on the Cron trigger.
4. Test-run the workflow and check the Twilio message delivery.

---

## Customization Ideas

* Add category filters or keywords to control which articles are included.
* Save daily summaries to a Google Sheet or database for an archive.
* Add image or link previews in WhatsApp message (if supported by Twilio and content type).
* Implement richer NLP: extract entities, sentiment, or headlines-only mode.

---

## Troubleshooting

* **No messages delivered:** Check Twilio sandbox join steps, credentials, and the `From`/`To` numbers format (`whatsapp:+<countrycode><number>`).
* **AI failures / rate limits:** Check API keys, quotas, and payload size. Chunk or shorten combined text before sending to the model.
* **Duplicate or irrelevant content:** Add de-duplication logic and stricter filters when extracting article text.

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

*Generated README — adapt the API names and config examples to the exact services you used.*
