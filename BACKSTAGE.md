# Backstage Registration Guide

This repository contains a **System** (praxent-skills) with multiple **Component** plugins. Each component has its own `catalog-info.yaml` file.

## Structure

```
praxent-skills/
├── catalog-info.yaml                      # System definition only
├── code-review-plugin/
│   └── catalog-info.yaml                  # Component: code-review-plugin
└── aws-helper-plugin/
    └── catalog-info.yaml                  # Component: aws-helper-plugin
```

## Registering in Backstage

### Recommended: Wildcard Pattern

Add to your Backstage `app-config.yaml`:

```yaml
catalog:
  locations:
    # Register the system
    - type: url
      target: https://github.com/nilo-praxent/praxent-skills/blob/main/catalog-info.yaml

    # Auto-discover all plugin catalog files
    - type: url
      target: https://github.com/nilo-praxent/praxent-skills/blob/main/*/catalog-info.yaml
      rules:
        - allow: [Component]
```

**Benefits:**
- ✅ Single configuration entry
- ✅ New plugins auto-discovered
- ✅ No duplicate definitions
- ✅ Easy to maintain

### Alternative: Manual Registration

If wildcards aren't working, register each individually in the Backstage UI:

1. Navigate to: **Create... → Register Existing Component**
2. Enter each URL:
   - `https://github.com/nilo-praxent/praxent-skills/blob/main/catalog-info.yaml`
   - `https://github.com/nilo-praxent/praxent-skills/blob/main/code-review-plugin/catalog-info.yaml`
   - `https://github.com/nilo-praxent/praxent-skills/blob/main/aws-helper-plugin/catalog-info.yaml`

### Alternative: GitHub Discovery

Enable automatic discovery of all catalog files in your org:

```yaml
# app-config.yaml
catalog:
  providers:
    github:
      providerId:
        organization: 'nilo-praxent'
        catalogPath: '**/catalog-info.yaml'
        filters:
          branch: 'main'
          repository: 'praxent-skills'
```

## Verification

After registration, verify in Backstage:

1. **System View**: Search for "Praxent Skills" - should show the system with 2 components
2. **Component View**: Each plugin should appear as an individual component
3. **Dependencies**: Components should show `system: praxent-skills` relationship

## Adding New Plugins

When you add a new plugin:

1. Create plugin directory with `catalog-info.yaml`
2. Ensure `spec.system: praxent-skills` is set
3. If using wildcards: ✅ Auto-discovered
4. If using manual: Register the new catalog file URL

## Troubleshooting

**Components not appearing?**
- Check GitHub URLs are accessible
- Verify YAML syntax with `backstage-cli validate`
- Check Backstage logs for ingestion errors
- Ensure `spec.system: praxent-skills` matches the system name

**Duplicate entities?**
- Remove duplicate definitions from root `catalog-info.yaml`
- Keep only System definition in root
- Each component only in its own folder's catalog file

## References

- [Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)
- [Descriptor Format](https://backstage.io/docs/features/software-catalog/descriptor-format)
- [Catalog Configuration](https://backstage.io/docs/features/software-catalog/configuration)
