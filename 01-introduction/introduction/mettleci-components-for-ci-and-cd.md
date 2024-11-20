# MettleCI Components for CI and CD

![](./attachments/MettleCI%20Conceptual%20Components.png)

# Relevant Components

*   **Work Item Management Tool:** A third-party system to organize units of work. 
    
*   **Git Platform:** A collaborative platform for tracking changes in source code during software development.
    
*   **CI/CD Build Tool:** Tools that automate the creation, and the limited testing, of executable applications from source code.
    
*   **MettleCI Workbench:** A browser-based user interface which is served from a lightweight agent, typically (but not necessarily) installed on the Customer’s DataStage Engine tier.
    
*   **CI/CD Build Agent:** One or more utilities supplied by the Customer’s build tool vendor to permit the integration of third-party systems (such as MettleCI) with the build tool.
    
*   **DataStage:** Customer’s development instance of Information Server, which may be deployed in any topology (SMP, Grid, HA) on any number of hosts.
    
*   **MettleCI Command Line Interface (CLI):** A suite of automated build and deployment utilities which provide a host of useful functionality to automated the deployment, testing, and execution of your DataStage solutions, accessible using a command line, either manually by a human or as part of a build plan executed by a Build tool.
    
*   **MettleCI Unit Test Harness:** An agent integrated into Customer’s DataStage Engine which selectively modifies DataStage job definitions at runtime to provide data interception and unit test execution capabilities.
    

# Relationships

1.  Work items in the user’s Work Item Management platform (Jira, ServiceNow, etc.) will be associated to Commits in the user’s Git platform (Bitbucket, GitHub, etc.) using capabilities native to those two platforms.
    
2.  The MettleCI Workbench supports searching work items in supported Work Item Management platforms for including as references in Git commit messages.
    
3.  The MettleCI Workbench will perform commits to the user’s Git platform.
    
4.  The MettleCI Workbench will be invoked from the user’s DataStage Designer client and will receive updates from the MettleCI Unit Test Harness.
    
5.  Commits to the user’s Git platform will trigger the invocation of a *build pipeline* in the user’s build platform.
    
6.  Pipelines often begin by establishing the environments, resources, and preconditions required to execute an integration test or deployment.
    
7.  Pipelines will need to perform scripted DataStage-related operations, such as export, import, compile, and test project assets.
    
8.  A user’s build tool will use one or more *build agents* to perform activities on remote resources.
    
9.  MettleCI provides a comprehensive command line interface which enables those build agents to perform DataStage-related operations.
    
10.  MettleCI’s command line uses DataStage client libraries and tools to provide some of its capabilities.
    
11.  The build pipeline will likely also orchestrate the execution of non-DataStage operations, such as functional test operations, for example.
    
12.  These non-DataStage operations will also utilize build agents to manage the invocation of functionality…
    
13.  …on systems providing access to the relevant testing capabilities.
    
14.  Pipelines often need to perform clean up operations on completion, such as publishing artefacts and removing temporary resources created as a by-product of the build activity.
    

# See also

*   [What is Git?](https://www.atlassian.com/git/tutorials/what-is-git)
    
*   [What is Continuous Integration?](https://www.atlassian.com/continuous-delivery/continuous-integration-intro)