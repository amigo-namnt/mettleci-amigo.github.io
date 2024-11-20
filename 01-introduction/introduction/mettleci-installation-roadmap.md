# MettleCI Installation Roadmap

Follow these steps to get up and running with MettleCI as quickly and easily as possible with one of your existing DataStage Projects.

# 1\. Gather your required information

Note that before you proceed with MettleCI installation and configuration you should have the following information to hand:

*   Your DataStage settings (Engine and Service Tier endpoints and credentials)
    
*   Your Git settings (endpoint and public SSH key)
    
*   Your Work Item Management settings (endpoint and public SSH key)
    

Perhaps you’ll need to create your first project Git repository. This will depend upon the Git technology you use, and will be subtly different for GitHub, GitLab, Bitbucket, Azure DevOps, etc. Follow the instructions for your preferred system and ensure you capture the information.

MILESTONE**:** You’ve verified that you can connect to DataStage, Git, and Work Item Management using your credentials/SSH keys.

# 2\. Install MettleCI Workbench

Start by installing MettleCI Workbench on your DataStage development **Engine tier** host.

See our super-simple instructions for Engine tiers hosted on [Unix](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/455802915/Installing+Workbench+on+Unix) and [Windows](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/455770155/Installing+Workbench+on+Windows) platforms.

MILESTONE**:** You can log in to the MettleCI Workbench using your DataStage credentials.

# 3\. On-board your first DataStage project

**3a. Establish version control baseline**

Extract a whole-of-Project archive (`.isx`) containing **only** the design information. Do not include any *executables* (i.e. binaries) nor any *dependent items*. See IBM’s instructions on using the istool to perform ISX exports [here](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.iisinfsv.assetint.doc/topics/istoolexp.html).

Process the archive and check it into the corresponding Git repository by following the instructions for [Bulk Check-in Using MettleCI Command Shell and Git](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/457867443/Bulk+Check-in+Using+MettleCI+Command+Shell+and+Git).

**3b. Register the Project in MettleCI Workbench**

MettleCI Workbench uses a selected DataStage Project for its working context. A DataStage project needs to be registered with the Workbench before you can use MettleCI with it. Follow the instructions for [registering a DataStage Project with MettleCI Workbench](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/458555971/Registering+DataStage+Projects+With+Workbench).

MILESTONE**:** MettleCI Workbench can operate on the DataStage project, and it is listed in the drop-down project list at the top of the Workbench.

# 4\. Try MettleCI Compliance

**4a. Create your compliance rule Git repository**

Follow the steps required to [create your Compliance Rule Git repository](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/468680880/Setting+up+your+Compliance+Repository).

MILESTONE**:** You have an operational Git repository containing a set of template MettleCI Compliance Rules.

**4b. Execute Compliance against a DataStage Job**

Follow the steps to [execute compliance against a selected DataStage job](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/375357479/Improve+Code+Quality+using+Compliance).

Note that you’ll definitely get some Compliance failures with your first execution! At the very least expect the supplied Job and Stage naming standards to differ to yours!

MILESTONE**:** Compliance results for one of your DataStage jobs.

# 5\. Try MettleCI Unit Testing

**5a. Install the Parallel Unit Test Harness (if you use Parallel jobs)**

Follow the steps to [install the Parallel Unit Test harness](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/454393879/Installing+MettleCI+Unit+Test+Harness).

**5b. Create your first Unit Test**

Follow the steps to [configure your environment for Unit Testing](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/415105082/Configure+your+Environment+for+Unit+Testing), then [create your first Unit Test](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/375455793/Creating+a+Unit+Test).

You’ll then need to either [manually create Unit Test data](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/466387402/Manually+Editing+Unit+Test+Data), or [capture it from existing Unit Test data](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/437518414/Capturing+Existing+Unit+Test+Data), after which you can [execute your Unit Test](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/466387242/Executing+a+Unit+Test).

MILESTONE**:** You can use MettleCI Workbench to observe Unit Test results for your selected DataStage job.

> [!NOTE]
> **Now you’re ready to start exploring MettleCI!**