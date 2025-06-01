

# Azure Deployment Templates

This directory contains the Azure Resource Manager (ARM) and Bicep templates for deploying the required Azure resources for MSP Recapp.

## Quick Deploy

Click the button below to deploy the resources directly to your Azure subscription:

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](
  https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMSP-Recapp%2Fazure-templates%2Fc509ace52692601ba5c3c6fe4064b7c34feaeeaa%2Fmsp-recapp-azure-resources.json
)

## What Gets Deployed

This template deploys the following Azure resources:

- **Azure Key Vault**: For secure storage of application secrets and certificates
- **User-Assigned Managed Identity**: For secure authentication to Azure services
- **Role Assignments**: Grants the managed identity appropriate permissions to the Key Vault

## Parameters

The template accepts the following parameters:

- `baseName` (string): Base name used for naming Azure resources (default: "msprecapp")
- `redirectUri` (string): The redirect URI for your MSP Recapp application (default: "https://msprecapp.lovable.app")
- `organizationName` (string): Your organization name for display purposes (default: "MSP Recapp")

## Deployment Methods

### 1. One-Click Deployment (Recommended)
Use the "Deploy to Azure" button above or the direct URL for instant deployment.

### 2. Azure CLI
```bash
# Deploy using Azure CLI
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file msp-recapp-azure-resources.json \
  --parameters @msp-recapp-azure-resources.parameters.json
```

### 3. Azure PowerShell
```powershell
# Deploy using Azure PowerShell
New-AzResourceGroupDeployment `
  -ResourceGroupName "<your-resource-group>" `
  -TemplateFile "msp-recapp-azure-resources.json" `
  -TemplateParameterFile "msp-recapp-azure-resources.parameters.json"
```

### 4. Bicep CLI
```bash
# Deploy using Bicep CLI
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file msp-recapp-azure-resources.bicep \
  --parameters baseName=<your-base-name> redirectUri=<your-redirect-uri> organizationName=<your-org-name>
```

## After Deployment

After the Azure resources are deployed, you'll need to:

1. **Create an App Registration** in Azure AD with the suggested name from the deployment outputs
2. **Configure API Permissions** for Microsoft Graph (User.Read.All, Directory.Read.All, Organization.Read.All)
3. **Generate a Client Secret** for the app registration
4. **Store the credentials** in the deployed Key Vault

The MSP Recapp setup wizard will guide you through these steps.

## Files

- `msp-recapp-azure-resources.json` - ARM JSON template
- `msp-recapp-azure-resources.bicep` - Bicep template (source)
- `msp-recapp-azure-resources.parameters.json` - Sample parameters file
- `README.md` - This file

## Support

For support with deployment or configuration, please refer to the main project documentation or contact our support team.
