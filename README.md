# Manage Google Calendar and Gmail via Webhook AI Assistant

![workflow](https://n8niostorageaccount.blob.core.windows.net/n8nio-strapi-blobs-prod/assets/Screenshot_2025_09_02_173202_fd39864888.png)
 
⚠️ **Disclaimer:** This workflow uses Gmail and Google Calendar nodes which you will need to configure with your own credentials.  

---

## Who’s it for  
This workflow is for developers, teams, and productivity enthusiasts who want to connect **any chatbot or frontend** (Discord, Telegram, WhatsApp, Slack, or a custom app) to an **AI-powered assistant** that can manage Gmail and Google Calendar.  
Instead of working inside n8n or Google UIs, you send natural language requests via a webhook, and the assistant handles the rest.  

---

## How it works  
- The **Webhook node** is the entry point. Any incoming request (chat message, API call, or app integration) triggers the assistant.  
- The **AI Agent** interprets natural language and decides which tool to use.  
- Uses **Google Calendar nodes** to:  
  - Check availability and list events.  
  - Create new events with attendees.  
  - Update existing events.  
- Uses **Gmail nodes** to:  
  - Send emails with clear subjects and professional body text.  
  - Retrieve and summarize recent messages.  
- The **Date & Time node** ensures proper handling of natural time requests like “tomorrow at 3 PM.”  
- The assistant includes **guardrails**: if details are missing, it asks for clarification before acting.  

---

## How to set up  
1. Import the workflow into your self-hosted n8n.  
2. Configure the **Webhook node** (default path: `/chat`).    
3. Create credentials for:  
   - Gmail API (OAuth2)  
   - Google Calendar API (OAuth2)  
   - AI provider (Google Gemini, OpenAI GPT, or another supported model)  
4. Update workflow defaults:  
   - Your Google Calendar email ID  
   - Timezone preferences  
   - Default conferencing (Google Meet included by default)  
5. Deploy the webhook endpoint and test with sample inputs like:  
   - “Schedule a meeting with alice@example.com tomorrow at 3 PM”  
   - “Check my inbox for emails from today”  
   - “What’s on my calendar this week?”  

---

## Test with a Webhook Chat Interface (optional)

If you want a simple chat UI to test this workflow without building your own frontend, you can use the chat interface here:

- Webhook Chatbot Interface: [webhook-chatbot-interface](https://github.com/Praneel7015/webhook-chatbot-interface)

How to use it:
1. Open `chat.html` from that repository in your browser.
2. In the file, set the fetch URL to your n8n webhook endpoint (for local testing, the default is `http://localhost:5678/webhook/chat`).
3. For deployment, replace the localhost URL with your publicly accessible webhook URL.

This provides a messenger-style interface that’s useful for quickly exercising your webhook and validating assistant behavior during development.

---

## Requirements  
- Self-hosted n8n instance  
- Gmail + Google Calendar account with API access enabled  
- Gmail and Google Calendar credentials set up in n8n  
- AI model credentials (Gemini, OpenAI, Claude, or other supported LLM)  
- An app or service to send requests to the webhook (chatbot or HTTP client)  

---

## Tools

### Webhook  
Entry point for the workflow. Receives text input from chatbots, apps, or HTTP requests.  

### AI Agent  
The “brain” of the assistant. Interprets requests and picks the correct tool. Always confirms before important actions.  

### Google Gemini Chat Model (or any LLM)  
Language model powering the assistant. Replaceable with OpenAI GPT, Claude, or local LLMs.  

### Simple Memory  
Maintains short-term context (last ~10 interactions). Helps the AI understand follow-up queries.  

### Gmail Tools  
- **Send a message in Gmail** → Sends emails (recipient, subject, body).  
- **Get many messages in Gmail** → Retrieves and summarizes recent emails.  

### Google Calendar Tools  
- **Get many events in Calendar** → Lists your schedule.  
- **Get availability** → Checks if you’re free.  
- **Create an event** → Books a new meeting with title, attendees, time, and Google Meet link.  
- **Update an event** → Edits existing meetings (time, attendees, details).  

### Date & Time  
Converts “tomorrow at 3 PM” into precise ISO timestamps.  

---

## How to customize the workflow  
- Swap the AI model (Gemini, OpenAI, Claude, or local).  
- Modify the system prompt to adjust tone or rules.  
- Add Slack/Teams/Notion integration alongside Gmail/Calendar.  
- Extend webhook responses with custom formatting (JSON, chat-style, etc.).  
- Add retry/error handling for scheduling conflicts.  

---

## Contributions  
- Contributions and issues are welcome.  
- Contact: open an issue or PR if you need help.  

