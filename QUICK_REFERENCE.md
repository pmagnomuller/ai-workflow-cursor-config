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

## API Credentials Needed

| Service | Where to Get | Required Scopes |
|---------|-------------|----------------|
| **Jira** | [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens) | API Token |
| **GitHub** | [GitHub Settings > Tokens](https://github.com/settings/tokens) | `repo` scope |
| **Notion** | [Notion Integrations](https://www.notion.so/my-integrations) | Read/Update content |

## File Locations

- **MCP Config**: `.cursor/mcp.json`
- **Workflow Rules**: `.cursorrules`
- **Agent Config**: `AGENTS.md`
- **Environment**: `.env` (create from `env.example`)
- **Setup Guide**: `SETUP.md`
- **Workflow Guide**: `WORKFLOW.md`

## Troubleshooting

**MCP servers not connecting?**
- Check `.env` file exists and has valid credentials
- Restart Cursor IDE
- Verify Node.js is installed

**Commands not working?**
- Ensure you're in the workspace directory
- Check `.cursorrules` file exists
- Verify API tokens have correct permissions

## Tips

- Be specific: "Start task PROJ-123" not "start work"
- Provide context: Include links to tickets or PRs
- Review AI suggestions before merging
- Customize `.cursorrules` for your team

