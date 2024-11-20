# Automating project creation with the Azure API

The MettleCI Azure DevOps DataStage pipeline examples require the setup of Azure ‘Environments’ (some requiring Approval) and Variable Groups to store MettleCI and DataStage installation information.

When configuring Azure to run MettleCI pipelines, there is a choice to be made between two different approaches:

*   Create one project containing a repository for each MettleCI/DataStage project, requiring
    
    *   Create 1 Environment for each Continuous Integration, plus any other environments ending in Production, per Azure Project
        
    *   Configure permissions for each Azure project
        
*   Create a separate Azure project (with default repository) for each DataStage project
    
    *   Create 1 Environment for each Continuous Integration, plus any other environments ending in Production, shared between all pipelines in the Azure project
        
    *   Create 1 Repository per DataStage/MettleCI project
        

The latter approach requires far less setup and configuration, so that is the approach we will document here.

# Guides

*   [Prerequisites](#prerequisites)
*   [Creating an Approvers Group (optional)](#creating-an-approvers-group-optional)
*   [Create Environment](#create-environment)

# Prerequisites

To automate the required steps in Azure DevOps, you will require…

*   The Azure Command Line Interface (see Microsoft’s documentation for [Installation instructions](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli))
    
*   An Azure DevOps user and a Personal Access Token that provides the permissions required to create and update…
    
    *   Azure DevOps Projects
        
    *   Agents and Agent Pools
        
    *   Environments
        
    *   Repositories
        
    *   Variable Groups and Variables
        
    *   Pipelines
        

MettleCI ships with an example repository which includes practical examples of how you can use the Microsoft Azure Command Line Interface to automate the creation of all the environmental assets necessary to establish a working Azure DevOps pipeline using the capabilities of MettleCI. These assets include …

| **Azure DevOps Asset** | **Description** |
| --- | --- |
| Projects | The container for Azure DevOps repositories, boards, and pipelines. |
| Agents and Agent Pools | Agent pools can be created easily using the Azure DevOps UI. Neither the number of pools you create, or the names you give them, are relevant to your MettleCI-enabled pipelines as jobs are automatically assigned to agents by Azure DevOps based on the demands required by each of your pipelines' steps and the matching capabilities advertised by your agents.<br><br>The definition of Agents requires you to install one or more self-hosted Azure agents on a suitably equipped host (see [https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/windows-agent?view=azure-devops](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/windows-agent?view=azure-devops)) and associate the agent(s) with a relevant agent pool. |
| Environments | The creation of Deployment Environments is not currently supported by the Azure CLI. Environments are created by the supplied pipelines as they are references. i.e., if you try and run a MettleCI deployment to an environment called MyQualityAssurance then environment of that name will be automatically created. Once a deploy environment has been created (either manually using the Azure UI or automatically) you can then configure its 'Approvals and checks' to restrict deployment to that environment as required. |
| Repositories | You’ll need two repositories: One for your DataStage assets and one for your Compliance rules. We provide commands to create these and import the supplied examples. |
| Variable Groups | You’ll need a variable group for each DataStage platform you operate. Typically, this will be one Development environment and one Production environment, and perhaps a separate Quality Assurance environment if your organisation structures its platforms like that.<br><br>We provide commands to crate the variable groups and populate them with example variables required to execute the sample pipelines. Passwords are configured as ‘secret’ variables. If you wish these values to reside in an Azure Key Store you’ll need to modify the supplied example commands to achieve that. |
| Pipelines | We provide four example pipelines:<br><br>*   `devops-ci.yml` - A DevOps continuous integration pipeline intended to be triggered by the commit of a DataStage asset to your repository. This pipeline demonstrates the invocation of Compliance and Unit Testing functions and the deployment of code to downstream environments.<br>    <br>*   `hotfix-ci.yml` - A pipeline which performs CI testing (Compliance and Unit Test operations) on a hotfix-specific branch of your code.<br>    <br>*   `hotfix-deploy.yml` - A pipeline which deploys your current DataStage software configuration from a hotfix-specific code branch directly into your production environment.<br>    <br>*   `upgrade-ci.yml` - A special case pipeline used to CI test commits from one environment and promote them into an environment running a different version of DataStage, converting artifacts as required in the process. This is commonly employed to provide a pipeline between DataStage v11.5 and v11.7 environments during an upgrade initiative. |

# Creating an Approvers Group (optional)

The purpose of this group is to approve promotion of code into an official environment, e.g., Test, QA, Pre-Production, Production. MettleCI CI projects are internal (or “unofficial”) and requiring approval for those would be counterproductive.

If required, create an appropriate approvers group from the Azure DevOps management console.

In order to use this group to automatically create an approval against an environment, we need information about the group we plan to use.

```
$> az devops security group list --org <ORGANISATION_URL> --scope organization --query "graphGroups[?displayName=='<GROUP_NAME>'] | [0]"
{
  ...
  "originId": "<GROUP_ORIGIN_ID>",
  "principalName": "<GROUP_PRINCIPAL_NAME>",
  ...
}
```

Record these values for use later, where we refer to them as `<GROUP_ORIGIN_ID>` and `<GROUP_PRINCIPAL_NAME>`.

Add secret value variables to the group individually for `MCIPASSWORD` and `IISPASSWORD`

```
$> az pipelines variable-group variable create \
  --org <ORGANISATION_URL> \
  --project <PROJECT_NAME> \
  --group-id <GROUP_ID> \
  --name <VARIABLE_NAME> \
  --secret true \
  --value <VARIABLE_VALUE>
```

> [!INFO]
> We have observed instances in Azure DevOps where the secret value variable is created but the value is not assigned. In this case you will need to update the value manually in the Azure DevOps administration console.

# Create Environment

Creating an Environment is currently not supported by the Azure CLI, but can be achieved using the REST API. All environments need to be created: MettleCI CI environments, and ‘official’ environments, i.e. Test, QA, Production, etc.

1.  Encode the previously-created PAT as Base64. Note that the colon `:` inside the single quotes, before the PAT, is critical.
    
    ```
    $> echo -n ':<PERSONAL_ACCESS_TOKEN>' | base64
    ```
    
2.  Add the encoded value as part of the authorisation in the cURL header.
    
    ```
    $> curl POST \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Basic <ENCODED_COLON_THEN_PAT>' \
    'https://dev.azure.com/<ORGANISATION_NAME>/<PROJECT_NAME>/_apis/distributedtask/environments?api-version=5.0-preview.1' \
    -d '{"description":"<ENVIRONMENT_DESCRIPTION>","name":"<ENVIRONMENT_NAME"}'
    ```
    
    Record the `id` field from the result. This is used below as `<ENVIRONMENT_ID>`.
    
3.  If the environment requires approval, use `<ENVIRONMENT_NAME>`, `<ENVIRONMENT_ID>`, `<GROUP_ORIGIN_ID>` and `<GROUP_PRINCIPAL_NAME>` to fill out the information required for the body of the request.
    
    ```
    $> curl POST \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Basic <ENCODED_COLON_THEN_PAT>' \
    'https://dev.azure.com/<ORGANISATION_NAME>/<PROJECT_NAME>/_apis/pipelines/checks/configurations?api-version=7.1-preview.1' \
    -d '{"type":{"id":"8C6F20A7-A545-4486-9777-F762FAFE0D4D","name":"Approval"},"settings":{"approvers":[{"displayName":"<GROUP_PRINCIPAL_NAME>","id":"<GROUP_ORIGIN_ID>"}],"executionOrder":1,"blockedApprovers":[],"minRequiredApprovers":0,"requesterCannotBeApprover":false},"resource":{"type":"environment","id":"<ENVIRONMENT_ID>","name":"<ENVIRONMENT_NAME"}}'
    ```
    

> [!INFO]
> In the creation of an Approval for an Environment, the `type` section (`{"id":"8C6F20A7-A545-4486-9777-F762FAFE0D4D","name":"Approval"}`) contains a hard-coded `id` value. This is neither project- nor pipeline-specific, but is the internal id of the “Approval” class in Azure DevOps, and should be used verbatim as described here.