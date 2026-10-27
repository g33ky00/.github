# .github — Organisation CI Standards

Reusable workflows and CI standards for the `g33ky00` GitHub organisation.

## Reusable workflow: UCQCS (Unified Code Quality Control System)

```yaml
jobs:
  ci:
    uses: g33ky00/.github/.github/workflows/ucqcs.yml@v4.5
    secrets: inherit
```

### Versioning
Tags follow `vMAJOR.MINOR`. Current stable: `v4.5`.

### Migration from inline ci-unified.yml
Replace the entire `ci-unified.yml` content with the caller snippet above.
