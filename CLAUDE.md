# Claude Code Instructions

## Project Overview

This repository contains reusable GitHub Actions workflows for building and deploying Helm charts to GCP (Artifact Registry/GKE) and AWS (ECR/EKS).

## Repository Structure

```
.github/
  workflows/
    build.yml    # Build and push Helm charts
    deploy.yml   # Deploy charts to Kubernetes clusters
    main.yml     # Tag and release workflow
docs/
  USAGE.md       # Detailed usage documentation
  CODESTYLE.md   # Code style guidelines
```

## Key Files

| File | Purpose |
|------|---------|
| `.github/workflows/build.yml` | Reusable workflow for linting, building, and pushing Helm charts |
| `.github/workflows/deploy.yml` | Reusable workflow for deploying charts to GKE/EKS clusters |
| `.github/workflows/main.yml` | CI workflow for tagging and releasing this repository |

## Development Guidelines

### Making Changes

1. Create a feature branch from `main`
2. Follow conventional commits for commit messages
3. Ensure workflow syntax is valid using `actionlint` if available
4. Update documentation if adding new inputs or changing behaviour

### Workflow Inputs

When adding new workflow inputs:
- Always include a `description` field
- Set `required: true/false` explicitly
- Provide sensible `default` values where appropriate
- Document the input in `docs/USAGE.md`

### Testing Changes

Workflows are tested by consuming repositories. To test locally:
1. Fork a repository that uses these workflows
2. Point the workflow reference to your branch
3. Trigger the workflow and verify behaviour

## Common Tasks

### Adding a New Input

1. Add the input to the workflow file under `inputs:`
2. Pass the input to the relevant action
3. Update `docs/USAGE.md` with the new input
4. Update examples in `README.md` if necessary

### Supporting a New Registry/Cloud Provider

1. Add conditional authentication steps
2. Add provider-specific inputs (e.g., `aws_role_arn`)
3. Update the underlying actions to support the new provider
4. Document the new provider in `docs/USAGE.md`

## Related Repositories

- `martoc/action-tag` - Semantic versioning action
- `martoc/action-helm-build` - Helm chart build action
- `martoc/action-helm-deploy` - Helm chart deployment action
- `martoc/action-release` - GitHub release action
