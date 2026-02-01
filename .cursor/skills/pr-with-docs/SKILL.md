---
name: pr-with-docs
description: Creates production-ready pull requests with automatically updated AGENTS.md and project docs. Use when the user asks to create a PR, make a PR, is ready to merge, has finished a feature and wants a PR, or says they're done for the day with changes to commit.
---

# PR with Docs

When the user asks to create a pull request (e.g. "make a PR with these changes", "create a PR for this", "ready to merge", "that's all for today, I added X"), follow this workflow to analyze changes, update AGENTS.md (and .cursor/rules if relevant), run the Git workflow, and create the PR.

## 1. Change Analysis

- Examine all modified, added, and deleted files in the current branch.
- Identify scope: features, bug fixes, refactors.
- Detect changes that require **AGENTS.md** updates:
  - New API endpoints or routes (`apps/api/app/routes/`, `apps/web/src/app/api/`)
  - Database schema or migrations (`apps/api/migrations/`)
  - New environment variables or config (`apps/api/app/core/config.py`, etc.)
  - Architecture or tech stack changes
  - New development commands or workflows
  - Auth flow changes
  - New third-party integrations or dependencies
  - New component or styling patterns

## 2. AGENTS.md and Rules Updates

- Read `AGENTS.md` (and relevant `.cursor/rules/*.mdc`) thoroughly.
- Update sections based on code changes; preserve structure and tone.
- Add new sections only for entirely new concepts.
- Ensure code examples match current patterns; keep terminology and style consistent.
- Do not remove information unless it is obsolete.
- If changes affect only API or only web, consider updating `.cursor/rules/python-api.mdc` or `.cursor/rules/nextjs-web.mdc` as appropriate.

## 3. Git Workflow

**Branch**

- Check branch: `git branch --show-current`.
- If on `main`/`master`, create a feature branch: `<type>/<brief-description>` (e.g. `feature/add-instagram-scraping`, `fix/auth-redirect-loop`, `docs/update-schema-info`). Types: `feature`, `fix`, `docs`, `refactor`, `chore`.
- If already on a feature branch, use it.

**Stash**

- Check uncommitted changes: `git status`.
- If there are uncommitted changes: `git stash push -m "Auto-stash before PR creation"`.
- Restore stash after operations if one was created.

**Commit**

- Stage docs first: `git add AGENTS.md` (and any `.cursor/rules/*.mdc` if changed).
- Commit docs: `git commit -m "docs: update AGENTS.md with [specific changes]"`.
- Stage rest: `git add .`
- Commit code with conventional commits: `<type>(<scope>): <description>` (e.g. `feat(auth): add Google OAuth support`).

**Publish**

- Push: `git push -u origin <branch-name>`.
- Handle push conflicts or errors.

## 4. Pull Request

- Use GitHub CLI: `gh pr create` (or host-appropriate CLI).
- PR description should include:
  - **Summary**: 2–3 sentence overview.
  - **Changes Made**: Bulleted list.
  - **Documentation Updates**: AGENTS.md (and rules) sections updated.
  - **Testing**: How changes were tested (if applicable).
  - **Breaking Changes**: Any breaking changes or migration steps.
  - **Related Issues**: Links if mentioned.
- Title in conventional commits style; add labels (feature, bugfix, documentation, etc.) if possible.

## When to Update AGENTS.md

| Change | Update |
|--------|--------|
| New files in `apps/api/` (routes, models, services) | Repo Layout, Conventions, Key Files |
| New files in `apps/api/migrations/` | Repo Layout, Database/Migrations |
| New env vars in code | Conventions / README env section |
| New packages | Repo Layout / Tech stack |
| New dev commands | Where to Run Commands |
| Auth logic changes | Conventions, Auth |
| New component/API patterns | Conventions, Key Files |
| New third-party integrations | Conventions or new subsection |

## When NOT to Update AGENTS.md

- Minor bug fixes that do not change architecture.
- Internal refactors that do not affect usage patterns.
- Styling tweaks following existing patterns.
- Test file additions (unless they introduce new testing patterns).

## Quality Before PR

1. AGENTS.md is valid Markdown with no syntax errors.
2. Code examples in AGENTS.md use correct syntax.
3. All Git operations completed successfully.
4. Commits follow conventional commits format.
5. PR description is accurate and complete.

## Error Handling

- If Git fails: clear error message and suggested fix.
- If AGENTS.md updates are unclear: ask the user.
- If PR creation fails: give the user the PR description for manual creation.
- Always clean up: restore stash, return to original branch if needed.

## Communication

- Give a short status at each phase.
- Say which AGENTS.md (and rules) sections you are updating and why.
- Show commit messages before committing and PR description before creating.
- Ask for confirmation if changes are ambiguous or potentially breaking.
- Proactively mention related docs that could be updated.

## Output Phases

1. **Analysis**: "Analyzing changes in current branch..."
2. **Documentation**: "Updating AGENTS.md sections: [list]..."
3. **Git**: "Creating branch / committing changes..."
4. **PR**: "Creating pull request..."
5. **Summary**: PR URL and brief summary of actions.

Goal: merge-ready PRs with documentation in sync with the codebase.
