# Azure DevOps Deployment Topology

# In-scope Hosts/Servers

**Developer's Workstation:** Where the Windows DataStage Designer client is typically run

**Azure DevOps:** An instance of Microsoft Azure DevOps, running either on-premises (known as "Azure Server") or as a service on Microsoft Azure ("Azure Services")

**Information Server Development Environment:** Your development instance of Information Server, which may be deployed in any topology, and on any number of hosts.

**Information Server Test Environment(s):** Downstream Information Server environments sitting between Development and Production.

**MettleCI Host:** A MettleCI-dedicated Windows-based DataStage Client tier used by your Azure Agent, in conjunction with the MettleCI Command Line Interface, to automate build and deployment activities.

# Connections

![](./attachments/MettleCI%20Topology%20(Azure%20DevOps).png)

| **Connection** | **Description** | **Notes** |
| --- | --- | --- |
| 1   | The MettleCI Workbench application running on your DataStage Engine tier needs to...<br><br>1.  perform a dynamic lookup of Work items when displaying the Git Commit page.<br>    <br>2.  commit to your Git platform | See:<br><br>*   [Configuring MettleCI Workbench SSH Authentication to Azure DevOps](../../azure-devops/azure-git-repositories/configure-mettleci-workbench-authentication-to-azure-git-repo.md)<br>    <br>*   [Integrating Azure DevOps Work Item Lookup with MettleCI Workbench](../../azure-devops/azure-work-item-management/integrating-azure-devops-work-item-lookup-with-mettleci-workbench.md) |
| 2   | The Developer Workstation provides data engineers with access to the Azure user interface via a supported web browser. | This is a standard browser interface, and requires no MettleCI-specific configuration.See the following links:<br><br>*   [Supported browsers and devices for Azure portal (Microsoft](https://docs.microsoft.com/en-us/azure/azure-portal/azure-portal-supported-browsers-devices))<br>    <br>*   [Navigating within the web portal (Microsoft](https://docs.microsoft.com/en-us/azure/devops/project/navigation/?view=azure-devops)) |
| 3   | Your Azure Pipelines perform their duties via an agent installed on the MettleCI-dedicated DataStage Client. | See<br><br>*   [Install and configure an Azure DevOps self-hosted agent](../azure-pipelines/install-and-configure-an-azure-devops-self-hosted-agent.md)<br>    <br>*   [Deploy an Azure Pipelines agent on Windows (Microsoft)](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-windows?view=azure-devops#permissions) |
| 4   | The Developer Workstation provides a DataStage client tier with access to the development environment's DataStage Engine and Services tiers. | The Developer Workstation and MettleCI Host (used to execute Azure Pipelines) both require identically-configure access to each DataStage platform with which it will communicate.<br><br>See:<br><br>*   [Configuring your network (IBM](https://www.ibm.com/docs/en/iis/11.7?topic=computers-configuring-your-network))<br>    <br>*   [Configuring MettleCI Workbench to use a Custom Port Number](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/588972035/Configuring+MettleCI+Workbench+to+use+a+Custom+Port+Number)<br>    <br>*   [Configuring the MettleCI Workbench to use HTTPS](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/458556297/Configuring+MettleCI+Workbench+to+use+HTTPS)<br>    <br><br>Note that if your plan to deploy to Production requires a MettleCI Host in a separate network zone you might be interested in adopting [a multi-agent topology](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1766817793/Using+Multiple+MettleCI+Agents#Separate-MettleCI-Agent-Hosts-per-network-zone). |
| 5   | The MettleCI Host requires regular access to the development environment's DataStage Engine and Services tiers, identical to that of Developer Workstations. |
| 6   | The MettleCI Host requires regular access to the downstream test environments' DataStage Engine and Services tiers, to affect automated deployment. |