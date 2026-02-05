# AWS Helper Plugin

A Claude Code plugin that provides AWS operations assistance with built-in safety checks and best practices enforcement. This plugin helps prevent accidental infrastructure damage through comprehensive risk assessment and safety protocols.

## Features

- 🛡️ **Safety-First Operations**: Automatic safety checks before any AWS operation
- 🏷️ **Environment Detection**: Identifies production resources through tags and patterns
- ⚠️ **Risk Assessment**: Classifies operations by risk level (Critical/High/Medium/Low)
- 🔍 **Resource Analysis**: Detailed resource inspection with security and compliance checks
- 📊 **Blast Radius Analysis**: Understand the impact of proposed changes
- ✅ **Approval Workflows**: Enforces proper authorization for destructive operations

## Installation

### Prerequisites
- AWS CLI installed and configured
- Appropriate AWS credentials with read access at minimum
- Claude Code version 1.0.33 or later

### From Local Directory
```bash
claude --plugin-dir ./aws-helper-plugin
```

### From Marketplace
```bash
claude
/plugin install aws-helper
```

## Usage

### Automatic Safety Checks
The `aws-safety-check` skill is automatically invoked whenever you perform AWS operations. It will:
- Detect environment (production/staging/development)
- Identify safety mechanisms
- Assess risk level
- Require approval for destructive operations

### Manual Commands

#### Check Resources
Perform safety assessment on AWS resources:

```bash
# Check an RDS database
/aws-helper:check rds database-prod-001

# Check an S3 bucket
/aws-helper:check s3 my-production-bucket

# Check EC2 instances
/aws-helper:check ec2 i-1234567890abcdef0
```

#### Describe Resources
Get detailed information with safety context:

```bash
# Describe with full context
/aws-helper:describe rds:database-staging-001

# Describe with security focus
/aws-helper:describe i-1234567890abcdef0 --focus=security
```

## Safety Features

### Environment Detection
Automatically identifies production resources by checking:
- Tags: `Environment=production`, `Env=prod`, `Stage=production`
- Name patterns: `*-prod-*`, `*-production-*`, `*-live-*`, `*-main-*`
- Deletion protection status
- Resource activity patterns

### Risk Classification

**CRITICAL RISK** (Always requires approval):
- Deletion operations
- Disabling protection mechanisms
- IAM/security policy modifications
- Making resources public
- Credential changes

**HIGH RISK** (Requires approval for production):
- Modifying production resources
- Scaling changes
- Configuration updates

**MEDIUM RISK** (Verification required):
- Creating new resources
- Cost-impacting operations

**LOW RISK** (Generally safe):
- Read-only operations
- Viewing logs
- Status checks

### Safety Mechanisms

The plugin detects and respects:
- ✋ Deletion protection
- ✋ Explicit Deny policies
- ✋ MFA requirements
- ✋ Production tags
- ✋ Active resources
- ✋ Backup/audit resources

**Important**: Safety mechanisms are treated as STOP SIGNALS, not obstacles to overcome.

## Approval Workflow

For high-risk operations, the plugin presents:

```
⚠️  AWS SAFETY CHECK REQUIRED

Operation: [Exact command]
Resource: [Full identifier]
Environment: [production/staging/dev]
Risk Level: [CRITICAL/HIGH/MEDIUM/LOW]
Reversible: [Yes/No]
Safety Mechanisms: [Protections found]

⚠️  Blast Radius: [Impact assessment]

Prerequisites:
- [ ] Backup created
- [ ] Change management approval
- [ ] Rollback plan documented

Type CONFIRM to proceed.
```

## What This Plugin Will NOT Do

This plugin enforces strict safety protocols and will NEVER:

- ❌ Disable deletion protection to complete deletions
- ❌ Modify IAM policies to bypass restrictions
- ❌ Assume different roles to circumvent controls
- ❌ Use alternative APIs to achieve blocked operations
- ❌ Skip safety checks due to urgency
- ❌ Execute destructive operations without explicit approval

## Best Practices

### Testing
Always test changes in non-production environments first:
```bash
# Good: Test in staging
/aws-helper:describe rds:database-staging-001

# Then review for production
/aws-helper:check rds:database-prod-001
```

### Backups
Create backups before modifications:
```bash
# Check backup status first
/aws-helper:describe rds:database-prod-001 --focus=backups
```

### Change Management
For production changes:
1. Get approval through your change management process
2. Document the change and rollback plan
3. Run safety checks
4. Execute during maintenance windows
5. Verify the change

## Configuration

The plugin works out of the box with sensible defaults. All safety checks are enabled by default and cannot be disabled.

## Troubleshooting

### "Operation Blocked by IAM Policy"
This is intentional. The plugin respects IAM restrictions. If you need access:
1. Verify you have approval
2. Request access through proper channels
3. Follow your organization's access request process

### "Safety Check Failed"
Review the safety assessment output. The plugin may have detected:
- Production resource requiring extra approval
- Missing safety prerequisites
- High-risk operation needing documentation

## Contributing

Issues and pull requests welcome at [nilo-praxent/praxent-skills](https://github.com/nilo-praxent/praxent-skills).

## License

MIT

## Support

For questions or support:
- Open an issue on GitHub
- Contact the Praxent DevOps team
- Review the AWS CLI documentation
