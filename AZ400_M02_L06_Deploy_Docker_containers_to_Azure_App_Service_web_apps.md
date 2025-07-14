---
lab:
  title: "Challenge Lab: Deploy Docker containers to Azure App Service web apps"
  module: "Module 02: Implement CI with Azure Pipelines and GitHub Actions"
---

# Challenge Lab: Deploy Docker containers to Azure App Service web apps

## Mission

Build and deploy a containerized .NET application using Azure DevOps CI/CD pipelines to demonstrate end-to-end Docker container deployment to Azure App Service.

## Learning Objectives

After completing this challenge, you will be able to:

- Build custom Docker images using Microsoft hosted Linux agents
- Push Docker images to Azure Container Registry
- Deploy containerized applications to Azure App Service using Azure DevOps pipelines
- Configure role assignments for container access between Azure services

## Success Criteria

- [ ] CI pipeline successfully builds and pushes Docker images to Azure Container Registry
- [ ] CD pipeline successfully deploys containerized application to Azure App Service
- [ ] eShopOnWeb application is accessible and running in Azure App Service
- [ ] Azure Container Registry contains the **eshoponweb/web** repository with **latest** tag
- [ ] All Azure resources are properly configured and communicating

## Critical Requirements ⚠️

**MANDATORY**: These exact values must be used for system compatibility:

- **Azure DevOps Project Name**: `eShopOnWeb` - Required for pipeline references
- **Work Item Process**: `Scrum` - Required for project configuration
- **Repository Source**: `https://github.com/MicrosoftLearning/eShopOnWeb.git` - Required for source code
- **Default Branch**: `main` - Required for pipeline execution
- **CI Pipeline File**: `/.ado/eshoponweb-ci-docker.yml` - Required for CI configuration
- **CD Pipeline File**: `/.ado/eshoponweb-cd-webapp-docker.yml` - Required for CD configuration
- **CI Pipeline Name**: `eshoponweb-ci-docker` - Required for identification
- **CD Pipeline Name**: `eshoponweb-cd-webapp-docker` - Required for identification
- **Resource Group**: `AZ400-RG1` (or your service connection resource group) - Required for resource organization
- **Container Repository**: `eshoponweb/web` - Required for container registry
- **Docker Image Reference**: `${acr.properties.loginServer}/eshoponweb/web:latest` - Required for App Service configuration
- **Bicep Templates**: `/infra/webapp-docker.bicep` and `/infra/webapp-to-acr-roleassignment.bicep` - Required for infrastructure
- **Role Assignment**: `AcrPull` - Required for container access

## Prerequisites

- Microsoft Edge or Azure DevOps supported browser
- Azure DevOps organization with appropriate permissions
- Azure subscription with Contributor or Owner role
- Microsoft account or Microsoft Entra account

## Your Challenge

You're tasked with implementing a complete CI/CD pipeline for a containerized .NET application. Here's what you need to accomplish:

### Phase 1: Environment Setup

Set up or make sure you have the eShopOnWeb project and repository. Make sure to configure the main branch as the default branch.

### Phase 2: CI Pipeline Implementation

Create a CI pipeline that:

- Builds a custom Docker image using the provided Dockerfile
- Deploys Azure Container Registry using Bicep templates
- Pushes the built image to Azure Container Registry with appropriate tags
- Handles Azure service connection permissions properly

### Phase 3: CD Pipeline Implementation

Create a CD pipeline that:

- Deploys Azure App Service using Bicep templates
- Configures proper role assignments for container access
- Deploys the containerized application to Azure App Service
- Ensures the web app can pull images from the container registry

### Phase 4: Validation

Ensure your deployed application is accessible and functioning correctly in Azure App Service.

**Estimated Time**: 20 minutes  
**Difficulty**: Intermediate

## Important Notes

- **Pipeline Permissions**: You must grant permission when pipelines request access to Azure resources - look for "This pipeline needs permission to access a resource" messages
- **Role Assignment Timing**: The role assignment for AcrPull may take time to propagate, which is why it's handled in a separate Bicep template

## Validation

How will you know you've succeeded:

- CI pipeline completes successfully and shows green status
- Azure Container Registry contains your Docker images with proper tags
- CD pipeline deploys without errors
- Azure App Service is running and accessible via browser
- eShopOnWeb application loads correctly in the browser
- All three Azure resources are present: App Service, App Service Plan, and Container Registry

## Resources

- [Azure DevOps Pipeline Tasks Reference](https://learn.microsoft.com/azure/devops/pipelines/tasks/reference/docker-v0?view=azure-pipelines)
- [Azure Container Registry Documentation](https://learn.microsoft.com/azure/container-registry/)
- [Azure App Service Documentation](https://learn.microsoft.com/azure/app-service/)
- [Azure Role-Based Access Control](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-list-portal)

---

_Remember: You have the skills to figure this out! Focus on understanding the pipeline structure and Azure resource relationships. The specific file paths and naming conventions are your roadmap to success._
