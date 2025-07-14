---
lab:
  title: "Challenge Lab: Configure agent pools and understand pipeline styles"
  module: "Module 02: Implement CI with Azure Pipelines and GitHub Actions"
---

# Challenge Lab: Configure agent pools and understand pipeline styles

## Mission

Configure a self-hosted Azure DevOps agent on an Azure VM and modify a YAML pipeline to use your custom agent pool instead of Microsoft-hosted agents.

## Learning Objectives

After completing this challenge, you will be able to:

- Create and configure Azure DevOps agent pools
- Deploy and configure self-hosted agents on Azure VMs
- Implement YAML-based pipelines with custom agent pools
- Configure agent authentication and security contexts

## Success Criteria

- [ ] Azure VM is provisioned with system-assigned managed identity enabled
- [ ] Self-hosted agent pool is created and configured in Azure DevOps
- [ ] Agent is installed, configured, and running as a Windows service
- [ ] YAML pipeline is modified to use the self-hosted agent pool
- [ ] Pipeline runs successfully on the self-hosted agent and produces artifacts

## Critical Requirements ⚠️

**MANDATORY**: These exact values must be used for system compatibility:

- **Azure DevOps Project Name**: `eShopOnWeb` - Required for pipeline references
- **Repository Source**: `https://github.com/MicrosoftLearning/eShopOnWeb.git` - Required for source code
- **Default Branch**: `main` - Required for pipeline execution
- **Resource Group**: `rg-eshoponweb-agentpool` - Required for resource organization
- **Agent Pool Name**: `eShopOnWebSelfPool` - Required for pipeline configuration
- **Agent Name**: `eShopOnWebSelfAgent` - Required for pipeline demands
- **VM Image**: `Windows Server 2022 Datacenter: Azure Edition - x64 Gen2` - Required for agent compatibility
- **PAT Token Name**: `eShopOnWebToken` - Required for authentication
- **PAT Scope**: `Agent Pools (Read & Manage)` - Required for minimal permissions
- **Service Context**: `NT AUTHORITY\SYSTEM` - Required for service security
- **YAML Pipeline File**: `/.ado/eshoponweb-ci-pr.yml` - Required for CI configuration
- **Pool Configuration**: Must include `name: eShopOnWebSelfPool` and `demands: Agent.Name -equals eShopOnWebSelfAgent`
- **Grant Access Option**: Must be **unchecked** - Required for security compliance

## Your Challenge

You're tasked with setting up a complete self-hosted agent infrastructure for Azure DevOps pipelines. Here's what you need to accomplish:

### Phase 1: Infrastructure Setup

Deploy an Azure VM with the correct specifications (Presets - Dev/Test) including system-assigned managed identity. To support pipeline operations, use the following PowerShell script to install the required prerequisites (Azure CLI and .NET 8.0 SDK) on the VM:

```powershell
# Use choco to install other tools
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Install .NET 8 SDK
choco install dotnet-sdk --version=8.0.403 -y

# Install Azure CLI
choco install azure-cli -y
```

### Phase 2: Agent Pool Configuration

Create a self-hosted agent pool in Azure DevOps with proper security settings. Download and configure the agent software on your VM using a Personal Access Token with minimal required permissions.

### Phase 3: Pipeline Modification

Take the existing YAML pipeline and modify it to run on your self-hosted agent instead of Microsoft-hosted agents. The pipeline should successfully build, test, and publish the .NET application.

### Phase 4: Validation

Ensure your pipeline runs successfully on the self-hosted agent and produces the expected build artifacts.

**Estimated Time**: 30 minutes  
**Difficulty**: Intermediate

## Important Notes

- **Agent Security**: Use the principle of least privilege when configuring service security contexts (check "Critical Requirements")
- **Pipeline Permissions**: You may need to grant permissions when the pipeline first runs on your agent pool
- **Service Management**: The agent must run as a Windows service for production scenarios

## Validation

How will you know you've succeeded:

- Agent appears as "Online" in Azure DevOps agent pool interface
- Pipeline runs successfully without errors on your self-hosted agent
- Build artifacts are produced from the .NET application build process
- Agent service is running and configured correctly in Windows Services
- Pipeline execution logs show it ran on your specific
