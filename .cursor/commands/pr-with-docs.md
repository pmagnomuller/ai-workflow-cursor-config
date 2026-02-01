Create a production-ready pull request with documentation in sync. Follow the **pr-with-docs** skill workflow:

1. **Analyze** all modified, added, and deleted files in the current branch and identify what requires AGENTS.md (or .cursor/rules) updates.
2. **Update docs**: Edit AGENTS.md and relevant `.cursor/rules/*.mdc` to match the code changes; preserve structure and tone.
3. **Git**: Ensure a feature branch (create one if on main/master), stash uncommitted changes if needed, commit docs first then code (conventional commits), push.
4. **PR**: Create the pull request with `gh pr create` (or host CLI), with a full description: Summary, Changes Made, Documentation Updates, Testing, Breaking Changes, Related Issues.

Use conventional commits for branch names and commit messages (`feature/`, `fix/`, `docs/`, etc.). Restore stash after finishing. If anything fails, report clearly and leave a clean state. Give a short status at each phase and the PR URL at the end.
