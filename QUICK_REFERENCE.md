# Quick Reference Card

## Common Commands

### Starting Work
```
Start task [Jira link]
```
Fetches ticket, prepares workspace, suggests implementation.

### Documentation
```
Update documentation
```
Syncs code changes with Notion automatically.

### Pull Requests
```
Open PR
```
Creates GitHub PR with description, links, and reviewers.

### Code Review
```
Review PR #42
```
Analyzes code changes and suggests improvements.

## Authentication Methods

| Service | Authentication Method | Configuration |
|---------|----------------------|---------------|
| **Jira** | Browser OAuth | MCP (automatic on first use) |
| **GitHub** | Personal Access Token | Cursor IDE Settings |
| **Notion** | Browser OAuth | MCP (automatic on first use) |

**Note**: Jira and Notion use browser-based OAuth (no tokens needed). GitHub requires a token configured in Cursor IDE Settings.

## File Locations

- **MCP Config**: `.cursor/mcp.json`
- **Workflow Rules**: `.cursorrules`
- **Agent Config**: `AGENTS.md`
- **Setup Guide**: `SETUP.md`
- **Workflow Guide**: `WORKFLOW.md`

## Troubleshooting

**MCP servers not connecting?**
- Try using a Jira or Notion command to trigger browser authentication
- Ensure browser allows pop-ups for OAuth
- Restart Cursor IDE
- Verify Node.js is installed

**Commands not working?**
- Ensure you're in the workspace directory
- Check `.cursorrules` file exists
- For GitHub: Check Cursor IDE Settings for token
- For Jira/Notion: Use a command to trigger browser authentication if not connected

## Tips

- Be specific: "Start task PROJ-123" not "start work"
- Provide context: Include links to tickets or PRs
- Review AI suggestions before merging
- Customize `.cursorrules` for your team

