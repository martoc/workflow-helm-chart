# Usage

## Overview

This repository provides reusable GitHub Actions workflows for building and deploying Helm charts to GCP Artifact Registry and Kubernetes clusters.

## Available Workflows

### build.yml

Builds and pushes Helm charts to GCP Artifact Registry.

**Inputs:**

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| `registry` | string | Yes | Registry type (e.g., `gcp`) |
| `workload_identity_provider` | string | No | GCP Workload Identity Provider |
| `service_account` | string | No | GCP Service Account |
| `region` | string | Yes | GCP region |
| `repository_name` | string | Yes | Artifact Registry repository name |
| `gcp_project_id` | string | No | GCP project ID |

**Example:**

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

### deploy.yml

Deploys Helm charts to GKE clusters.

**Inputs:**

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| `registry` | string | Yes | Registry type |
| `repository_name` | string | Yes | Repository name |
| `region` | string | Yes | GCP region |
| `environment` | string | No | Environment name |
| `cluster_name` | string | Yes | GKE cluster name |
| `chart_name` | string | Yes | Helm chart name |
| `chart_version` | string | Yes | Chart version |
| `chart_value_file` | string | Yes | Path to values file |
| `workload_identity_provider` | string | No | WIF provider |
| `service_account` | string | No | Service account |
| `gcp_project_id` | string | No | GCP project ID |
| `ref` | string | No | Git ref (default: `main`) |
| `version` | string | No | Version override |

**Example:**

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
