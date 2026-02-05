---
description: Check AWS resources for safety markers, production indicators, and risk assessment
---

# AWS Resource Check Command

Perform a comprehensive safety check on AWS resources specified in: **$ARGUMENTS**

## Check Process

1. **Parse Arguments**: Extract resource identifiers, ARNs, or resource types from $ARGUMENTS
2. **Invoke Safety Skill**: Use the aws-safety-check skill to analyze resources
3. **Gather Information**: Use AWS CLI (read-only commands only) to gather resource details
4. **Assess Risk**: Determine environment, safety mechanisms, and risk level
5. **Report Findings**: Present a clear safety assessment

## Report Structure

### 📋 Resource Summary
- Resource Type: [EC2, RDS, S3, etc.]
- Resource ID/ARN: [full identifier]
- Region: [aws region]
- Account: [account ID if available]

### 🏷️ Environment Classification
- Environment: [production/staging/development/unknown]
- Confidence: [High/Medium/Low]
- Indicators: [tags, name patterns, protection status]

### 🛡️ Safety Mechanisms
List all protective measures found:
- [ ] Deletion protection
- [ ] Explicit deny policies
- [ ] MFA requirements
- [ ] Production tags
- [ ] Backup policies
- [ ] Encryption enabled

### ⚠️ Risk Assessment
- Current Risk Level: [NONE/LOW/MEDIUM/HIGH/CRITICAL]
- Operations Allowed: [List safe operations]
- Operations Requiring Approval: [List restricted operations]
- Operations Prohibited: [List blocked operations]

### 💡 Recommendations
- Safe actions you can take now
- Proper procedures for restricted actions
- Who to contact for approvals
- Documentation requirements

## Examples

```bash
# Check a specific RDS instance
/aws-helper:check rds database-prod-001

# Check an S3 bucket
/aws-helper:check s3 my-production-bucket

# Check multiple resources
/aws-helper:check ec2 i-1234567890abcdef0 rds database-staging-001
```

## Important Notes

- This command only performs READ-ONLY checks
- No resources will be modified
- All AWS CLI commands used will be displayed
- If you need to perform operations, they will require separate approval
