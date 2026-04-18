---
name: humaneval-plus-runner
description: |
  Runs Claude Code code-generation on HumanEval+ and MBPP+, which add 80x more test cases than originals to catch overfit solutions. Reports pass@1 / pass@10 with execution sandboxing.
allowed-tools: Read, Write, Bash(cmd:*)
version: 1.0.0
author: Claude Skills Agents <suvom2024@github.com>
license: MIT
compatible-with: claude-code, codex, openclaw
tags: [ai, evals, code-gen]
---
# Humaneval Plus Runner

## Overview

Runs Claude Code code-generation on HumanEval+ and MBPP+, which add 80x more test cases than originals to catch overfit solutions. Reports pass@1 / pass@10 with execution sandboxing.

## Prerequisites

- Relevant development environment configured
- Basic familiarity with the technology domain

## Instructions

1. Assess the current project requirements and technology stack
2. Apply the patterns and best practices specific to this skill
3. Validate the implementation against documented standards
4. Test the integration thoroughly before deployment

## Output

- Implementation following documented best practices
- Configuration files as needed
- Integration tests where applicable

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Configuration mismatch | Incorrect setup parameters | Verify environment and dependency versions |
| Integration failure | Incompatible dependencies | Check compatibility matrix in references |

## Resources

- See ${CLAUDE_SKILL_DIR}/references/ for detailed documentation
