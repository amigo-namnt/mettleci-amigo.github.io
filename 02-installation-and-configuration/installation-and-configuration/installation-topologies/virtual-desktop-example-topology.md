# Virtual Desktop Example Topology

An example topology for an environment using the following technologies:

*   Citrix desktop virtualisation
    
*   Atlassian Bitbucket Git repository
    
*   Atlassian Jira work item management platform
    
*   Jenkins build tool
    

![](./attachments/Citrix%20Topology.png)

# Components connections

| **#** | **Description** | **Access notes** |
| --- | --- | --- |
| 1   | The Citrix client running on your Developer Workstation presents a virtualised DataStage Designer client to your Developer | Dependent upon your Citrix configuration. See the [Citrix documentation](https://docs.citrix.com/en-us/tech-zone/build/tech-papers/citrix-communication-ports.html). |
| 2   | Depending upon your Citrix configuration, the MettleCI menu items in the virtualised DataStage client invoke the MettleCI Workbench interface in a virtualised browser window served by Citrix, or… | The browser running on your Citrix DataStage Client can access the MettleCI Workbench Service using a port that [you choose and configure](../../installation-and-configuration/installing-mettleci-workbench/customizing-your-mettleci-workbench-installation/configuring-mettleci-workbench-to-use-a-custom-port-number.md). |
| 3   | .. in a native browser window on your Developer Workstation. In either case this communicates (over ports you configure) with the MettleCI Workbench Service running on your DataStage Engine. | The browser running natively on your local machine can access the MettleCI Workbench Service using a port that [you choose and configure](../../installation-and-configuration/installing-mettleci-workbench/customizing-your-mettleci-workbench-installation/configuring-mettleci-workbench-to-use-a-custom-port-number.md). |
| 4   | Your work item management tool (e.g. Atlassian Jira) can be accessed from your Developer Workstation by configuring network access to the the relevant host ports. | The Jira user interface accessed from your browser [configured to use any port you wish](https://confluence.atlassian.com/adminjiraserver/changing-jira-application-tcp-ports-938847762.html). |
| 5   | Your Git tool (e.g. Atlassian Bitbucket) can be accessed from your Developer Workstation by configuring network access to the the relevant host ports. | Your Git tool is accessed using ports configured within that tool. For example, you can configure the ports for [Atlassian Bitbucket Server](https://confluence.atlassian.com/bitbucketserverkb/which-ports-does-bitbucket-server-listen-on-and-what-are-they-used-for-806029586.html). |
| 6   | Your build tool (e.g. Jenkins) can be accessed from your Developer Workstation by configuring network access to the the relevant host ports. | The Jenkins Controller and Agents communicate using [a set of default ports](https://www.jenkins.io/doc/book/security/services/) which can be modified through the [use of a reverse proxy](https://www.jenkins.io/doc/book/system-administration/reverse-proxy-configuration-with-jenkins/). |
| 7   | The virtualised DataStage Designer client running on Citrix will need regular access to DataStage Service and Engine tiers, as documented by IBM. | The DataStage Client tier running on your Citrix environment uses [standard IBM DataStage ports](https://www.ibm.com/docs/en/iis/11.7?topic=computers-configuring-your-network). |
| 8   | Your MettleCI Workbench will need network access to your Jira server to perform Work item lookup from the Workbench’s Git Commit page. | The Jira API uses the same as is used to access the Jira user interface from your browser, [whatever your organization has configured that to be](https://confluence.atlassian.com/adminjiraserver/changing-jira-application-tcp-ports-938847762.html). |
| 9   | Your MettleCI Workbench will need network access to your Bitbucket server to commit work to your Git repositories. | Workbench accesses your Git repositories using the references they publish - usually via HTTPS (port 443) or SSH (port 22). |
| 10  | The Jenkins Controller running on your Jenkins host will need network access to your Bitbucket instance to poll for, and retrieve, changes to your Git repositories | TBC |
| 11  | The Jenkins Controller running on your Jenkins host will need network access to the Jenkins Agent running on the MettleCI Agent Host. | The Jenkins Controller and Agents communicate with reach other using [a set of default ports](https://www.jenkins.io/doc/book/security/services/) which can be modified through the [use of a reverse proxy](https://www.jenkins.io/doc/book/system-administration/reverse-proxy-configuration-with-jenkins/). |
| 12  | The Jenkins Agent will require access to the Bitbucket repository in order to checkout newly-committed artefacts for deployment, as well as accessing the Compliance repository to fetch its constituent rules. | The Jenkins Agent accesses your Git repositories using the references they publish - usually via HTTPS (port 443) or SSH (port 22). |
| 13  | The Jenkins Agent, MettleCI CLI, and DataStage Client programs running on the MettleCI Agent Host will require network access to the DataStage Service and Engine tiers. | The DataStage Client tier running on your Citrix environment uses [standard IBM DataStage ports](https://www.ibm.com/docs/en/iis/11.7?topic=computers-configuring-your-network).<br><br>The MettleCI CLI will communicate with the DataStage host over SSH on your specified port. |