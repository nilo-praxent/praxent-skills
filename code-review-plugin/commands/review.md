---
description: Perform a comprehensive code review on specified files or the current project
---

# Code Review Command

You are performing a comprehensive code review on: **$ARGUMENTS**

If no specific files are provided in $ARGUMENTS, review recently modified files in the current git repository.

## Review Process

1. **Identify Files**: Determine which files to review based on $ARGUMENTS or recent git changes
2. **Read Code**: Use the Read tool to examine the code in each file
3. **Analyze**: Apply the code-review skill to analyze each file
4. **Report**: Provide a comprehensive review report

## Review Report Structure

Organize your findings by severity:

### 🔴 Critical Issues
Issues that must be fixed before deployment (security vulnerabilities, data loss risks)

### 🟠 High Priority
Issues that should be fixed soon (bugs, performance problems)

### 🟡 Medium Priority
Issues that improve code quality (refactoring opportunities, code smells)

### 🟢 Low Priority / Suggestions
Nice-to-have improvements (style, documentation)

## Summary
- Total files reviewed: X
- Issues found: Y
- Estimated fix time: Z

Be thorough but constructive. Focus on actionable feedback with specific examples and recommendations.
