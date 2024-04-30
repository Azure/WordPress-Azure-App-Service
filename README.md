# Deploy a WordPress App to Azure Action

## Description

This GitHub Action automates the deployment of a WordPress Web App on a Windows App Service with MySQL in app.

[For more information on this quickstart template](https://learn.microsoft.com/en-us/samples/azure/azure-quickstart-templates/wordpress-app-service-mysql-inapp/)

**This documentation is for v4 of vaibbavisk20/deploy_wordpress_app**

## Inputs

Please install the Azure OIDC app from the GitHub Marketplace to populate the below inputs as secrets in your repo

- **client-id** (required): Client ID used for Azure login.
- **tenant-id** (required): Tenant ID used for Azure login.
- **subscription-id** (required): Azure subscription ID used with the `az login`.
- **resource-group-name** (required): Resource group where Azure resources will be deployed.

## Usage

Create this workflow in your repo on this path: `.github/workflows/workflow_file.yml`

```yaml
name: Workflow to deploy WordPress VM on Azure

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:

permissions:
  id-token: write
  contents: read

jobs:
  deploy-resources-to-azure:
    runs-on: ubuntu-latest
    steps:
        - name: Checkout main
          uses: actions/checkout@v3
          
        - name: Deploy a WordPress App to Azure action
          uses: vaibbavisk20/deploy_wordpress_app@v4
          with:
            client-id: ${{ secrets.AZURE_CLIENT_ID }}
            tenant-id: ${{ secrets.AZURE_TENANT_ID }}
            subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
            resource-group-name: ${{secrets.AZURE_RG}}
```
## Output

The action creates a Wordpress App which can be viewed on portal.azure.com and provides information about the deployed resources.
