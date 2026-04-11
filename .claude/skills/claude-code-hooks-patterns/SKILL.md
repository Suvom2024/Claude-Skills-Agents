---
name: claude-code-hooks-patterns
description: |
  Configure Claude Code hooks in settings.json for automated workflows. Covers PreToolUse, PostToolUse, Notification hooks, matcher patterns, and building hook-driven development workflows. Trigger: "hooks", "pre-tool", "post-tool", "automated workflow", "settings.json hooks".
allowed-tools: Read, Write, Bash(cmd:*)
version: 1.0.0
author: Claude Skills Agents <suvom2024@github.com>
license: MIT
compatible-with: claude-code
tags: [claude-code, hooks, automation]
---
# Claude Code Hooks Patterns

## Overview

Claude Code hooks let you run shell commands automatically in response to tool calls and events. Configure them in `.claude/settings.json` to enforce linting, run tests, validate security, and automate repetitive workflows.

## Prerequisites

- Claude Code CLI installed
- Project with `.claude/` directory initialized

## Instructions

### 1. Hook Types

| Hook Type | When It Fires | Use Case |
|-----------|--------------|----------|
| `PreToolUse` | Before a tool executes | Validate, block, or modify tool calls |
| `PostToolUse` | After a tool completes | Lint, test, format changed files |
| `Notification` | On status changes | Alert, log, or trigger external systems |
| `Stop` | When Claude finishes a response | Run final validation checks |

### 2. Basic Hook Configuration

Add to `.claude/settings.json`:
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "echo 'File being modified: $CLAUDE_FILE_PATH'"
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "npx eslint --fix $CLAUDE_FILE_PATH 2>/dev/null || true"
      }
    ],
    "Notification": [
      {
        "matcher": ".*",
        "command": "echo \"$(date): $CLAUDE_NOTIFICATION\" >> .claude/activity.log"
      }
    ]
  }
}
```

### 3. Matcher Patterns

Matchers use regex to select which tool calls trigger the hook:
- `"Write"` - Only Write tool calls
- `"Write|Edit"` - Write or Edit tool calls
- `"Bash"` - Any Bash command
- `"Bash\\(npm.*\\)"` - Bash commands matching npm
- `".*"` - All tool calls

### 4. Production Hook Recipes

**Auto-format on file changes:**
```json
{
  "PostToolUse": [
    {
      "matcher": "Write|Edit",
      "command": "if [[ $CLAUDE_FILE_PATH == *.ts ]] || [[ $CLAUDE_FILE_PATH == *.tsx ]]; then npx prettier --write $CLAUDE_FILE_PATH 2>/dev/null; fi"
    }
  ]
}
```

**Block writes to protected files:**
```json
{
  "PreToolUse": [
    {
      "matcher": "Write|Edit",
      "command": "if echo $CLAUDE_FILE_PATH | grep -qE '\\.(env|pem|key)$'; then echo 'BLOCKED: Cannot modify secrets files' >&2; exit 1; fi"
    }
  ]
}
```

**Run tests after code changes:**
```json
{
  "PostToolUse": [
    {
      "matcher": "Write|Edit",
      "command": "if [[ $CLAUDE_FILE_PATH == *.test.* ]]; then npx vitest run $CLAUDE_FILE_PATH --reporter=verbose 2>&1 | tail -20; fi"
    }
  ]
}
```

**Security scanning on new files:**
```json
{
  "PostToolUse": [
    {
      "matcher": "Write",
      "command": "npx secretlint $CLAUDE_FILE_PATH 2>/dev/null || true"
    }
  ]
}
```

### 5. Environment Variables Available in Hooks

| Variable | Description |
|----------|------------|
| `$CLAUDE_FILE_PATH` | Path of the file being modified |
| `$CLAUDE_TOOL_NAME` | Name of the tool being called |
| `$CLAUDE_NOTIFICATION` | Notification message text |
| `$CLAUDE_SESSION_ID` | Current session identifier |

### 6. Hook Best Practices

- **Keep hooks fast** (<2 seconds) to avoid slowing down Claude
- **Use `|| true`** to prevent hook failures from blocking Claude
- **Log hook output** to a file for debugging
- **Test hooks manually** before adding to settings.json
- **Use PreToolUse sparingly** - blocking tools disrupts Claude's workflow

## Output

- Configured `.claude/settings.json` with appropriate hooks
- Automated linting, formatting, and validation on file changes
- Activity logging for audit trails

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Hook blocks all writes | Overly broad matcher regex | Narrow the matcher pattern |
| Slow Claude responses | Hook command takes too long | Optimize or add timeout |
| Hook not firing | Invalid matcher regex | Test regex with echo and grep |
| Permission denied | Hook script not executable | Check file permissions |

## Resources

- Claude Code hooks documentation
- See `${CLAUDE_SKILL_DIR}/references/` for more hook recipes
