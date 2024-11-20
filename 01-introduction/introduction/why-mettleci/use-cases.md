# Use Cases

For teams building solutions with IBM Information Server, Data Migrators' MettleCI fulfils two principal roles, both characterised by high levels of automation:

*   Enabling Agile DevOps with DataStage, and
    
*   Facilitating the rapid upgrade of a DataStage environment (whether to DataStage v11.7 or to one of the Cloud Pak for Data self-hosted or SaaS offerings) and leaving behind, in its wake, a suite of test cases which support the DevOps use case.
    

## DevOps

MettleCI dramatically improves a solution governance, quality, transparency, and team productivity by removing all the intense manual effort in shepherding DataStage artefacts through the processes and environments supporting a customer’s SDLC. Code review, testing, version control, and deployment are all handled in the background by push-button processes.

## Upgrade

IBM's Rapid DataStage Upgrade is a combined software-and-services offering which addresses these anxieties using well proven, automation-driven tools and techniques:

*   A no-charge online upgrade assessment which performs a detailed, automated analysis of DataStage solutions to identify and quantify any potential impediments to an upgrade process
    
*   Automation of the upgrade steps, including the creation of a full regression test suite, enabling integration testing within days
    
*   Repeatable processes, supporting a project-by-project go-live through continuous integration and deployment.
    
*   Flexible month-by-month subscription to the offering's software and elite services
    
*   This offering minimizes or eliminates code freezes and downtime while re-assuring both developers and budget-holders with frequent, highly-visible progress.
    

# How does it do this?

The MettleCI features supporting these two use cases are:

*   Static code analysis, optionally enforcing your solution’s compliance with a supplied library of fully customisable and extensible Information Server best practices
    
*   Automated unit testing, featuring the ability to auto-provision test data by either intercepting existing job test data, of using MettleCI’s data fabrication engine
    
*   Full integration will **all available** variations of Git repository
    
    *   Dynamic lookup of work items in a work item repository (currently Atlassian Jira, Azure DevOps, and Service Now)
        
    *   Automated association of DataStage artefacts and work items for all Git Commits
        
*   An extensive library of Continuous Integration (CI) and Continuous Deployment (CD) components which are available through a set of build system-specific user interfaces, or a product-agnostic command line interface. These interfaces can be used to construct CI/CD pipelines in any popular build and deployment platform.
    
    *   Atlassian Bamboo
        
    *   GitHub
        
    *   GitLab
        
    *   Jenkins
        
    *   Microsoft Azure DevOps
        
    *   Others (CircleCI, Pivotal, etc.) are supported via the MettleCI Command Line Interface.