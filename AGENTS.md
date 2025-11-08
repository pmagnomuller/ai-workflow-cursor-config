# AI Agent Configuration

This file defines how AI agents should behave when working in this repository. Agents use MCPs (Model Context Protocols) to interact with Jira, GitHub, and Notion, creating a seamless workflow without context-switching.

## Agent Capabilities

Agents in this workflow have access to:

- **Jira MCP**: Fetch tickets, update status, create issues (browser OAuth, configured via `.cursor/mcp.json`)
- **GitHub**: Create PRs, review code, manage branches (configured in Cursor IDE Settings)
- **Notion MCP**: Read and update documentation pages (browser OAuth, configured via `.cursor/mcp.json`)
- **Codebase**: Full access to project files and structure

**Note**: Jira and Notion use browser-based OAuth authentication (no tokens needed), while GitHub requires a token in Cursor IDE Settings.

## Agent Workflows

### Task Initiation Agent

**Trigger**: "Start task [Jira link]"

**Behavior**:
1. Use Jira MCP to fetch ticket details (title, description, acceptance criteria, labels, assignee)
2. Analyze the codebase to identify relevant files and patterns
3. Create a feature branch following the pattern: `feature/TICKET-NUMBER-short-description`
4. Generate an implementation plan based on:
   - Ticket requirements
   - Existing code patterns
   - Related files and dependencies
5. Present a structured summary with:
   - Key ticket information
   - Relevant files to modify
   - Suggested implementation steps
   - Potential challenges or considerations

**Example Output**:
```
✓ Fetched Jira ticket PROJ-123: "Add user authentication"
✓ Created branch: feature/PROJ-123-user-authentication

Implementation Plan:
1. Create authentication service (src/auth/service.ts)
2. Add login endpoint (src/api/auth.ts)
3. Implement JWT token generation
4. Add unit tests (tests/auth.test.ts)
5. Update API documentation

Relevant files:
- src/auth/types.ts (existing)
- src/middleware/auth.ts (needs update)
```

### Documentation Agent

**Trigger**: "Update documentation" or "Sync docs"

**Behavior**:
1. Identify code changes in the current branch
2. Use Notion MCP to find relevant documentation pages
3. Analyze what documentation needs updating:
   - New features → Add new sections
   - API changes → Update endpoint docs
   - Configuration changes → Update setup guides
   - Breaking changes → Add migration notes
4. Update documentation with:
   - Code examples from actual implementation
   - Clear explanations of changes
   - Before/after comparisons if applicable
   - Links to related documentation
5. Verify documentation accuracy and completeness

**Example Output**:
```
✓ Analyzed code changes in feature/PROJ-123-user-authentication
✓ Found documentation page: "Authentication Guide"
✓ Updated sections:
  - Added "JWT Authentication" section
  - Updated "API Endpoints" with new login endpoint
  - Added code examples for token refresh
  - Updated "Security Best Practices"

Documentation synced to Notion.
```

### Pull Request Agent

**Trigger**: "Open PR" or "Create PR"

**Behavior**:
1. Review all changes in the current branch:
   - Files modified/added/deleted
   - Code quality and patterns
   - Test coverage
   - Documentation updates
2. Use GitHub (via Cursor's built-in integration) to fetch repository information
3. Generate comprehensive PR description:
   - **Summary**: Clear overview of changes
   - **Changes**: Detailed list of modifications
   - **Related Ticket**: Link to Jira ticket
   - **Testing**: Test coverage and manual testing notes
   - **Screenshots**: If UI changes are present
   - **Breaking Changes**: If any
   - **Migration Guide**: If needed
4. Use GitHub (via Cursor's built-in integration) to create the PR with:
   - Descriptive title: `[PROJ-123] Short description`
   - Generated description
   - Appropriate labels (from Jira ticket or codebase)
   - Suggested reviewers (based on file changes or team conventions)
5. Link PR to Jira ticket (if Jira MCP supports it)

**Example PR Description**:
```markdown
## Summary
Implements user authentication system with JWT tokens and refresh token support.

## Changes
- Added `AuthService` class with login/logout methods
- Created `/api/auth/login` and `/api/auth/refresh` endpoints
- Implemented JWT token generation and validation middleware
- Added refresh token rotation mechanism
- Created comprehensive unit tests (coverage: 87%)
- Updated API documentation in Notion

## Related Ticket
[Jira PROJ-123](https://your-company.atlassian.net/browse/PROJ-123)

## Testing
- [x] Unit tests passing (87% coverage)
- [x] Integration tests passing
- [x] Manual testing completed
- [x] Security review passed

## Breaking Changes
None

## Migration Guide
N/A - New feature

## Screenshots
[If applicable]

## Reviewers
@team-lead @security-reviewer
```

### Code Review Agent

**Trigger**: "Review PR #42" or "Analyze changes"

**Behavior**:
1. Use GitHub (via Cursor's built-in integration) to fetch PR details:
   - Files changed
   - Diff content
   - Comments and discussions
   - CI/CD status
2. Analyze code changes for:
   - **Code Quality**: Readability, maintainability, patterns
   - **Security**: Potential vulnerabilities, best practices
   - **Performance**: Optimization opportunities
   - **Testing**: Coverage, edge cases, test quality
   - **Documentation**: Code comments, API docs
3. Cross-reference with:
   - Related Jira ticket (requirements)
   - Notion documentation (consistency)
   - Codebase patterns (consistency)
4. Generate review summary:
   - Overall assessment
   - Strengths
   - Issues and suggestions
   - Action items
5. Provide specific, actionable feedback

**Example Output**:
```
PR #42 Review Summary

Overall: ✅ Good implementation with minor improvements needed

Strengths:
- Clean code structure following project patterns
- Comprehensive test coverage (87%)
- Good error handling
- Documentation updated

Issues Found:
1. ⚠️ Missing rate limiting on new endpoints
   - Location: src/api/auth.ts:45
   - Suggestion: Add rate limiting middleware

2. ⚠️ Error messages could be more specific
   - Location: src/auth/service.ts:123
   - Suggestion: Use specific error types instead of generic messages

3. ⚠️ Missing input validation
   - Location: src/api/auth.ts:67
   - Suggestion: Add validation for email format and password strength

4. ℹ️ Test coverage missing for edge cases
   - Location: tests/auth.test.ts
   - Suggestion: Add tests for token expiration, invalid tokens

Action Items:
- [ ] Add rate limiting
- [ ] Improve error messages
- [ ] Add input validation
- [ ] Expand test coverage
```

## Agent Communication Patterns

### Proactive Suggestions
Agents should proactively suggest:
- Related files that might need updates
- Potential issues before they become problems
- Documentation that might be outdated
- Test cases that might be missing

### Context Awareness
Agents should maintain awareness of:
- Current branch and changes
- Related Jira tickets
- Recent PRs and discussions
- Team conventions and patterns
- Project architecture and structure

### Error Handling
When agents encounter errors:
1. Provide clear, actionable error messages
2. Suggest solutions or workarounds
3. Log errors for debugging
4. Continue with partial results when possible
5. Ask for clarification when needed

## Agent Best Practices

### For Developers

1. **Be Specific**: Provide clear context and requirements
2. **Use Links**: Include Jira ticket links, PR numbers, etc.
3. **Iterate**: Start broad, then refine with follow-up questions
4. **Review**: Always review agent suggestions before implementing
5. **Customize**: Adjust agent behavior via `.cursorrules` for team needs

### For Agents

1. **Verify**: Always verify information from MCPs before using
2. **Explain**: Provide reasoning for suggestions and decisions
3. **Link**: Connect related information (tickets, PRs, docs)
4. **Learn**: Adapt to codebase patterns and team conventions
5. **Communicate**: Keep developers informed of actions taken

## Multi-Agent Coordination

When multiple agents work together:

1. **Task Agent** → **Documentation Agent**: After implementation, automatically suggest doc updates
2. **PR Agent** → **Review Agent**: After PR creation, automatically trigger review
3. **Review Agent** → **Task Agent**: After review, suggest follow-up tasks

## Customization

To customize agent behavior for your team:

1. Edit `.cursorrules` for workflow-specific rules
2. Modify this `AGENTS.md` for agent-specific instructions
3. Update `.cursor/mcp.json` to add/remove MCP servers
4. Create team-specific agent profiles if needed

## Agent Limitations

Agents are powerful but have limitations:

- **Cannot commit code** without explicit approval
- **Cannot merge PRs** without human review
- **Cannot access** systems not configured (MCP for Jira/Notion, Cursor Settings for GitHub)
- **May make mistakes** - always review agent suggestions
- **Require valid credentials** - ensure API tokens are current

## Troubleshooting Agents

**Agent not responding?**
- Check MCP server connections in Cursor status bar (for Jira and Notion)
- For Jira/Notion: Try using a command to trigger browser authentication if not connected
- For GitHub: Verify token is configured in Cursor IDE Settings
- Restart Cursor IDE

**Agent making incorrect suggestions?**
- Review and update `.cursorrules` and `AGENTS.md`
- Provide more context in your requests
- Check that MCPs are returning correct data

**Agent not using integrations?**
- **For Jira/Notion (MCP)**: Use a command to trigger browser authentication, check `.cursor/mcp.json` configuration
- **For GitHub**: Verify token is configured in Cursor IDE Settings → GitHub/Integrations
- Test connections individually (Jira/Notion via browser OAuth, GitHub via Cursor Settings)

## Next Steps

1. Customize agent behaviors in this file for your team
2. Add team-specific workflows and patterns
3. Create agent profiles for different project types
4. Share improvements with the community

---

**Remember**: Agents are here to assist, not replace, human judgment. Always review agent suggestions and maintain control of your workflow.

