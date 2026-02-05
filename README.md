# Praxent Skills

A collection of Claude Code plugins and skills designed to enhance development workflows at Praxent. These plugins are cataloged in Backstage for easy discovery and installation across the organization.

## Available Plugins

### 🔍 Code Review Plugin
Automated code review capabilities with comprehensive security and quality analysis.

**Features:**
- Security vulnerability detection (OWASP Top 10)
- Best practices enforcement
- Code quality assessment
- Performance analysis
- Structured reports with severity levels

[View Plugin →](./code-review-plugin)

**Installation:**
```bash
# Local testing
claude --plugin-dir ./code-review-plugin

# From marketplace (once published)
claude
/plugin install code-review
```

**Usage:**
```bash
# Review specific files
/code-review:review src/app.js

# Auto-invokes during code analysis
# Just ask: "Review the authentication code"
```

---

### 🛡️ AWS Helper Plugin
Safe AWS operations with built-in safety checks and environment detection.

**Features:**
- Automatic production resource detection
- Risk assessment and classification
- Safety mechanism enforcement
- Blast radius analysis
- Approval workflows for destructive operations

[View Plugin →](./aws-helper-plugin)

**Installation:**
```bash
# Local testing
claude --plugin-dir ./aws-helper-plugin

# From marketplace (once published)
claude
/plugin install aws-helper
```

**Usage:**
```bash
# Check resource safety
/aws-helper:check rds database-prod-001

# Describe with context
/aws-helper:describe i-1234567890abcdef0
```

---

## Repository Structure

```
praxent-skills/
├── catalog-info.yaml                    # Backstage catalog for the system
├── code-review-plugin/
│   ├── .claude-plugin/
│   │   └── plugin.json                  # Plugin manifest
│   ├── skills/
│   │   └── code-review/
│   │       └── SKILL.md                 # Auto-invoked skill
│   ├── commands/
│   │   └── review.md                    # Manual command
│   ├── catalog-info.yaml                # Backstage catalog entry
│   └── README.md
└── aws-helper-plugin/
    ├── .claude-plugin/
    │   └── plugin.json                  # Plugin manifest
    ├── skills/
    │   └── aws-safety/
    │       └── SKILL.md                 # Auto-invoked skill
    ├── commands/
    │   ├── check.md                     # Safety check command
    │   └── describe.md                  # Describe command
    ├── catalog-info.yaml                # Backstage catalog entry
    └── README.md
```

## Backstage Integration

This repository is registered in Backstage as a **System** that groups related Claude Code plugins. Each plugin has its own `catalog-info.yaml` file and is cataloged as a **Component** with:

- Proper metadata and tags for discovery
- Links to documentation and source code
- Lifecycle and ownership information
- Dependencies and system relationships

**Catalog Structure:**
- `catalog-info.yaml` (root) - System definition only
- `*/catalog-info.yaml` - Individual component definitions

**📖 See [BACKSTAGE.md](./BACKSTAGE.md) for registration instructions and wildcard patterns.**

### Viewing in Backstage

1. Navigate to the Backstage Catalog
2. Search for "Praxent Skills" or filter by tag `claude-code`
3. Explore individual plugins and their documentation
4. Access installation instructions and usage examples

## Development

### Creating New Plugins

1. **Create plugin directory structure:**
   ```bash
   mkdir -p my-plugin/.claude-plugin
   mkdir -p my-plugin/skills
   mkdir -p my-plugin/commands
   ```

2. **Create manifest:**
   ```json
   {
     "name": "my-plugin",
     "description": "Plugin description",
     "version": "1.0.0",
     "author": {
       "name": "Praxent",
       "email": "developers@praxent.com"
     }
   }
   ```

3. **Add skills and commands** following the patterns in existing plugins

4. **Create catalog-info.yaml** for Backstage registration

5. **Test locally:**
   ```bash
   claude --plugin-dir ./my-plugin
   ```

6. **Update root catalog-info.yaml** to include your new plugin

### Testing Plugins

```bash
# Test single plugin
claude --plugin-dir ./code-review-plugin

# Test multiple plugins
claude --plugin-dir ./code-review-plugin --plugin-dir ./aws-helper-plugin
```

### Best Practices

- Use semantic versioning in `plugin.json`
- Include comprehensive README.md for each plugin
- Add proper Backstage metadata for discovery
- Test plugins thoroughly before sharing
- Document all commands and skills
- Follow security best practices

## Documentation

- [Claude Code Plugin Documentation](https://code.claude.com/docs/en/plugins)
- [Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)
- [Claude Code Skills](https://code.claude.com/docs/en/skills)

## Contributing

1. Create a new branch for your plugin
2. Follow the development guidelines above
3. Test thoroughly with `--plugin-dir`
4. Update documentation
5. Submit a pull request
6. Add catalog-info.yaml entry

## Support

For questions or issues:
- Open an issue on GitHub
- Contact the Praxent DevOps team
- Review the Claude Code documentation

## License

MIT
