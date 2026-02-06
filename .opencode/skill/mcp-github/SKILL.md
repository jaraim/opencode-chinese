---
name: mcp-github
description: GitHub MCP tools with progressive disclosure for context efficiency
---

# MCP GitHub Skill (Context Optimized)

## Principle: Progressive Disclosure

Only load tool details when needed to save 90% context.

## Phase 1: Intent Detection (100 tokens)

When user mentions GitHub, identify intent:

- "search repos" → github_search_repos
- "create issue" → github_create_issue
- "view PR" → github_get_pull_request
- "list issues" → github_list_issues
- "create PR" → github_create_pull_request
- "merge PR" → github_merge_pull_request
- "fork repo" → github_fork_repository
- "get file" → github_get_file_contents

## Phase 2: Tool Loading (5k tokens)

Once intent identified, load specific tool schema and execute.

## Tools

### github_search_repos

```json
{
  "name": "github_search_repos",
  "description": "Search GitHub repositories",
  "parameters": {
    "query": { "type": "string", "description": "Search query" },
    "sort": { "type": "string", "enum": ["stars", "forks", "updated"] },
    "perPage": { "type": "number", "default": 30 }
  }
}
```

### github_create_issue

```json
{
  "name": "github_create_issue",
  "description": "Create a new issue in a GitHub repository",
  "parameters": {
    "owner": { "type": "string", "description": "Repository owner" },
    "repo": { "type": "string", "description": "Repository name" },
    "title": { "type": "string", "description": "Issue title" },
    "body": { "type": "string", "description": "Issue body" },
    "labels": { "type": "array", "items": { "type": "string" } }
  }
}
```

### github_get_pull_request

```json
{
  "name": "github_get_pull_request",
  "description": "Get details of a specific pull request",
  "parameters": {
    "owner": { "type": "string", "description": "Repository owner" },
    "repo": { "type": "string", "description": "Repository name" },
    "pull_number": { "type": "number", "description": "Pull request number" }
  }
}
```

### github_list_issues

```json
{
  "name": "github_list_issues",
  "description": "List issues in a GitHub repository",
  "parameters": {
    "owner": { "type": "string", "description": "Repository owner" },
    "repo": { "type": "string", "description": "Repository name" },
    "state": { "type": "string", "enum": ["open", "closed", "all"], "default": "open" },
    "labels": { "type": "array", "items": { "type": "string" } }
  }
}
```

### github_create_pull_request

```json
{
  "name": "github_create_pull_request",
  "description": "Create a new pull request",
  "parameters": {
    "owner": { "type": "string", "description": "Repository owner" },
    "repo": { "type": "string", "description": "Repository name" },
    "title": { "type": "string", "description": "PR title" },
    "body": { "type": "string", "description": "PR description" },
    "head": { "type": "string", "description": "Branch with changes" },
    "base": { "type": "string", "description": "Target branch" }
  }
}
```

## Workflow

1. **Detect Intent**: Parse user query for GitHub keywords
2. **Map to Tool**: Match intent to specific MCP tool
3. **Load Schema**: Load only required tool parameters
4. **Execute**: Call MCP tool with extracted parameters
5. **Present**: Show results in user-friendly format

## Context Saving Strategy

- Don't load all GitHub tools upfront (50k tokens)
- Load only intent detection rules (100 tokens)
- Lazy-load tool schemas on demand (5k tokens each)
- Total context used: ~5.1k vs 50k tokens (90% savings)

## Examples

**User**: "Search for opencode repos on GitHub"
**Intent**: github_search_repos
**Action**: Load search tool, execute query

**User**: "Create an issue for bug in login"
**Intent**: github_create_issue  
**Action**: Load create_issue tool, prompt for repo details

**User**: "What's the status of PR #123?"
**Intent**: github_get_pull_request
**Action**: Load get_pr tool, extract PR number
