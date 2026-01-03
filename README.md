[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# workflow-helm-chart

Reusable GitHub Actions workflows for building and deploying Helm charts to GCP Artifact Registry and Kubernetes clusters.

## Features

- Helm chart linting and packaging
- Push to GCP Artifact Registry
- Deploy to GKE clusters
- Automatic semantic versioning
- Workload Identity Federation support

## Quick Start

### Build Workflow

```yaml
jobs:
  build:
    permissions:
      contents: write
      id-token: write
    uses: martoc/workflow-helm-chart/.github/workflows/build.yml@v0
    with:
      registry: gcp
      region: europe-west2
      repository_name: helm-charts
      gcp_project_id: my-project
      workload_identity_provider: ${{ vars.WIF_PROVIDER }}
      service_account: ${{ vars.SERVICE_ACCOUNT }}
```

### Deploy Workflow

```yaml
jobs:
  deploy:
    permissions:
      contents: read
      id-token: write
    uses: martoc/workflow-helm-chart/.github/workflows/deploy.yml@v0
    with:
      registry: gcp
      region: europe-west2
      repository_name: helm-charts
      gcp_project_id: my-project
      cluster_name: my-cluster
      chart_name: my-app
      chart_version: "1.0.0"
      chart_value_file: values/production.yaml
      workload_identity_provider: ${{ vars.WIF_PROVIDER }}
      service_account: ${{ vars.SERVICE_ACCOUNT }}
```

## Documentation

- [Usage Guide](./docs/USAGE.md) - Detailed usage instructions and examples
- [Code Style](./docs/CODESTYLE.md) - Code style guidelines for contributors

## Available Workflows

| Workflow | Description |
|----------|-------------|
| `build.yml` | Build and push Helm charts to GCP Artifact Registry |
| `deploy.yml` | Deploy Helm charts to GKE clusters |

## Licence

This project is licenced under the MIT Licence - see the [LICENCE](LICENSE) file for details.
