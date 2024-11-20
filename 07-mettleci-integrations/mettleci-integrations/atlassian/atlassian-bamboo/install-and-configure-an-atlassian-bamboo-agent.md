# Install and configure an Atlassian Bamboo Agent

When Bamboo needs to execute one or more MettleCI tasks (e.g. export from a DataStage Project), the following steps occur:

1.  MettleCI-relevant Bamboo Tasks will identify which version of a DataStage client or Engine they require
    
2.  Bamboo will allocate any available Bamboo [Agent](https://confluence.atlassian.com/bamboo/agent-289277442.html) that has been configured with the DataStage [Capability](https://confluence.atlassian.com/bamboo/agents-and-capabilities-289277114.html) for the required DataStage version.
    
3.  The Tasks will then execute on the allocated Agent.
    

> [!WARNING]
> If you are using Bamboo for the first time, we recommend that you start with Local Agents **only**.

MettleCI adds a DataStage Capability type to Bamboo's Agent Capabilities. Once this Capability is [configured](https://confluence.atlassian.com/bamboo/configuring-agents-289277172.html), you can add it to a Bamboo Agent. This, in turn, gives that Bamboo Agent the ability to be used by Bamboo Plans that require the DataStage Capability.

> [!CAUTION]
> You will not be able to use MettleCI until at least one Bamboo Agent is configured with a [DataStage Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability).

## Defining a DataStage Capability on the Bamboo Server (Local Agent)

Bamboo Server Capabilities are inherited by all Local Agents ([Defining a Bamboo Capability](https://confluence.atlassian.com/bamboo/defining-a-new-executable-capability-289277164.html)).

Before defining a DataStage Capability you must have [installed an IBM Information Server client](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.5.0/com.ibm.swg.im.iis.productization.iisinfsv.install.doc/topics/wsisinst_install_start_install_gui.html) and all relevant fix packs on the Bamboo Server.

**Steps**

1.  Click the **cog** icon in the Bamboo header and choose  **Overview**.
    
2.  Click **Server Capabilities** in the left navigation panel.
    
3.  Choose **Capability Type** > **DataStage** in the 'Add Capability' section at the end of the page.
    
4.  If you can't find the DataStage Capability type, check the add-on **MettleCI - DataStage Capability Plugin** (dm-Capability-plugin.jar) has been [https://datamigrators.atlassian.net/wiki/spaces/AET/pages/291733561](https://datamigrators.atlassian.net/wiki/spaces/AET/pages/291733561).
    
5.  In the **Install Label** field, type a name/label for this version of DataStage. MettleCI uses this name in the **Executables** dropdown list whenever a [MettleCI task is configured](../atlassian-bamboo/bamboo-tasks.md).
    
    **NOTE:** When setting the **Install Label**, we recommend following a **DataStage v<version number>** naming standard, for example, **DataStage v11.5**.  There is no need to distinguish between DataStage clients and engines, MettleCI Tasks automatically determine if they can run on a DataStage client, engine or both.
    
6.  In the **Path** field, type the path to the DataStage client "classic" folder or to the engine home directory (e.g. **'C:\\IBM\\InformationServer\\Clients\\Classic'** or **'/opt/IBM/InformationServer/Server/DSEngine'**).
    
7.  Click **Add**.
    

![](./attachments/DataStage%20Capability.png)

## Defining a DataStage Capability on a Remote Agent

An Agent-specific Capability applies to one Agent only. Before defining a DataStage Capability on a remote Agent, you must either:

*   [Install an IBM Information Server client](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.productization.iisinfsv.install.doc/topics/wsisinst_install_start_install_gui.html) and all relevant fix packs on the same box where you have an existing Remote Agent.
    
*   [Install a new Remote Agent](https://confluence.atlassian.com/bamboo/bamboo-remote-agent-installation-guide-289276832.html) on an existing DataStage engine tier. We recommend that you [install the Remote Agent as a Windows Service](https://confluence.atlassian.com/bamboo/additional-remote-agent-options-436044733.html).
    

While all MettleCI Professional tasks can use a DataStage client or engine during execution, most MettleCI enterprise tasks require a client.  When possible, we recommend using DataStage clients to prevent resource contention when the DataStage engine is executing heavy jobs and to provide maximum flexibly when using MettleCI enterprise tasks.

**Steps**

1.  Click the **cog** icon in the Bamboo header and choose  **Overview**.
    
2.  Click **Agents** in the left panel.
    
3.  Click the name of the required Agent.
    
4.  Click the **Capabilities** tab, and then **Add Capability** (to the right of 'Agent-Specific Capabilities').
    
5.  Choose **Capability Type** > **DataStage** in the 'Add Capability' section at the end of the page.
    
6.  If you can't find the DataStage Capability type, check the add-on **MettleCI - DataStage Capability Plugin** (dm-Capability-plugin.jar) has been [installed and is enabled](../atlassian-bamboo/atlassian-bamboo-mettleci-plugins-installation.md).
    
7.  In the **Install Label** field, type a name/label for this version of DataStage. MettleCI uses this name in the **Executables** list whenever a [MettleCI task is configured](../atlassian-bamboo/bamboo-tasks.md).
    
    **NOTE:** When setting the **Install Label**, we recommend following a **DataStage v<version number>** naming standard, for example, **DataStage v11.5**.  There is no need to distinguish between DataStage clients and engines, MettleCI Tasks automatically determine if they can run on a DataStage client, engine or both.
    
8.  In the **Path** field, type the path to the DataStage client "classic" folder or to the engine home directory (e.g. **'C:\\IBM\\InformationServer\\Clients\\Classic'** or **'/opt/IBM/InformationServer/Server/DSEngine'**).
    
9.  Click **Add**.
    

![](./attachments/DataStage%20Capability.png)