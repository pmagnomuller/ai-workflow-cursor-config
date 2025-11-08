# AI Workflow Guide

This document provides detailed examples and explanations of how to use the AI-assisted development workflow.

## Workflow Overview

The workflow eliminates context-switching by integrating Jira, GitHub, and Notion directly into Cursor IDE through MCPs (Model Context Protocols).

## Common Workflows

### 1. Starting a New Task

**Command:**
```
Start task https://your-company.atlassian.net/browse/PROJ-123
```

**What happens:**
1. AI fetches ticket details from Jira (title, description, acceptance criteria)
2. Analyzes the codebase to find relevant files
3. Suggests implementation approach
4. Creates a feature branch: `feature/PROJ-123-short-description`
5. Sets up initial commit structure

**Example AI Response:**
```
✓ Fetched Jira ticket PROJ-123: "Add user authentication"
✓ Found relevant files:
  - src/auth/login.ts
  - src/auth/types.ts
  - tests/auth.test.ts

Suggested implementation:
1. Create authentication service
2. Add login endpoint
3. Write unit tests
4. Update API documentation

Branch created: feature/PROJ-123-user-authentication
```

### 2. Updating Documentation

**Command:**
```
Update documentation for the authentication changes
```

**What happens:**
1. AI identifies what changed in the code
2. Finds relevant Notion pages using MCP
3. Updates documentation with:
   - Code examples
   - API changes
   - Configuration notes
   - Migration guides (if needed)

**Example AI Response:**
```
✓ Found documentation page: "Authentication Guide"
✓ Updated sections:
  - Added new login endpoint documentation
  - Updated authentication flow diagram
  - Added code examples for token refresh

Documentation synced to Notion.
```

### 3. Creating a Pull Request

**Command:**
```
Open PR for feature/PROJ-123-user-authentication
```

**What happens:**
1. AI reviews all changes in the branch
2. Generates comprehensive PR description:
   - Summary of changes
   - Related Jira ticket link
   - Testing notes
   - Screenshots (if applicable)
3. Creates PR on GitHub via MCP
4. Adds labels and assigns reviewers
5. Links PR to Jira ticket

**Example PR Description:**
```markdown
## Summary
Implements user authentication system with JWT tokens and refresh token support.

## Changes
- Added authentication service with login/logout
- Created JWT token generation and validation
- Implemented refresh token mechanism
- Added unit tests (coverage: 85%)

## Related Ticket
[Jira PROJ-123](https://your-company.atlassian.net/browse/PROJ-123)

## Testing
- [x] Unit tests passing
- [x] Integration tests passing
- [x] Manual testing completed

## Screenshots
[Login flow diagram]

## Reviewers
@team-lead @security-reviewer
```

### 4. PR Review Assistance

**Command:**
```
Review PR #42 and suggest improvements
```

**What happens:**
1. AI fetches PR details from GitHub
2. Analyzes code changes
3. Summarizes changes in plain language
4. Suggests improvements:
   - Code quality issues
   - Performance optimizations
   - Security concerns
   - Best practices

**Example AI Response:**
```
PR #42 Summary:
- Added 3 new endpoints for user management
- Updated authentication middleware
- Added 5 new test cases

Suggestions:
1. Consider adding rate limiting to new endpoints
2. Error handling could be more specific
3. Missing input validation on user creation endpoint
4. Tests cover happy path but missing edge cases
```

## Advanced Workflows

### Multi-Ticket Workflow

```
Start tasks:
- https://your-company.atlassian.net/browse/PROJ-123
- https://your-company.atlassian.net/browse/PROJ-124
```

The AI can handle multiple related tickets and create a unified implementation plan.

### Documentation-First Workflow

```
Create documentation for the new payment feature, then implement it
```

The AI will:
1. Create documentation structure in Notion
2. Define the API contract
3. Generate implementation plan
4. Create feature branch
5. Implement following the documented spec

### Code Review Workflow

```
Review all open PRs and create a summary for the team
```

The AI will:
1. Fetch all open PRs from GitHub
2. Analyze each one
3. Create a summary document
4. Post to team channel or Notion

## Tips for Best Results

1. **Be Specific**: Instead of "fix bug", say "fix authentication bug in PROJ-123"
2. **Provide Context**: Include links to tickets, PRs, or documentation
3. **Iterate**: Start with high-level commands, then refine with follow-ups
4. **Review AI Suggestions**: Always review AI-generated code and PRs before merging
5. **Customize Rules**: Adjust `.cursorrules` to match your team's conventions

## Troubleshooting

### MCP Servers Not Connecting

1. Check that `.env` file exists and has valid credentials
2. Verify MCP servers are installed: `npm list -g | grep mcp`
3. Restart Cursor IDE
4. Check Cursor's MCP status in the status bar

### Commands Not Working

1. Ensure you're in a workspace with `.cursor/mcp.json`
2. Check `.cursorrules` file exists
3. Verify API tokens have correct permissions
4. Check Cursor IDE logs for errors

### Documentation Not Updating

1. Verify Notion integration has access to the pages
2. Check Notion API key is valid
3. Ensure page IDs are correct in Notion MCP config

## Next Steps

- Customize `.cursorrules` for your team's workflow
- Add additional MCP servers (Slack, Linear, etc.)
- Create team-specific workflow shortcuts
- Share improvements with the community

