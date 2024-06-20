# K8S Setup

Prepare for communication with a particular cluster on:
- DigitalOcean
- Scaleway

## Input

```yaml
inputs:
  vendor:
    description: The vendor to communicate with (digitalocean, scaleway)
    required: true
  cluster-id:
    description: Target cluster ID
    required: true

  # Vendor: DigitalOcean
  digitalocean-api-token:
    description: DigitalOcean API token
    required: false

  # Vendor: Scaleway
  scaleway-organization-id:
    description: Scaleway organization ID
    required: false
  scaleway-project-id:
    description: Scaleway project ID
    required: false
  scaleway-region:
    description: Scaleway deployment region (such as nl-ams)
    required: false
  scaleway-access-key:
    description: Scaleway API key ID
    required: false
  scaleway-secret-key:
    description: Scaleway API key secret
    required: false
```

## Usage

```yaml
name: Pull Request
on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  setup-scw:
    steps:
      - uses: wisemen-digital/devops-ga-k8s-setup@main
        with:
          vendor: scaleway
          cluster-id: ${{ vars.K8S_CLUSTER_ID }}
          scaleway-organization-id: ${{ vars.SCALEWAY_ORGANIZATION_ID }}
          scaleway-project-id: ${{ vars.SCALEWAY_PROJECT_ID }}
          scaleway-region: ${{ vars.SCALEWAY_REGION }}
          scaleway-cluster-id: ${{ vars.K8S_CLUSTER_ID }}
          scaleway-access-key: ${{ secrets.SCALEWAY_ACCESS_KEY }}
          scaleway-secret-key: ${{ secrets.SCALEWAY_SECRET_KEY }}

  setup-do:
    steps:
      - uses: wisemen-digital/devops-ga-k8s-setup@main
        with:
          vendor: digitalocean
          cluster-id: ${{ vars.K8S_CLUSTER_ID }}
          digitalocean-api-token: ${{ secrets.DIGITALOCEAN_API_TOKEN }}
```
