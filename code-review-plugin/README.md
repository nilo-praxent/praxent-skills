# Code Review Plugin

A Claude Code plugin that provides automated code review capabilities with a focus on security, best practices, and code quality.

## Features

- 🔍 **Comprehensive Analysis**: Reviews code for security issues, bugs, and best practices
- 🎯 **Contextual Reviews**: Automatically invoked during code analysis or PR reviews
- 📊 **Structured Reports**: Organized by severity with actionable recommendations
- 🛡️ **Security-Focused**: Identifies OWASP Top 10 vulnerabilities and security anti-patterns

## Installation

### From Local Directory
```bash
claude --plugin-dir ./code-review-plugin
```

### From Marketplace
```bash
claude
/plugin install code-review
```

## Usage

### Automatic Skill Invocation
The code-review skill is automatically invoked when Claude detects code review tasks:
- Analyzing code quality
- Reviewing pull requests
- Checking for bugs or issues

### Manual Command
Use the `/code-review:review` command to trigger a review:

```bash
# Review specific files
/code-review:review src/app.js src/utils/auth.js

# Review recent changes
/code-review:review

# Review all TypeScript files
/code-review:review **/*.ts
```

## What It Checks

### Security
- SQL Injection vulnerabilities
- Cross-Site Scripting (XSS)
- Authentication/Authorization issues
- Hardcoded credentials
- Input validation

### Code Quality
- Design patterns and SOLID principles
- Code duplication
- Naming conventions
- Function complexity
- Error handling

### Performance
- Inefficient algorithms
- Memory leaks
- Unnecessary re-renders
- Resource cleanup

### Best Practices
- Framework-specific patterns
- Test coverage
- Documentation
- Dependency management

## Report Format

Reviews are organized by severity:

- 🔴 **Critical**: Must fix before deployment
- 🟠 **High**: Should fix soon
- 🟡 **Medium**: Quality improvements
- 🟢 **Low**: Suggestions

Each issue includes:
- Location (file:line)
- Description
- Recommendation
- Code example

## Configuration

No additional configuration required. The plugin works out of the box with sensible defaults.

## Contributing

Issues and pull requests welcome at [nilo-praxent/praxent-skills](https://github.com/nilo-praxent/praxent-skills).

## License

MIT
