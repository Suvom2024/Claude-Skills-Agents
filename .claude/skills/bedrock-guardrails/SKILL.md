---
name: bedrock-guardrails
description: |
  Configure AWS Bedrock Guardrails with denied topics, content filters, word policies, contextual grounding, and PII redaction. Attaches guardrail IDs to Bedrock agent invocations and validates coverage.
allowed-tools: Read, Write, Bash(cmd:*)
version: 1.0.0
author: Claude Skills Agents <suvom2024@github.com>
license: MIT
compatible-with: claude-code, codex, openclaw
tags: [ai, safety, aws]
---
# Bedrock Guardrails

## Overview

Configure AWS Bedrock Guardrails with denied topics, content filters, word policies, contextual grounding, and PII redaction. Attaches guardrail IDs to Bedrock agent invocations and validates coverage.

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
