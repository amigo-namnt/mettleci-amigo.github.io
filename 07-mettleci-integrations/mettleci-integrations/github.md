# GitHub

![](./attachments/image-20200511-125210.png)

GitHub is a a subsidiary of Microsoft that provides hosting for software development version control using Git. It offers the distributed version control and source code management (SCM) functionality of Git, plus its own features. It provides access control and several collaboration features such as bug tracking, feature requests, task management, and wikis for every project.

> [!INFO]
> ## **Git ≠ GitHub**
> It’s still the case that some people use the terms **Git** and **GitHub** interchangeably so it’s important to understand that these are strongly related but critically different.
> **Git** is a version control system that lets you manage and keep track of your source code history. See [our page on Git integration](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/772898842/Git+and+MettleCI).
> **GitHub** is a commercial hosting service owned by Microsoft that provides a Git repositories as a SaaS solution. Microsoft also provide **GitHub Enterprise** which is a service equivalent to the SaaS offering which is installed on-premises in a customer’s data center.
> Watch [this short video](https://www.youtube.com/watch?v=wpISo9TNjfU) for a description of the differences between Git and GitHub.

### Ways MettleCI can integrate with GitHub

*   Commit to GitHub repositories
    
*   Source Compliance Rules from a GitHub repository
    
*   Perform a live issue lookup against GitHub issues when prompting a user performing a Git commit
    
*   Enable the creation of GitHub Actions workflows for Information Server
    
*   Provide Compliance, Unit Test, and Integration Test results as JUnit test reports
    
    *   Note that GitHub relies on open-source third-party libraries for its support for XUnit-based test results
        

* * *

## Detailed Integration Steps (under development)

*   [GitHub Authentication](./github/github-authentication.md)
*   [GitHub Pipelines](./github/github-pipelines.md)