# Detailed Setup Instructions

This guide walks you through setting up the AI-powered development workflow step by step.

## Step 1: Install Cursor IDE

1. Download Cursor IDE from [cursor.sh](https://cursor.sh/)
2. Install and open Cursor IDE
3. Sign in or create an account

## Step 2: Configure Integrations

### Jira & Notion (MCP with Browser Authentication)

**Note**: Jira and Notion use browser-based OAuth authentication. No API tokens or environment variables needed!

1. **Open in Cursor IDE**
   - File → Open Folder → Select this repository folder
   - Cursor will automatically detect the `.cursor/mcp.json` configuration

2. **Authenticate via Browser**
   - When you first use Jira or Notion commands, Cursor will open your browser
   - Sign in to your Jira/Atlassian account
   - Sign in to your Notion account
   - Authorize the MCP connection
   - The browser will redirect back to Cursor automatically

3. **Verify MCP connections**
   - Check the status bar for MCP server connections
   - You should see "notion" and "atlassian" servers connected
   - If authentication fails, try the command again to re-authenticate

### GitHub Configuration

**Note**: GitHub is configured directly in Cursor IDE settings, not via MCP like Jira and Notion.

1. Go to [GitHub Settings > Developer settings > Personal access tokens > Tokens (classic)](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Give it a descriptive name (e.g., "Cursor IDE")
4. Select scopes:
   - `repo` (full control of private repositories)
   - `read:org` (optional, for organization access)
5. Click "Generate token"
6. Copy the token immediately (you won't see it again!)
7. **Configure in Cursor IDE**:
   - Open Cursor IDE Settings (Cmd/Ctrl + ,)
   - Go to "GitHub" or "Integrations" section
   - Paste your Personal Access Token
   - Save settings

## Step 3: Clone and Open Repository

1. **Clone or download this repository**
   ```bash
   git clone <this-repo-url>
   cd ai-workflow-cursor-config
   ```

2. **Open in Cursor IDE**
   - File → Open Folder → Select this repository folder
   - Cursor will automatically detect the `.cursor/mcp.json` configuration

## Step 5: Authenticate MCP Servers (Jira & Notion)

When you first use Jira or Notion commands, Cursor will prompt you to authenticate via browser:

1. **For Jira/Atlassian**:
   - Try a command like: `Fetch Jira ticket PROJ-123`
   - Your browser will open for OAuth authentication
   - Sign in to your Atlassian account
   - Authorize the connection
   - Browser will redirect back to Cursor

2. **For Notion**:
   - Try a command like: `List Notion pages in my workspace`
   - Your browser will open for OAuth authentication
   - Sign in to your Notion account
   - Authorize the connection
   - Browser will redirect back to Cursor

3. **Verify connections**:
   - Check the status bar for MCP server connections
   - You should see "notion" and "atlassian" servers connected
   - Authentication is saved, so you won't need to re-authenticate unless you revoke access

## Step 6: Verify Setup

Test each integration:

### Test Jira Connection (MCP with Browser Auth)
In Cursor's chat, try:
```
Fetch Jira ticket PROJ-123
```
(Replace PROJ-123 with an actual ticket from your Jira)
- First time will open browser for authentication
- Subsequent uses will work automatically

### Test Notion Connection (MCP with Browser Auth)
```
List Notion pages in my workspace
```
- First time will open browser for authentication
- Subsequent uses will work automatically

### Test GitHub Connection (Cursor Settings)
GitHub is accessed through Cursor's built-in integration:
```
List open pull requests in this repository
```

**Note**: If GitHub commands don't work, verify your GitHub token is configured in Cursor IDE Settings.

## Troubleshooting

### MCP Servers Not Connecting

**Problem**: MCP servers show as disconnected in Cursor

**Solutions**:
1. Try using a Jira or Notion command to trigger browser authentication
2. Ensure your browser allows pop-ups/redirects for authentication
3. Check that you're signed in to the correct accounts (Jira/Atlassian and Notion)
4. Restart Cursor IDE
5. Check Cursor's output panel for MCP errors
6. Verify Node.js is installed: `node --version`

### "Command not found" Errors

**Problem**: MCP servers can't be found

**Solutions**:
1. Ensure Node.js is installed: `node --version`
2. The Atlassian MCP uses `npx` which will auto-install when first used
3. Notion MCP uses a remote server, so no local installation needed
4. Restart Cursor IDE after ensuring Node.js is available

### Authentication Errors

**Problem**: Getting 401/403 errors from APIs

**Solutions**:
1. **Jira/Atlassian**: 
   - Re-authenticate by using a Jira command (will open browser)
   - Ensure you're signed in to the correct Atlassian account
   - Check that you authorized the MCP connection
   - Try revoking and re-authorizing if issues persist
2. **GitHub**:
   - Verify token is configured in Cursor IDE Settings
   - Verify token has correct scopes (`repo` is required)
   - Check token hasn't been revoked
   - Ensure token is for the correct account
   - Restart Cursor IDE after updating GitHub settings
3. **Notion**:
   - Re-authenticate by using a Notion command (will open browser)
   - Ensure you're signed in to the correct Notion account
   - Check that you authorized the MCP connection
   - Ensure pages are accessible to your account

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

