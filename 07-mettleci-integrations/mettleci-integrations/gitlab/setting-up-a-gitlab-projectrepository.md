# Setting up a GitLab Project/Repository

MettleCI works with assets that are kept in Git repositories, notably the repository associated with a DataStage project and the repository associated with the compliance rules. Achieving a usable MettleCI instance includes the configuration of these repositories within GitLab. **Note:** GitLab differs from similar tools in its application of meanings to common terms.

> [!INFO]
> [Avoiding confusion over common terms in GitHub, Bitbucket, and GitLab](https://about.gitlab.com/blog/2017/09/11/comparing-confusing-terms-in-github-bitbucket-and-gitlab/#:~:text=In%20GitHub%2C%20repositories%20contain%20the,%2C%20milestones%2C%20and%20much%20more)
> Despite Git being a well established standard, different vendors' Git-based version control systems can use terminology like Repository and Project differently, creating the potential for confusion.
> In other platforms such as GitHub and Bitbucket, “repositories” contain the Git code repository along with other project-related assets such as issues, contribution metrics, etc. However the Git**H**ub community often uses the terms repository and project interchangeably. In Git**L**ab, the overarching container is called a [Project](https://docs.gitlab.com/ee/user/project/). A Project includes the Git repository, issues, merge requests, milestones, and more.
> It's important to make this distinction because you import a Project in GitLab, regardless of whether that is called a Repository elsewhere. In GitLab, the Repository is a component part of a Project. Thus, GitLab tightly couples project and repository, and each project may have only one Git repository.

**Note:** One may keep MettleCI Compliance rules in the same repository as the DataStage assets but it’s generally recommended that a repository be dedicated to those Compliance rules intended for use by multiple pipelines (across all your DataStage-related GitLab projects). That means GitLab pipelines must be configured to explicitly clone that Compliance repository so it’s available when the pipeline reaches the Compliance execution step. The example GitLab pipeline provided with MettleCI reflects this dependency.

Because the details of how to create and manage projects vary among GitLab releases, we speak in general terms only, and note MettleCI specific considerations.

# Steps

1.  Create a blank GitLab project by selecting **new project** from your GitLab dashboard, or visiting http://your.gitlab.server/projects/new. The recommended practice is to create a new GitLab project for each DataStage project, plus one for your Compliance rules. You may want to collect your GitLab projects into [groups](https://docs.gitlab.com/ee/user/group/index.html#groups). See [https://docs.gitlab.com/ee/user/project/](https://docs.gitlab.com/ee/user/project/) for more information on projects.
    
2.  [Clone the empty repository](https://docs.gitlab.com/ee/user/project/repository/#clone-a-repository) to somewhere convenient, such as your local DataStage client machine. Create a [README](https://docs.gitlab.com/ee/user/project/repository/#readme-and-index-files) file in the root folder of the repository which ensures the repository is initialized, has a default branch, and can be cloned. A sample README file is supplied in the template repository supplied with MettleCI.
    
3.  For integration with MettleCI Workbench, with CI/CD pipelines, and with external entities (such as code authoring systems) in general, you will need to set up access to the repository associated with the project.
    
    1.  Decide what credentials type you will use: userid/password, userid/PAT, deploy keys (a kind of SSH key) or regular SSH. SSH is recommended and this page has more details on why: [Configuring MettleCI Workbench SSH Authentication to GitLab](../gitlab/configuring-mettleci-workbench-ssh-authentication-to-gitlab.md)
        
    2.  If following the above recommendation, create a public/private key pair and then add it to the project. See[Adding public keys to GitLab](#) for more details.
        
4.  Set up access between GitLab and the MettleCI Workbench service (typically running on your DataStage Engine host)
    
    1.  Obtain the “clone URL” for the project
        
    2.  Configure the project in MettleCI Workbench. Refer to [MettleCI Workbench Configure First Project](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2239201281/MettleCI+Workbench+Configure+First+Project) for instructions.
        
    3.  Test this setup by using MettleCI Workbench to run a Compliance check (confirming read-only access to Compliance) and perform a commit to the repository (confirming write access to the Project repository).
        
5.  Set up access between GitLab and your build server. The easiest way to do this is to create a (project-specific or public) [deploy key](https://docs.gitlab.com/ee/user/project/deploy_keys/). Public keys can be used across multiple GitLab projects, once the project administrator grants access, while private keys only grant access to one project. You can also use a [deploy token](https://docs.gitlab.com/ee/user/project/deploy_tokens/) instead.
    
    1.  This page, while targeted at MettleCI Workbench setup, also covers how to create Deploy **keys** ([Configuring MettleCI Workbench SSH Authentication to GitLab](../gitlab/configuring-mettleci-workbench-ssh-authentication-to-gitlab.md) ). They are created the same way you create other SSH keys, and are actually a pair of keys, public and private.
        
    2.  Once you have a deploy key you will place the public part in the http://your.gitlab.server/your\_project/-/settings/repository repository portion of the project settings page.
        
    3.  Deploy tokens are generated for you by GitLab via the same project repository settings page and you must record them for later use. You only get a single opportunity to view them during the setup process. This makes them both more secure and less convenient than deploy keys, which are retained on the file system of the machine communicating with GitLab. See [GitLab deploy tokens](https://docs.gitlab.com/ee/user/project/deploy_tokens/) for more information.