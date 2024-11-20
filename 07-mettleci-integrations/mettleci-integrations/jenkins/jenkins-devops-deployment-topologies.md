# Jenkins DevOps Deployment Topologies

*   [Topology Components](#topology-components)
*   [Topology Connections](#topology-connections)
*   [Using Multiple Engines and Multiple Jenkins Agents](#using-multiple-engines-and-multiple-jenkins-agents)

# Topology Components

**Jenkins Host:** Where the Jenkins controller (providing build/deploy services as part of ALM) is run

**Application Lifecycle Management Tools:** One or more hosts running Work Item Management, and Git services

**Developer's Workstation:** Where the Windows DataStage Designer client is typically run

**Information Server Development Environment:** Your development instance of Information Server, which may be deployed in any topology, and on any number of hosts.

**Other Information Server Environment(s):** Downstream Information Server environments, including testing and (optionally) Production. These environments can be MettleCI deployment targets without requiring the deployment of any MettleCI components.

**MettleCI Agent Host:** A MettleCI-dedicated Windows server hosting an IBM DataStage Client tier which is used by your Build system's agent, in conjunction with the MettleCI Command Line Interface, to automate build and deployment activities.

# Topology Connections

The following high-level MettleCI architecture shows the key software components to be installed, and their communications between hosts. 

![](./attachments/MettleCI%20Topology%20(Jenkins).png)

> [!NOTE]
> The above diagram is one possible configuration, and is presented as an example only.

1.  The MettleCI Workbench application running on your DataStage Engine tier needs to perform a dynamic lookup of Work items when displaying the Git Commit page.
    
2.  The MettleCI Workbench application running on your DataStage Engine tier needs to commit to your Git platform.
    
3.  The Jenkins Host and your Git repository need to communicate in order to configure Git commits to automatically trigger Jenkins pipelines. Jenkins then needs access to your Git repository to source the artefacts for build and deployment. The Jenkins pipeline definitions ('Jenkinsfiles') are themselves stored and managed in a Git repository.
    
4.  The Developer Workstation provides data engineers with access to your ALM tools' user interfaces via a supported web browser.
    
5.  The Developer Workstation provides data engineers with access to your Jenkins user interfaces via a supported web browser.
    
6.  The Developer Workstation provides a DataStage client tier with access to the development environment's DataStage Engine and Services tiers.
    
7.  Your Jenkins pipeline perform their duties via an agent installed on the MettleCI Host. (Read about [Jenkins ports and services here](https://www.jenkins.io/doc/book/security/services/#:~:text=The%20web%20UI%20served%20via,by%20default%20on%20port%208080.))
    
8.  The MettleCI Host requires regular access to the development environment's DataStage Engine and Services tiers, identical to that of Developer Workstations.
    
9.  The MettleCI Host requires regular access to the downstream test environments' DataStage Engine and Services tiers, to affect automated deployment.
    

# Using Multiple Engines and Multiple Jenkins Agents

In real-world scenarios it’s possible that security restrictions or network zoning prohibit a single **MettleCI Agent Host** from communicating with DataStage environments across development, testing, and production domains. In this case you may need to consider a deployment topology using multiple Jenkins Agents, each running on a dedicated MettleCI Agent Host.

The diagram above (explained in more detail on [this page](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1766817793/Using+Multiple+MettleCI+Agents)) describes how you might deploy Jenkins Agents in complex multi-environment DataStage topologies.

This is by no means the only way to support multiple DataStage environments, but is certainly one of the easiest solutions to understand and maintain.