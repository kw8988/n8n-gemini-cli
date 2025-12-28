# n8n Gemini CLI Agent (Telegram Edition)

> **Credit:** This project is inspired by and adapted from [NetworkChuck's n8n-claude-code-guide](https://github.com/theNetworkChuck/n8n-claude-code-guide).

While the original guide focuses on **Claude Code** and **Slack**, this project adapts the concept for **Google Gemini** and **Telegram**, making it a perfect fit for users in the Google ecosystem or those who prefer Telegram for their home automation notifications.

## 🤖 What is this?

![n8n Gemini Workflow](./assets/img/workflow_preview.png)

This project creates a bridge between **n8n** and the **Google Gemini CLI**. It allows you to chat with a powerful, context-aware AI agent directly from Telegram, with the AI running locally on your server (via SSH).

**Key Differences from the Original:**
*   **AI Engine:** Replaces `claude` with `gemini` CLI.
*   **Interface:** Replaces **Slack** with **Telegram**.
*   **Cost:** Leveraging Gemini's API (often free/lower cost for personal use tiers) vs. Anthropic's pricing.

## 🚀 Features

- **📱 Telegram Interface:** Chat with your AI agent on the go.
- **🧠 Context Awareness:** The workflow uses your Telegram Chat ID as a session key, so the bot remembers your conversation history.
- **🔒 Secure Execution:** Runs commands on your local machine via a secure SSH connection from n8n.
- **⚡ Fast Responses:** Optimized for the Gemini CLI.

## ⚙️ Architecture

1.  **Trigger:** You send a message to your Telegram Bot.
2.  **n8n Processing:**
    *   Sanitizes your text.
    *   Sets the session ID (to remember context).
3.  **SSH Tunnel:** n8n logs into your host machine via SSH.
4.  **Gemini Execution:** It runs the command: `gemini "Your prompt" --resume session_id`.
5.  **Reply:** The output is sent back to your Telegram chat.

## 🛠️ Prerequisites

1.  **n8n:** Installed and running (Docker or Local).
2.  **Google Gemini CLI:** Installed on your host machine.
    *   *Tip:* Ensure you can run `gemini "hello"` in your terminal first.
3.  **Telegram Bot:**
    *   Chat with `@BotFather` on Telegram to create a new bot and get your **API Token**.
4.  **SSH Access:** n8n needs SSH access to the machine running the Gemini CLI.

## 📥 Setup Guide

### 1. Clone & Prepare
```bash
git clone https://github.com/yourusername/n8n-gemini-cli.git
cd n8n-gemini-cli
```

### 2. Configure Credentials in n8n
Before importing the workflow, set up these credentials in n8n:
*   **Telegram API:** Use the token from `@BotFather`.
*   **SSH Password/Key:** Provide the login details for the machine running Gemini.

### 3. Import the Workflow
1.  Open your n8n dashboard.
2.  Go to **Workflows** > **Import from File**.
3.  Select `workflows/GeminiCLI.json` from this repository.
4.  **Update the Nodes:**
    *   Open the **Telegram Trigger** and **Telegram Reply** nodes and select your new Telegram credentials.
    *   Open the **Execute Command** (SSH) node and select your SSH credentials.
    *   *Important:* Check the **CWD** (Current Working Directory) in the SSH node. It defaults to `/path/to/workdir`. Change this to your actual home directory (e.g., `/home/youruser`).

### 4. Test It!
Start the workflow and send "Hello" to your Telegram bot. If everything is wired up, Gemini will reply!

## 📂 Project Structure

```
n8n-gemini-cli/
├── workflows/    # The "Brains" - Import this JSON into n8n
├── src/          # Helper scripts (if needed)
├── docs/         # Additional notes
└── .env.example  # Env var template
```

## 📄 License

This project is licensed under the MIT License.