# Detailed Setup Instructions

This guide walks you through setting up the AI-powered development workflow step by step.

## Step 1: Install Cursor IDE

1. Download Cursor IDE from [cursor.sh](https://cursor.sh/)
2. Install and open Cursor IDE
3. Sign in or create an account

## Step 2: Get API Credentials

### Jira API Token

1. Go to [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens)
2. Click "Create API token"
3. Give it a label (e.g., "Cursor IDE Workflow")
4. Copy the token (you won't see it again!)
5. Note your Jira URL (e.g., `https://your-company.atlassian.net`)
6. Note your email address used for Jira

### GitHub Personal Access Token

1. Go to [GitHub Settings > Developer settings > Personal access tokens > Tokens (classic)](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Give it a descriptive name (e.g., "Cursor IDE MCP")
4. Select scopes:
   - `repo` (full control of private repositories)
   - `read:org` (optional, for organization access)
5. Click "Generate token"
6. Copy the token immediately (you won't see it again!)

### Notion API Key

1. Go to [Notion Integrations](https://www.notion.so/my-integrations)
2. Click "New integration"
3. Give it a name (e.g., "Cursor IDE Workflow")
4. Select your workspace
5. Set capabilities:
   - Read content
   - Update content
   - Insert content
6. Click "Submit"
7. Copy the "Internal Integration Token" (starts with `secret_`)
8. **Important**: Share your Notion pages with this integration:
   - Open each page you want to update
   - Click "..." menu → "Add connections"
   - Select your integration

## Step 3: Configure the Template

1. **Clone or download this repository**
   ```bash
   git clone <this-repo-url>
   cd ai-workflow-cursor-config
   ```

2. **Create your `.env` file**
   ```bash
   cp env.example .env
   ```

3. **Edit `.env` with your credentials**
   ```bash
   # Open in your editor
   nano .env
   # or
   code .env
   ```
   
   Fill in your values:
   ```env
   JIRA_URL=https://your-company.atlassian.net
   JIRA_EMAIL=your.email@company.com
   JIRA_API_TOKEN=ATATT3xFfGF0...
   
   GITHUB_PERSONAL_ACCESS_TOKEN=ghp_xxxxxxxxxxxxx
   
   NOTION_API_KEY=secret_xxxxxxxxxxxxx
   ```

4. **Install MCP servers** (optional, but recommended)
   
   The MCP servers will be installed automatically when Cursor first uses them, but you can pre-install them:
   ```bash
   npm install -g @modelcontextprotocol/server-jira
   npm install -g @modelcontextprotocol/server-github
   npm install -g @modelcontextprotocol/server-notion
   ```

## Step 4: Open in Cursor IDE

1. Open Cursor IDE
2. File → Open Folder → Select this repository folder
3. Cursor will automatically detect the `.cursor/mcp.json` configuration
4. Check the status bar for MCP server connections

## Step 5: Verify Setup

Test each integration:

### Test Jira Connection
In Cursor's chat, try:
```
Fetch Jira ticket PROJ-123
```
(Replace PROJ-123 with an actual ticket from your Jira)

### Test GitHub Connection
```
List open pull requests in this repository
```

### Test Notion Connection
```
List Notion pages in my workspace
```

## Troubleshooting

### MCP Servers Not Connecting

**Problem**: MCP servers show as disconnected in Cursor

**Solutions**:
1. Check `.env` file exists and has correct values
2. Verify no typos in environment variable names
3. Restart Cursor IDE
4. Check Cursor's output panel for MCP errors
5. Verify Node.js is installed: `node --version`

### "Command not found" Errors

**Problem**: MCP servers can't be found

**Solutions**:
1. Install MCP servers globally:
   ```bash
   npm install -g @modelcontextprotocol/server-jira
   npm install -g @modelcontextprotocol/server-github
   npm install -g @modelcontextprotocol/server-notion
   ```
2. Or use npx (already configured in `mcp.json`)

### Authentication Errors

**Problem**: Getting 401/403 errors from APIs

**Solutions**:
1. **Jira**: 
   - Verify API token is correct
   - Check email matches your Jira account
   - Ensure token hasn't expired
2. **GitHub**:
   - Verify token has correct scopes (`repo` is required)
   - Check token hasn't been revoked
   - Ensure token is for the correct account
3. **Notion**:
   - Verify integration token is correct
   - Ensure pages are shared with the integration
   - Check integration capabilities match your needs

### Environment Variables Not Loading

**Problem**: MCP servers can't read environment variables

**Solutions**:
1. Ensure `.env` file is in the repository root
2. Verify `.env` file format (no spaces around `=`)
3. Check file permissions
4. Restart Cursor IDE after creating `.env`

## Next Steps

Once setup is complete:

1. Read [WORKFLOW.md](./WORKFLOW.md) for usage examples
2. Customize [.cursorrules](./.cursorrules) for your team
3. Try your first workflow command:
   ```
   Start task https://your-company.atlassian.net/browse/PROJ-123
   ```

## Security Best Practices

1. **Never commit `.env`** - It's already in `.gitignore`
2. **Rotate tokens regularly** - Set reminders to update tokens every 90 days
3. **Use minimal permissions** - Only grant necessary scopes
4. **Separate environments** - Use different tokens for dev/staging/prod
5. **Team sharing** - Share `.env.example`, not `.env`

## Getting Help

- Check [Cursor IDE Documentation](https://docs.cursor.sh/)
- Review [MCP Documentation](https://modelcontextprotocol.io/)
- Open an issue in this repository
- Check Cursor's MCP status in the status bar

