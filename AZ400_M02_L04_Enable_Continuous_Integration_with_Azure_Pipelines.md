# Challenge Lab: Enable Continuous Integration with Azure Pipelines

## Mission

Configure a complete CI/CD workflow using Azure DevOps pipelines with pull request validation and automated builds triggered by code changes.

## Learning Objectives

- Implement pull request validation using build pipelines
- Configure branch policies for code quality enforcement
- Set up continuous integration with YAML pipelines
- Work with build artifacts and build validation

## Success Criteria

- [ ] Pull requests require build validation and reviewer approval before merging
- [ ] CI pipeline automatically triggers on code changes to main branch
- [ ] Build artifacts are published and available for deployment
- [ ] Branch policies protect the main branch from direct commits

## Prerequisites

- Basic understanding of YAML and branching workflows

## Your Challenge

You need to transform a basic repository into a production-ready development environment with proper CI/CD practices. Here's what you must accomplish:

### Phase 1: Azure DevOps project Setup

Use the eShopOnWeb project and repository. Configure the main branch as the default and ensure the project structure is ready for pipeline implementation.

**MANDATORY**: These exact values must be used for system compatibility:
- **Azure DevOps Project Name**: `eShopOnWeb` - On Cloudslice a random number suffix is added to the project name, please use that one
- **Repository Source**: `https://github.com/MicrosoftLearning/eShopOnWeb.git` - Required for source code, should be already imported as `eShopOnWeb`
- **Default Branch**: `main` - Required for pipeline execution

### Phase 2: Pull Request Validation

Implement a system where no code can be directly committed to the main branch. All changes must go through pull requests that require both human approval and automated build validation.

**Key Components:**

- Import and configure the PR validation pipeline `/.ado/eshoponweb-ci-pr.yml`
- Set up branch policies with minimum reviewer requirements
- Configure build validation using the imported pipeline

### Phase 3: Continuous Integration

Set up an automated build system that triggers whenever changes are made to the web application code in the main branch. The system should build, test, and publish artifacts.

**Key Components:**

- Import and configure the CI pipeline `/.ado/eshoponweb-ci.yml`
- Enable automatic triggers for main branch changes
    - **Trigger Configuration**:
    ```yaml
    trigger:
      branches:
        include:
          - main
      paths:
        include:
          - src/web/*
    ```
- Ensure proper artifact publishing (Website and Bicep)

### Phase 4: Testing and Validation

Prove your implementation works by creating test branches, making code changes, and demonstrating that the pull request and CI workflows function correctly.

**Test Scenarios:**

- Create feature branches and test PR validation (**Test Branch Names**: `Feature01` and `Feature02`)
- Verify build triggers work correctly
- Confirm artifacts are published successfully

**Estimated Time**: 30 minutes
**Difficulty**: Intermediate

## Validation

How will you know you've succeeded:

- Direct commits to main branch are blocked
- Pull requests trigger the PR validation pipeline automatically
- PR validation includes build, test, and requires reviewer approval
- Merging PR to main triggers the CI pipeline automatically
- CI pipeline publishes both Website and Bicep artifacts
- Test file changes (adding/removing comments in Program.cs) demonstrate the full workflow
- Pipeline names match the required naming convention
- Branch policies enforce the minimum reviewer requirement

## Expected Artifacts

After successful completion, you should have:

- **Website artifact**: Published app ready for deployment
- **Bicep artifact**: Infrastructure templates for deployment
- **Two named pipelines**: `eshoponweb-ci-pr` and `eshoponweb-ci`
- **Protected main branch**: With policies preventing direct commits
- **Working PR workflow**: Demonstrating build validation and approval process

## Resources

- [Azure DevOps Pipeline Documentation](https://docs.microsoft.com/azure/devops/pipelines/)
- [Branch Policies Documentation](https://docs.microsoft.com/azure/devops/repos/git/branch-policies)
- [YAML Pipeline Reference](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema)
- [Create an Azure DevOps Organization](https://docs.microsoft.com/azure/devops/organizations/accounts/create-organization)

## Pro Tips

- The imported pipelines already contain the correct build tasks - focus on configuration and policies
- Branch policies are key to enforcing your CI/CD workflow
- Test your setup by actually making code changes and creating pull requests
- Pay attention to the trigger configuration in the CI pipeline - it should only trigger on web app changes
- Remember to rename pipelines after import for better identification
- Use the exact file paths and branch names specified in the critical requirements
- The "Allow requestors to approve their own changes" setting is necessary for single-user lab environments

## Troubleshooting Hints

- If builds aren't triggering, check your trigger configuration syntax
- If PR validation isn't working, verify the build policy is correctly associated with the pipeline
- If you can't complete PRs, ensure you've approved them and all validations have passed
- Pipeline artifacts should be visible under "Related > Published" after successful builds
