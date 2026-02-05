---
name: code-review
description: Reviews code for best practices, security issues, and potential bugs. Automatically invoked when analyzing code quality or reviewing pull requests.
---

# Code Review Skill

When reviewing code, analyze the following aspects:

## 1. Code Organization and Structure
- Check for proper separation of concerns
- Verify consistent naming conventions
- Ensure appropriate use of design patterns
- Look for code duplication (DRY principle)

## 2. Security Concerns
- Identify potential security vulnerabilities (SQL injection, XSS, CSRF)
- Check for hardcoded credentials or sensitive data
- Verify input validation and sanitization
- Review authentication and authorization logic
- Check for proper error handling that doesn't leak sensitive information

## 3. Error Handling and Reliability
- Ensure proper error handling with try-catch blocks
- Check for edge cases and null/undefined handling
- Verify graceful degradation
- Look for potential race conditions or concurrency issues

## 4. Performance Considerations
- Identify inefficient algorithms or queries
- Check for unnecessary re-renders (React) or re-computations
- Look for memory leaks
- Verify proper resource cleanup

## 5. Testing and Maintainability
- Assess test coverage
- Check for testable code structure
- Verify code is documented where necessary
- Look for overly complex functions that should be broken down

## 6. Best Practices by Language/Framework
- Follow language-specific idioms
- Use framework-recommended patterns
- Check for deprecated APIs or patterns
- Verify proper dependency management

## Output Format
Provide a structured review with:
- **Severity** (Critical, High, Medium, Low, Info)
- **Location** (file:line)
- **Issue** description
- **Recommendation** for improvement
- **Code snippet** when helpful
