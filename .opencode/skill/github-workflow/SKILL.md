---
name: github-workflow
description: Use local GitHub MCP server for common GitHub workflows and automation
---

# GitHub Workflow Skill

Leverage the local GitHub MCP server (`@modelcontextprotocol/server-github`) for streamlined GitHub operations.

## Prerequisites

Ensure GitHub MCP is configured in `opencode.json`:

```json
{
  "mcp": {
    "Github": {
      "type": "local",
      "command": ["bun", "x", "@modelcontextprotocol/server-github"],
      "environment": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token"
      }
    }
  }
}
```

## Available MCP Tools

### Repository Operations

- `github_search_repositories` - Search GitHub repos
- `github_get_repository` - Get repo details
- `github_create_repository` - Create new repo
- `github_fork_repository` - Fork a repo

### Issue Management

- `github_list_issues` - List repo issues
- `github_create_issue` - Create new issue
- `github_update_issue` - Update existing issue
- `github_get_issue` - Get issue details
- `github_add_issue_comment` - Comment on issue

### Pull Request Operations

- `github_list_pull_requests` - List PRs
- `github_create_pull_request` - Create PR
- `github_get_pull_request` - Get PR details
- `github_update_pull_request` - Update PR
- `github_merge_pull_request` - Merge PR
- `github_get_pull_request_files` - List changed files

### Code Operations

- `github_search_code` - Search code across repos
- `github_get_file_contents` - Get file content
- `github_create_or_update_file` - Create/update file
- `github_push_files` - Push multiple files

## Common Workflows

### Workflow 1: Create Bug Report

```
1. github_create_issue
   - owner: repo owner
   - repo: repository name
   - title: "[Bug] Brief description"
   - body: Detailed bug report
   - labels: ["bug"]
```

### Workflow 2: Review and Merge PR

```
1. github_get_pull_request - Get PR details
2. github_get_pull_request_files - Review changes
3. github_create_pull_request_review - Submit review
4. github_merge_pull_request - Merge if approved
```

### Workflow 3: Quick Fix & PR

```
1. Edit files locally
2. git add & git commit
3. git push
4. github_create_pull_request
   - title: "Fix: Description"
   - body: Change summary
   - head: feature-branch
   - base: main
```

### Workflow 4: Find Issues to Contribute

```
1. github_search_repositories - Find interesting repos
2. github_list_issues - Filter by "good first issue" or "help wanted"
3. github_fork_repository - Fork the repo
4. git clone & work locally
```

## Best Practices

1. **Use descriptive titles** - Include type prefix like `[Bug]`, `[Feature]`, `[Docs]`
2. **Reference issues** - Use `Fixes #123` or `Closes #456` in PR descriptions
3. **Review before merge** - Always review PRs before merging
4. **Use labels** - Categorize issues with appropriate labels
5. **Protect main branch** - Require PR reviews before merging to main

## Environment Variables

The MCP server requires:

- `GITHUB_PERSONAL_ACCESS_TOKEN` - GitHub personal access token with appropriate scopes

Token scopes needed:

- `repo` - Full repository access
- `read:user` - Read user profile
- `read:org` - Read organization data

## Examples

**Find popular repos:**

```
Search for "machine learning" repos with most stars
→ github_search_repositories
  query: "machine learning language:python stars:>1000"
  sort: "stars"
```

**Create feature request:**

```
Create issue for new feature
→ github_create_issue
  owner: "anomalyco"
  repo: "opencode"
  title: "[Feature] Add dark mode toggle"
  body: "## Description\nAdd a toggle for dark mode..."
  labels: ["enhancement"]
```

**Review pending PR:**

```
Review PR #42
→ github_get_pull_request
  owner: "anomalyco"
  repo: "opencode"
  pull_number: 42
→ github_get_pull_request_files (same params)
→ github_create_pull_request_review
  event: "APPROVE"
  body: "LGTM! Great work."
```
