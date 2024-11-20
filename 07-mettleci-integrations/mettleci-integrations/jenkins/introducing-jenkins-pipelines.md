# Introducing Jenkins Pipelines

*   [Introduction](#introduction)
*   [Structure and Terminology](#structure-and-terminology)
*   [MettleCI Jenkins Components](#mettleci-jenkins-components)

# Introduction

A Jenkins Pipeline is a definition of an automated workflow enabled by a suite of Jenkins plugins (centred around the [Declarative Pipeline plugin](https://plugins.jenkins.io/pipeline-model-definition/)) which work together to support the implementation of continuous integration and deployment. A Pipeline provides an extensible set of tools for modelling your MettleCI delivery workflows *as code* using the Jenkins Pipeline domain-specific language (DSL) syntax, Groovy, and the MettleCI Command Line Interface.

A Jenkins Pipeline is most commonly defined in a plain text file called a **Jenkinsfile** which must be committed to a project’s source control Git repository. In this regard the Pipeline definition is treated as part of the application to be versioned and reviewed, just like your DataStage assets themselves. Pipelines can be triggered by one or more [user-configurable events](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2240610366/Pipeline+Trigger+Strategies).

# Structure and Terminology

![](./attachments/Jenkins%20Pipeline%20Structure.png)

**Pipeline:** A **Jenkins Pipeline** is a user-defined model of a CI/CD pipeline. A Pipeline’s code defines your entire build and deployment process, which typically includes steps for building, testing and then deploying an application.

**Reusable Pipeline:** A Shared Library is a separate file which contains definitions of one of more Custom Steps written in Groovy using [Jenkins Scripted Pipeline syntax](https://www.jenkins.io/doc/book/pipeline/#declarative-versus-scripted-pipeline-syntax). Read more about these [here](../jenkins/reusable-pipeline-templates-in-jenkins.md).

**Stage:** A **Stage** block defines a conceptually distinct subset of tasks performed through the entire Pipeline (e.g. "Build", "Test" and "Deploy" stages), which is used by many plugins to visualize or present Jenkins Pipeline status/progress.

**Step:** A single task which tells Jenkins what to do at a particular point in time. This may involve executing a shell command or copying a file, for example. This is also where the [MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/458850547/MettleCI+Command+Line+Reference) will be used to enact the tasks required of a DataStage CI/CD Pipeline.

A Jenkins Pipeline is executed by one or more **Nodes** which are hosts, with a [Jenkins Agent](https://www.jenkins.io/doc/book/using/using-agents/) installed, which is part of the Jenkins environment and is capable of executing one or more **Pipeline** **Steps**.

# MettleCI Jenkins Components

A `Jenkinsfile` can be written using two types of syntax - Declarative and Scripted. MettleCI provides an example Jenkinsfile (top-level pipeline) as a *Declarative* Pipeline definition, written using [Pipeline domain-specific language (DSL) syntax](https://www.jenkins.io/doc/book/pipeline/syntax) and enabled by the [Declarative Pipeline plugin](https://plugins.jenkins.io/pipeline-model-definition/). MettleCI also provides reusable components written as [Jenkins Groovy](https://www.jenkins.io/doc/pipeline/steps/workflow-cps/) methods and supplied in separate [Shared Library](https://www.jenkins.io/doc/book/pipeline/shared-libraries/) repository.

| **MettleCI Shipped Asset** | **Language** | **Description** |
| --- | --- | --- |
| `Jenkinsfile` | Jenkins Pipeline DSL syntax | Principal pipeline definition |
| `mci_ccmt.groovy` | Jenkins Scripted Pipeline syntax (Groovy) | [CCMT Upgrade process](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2178875414/MettleCI+DataStage+Upgrade+Pipeline#CCMT-Upgrade-of-Target) |
| `mci_compliance.groovy` | Jenkins Scripted Pipeline syntax (Groovy) | [Compliance process](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2178875414/MettleCI+DataStage+Upgrade+Pipeline#Compliance-Test-Warnings) |
| `mci_deploy.groovy` | Jenkins Scripted Pipeline syntax (Groovy) | [Deploy process](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2178875414/MettleCI+DataStage+Upgrade+Pipeline#5.-Deploy-Target-CI) |
| `mci_unittest.groovy` | Jenkins Scripted Pipeline syntax (Groovy) | [Unit Test processa](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2178875414/MettleCI+DataStage+Upgrade+Pipeline#Legacy-Unit-Test) |