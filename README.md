# .github — Organisation CI Standards

[![UCQCS](https://img.shields.io/badge/UCQCS-v4.8-blue)](https://github.com/g33ky00/.github)

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

## About

Organisation-level reusable workflows, Dependabot config and CI standards for `g33ky00`.

## Structure

```
.github/
└── workflows/
    └── ucqcs.yml   # reusable UCQCS workflow (v4.8)
```

## Stack

- GitHub Actions (reusable workflows)

## Contributing

Changes to shared workflows affect the whole fleet. Open a PR and bump the tag.

## License

MIT — see [LICENSE](LICENSE).
