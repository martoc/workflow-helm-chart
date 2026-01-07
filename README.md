[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# workflow-helm-chart

Reusable GitHub Actions workflows for building and deploying Helm charts to cloud container registries and Kubernetes clusters.

## Supported Platforms

| Platform | Registry | Cluster | Authentication |
|----------|----------|---------|----------------|
| GCP | Artifact Registry | GKE | Workload Identity Federation |
| AWS | ECR | EKS | IAM Role ARN (OIDC) |

## Features

- Helm chart linting and packaging
- Push to GCP Artifact Registry or AWS ECR
- Deploy to GKE or EKS clusters
- Automatic semantic versioning
- Workload Identity Federation support (GCP)
- OIDC authentication support (AWS)
- GitHub Environment protection for deployments

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

### Deploy Workflow (GCP)

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

### Deploy Workflow (AWS)

```yaml
jobs:
  deploy:
    permissions:
      contents: read
      id-token: write
    uses: martoc/workflow-helm-chart/.github/workflows/deploy.yml@v0
    with:
      registry: aws
      region: eu-west-1
      repository_name: helm-charts
      cluster_name: my-eks-cluster
      chart_name: my-app
      chart_version: "1.0.0"
      chart_value_file: values/production.yaml
      aws_role_arn: ${{ vars.AWS_ROLE_ARN }}
      aws_role_arn_registry: ${{ vars.AWS_ROLE_ARN_REGISTRY }}  # Optional
```

## Documentation

- [Usage Guide](./docs/USAGE.md) - Detailed usage instructions, all inputs, and examples
- [Code Style](./docs/CODESTYLE.md) - Code style guidelines for contributors

## Available Workflows

| Workflow | Description |
|----------|-------------|
| `build.yml` | Build and push Helm charts to container registry |
| `deploy.yml` | Deploy Helm charts to Kubernetes clusters |

## Licence

This project is licenced under the MIT Licence - see the [LICENCE](LICENSE) file for details.
