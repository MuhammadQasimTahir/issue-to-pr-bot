# Autonomous GitHub Issue-to-PR "Code Copilot" Agent

An event-driven AI workflow built in n8n that acts as an autonomous software engineering copilot. When a new GitHub issue is opened, the agent autonomously explores the repository to find the root cause, writes a code patch, and automatically opens a Pull Request while dispatching a review notification to Discord.

## 🚀 Core Features

* **Event-Driven Trigger:** Captures `issues.opened` GitHub webhooks, validating payload length and specific issue labels (e.g., `bug`) before execution.
* **Agentic Repository Exploration:** Utilizes a LangChain AI Agent equipped with custom GitHub REST tools (`list_directory`, `search_repo_code`, `get_file_contents`) to autonomously navigate and debug the codebase.
* **Programmatic Git Operations:** Dynamically fetches base commit SHAs, creates isolated hotfix branches (`fix/issue-{number}`), base64-encodes patches, and commits updates entirely via the GitHub API.
* **Human-in-the-Loop Review:** Automatically opens structured Pull Requests with auto-closing keywords and dispatches interactive review cards to Discord.

## 🛠️ Prerequisites

* **n8n Instance:** Running locally (via Docker) or cloud-hosted.
* **GitHub Personal Access Token (PAT):** With repository read/write permissions (`repo` scope).
* **Google Gemini API Key:** For the underlying AI Agent processing.
* **Discord Bot Token & Channel ID:** For real-time review alerts.

## ⚙️ Setup Instructions

1. **Import the Workflow:** Download the workflow JSON file and import it directly into your n8n workspace.
2. **Configure Credentials:** Add and link your GitHub PAT and Google Gemini API keys in the respective n8n credential managers.
3. **Update Target Repository:** Open the **Github Trigger** node and update the `Owner` to `<your-github-username>` and the `Repository` to `<your-repo-name>`.
4. **Configure Discord Secrets:** Ensure your n8n environment has the following variables securely configured for the webhook alerts:
   * `DISCORD_BOT_TOKEN`
   * `DISCORD_CHANNEL_ID`
5. **Activate & Test:** Toggle the workflow to **Active**. Open a new issue in your repository, apply the required trigger label, and watch the Copilot resolve it!
