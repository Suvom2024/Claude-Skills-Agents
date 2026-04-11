---
name: claude-md-optimization
description: |
  Best practices for writing CLAUDE.md files that maximize Claude Code effectiveness. Covers structuring project context, encoding build/test commands, defining coding standards, layering with nested CLAUDE.md files, and managing file size. Trigger: "CLAUDE.md", "claude md", "project context", "claude code setup".
allowed-tools: Read, Write, Bash(cmd:*)
version: 1.0.0
author: Claude Skills Agents <suvom2024@github.com>
license: MIT
compatible-with: claude-code
tags: [claude-code, configuration, productivity]
---
# CLAUDE.md Optimization

## Overview

CLAUDE.md is the primary mechanism for giving Claude Code persistent project context. A well-structured CLAUDE.md dramatically improves code quality, reduces errors, and ensures Claude follows your team's conventions. This skill teaches you to write high-impact CLAUDE.md files.

## Prerequisites

- Claude Code CLI installed and configured
- A software project with established conventions

## Instructions

### 1. File Hierarchy and Loading Order

Claude Code loads CLAUDE.md files hierarchically:
```
~/.claude/CLAUDE.md              # User-level (personal preferences)
/project-root/CLAUDE.md          # Project-level (team conventions)
/project-root/src/CLAUDE.md      # Directory-level (subsystem context)
/project-root/.claude/CLAUDE.md  # Claude config directory
```

**Key rules:**
- Root CLAUDE.md is ALWAYS loaded
- Subdirectory CLAUDE.md files load only when working in that directory
- User-level CLAUDE.md applies across ALL projects
- Keep root CLAUDE.md under 500 lines for token efficiency

### 2. Essential Sections

Structure your CLAUDE.md with these sections:

```markdown
# Project Name

## Build & Test Commands
- `npm run dev` - Start development server
- `npm test` - Run all tests
- `npm run test:unit -- path/to/file` - Run single test file
- `npm run lint` - Lint the codebase
- `npm run build` - Production build

## Tech Stack
- Next.js 15 with App Router
- TypeScript 5.7 strict mode
- Tailwind CSS v4 + shadcn/ui
- Drizzle ORM + PostgreSQL
- Vitest for testing

## Code Conventions
- Use functional components with hooks (no class components)
- Prefer named exports over default exports
- Use `type` for type aliases, `interface` for object shapes
- Error handling: use Result pattern, never throw in business logic
- File naming: kebab-case for files, PascalCase for components

## Project Structure
- `src/app/` - Next.js App Router pages
- `src/components/` - Reusable UI components
- `src/lib/` - Business logic and utilities
- `src/db/` - Database schema and queries

## Important Patterns
- All database queries go through the repository pattern in `src/db/`
- API responses use the standard envelope: `{ data, error, meta }`
- Authentication uses Clerk middleware in `src/middleware.ts`
```

### 3. Anti-Patterns to Avoid

| Anti-Pattern | Why It's Bad | Better Approach |
|-------------|-------------|-----------------|
| Pasting entire config files | Wastes context tokens | Reference file paths instead |
| Vague instructions ("write good code") | No actionable guidance | Specific rules with examples |
| Duplicating README content | Redundant information | Link to README, add only dev context |
| Including credentials/secrets | Security risk | Use environment variable references |
| Over-specifying obvious conventions | Token waste | Focus on project-unique patterns |

### 4. Advanced Patterns

**Conditional Context with Subdirectory Files:**
```
# /src/api/CLAUDE.md
## API Development Rules
- All endpoints return standard ApiResponse<T> type
- Use Zod for request validation
- Rate limiting is handled by middleware, don't add per-route
- Database transactions: use db.transaction() for multi-step operations
```

**Token Budget Management:**
- Root CLAUDE.md: ~200-400 lines (critical context)
- Subdirectory CLAUDE.md: ~50-100 lines (domain-specific)
- Total loaded context should stay under 800 lines

## Output

- A well-structured CLAUDE.md file tailored to your project
- Optional subdirectory CLAUDE.md files for complex subsystems
- User-level ~/.claude/CLAUDE.md for personal preferences

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Claude ignores conventions | CLAUDE.md too long, key rules buried | Move critical rules to top, reduce noise |
| Inconsistent behavior across dirs | Missing subdirectory context | Add CLAUDE.md to key subdirectories |
| Slow response times | CLAUDE.md includes large code blocks | Replace with file path references |
| Claude can't find commands | Build commands not in CLAUDE.md | Add explicit Build & Test Commands section |

## Resources

- Claude Code documentation on CLAUDE.md files
- See `${CLAUDE_SKILL_DIR}/references/` for templates and examples
