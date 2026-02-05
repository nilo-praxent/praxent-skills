---
description: Describe AWS resources with safety context and operational recommendations
---

# AWS Resource Describe Command

Provide detailed information about AWS resources: **$ARGUMENTS**

## Description Process

1. **Identify Resources**: Parse resource identifiers from $ARGUMENTS
2. **Gather Details**: Use appropriate AWS describe commands (read-only)
3. **Safety Context**: Apply aws-safety-check skill for safety assessment
4. **Operational Context**: Provide actionable recommendations

## Output Structure

### 📦 Resource Details
[Comprehensive resource configuration details from AWS]

### 🔧 Configuration
- Creation Date: [when resource was created]
- Last Modified: [last modification time]
- Current State: [running, stopped, available, etc.]
- Cost: [estimated monthly cost if calculable]

### 🔗 Dependencies
- Resources this depends on
- Resources that depend on this
- Network connectivity
- Security groups / IAM roles

### 📊 Metrics & Health
- Performance metrics (if available)
- Recent CloudWatch alarms
- Health check status
- Resource utilization

### 🛡️ Security & Compliance
- Encryption status
- Public accessibility
- Security group rules
- IAM policies attached
- Compliance tag status

### 💭 Operational Recommendations

Based on the resource configuration and safety assessment:

**Optimization Opportunities:**
- Cost savings recommendations
- Performance improvements
- Security enhancements

**Maintenance Required:**
- Outdated configurations
- Missing backups
- Compliance gaps

**Risk Mitigation:**
- Security vulnerabilities
- Single points of failure
- Missing redundancy

## Safe Operations You Can Perform

List operations that are safe to perform on this resource without approval.

## Operations Requiring Approval

List operations that require explicit approval with reasoning.

## Examples

```bash
# Describe an RDS instance
/aws-helper:describe rds:database-prod-001

# Describe an EC2 instance
/aws-helper:describe i-1234567890abcdef0

# Describe with specific focus
/aws-helper:describe rds:database-prod-001 --focus=security
```
