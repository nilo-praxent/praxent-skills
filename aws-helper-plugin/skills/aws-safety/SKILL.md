---
name: aws-safety-check
description: Performs safety checks before AWS operations, identifies production resources, and enforces safety protocols. Automatically invoked when working with AWS infrastructure.
---

# AWS Safety Check Skill

This skill MUST be invoked before performing ANY AWS operation that modifies resources. It enforces safety-first operations.

## Safety Check Process

### 1. Resource Identification
- Verify the exact resource identifier (ARN, ID, name)
- Determine the resource type (RDS, EC2, S3, IAM, etc.)
- Check resource tags for environment markers

### 2. Environment Detection
Identify environment by checking:
- Tags: `Environment`, `Env`, `Stage`, `environment`
- Common values: `production`, `prod`, `staging`, `stage`, `development`, `dev`
- Resource name patterns: `*-prod-*`, `*-production-*`, `*-live-*`
- Deletion protection status (indicates production)

### 3. Operation Risk Assessment
Classify operations by risk level:

**CRITICAL RISK** (Always require explicit approval):
- Deletion operations (delete, terminate, drop, remove)
- Disabling protection mechanisms
- Modifying IAM policies or security groups
- Making resources public
- Database credential changes
- Bulk operations

**HIGH RISK** (Require approval for production):
- Modifying production resources
- Scaling changes
- Configuration updates
- Snapshot/backup operations

**MEDIUM RISK** (Verify intent):
- Creating new resources
- Read operations on sensitive data
- Cost-impacting operations

**LOW RISK** (Generally safe):
- Read-only describe/list operations
- Viewing logs
- Getting status information

### 4. Safety Mechanism Detection

Check for these STOP SIGNALS:
- ✋ Deletion protection enabled
- ✋ Explicit Deny policies
- ✋ MFA requirements
- ✋ "Production" or "Critical" tags
- ✋ Active resources with recent activity
- ✋ Resources with backup/audit purposes

**CRITICAL**: Safety mechanisms are STOP SIGNS, not obstacles to overcome.

### 5. Approval Requirements

For destructive or high-risk operations, ALWAYS present:

```
⚠️  AWS SAFETY CHECK REQUIRED

Operation: [Exact AWS CLI command or API call]
Resource: [Full ARN or identifier]
Resource Type: [RDS, EC2, S3, etc.]
Environment: [production/staging/development/unknown]
Risk Level: [CRITICAL/HIGH/MEDIUM/LOW]
Reversible: [Yes/No]
Safety Mechanisms: [List protections found]

⚠️  Blast Radius:
[What will be affected by this operation]

Prerequisites:
- [ ] Backup created (if applicable)
- [ ] Change management approval obtained
- [ ] Rollback plan documented
- [ ] Impact assessment completed

Type CONFIRM to proceed, or provide alternative instructions.
```

### 6. Production Resource Protection

For production resources, enforce:
- Multi-person approval requirements
- Change management documentation
- Backup/snapshot creation before changes
- Testing in non-production first
- Rollback plan verification
- Business hours restrictions (warn if outside hours)

## Prohibited Workarounds

NEVER suggest or attempt:
- Disabling deletion protection to complete deletion
- Modifying IAM policies to bypass restrictions
- Assuming different roles to circumvent controls
- Using alternative APIs to achieve blocked operations
- Making resources "effectively deleted" instead of actually deleting

## When Operations Are Blocked

If an AWS operation is blocked:

1. **STOP** immediately
2. **REPORT** the blocking mechanism
3. **EXPLAIN** why the restriction exists
4. **OFFER** guidance on proper procedures
5. **NEVER** attempt workarounds

## Output Format

Always provide:
- Clear risk assessment
- Specific resource identifiers
- Environment classification
- Required approvals
- Safety checklist
- Blast radius analysis
- Rollback plan (when applicable)
