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
- API access to:
  - Jira (API token)
  - GitHub (Personal Access Token)
  - Notion (Integration API key)

### Setup Steps

For detailed setup instructions, see [SETUP.md](./SETUP.md).

**Quick Setup:**

1. **Clone this repository**
   ```bash
   git clone <this-repo-url>
   cd ai-workflow-cursor-config
   ```

2. **Configure environment variables**
   ```bash
   cp env.example .env
   ```
   
   Edit `.env` and add your API credentials (see [SETUP.md](./SETUP.md) for detailed instructions):
   - **Jira**: API token from [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens)
   - **GitHub**: Personal Access Token with `repo` scope from [GitHub Settings](https://github.com/settings/tokens)
   - **Notion**: Integration API key from [Notion Integrations](https://www.notion.so/my-integrations)

3. **Open in Cursor IDE**
   
   The MCP configuration is already set up in `.cursor/mcp.json`. Cursor will automatically load this configuration when you open the workspace.

4. **Verify Setup**
   
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
├── env.example          # Template for environment variables
├── README.md            # This file
├── SETUP.md             # Detailed setup instructions
└── WORKFLOW.md          # Workflow usage guide
```

## 🔧 Configuration Details

### MCP Servers

The workflow uses three MCP servers:

1. **Jira MCP** - Fetches tickets, updates status, creates issues
2. **GitHub MCP** - Creates PRs, reviews code, manages branches
3. **Notion MCP** - Reads and updates documentation pages

All servers are configured in `.cursor/mcp.json` and use environment variables from your `.env` file.

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

1. **Keep your `.env` file secure** - Never commit it to version control
2. **Customize `.cursorrules`** - Adapt the workflow rules to your team's needs
3. **Use descriptive branch names** - Follow the pattern: `feature/TICKET-NUMBER-short-description`
4. **Link everything** - Always link PRs to Jira tickets for traceability

## 🔒 Security Notes

- The `.env` file is gitignored by default
- API tokens should have minimal required permissions
- Rotate tokens regularly
- Use separate tokens for different environments

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

