# Code Style

## YAML Formatting

Workflow files should follow GitHub Actions best practices and maintain consistent formatting.

### Key Guidelines

- Use 2 spaces for indentation
- Avoid trailing whitespace
- Use lowercase for keys
- Use descriptive names for jobs and steps
- Always include step names for clarity
- Use quotes for string values that could be interpreted as other types

### Workflow Structure

```yaml
on:
  workflow_call:
    inputs:
      example_input:
        required: true
        type: string
        description: "Clear description of the input"

jobs:
  job-name:
    runs-on: ubuntu-24.04
    steps:
      - name: Descriptive Step Name
        uses: actions/checkout@v4
```

### Conditional Steps

Use GitHub Actions expression syntax for conditionals:

```yaml
- name: GCP Authentication
  uses: google-github-actions/auth@v3
  if: ${{ inputs.registry == 'gcp' }}
```

## Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

| Type | Description |
|------|-------------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation changes |
| `chore:` | Maintenance tasks |
| `refactor:` | Code refactoring |
| `test:` | Adding or updating tests |

### Examples

```
feat: add AWS EKS deployment support
fix: correct environment name in deploy workflow
docs: update usage guide with AWS examples
```

## Pull Requests

- Create feature branches from `main`
- Use descriptive branch names: `feat/description`, `fix/description`
- Ensure all CI checks pass before requesting review
- Keep changes focused and atomic
- Update documentation when adding new features

## Security

- Never commit secrets or credentials
- Use GitHub Secrets for sensitive values
- Use Workload Identity Federation (GCP) or OIDC (AWS) for authentication
- Avoid hardcoding project IDs, regions, or account numbers
