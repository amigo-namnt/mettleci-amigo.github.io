# GitLab

![](./attachments/image-20200511-041320.png)

GitLab is a web-based DevOps lifecycle tool that provides a Git-repository manager providing wiki, issue-tracking and continuous integration, and continuous deployment pipeline features, using an open-source license, developed by GitLab Inc. That is, it is a git repository, an issue manager, and an application lifecycle manager. This is similar to Azure Devops, but dissimilar from Jenkins, which is only an application lifecycle manager.

## Ways MettleCI can integrate with GitLab

#### GitLab as a git repository

*   Commit DataStage assets to GitLab repositories
    
*   Source Compliance Rules from a GitLab repository
    
*   Source DataStage assets during pipeline execution
    

#### GitLab as an issue management system

*   Perform a live issue lookup when prompting a user performing a Git commit
    

#### GitLab as an application lifecycle manager

*   Enable sophisticated CI/CD GitLab Pipelines for Information Server via the [MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408354840/MettleCI+CLI+Operating+Modes)
    
*   Provide Compliance, Unit Test, and Integration Test results as GitLab-compatible [JUnit test reports](https://docs.gitlab.com/ee/ci/junit_test_reports.html)
    

You do not need to use all 3 major roles of GitLab, and which of the detailed integration steps you need to execute depends on which role(s) you are using it for.

* * *

## Detailed Integration Steps

*   [Setting up a GitLab Project/Repository](./gitlab/setting-up-a-gitlab-projectrepository.md)
*   [Configuring MettleCI Workbench SSH Authentication to GitLab](./gitlab/configuring-mettleci-workbench-ssh-authentication-to-gitlab.md)
*   [Integrating GitLab Issue Lookup with MettleCI Workbench](./gitlab/integrating-gitlab-issue-lookup-with-mettleci-workbench.md)
*   [Automating project creation with the GitLab API](./gitlab/automating-project-creation-with-the-gitlab-api.md)

## See also

*   [Generic MettleCI Pipeline Description](#)
    
*   [MettleCI Example Pipeline for DevOps](#)
    
*   [MettleCI Example Pipeline for Upgrades](#)