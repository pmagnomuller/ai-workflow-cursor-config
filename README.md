# AI-Powered Development Workflow Template

This repository provides a template for setting up an AI-assisted development workflow using **Cursor IDE** and **Model Context Protocols (MCPs)**. It automates repetitive tasks like managing tickets, updating documentation, and creating pull requests, allowing you to stay focused on problem-solving.

## 🎯 What This Workflow Does

Instead of constantly switching between Jira, Notion, and GitHub, you can work entirely within Cursor IDE using natural language commands:

- **"Start task [Jira link]"** - Fetches ticket details, prepares your workspace, and suggests implementation steps
- **"Update documentation"** - Automatically syncs code changes with Notion documentation
- **"Open PR"** - Creates a GitHub PR with formatted description, links, and all necessary details
- **PR Review** - AI analyzes code, summarizes changes, and suggests improvements

## 🚀 Quick Start

### Prerequisites

- [Cursor IDE](https://cursor.sh/) installed
- Node.js (for MCP servers)
- Accounts for:
  - Jira/Atlassian - authenticated via browser (MCP)
  - GitHub - Personal Access Token in Cursor IDE Settings
  - Notion - authenticated via browser (MCP)

### Setup Steps

For detailed setup instructions, see [SETUP.md](./SETUP.md).

**Quick Setup:**

1. **Clone this repository**
   ```bash
   git clone <this-repo-url>
   cd ai-workflow-cursor-config
   ```

2. **Configure GitHub in Cursor IDE Settings**
   
   GitHub is configured separately in Cursor IDE Settings (not via MCP):
   - Open Cursor IDE Settings (Cmd/Ctrl + ,)
   - Go to "GitHub" or "Integrations" section
   - Add your GitHub Personal Access Token with `repo` scope
   - Get token from [GitHub Settings](https://github.com/settings/tokens)

3. **Open in Cursor IDE**
   
   The MCP configuration for Jira and Notion is already set up in `.cursor/mcp.json`. Cursor will automatically load this configuration when you open the workspace.

4. **Authenticate Jira & Notion (Browser OAuth)**
   
   When you first use Jira or Notion commands, Cursor will open your browser for OAuth authentication:
   - Sign in to your accounts
   - Authorize the MCP connections
   - Authentication is saved for future use

5. **Verify Setup**
   
   You should see MCP servers connected in the status bar. Try a command like:
   ```
   Start task https://your-company.atlassian.net/browse/PROJ-123
   ```

## 📁 Repository Structure

```
.
├── .cursor/
│   └── mcp.json          # MCP server configurations
├── .cursorrules          # Cursor IDE workflow rules
├── .gitignore           # Git ignore rules
├── AGENTS.md            # AI agent configuration and behaviors
├── README.md            # This file
├── SETUP.md             # Detailed setup instructions
└── WORKFLOW.md          # Workflow usage guide
```

## 🔧 Configuration Details

### Integration Configuration

The workflow uses different configuration methods for each service:

1. **Jira MCP** - Configured via `.cursor/mcp.json` with browser-based OAuth authentication
   - Fetches tickets, updates status, creates issues
   - First use opens browser for authentication
   - No API tokens or environment variables needed
   
2. **Notion MCP** - Configured via `.cursor/mcp.json` with browser-based OAuth authentication
   - Reads and updates documentation pages
   - First use opens browser for authentication
   - No API tokens or environment variables needed

3. **GitHub** - Configured directly in Cursor IDE Settings (not via MCP)
   - Creates PRs, reviews code, manages branches
   - Access Cursor Settings → GitHub/Integrations section
   - Requires Personal Access Token

**Note**: Jira and Notion use browser-based OAuth authentication (no `.env` file needed), while GitHub requires a token in Cursor IDE Settings.

### Cursor Rules & Agents

- **`.cursorrules`**: Defines how the AI should respond to workflow commands
- **`AGENTS.md`**: Configures AI agent behaviors, capabilities, and workflows

You can customize both files to match your team's specific needs.

## 💡 Usage Examples

### Starting a New Task

```
Start task https://your-company.atlassian.net/browse/PROJ-123
```

The AI will:
- Fetch ticket details from Jira
- List relevant files
- Suggest implementation steps
- Create a feature branch

### Updating Documentation

```
Update documentation for the new authentication feature
```

The AI will:
- Find relevant Notion pages
- Update documentation with code changes
- Add examples and context

### Creating a Pull Request

```
Open PR for feature/PROJ-123-new-auth
```

The AI will:
- Review all changes
- Generate PR description
- Link to Jira ticket
- Add labels and reviewers
- Create the PR on GitHub

## 🎓 Best Practices

1. **Authenticate once** - Browser OAuth for Jira and Notion saves your credentials securely
2. **Customize `.cursorrules`** - Adapt the workflow rules to your team's needs
3. **Use descriptive branch names** - Follow the pattern: `feature/TICKET-NUMBER-short-description`
4. **Link everything** - Always link PRs to Jira tickets for traceability

## 🔒 Security Notes

- Jira and Notion use secure browser-based OAuth (no tokens stored locally)
- GitHub token is stored securely in Cursor IDE Settings
- API tokens should have minimal required permissions
- Rotate GitHub tokens regularly
- OAuth sessions can be revoked from your account settings

## 🤝 Contributing

This is a template repository. Feel free to:
- Fork it for your team
- Customize the workflow rules
- Add additional MCP servers
- Share improvements back to the community

## 📚 Resources

- [Cursor IDE Documentation](https://docs.cursor.sh/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [MCP Server Registry](https://github.com/modelcontextprotocol/servers)

## 📝 License

MIT License - feel free to use this template for your projects.

---

**Built with ❤️ for developers who want to focus on solving problems, not managing tools.**

