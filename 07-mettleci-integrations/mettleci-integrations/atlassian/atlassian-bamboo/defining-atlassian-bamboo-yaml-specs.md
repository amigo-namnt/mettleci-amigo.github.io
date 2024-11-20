# Defining Atlassian Bamboo YAML Specs

> [!WARNING]
> Note that this functionality is available in MettleCI Release 1.3 onwards.

*   [Configuring your Bamboo build environment](#configuring-your-bamboo-build-environment)
    *   [Prerequisite steps](#prerequisite-steps)
    *   [Create and Populate Repositories](#create-and-populate-repositories)
    *   [Link repositories to Bamboo](#link-repositories-to-bamboo)
    *   [Create some Shared Credentials](#create-some-shared-credentials)
        *   [SSH Credentials](#ssh-credentials)
        *   [Username and password](#username-and-password)
    *   [Identify Plan variables](#identify-plan-variables)
    *   [Register your DataStage project with Workbench](#register-your-datastage-project-with-workbench)
    *   [Create Bamboo Project](#create-bamboo-project)
*   [Configure your Bamboo specs build plans](#configure-your-bamboo-specs-build-plans)
    *   [Add Compliance repository to the project’s Bamboo Specs repositories](#add-compliance-repository-to-the-projects-bamboo-specs-repositories)
    *   [Grant access to the DataStage Asset repository from your Compliance repository](#grant-access-to-the-datastage-asset-repository-from-your-compliance-repository)
    *   [Allow project creation from DataStage Asset repository](#allow-project-creation-from-datastage-asset-repository)
    *   [Set DataStage Asset Repository as the Specs repository](#set-datastage-asset-repository-as-the-specs-repository)
*   [Deployment Plan](#deployment-plan)

# Configuring your Bamboo build environment

## Prerequisite steps

The instructions on this page depend upon the following prerequisite steps:

*   [Enable and download](https://confluence.atlassian.com/bamboo/bamboo-remote-agent-installation-guide-289276832.html) one or more Bamboo remote agents.
    
*   On your [Mettle Agent Host](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2327019539/The+Mettle+Agent+Host) …
    
    *   [Install the MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488898631), and
        
    *   Install one or more of your Bamboo remote agents.
        
*   Configure your Bamboo agents' [DataStage Capabilities](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability).
    

## Create and Populate Repositories

Start by [deploying the supplied repository template files](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/507019277/Deploying+MettleCI+repository+templates+to+your+Git+platform) to your selected Git hosting solution.

> [!INFO]
> **Note:**
> 1.  Bamboo specs will still work with Git platforms other than Atlassian Bitbucket.
>     
> 2.  The example pipelines supplied with MettleCI will not work with ‘local’ (filesystem-based) repositories.

## Link repositories to Bamboo

Next, you need to tell Bamboo where your code repositories (called [Linked Repositories](https://confluence.atlassian.com/bamboo/linking-to-source-code-repositories-671089223.html)) are located by selecting menu item **Bamboo Administration** → **Linked Repositories** → **Add Repository**.

Whether you elect to make the repository linkage available globally within your Bamboo installation, or whether you restrict the linkage to a specific plan, is a organizational decision. Both options will work. You can leave all **Advanced options** with their default values. You will [set up Bamboo spec scanning](https://confluence.atlassian.com/bamboo/enabling-repository-stored-bamboo-specs-938641941.html) in a later step, so leave that option unchecked for now.

## Create some Shared Credentials

Next, [create two sets of Bamboo Shared Credentials](https://confluence.atlassian.com/bamboo/shared-credentials-424313357.html) to protect access your Bamboo and DataStage resources:

### SSH Credentials

These credentials are used by your Bamboo Specs pipeline to deploy DataStage configuration and file system assets to a remote host.

Start by [creating an SSH key pair](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/457900052) (or identify an existing key pair you wish to use) then …

Select the menu item **Bamboo Administration** → **Overview** → **Shared credentials** → **Add new credentials** → **SSH**

Then …

1.  Enter an (arbitrary) name for your SSH credentials.
    
2.  Enter the private key from your SSH key pair in the **SSH Key** field.
    
3.  If you gave your SSH key pair a passphrase then enter it in the SSH Passphrase field.
    
4.  Configure your Git repository platform with the associated public key of your new key pair.
    
5.  For more background on the use of SSH keys within MettleCI see [SSH Configuration](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2396487711) and [Using SSH keys in MettleCI pipelines](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2377056265/Using+SSH+Keys+in+MettleCI+CI+CD+Pipelines).
    

### Username and password

These credentials authenticate an Information Server user and are used by your Bamboo Specs pipeline to deploy assets into a specified target DataStage project.

Select the menu item **Bamboo Administration** → **Add new credentials** → **Username and password**

Then …

1.  Enter an (arbitrary) name for your DataStage credentials.
    
2.  Enter the username and password of the Information Server account you want your Bamboo pipeline to use for interacting with your DataStage environments.
    

## Identify Plan variables

The example build plans shipped with MettleCI use a number of Plan variables which you will need to provide before you can use the examples on your environment. Bamboo Plan variables override any variables of the same name that have been established at the Global or Project levels.

| **Variable name** | **Example Value** | **Description** |
| --- | --- | --- |
| DomainName | `services-tier.myorganization.com:59445` | The URL and port of your DataStage services tier |
| ServerName | `engine-tier.myorganization.com` | The URL of your DataStage engine tier |
| EnvironmentID | `ci` | project suffix indicated the environment to be built |
| ProjectName | `myproject_${bamboo.EnvironmentID}` | your-datastage-project |
| ServerUsername | `ec2-user` | your-username-for-the-engine-tier-server |
| SshCredentials | IBM117<br><br>[Lance Short](https://datamigrators.atlassian.net/wiki/people/60496fdeb020eb006854724d?ref=confluence) can we choose a better value for this example? | your-bamboo-shared-credential-for-ssh |
| DatastageCredentials | DataStage v11.7 Test2<br><br>[Lance Short](https://datamigrators.atlassian.net/wiki/people/60496fdeb020eb006854724d?ref=confluence) can we choose a better value for this example? | your-datastage-login-shared-credentials |

## Register your DataStage project with Workbench

If you have not already done so, [register your DataStage project with your MettleCI Workbench instance](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2239201281/MettleCI+Workbench+Configure+First+Project), ensuring you connect the DataStage and Compliance repositories you established in the steps above.

## Create Bamboo Project

Create a Bamboo project in the normal way. Leave it empty for now but it is needed in the following steps.

# Configure your Bamboo specs build plans

Bamboo is capable of using [YAML-based pipeline definitions](https://confluence.atlassian.com/bamboo/bamboo-yaml-specs-938844479.html), examples of which ship with MettleCI. The files that comprise your Bamboo pipeline definition exist within a `bamboo-specs` directory in the root of your DataStage repository:

| **Name** | **Description** |
| --- | --- |
| bamboo.yml | A `bamboo.yaml` file is required to define build and deployment plans. Bamboo is looking for this file in the bamboo-specs directory. |
| PlanPermissions.yml | Added as an !include to `bamboo.yml` to define plan permissions |
| DeploymentPermissions.yml | Added as an !include to `bamboo.yml` to define deployment permissions |
| ContinuousIntegrationFull.yml | Added as an !include to bamboo.yml to define the build plan for continuous integraion |
| MyProjectDeployment\_QA\_PROD.yml | added as an !include to bamboo.yml to define the deployment plan and its enviornments |

> [!INFO]
> Note: There are other ways to structure this collection but by using includes for most everything, it makes it easy to first get your build plan working and then get your deploy plan working.

1.  Edit `bamboo.yml` to include only references to the `PlanPermissions.yml` and `ContinuousIntergrationFull.yml` files. If you are working from the supplied reference implementation, it may have more includes and you should (temporarily) remove them, they will be added back in a later step.
    

```
!include 'PlanPermissions.yml'
---
!include 'ContinuousIntegrationFull.yml'
```

2.  Replace the key and user values in `PlanPermissions.yml` with those appropriate to your environment. The key under `plan` is a composite of the project key and the plan key connected by a '-'
    

> [!INFO]
> Note that the entire file is not always shown in this and following excerpts.

```
plan:  
  key: MYYAM-CIFL
plan-permissions:
- users:  
  - lance
```

3.  Replace the plan and variable values in `ContinuousIntergrationFull.yml` with those appropriate to your environment.
    

```
plan:  
  project-key: MYYAM     # Links plan to it's parent project.  The key is specified when creating the project.  
  key: CIFL              # Unique plan identifier  
  name: Continuous Integration - Full
variables:                # Plan specific variables.  Overrides global and project variables with the same name.  
  DomainName: test2-svcs.datamigrators.io:59445  
  EnvironmentID: ci  
  ProjectName: myproject_${bamboo.EnvironmentID}  
  ServerName: TEST2-ENGN.DATAMIGRATORS.IO  
  ServerUsername: ec2-user  
  DatastageCredentials: &datastage_credentials Datatage v11.7 Test2     #anchor for Datastage shared credential variable substitution  
  SshCredentials: &ssh_credentials IBM117     # Anchor for SSH shared credential variable substitutionTesting a pipeline
```

4.  Replace ‘Static Analysis’ checkout repository value in `ContinuousIntegragtionFull.yml` with a reference to the Compliance Repository for your environment. You will use this value in a later step when linking repositories, so record it.
    

```
Static Analysis:    # Compliance Testing definitions
  key: SA 
  tasks:
   - clean
   - checkout:
       repository: Compliance_LS     # Name of compliance rules repository linked to the Bamboo project
       path: rules
       force-clean-build: true
       description: Checkout Compliance repository
```

5.  Replace repository entries to match your environment throughout
    

```
repositories:
- myproject:          # Linked repository of datastage assets. Note:permission must be granted to compliance repository
    scope: global
- Compliance_LS:      # Linked repository of compliance rules. Note:permission must be granted to datastage reposittory 
   scope: global
triggers:             # Definition of plan execution trigger
- polling:
    period: '30'
    description: RepoCheckin
    repositories:
    - myproject
```

6.  Add these two YAML files to the bamboo-specs directory of your DataStage assets repository.
    
7.  Commit your changes.
    

## Add Compliance repository to the project’s Bamboo Specs repositories

DO NOT ADD the DataStage Asset repository. We will do that differently in a later step that will trigger build creation. The name you choose here should match the one you used above.

Select the menu item **Project Settings >> Bamboo Specs repositories** then…

select your compliance repository and add it.

## Grant access to the DataStage Asset repository from your Compliance repository

1.  Go to **Administration >> Linked Repositories**
    
2.  Choose your Compliance Repository. (for example, `Compliance_LS`, the name you used above)
    
3.  Choose **Permissions** from the tabs.
    
4.  Scroll down to **Bamboo Specs repositories access**. Choose your DataStage Asset repository from the list. (for example, `myproject`)
    
5.  Click **Add**
    

## Allow project creation from DataStage Asset repository

1.  Go to **Administration >> Linked Repositories**
    
2.  Choose your DataStage Repository. (for example, `myproject`)
    
3.  Choose **Bamboo Specs** from the tabs.
    
4.  In the **Scan for Bamboo** Specs section, check **Allow Bamboo to scan this repository…** If you get a tutorial dialog you can close it or review the tutorial at this point.
    
5.  In the **Access** section, check **Project creation allowed**
    

## Set DataStage Asset Repository as the Specs repository

By default Bamboo will not look for Bamboo Specs in the Git repository until your explicitly tell it to do so.

1.  Select Specs from the top level menu, then go to  **Specs** >> **Set up Specs repository**. 
    
2.  Select your build project (for example, `MyProject`).
    
3.  Select **Previously** **linked repository**
    
4.  Choose your DataStage Asset repository from the list (for example, `myproject`)
    
5.  Click **Confirm**.
    

If all files are correct, this will trigger Bamboo to create/update and execute your build plan. Any subsequent commit of assets to your DataStage repository will trigger the same plan again.

If there is an error at this point, check your mail. You will receive a message with the error, and a link to the log. Most errors are self-explanatory.

Once you get past this point, the plan will appear in your project. It may not execute correctly, so you may still have some errors to correct.

We recommend that you get this plan to run correctly before you go on to the next step, setting up the deployment plan. This may take some debugging, which is out of scope for this document, but start with a careful review of the information you gathered and entered, as well as the error messages you received.

# Deployment Plan

Once your build plan is running correctly (and the CI DataStage project is getting correctly updated with newly committed changes) you will set up the Deployment Plan

1.  Go to **Create >> Create Deployment Project**
    
2.  Choose a name (for example, `MyProjectDeployment`). This name will be used in your YAML.
    
3.  Link to the build plan you created in the previous steps (`MyProject` → `Continuous Integration - Full`, for example). You can search for the plan by starting to type the name in Build plan drop down.
    
4.  Leave all other fields as defaulted.
    
5.  Click **Create deployment project**.
    
6.  From the configurations page Click **Bamboo Specs repositories**.
    
7.  **Add** your DataStage Asset repository from the drop down.
    
8.  Click Deployment configuration to return to the configuration page.
    
9.  Click **Edit Build Plan**.
    
10.  Click **Save deployment project**.
    
11.  Click **Source Build Plan** to return to your plan in the dashboard.
    
12.  Edit `bamboo.yml` to include `DeploymentPermissions.yml` and `MyProjectDeployment_QA_PROD.yml`. The order matters. Do not commit these changes yet, as doing so will cause this plan to run prematurely and generate an error.
    

```
!include 'PlanPermissions.yml'
---
!include 'DeploymentPermissions.yml'
---
!include 'ContinuousIntegrationFull.yml'
---
!include 'MyProjectDeployment_QA_PROD.yml'
```

12.  Replace deployment plan name and source-plan values in `MyProjectDeployment_QA_PROD.yml` with those appropriate to your environment from the earlier step.
    

```
deployment:
  name: Deployment for MyYamlTest
  source-plan: MYYAM-CIFL
```

13.  Replace name and user values in each section of the `DeploymentPermissions.yml`
    

```
version: 2
deployment: 
 name: Deployment for MyYamlTest
 
deployment-permissions:
- users:
  - lance
  ...
```

14\. Now that you have made changes in all the relevant files, commit them. The build plan will scan the YAML, then run (since it is triggered by any commit).  
  
If the scan fails, you will get a mail with information and a link to the log. Correct the issues. You may need to reenable the build plan and force a manual run.

Once the scan succeeds the deployment plan is set up and the environments are created. You can then manually run the deployment as needed for each environment defined in the deployment plan. Again, you may need to debug things and iterate as needed.