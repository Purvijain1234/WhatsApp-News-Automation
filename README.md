# n8n AI News Summarizer

**Automated daily news summaries delivered to WhatsApp using n8n, AI, and Twilio.**

---

## Workflow


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

## Setup & Installation

### Prerequisites

* n8n (cloud or self-hosted)
* Twilio account with WhatsApp sandbox or approved WhatsApp sender
* API key(s) for chosen news provider(s)
* AI model API key or access (OpenAI, Google, Ollama, etc.)

### Example prompt (for summarization)

```
You are an assistant that writes a concise 5-7 sentence summary of the following news items. Keep it neutral, accurate, and include the most important facts and one-sentence call-to-action to read more.

[INSERT COMBINED ARTICLES HERE]
```

---

## How to Run (Quick)

1. Import the provided n8n workflow JSON into your n8n instance.
2. Add credentials for News API, AI provider, and Twilio in n8n Credentials.
3. Configure schedule on the Cron trigger.
4. Test-run the workflow and check the Twilio message delivery.

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
