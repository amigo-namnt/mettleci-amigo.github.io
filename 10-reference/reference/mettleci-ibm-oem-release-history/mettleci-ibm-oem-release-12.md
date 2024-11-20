# MettleCI IBM OEM Release 1.2

*   [Package Summary](#package-summary)
*   [Package Contents](#package-contents)
*   [Change Log](#change-log)
    *   [Significant New Features](#significant-new-features)
    *   [New and Deprecated MettleCI Compliance Rules](#new-and-deprecated-mettleci-compliance-rules)
    *   [Fixes](#fixes)
        *   [MettleCI Foundations](#mettleci-foundations)
        *   [MettleCI Workbench](#mettleci-workbench)
        *   [MettleCI Unit Test Harnesses](#mettleci-unit-test-harnesses)
        *   [MettleCI Command Line Interface](#mettleci-command-line-interface)
*   [Upgrade Process](#upgrade-process)
*   [Known Issues](#known-issues)
*   [Notes](#notes)

# Package Summary

|     |     |
| --- | --- |
| **Package name** | MettleCI v1.2.0 Multiplatform English |
| **Release Date (yyyy-mm-dd)** | 2023-11-29 |
| **IBM Part Number** | M0F85EN |

# Package Contents

> [!NOTE]
> This release also bundles **S2PX v.1.2**.
> See [this page](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2532245522) for detailed release notes for S2PX.

This MettleCI v1.2 package contains a complete set of MettleCI and S2PX assets which give you everything you need to get up and running with these tools. You do **not** need to install any previous MettleCI or S2PX releases to use this package.

```
.
└── Software
    ├── CLI
    │   ├── dm-mettleci-command-shell-1.1-255-dist.zip
    │   └── dm-mettleci-command-shell-1.1-255.noarch.rpm
    ├── License
    │   ├── mettleci.lic
    │   └── properties.txt
    ├── Repositories
    │   ├── dm-compliance-rules-278.zip
    │   └── mettleci-repo-template-73.zip
    ├── S2PX
    │   ├── dm-s2px-analysis-plugin-1.0-134.jar
    │   └── dm-s2px-conversion-plugin-1.0-628.jar
    ├── Unit Test Harness
    │   ├── dm-server-unit-test-harness-routine-1.3-464.zip
    │   ├── dm-unittest-harness-1.3-464-setup.exe
    │   └── dm-unittest-harness-1.3-464.noarch.rpm
    └── Workbench
        ├── dm-mettleci-workbench-1.2-1701-setup.exe
        └── dm-mettleci-workbench-1.2-1701.noarch.rpm

```

| **Function** | **File** | **Notes** |
| --- | --- | --- |
| Command Shell | `dm-mettleci-command-shell-1.1-255-dist.zip` WINDOWS<br><br>`dm-mettleci-command-shell-1.1-255.noarch.rpm` UNIX | These operating system-specific [MettleCI Command Shell](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2216886273/MettleCI+Command+Line+Interface) distributions each include a full set of the latest versions of all [MettleCI CLI plugins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2125725711/CLI+Plugins). |
| Compliance Rules | `dm-compliance-rules-278.zip` ALL PLATFORMS | A ready-to-deploy Git repository containing all the MettleCI sample [Compliance Rules](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2213085185/MettleCI+Compliance+Rules+Reference). |
| Template Git Repositories | `mettleci-repo-examples-73.zip` ALL PLATFORMS | Contains two example Git repositories:<br><br>*   `jenkins-mci-shared-libraries.zip` (ALL PLATFORMS) containing example [Jenkins Reusable Pipeline Components](#).<br>    <br>*   `mettleci-repo-template.zip` (ALL PLATFORMS) containing example CI/CD pipeline definitions for…<br>    <br>    *   [GitHub](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741376173/GitHub)<br>        <br>    *   [GitLab](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741244932/GitLab)<br>        <br>    *   [Jenkins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/731709604/Jenkins)<br>        <br>    *   [Microsoft Azure DevOps](#).<br>        <br><br>> [!NOTE]<br>> **Unsupported Examples**<br>> Note that despite being fully tested with their respective CI/CD software, these assets are supplied without warranty or support and are provided to serve as examples of how you can use the MettleCI Command Line Interface to construct your own build and deployment pipelines to meet your unique requirements. |
| License | `mettleci.lic` ALL PLATFORMS<br><br>`properties.txt` ALL PLATFORMS | The MettleCI license file (valid to the end of 2099) required to enable MettleCI functionality, along with a human-readable properties file describing the license constraints.<br><br>> [!NOTE]<br>> **Licence Update**<br>> If you download this MettleCI Release package v1.2 from IBM Passport Advantage (or a similar IBM site **excluding Fix Central**) then it includes a full IBM OEM MettleCI license file. |
| Server Unit Test Harness | `dm-server-unit-test-harness-routine-1.3-464.zip`  ALL PLATFORMS | The MettleCI [Server Job Unit Test Harness for installation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/455737424/Installing+or+Upgrading+the+Server+Job+Unit+Test+Harness) on your DataStage Engine. |
| Parallel Unit Test Harness | `dm-unittest-harness-1.3-464-setup.exe` WINDOWS<br><br>`dm-unittest-harness-1.3-464.noarch.rpm` UNIX | The MettleCI [Parallel Job Unit Test Harness for installation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/455868494/Installing+or+Upgrading+the+Parallel+Job+Unit+Test+Harness+on+Unix) on your Unix (`.rpm`) or Windows (`.exe`) DataStage Engine. |
| Workbench | `dm-mettleci-workbench-1.2-1701-setup.exe` WINDOWS<br><br>`dm-mettleci-workbench-1.2-1701.noarch.rpm` UNIX | The [MettleC Workbench Service](#). |
| S2PX | `dm-s2px-analysis-plugin-1.0-134.jar` ALL PLATFORMS<br><br>`dm-s2px-conversion-plugin-1.0-628.jar` ALL PLATFORMS | Two [MettleCI CLI Plugins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2125725711/CLI+Plugins) which perform [pre-conversion analysis](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2080440325/Running+S2PX+Analysis) of a DSX containing Server Jobs and the [Server-to-Parallel conversion](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2080440348/Running+S2PX+Conversion) of an ISX containing Server Jobs. See [http://s2px.mettleci.io](http://s2px.mettleci.io/) for more details. |

# Change Log

## Significant New Features

*   Support for [signed commits](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/790659097/Signed+Commits) on Git platforms that support this functionality.
    
*   Introduction of [Compliance tagging](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2472050689/Compliance+Rule+Tags)
    
*   Updated release of Azure and Jenkins pipeline examples incorporating demonstration of how to manage Production Hotfixes.
    
*   More new Compliance rules (details below)
    

## New and Deprecated MettleCI Compliance Rules

This release introduces a number of new Compliance rules and deprecates a number of now-redundant rules. Details of all rules shipped are below. Rules not described below remain unaltered from the previous release.

|     |     |     |
| --- | --- | --- |
| **MettleCI v1.1** | **MettleCI v1.2** | **Notes** |
| \-  | `Aggregator Stage Not Preceded by Check Sort Stage.pjb.grm` | [MCI-4975](https://datamigrators.atlassian.net/browse/MCI-4975) - New rule ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2351529985](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2351529985)) |
| `Audit Drivers.pjb.grm` | \-  | Deprecated. No longer required. |
| `Audit Output.pjb.grm` | \-  | Deprecated. No longer required. |
| `Auditing Monitor.pjb.grm` | \-  | Deprecated. No longer required. |
| `Auditing Variance.*.grm` | \-  | Deprecated. No longer required. |
| `CCMigrateTool Stages.*.grm` | \-  | Deprecated. No longer required. |
| `DB tables reference are fully qualified.*.grm` | `Database Table References Are Fully Qualified.*.grm` | Renamed ([documentation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2219245789/DB+tables+reference+are+fully+qualified)) |
| \-  | `Database Connector does not Auto-Generate SQL.*.grm` | [MCI-2847](https://datamigrators.atlassian.net/browse/MCI-2847) - New rule ([documentation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2508357633/Database+Connector+does+not+Auto-Generate+SQL)) |
| `DataStage Flow Designer Stages.*.grm` | \-  | Deprecated. No longer required. |
| `ICP4D Unsupported Stages.*.grm` | `CP4D Unsupported Stages.*.grm` | Renamed ([documentation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2218721341/CP4D+Unsupported+Stages)) |
| \-  | `Job Activity References Deleted Child Parameter.qjb.grm` | [MCI-5244](https://datamigrators.atlassian.net/browse/MCI-5244) - New rule ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2508390401](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2508390401)) |
| \-  | `Job Parameter Not Used in a Job.pjb.grm` | [MCI-5244](https://datamigrators.atlassian.net/browse/MCI-5244) - New rule ([documentation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2532245505/Job+Parameter+Not+Used+in+a+Job)) |

## Fixes

### MettleCI Foundations

These are cross-module fixes, often related to security enhancements or updates to [third party libraries](../../reference/mettleci-open-source-reference.md).

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5230](https://datamigrators.atlassian.net/browse/MCI-5230) | Address SnakeYAML CVE |
| [MCI-5503](https://datamigrators.atlassian.net/browse/MCI-5503) | Address critical CVE on Apache SSH library |

### MettleCI Workbench

> [!INFO]
> Starting from this release the MettleCI Workbench Setup Wizard now generates [SHA2 keys](https://devblogs.microsoft.com/devops/supporting-sha-2-algorithm-in-ssh-on-azure-devops/) which is a format accepted by all the [Application Lifecycle Management systems](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/733675552/MettleCI+Integrations) against which MettleCI has been tested.

In addition to a number of minor cosmetic and usability issues, the following notable fixes and improvements were introduced:

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-3138](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3138) | Remove unnecessary 'Play' button from Unit Test Spec page. |
| [MCI-3455](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3455) | Prevent issue caused by caching when searching for issues in Issue Management Services |
| [MCI-3735](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3735) | Fix issue with enablement of Submit button at end of Workbench Setup Wizard |
| [MCI-4271](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4271) | Enhance workbench so that non-admin users can only see projects to which they are entitled |
| [MCI-4982](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4982) | Project registration wizard should exclude already-registered projects from drop down |
| [MCI-5068](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5068) | Workbench 'Create Unit Test' for a Sequence returned an error rather than declining gracefully |
| [MCI-5095](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5095) | Added setting to specify distinct locations for DataStage and Unit Test assets |
| [MCI-5099](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5099) | Regression in Workbench's display of project list |
| [MCI-5100](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5100) | Workbench REST endpoint incorrectly exposed some user details |
| [MCI-5103](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5103) | Workbench Jira Issue Management private key configuration security improvements |
| [MCI-5175](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5175) | Implement Compliance tagging system |
| [MCI-5176](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5176) | Implement private key fixes for non-Jira Issue Management Services |
| [MCI-5180](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5180) | ServiceNow config page crashed when visited from another Issue Management config page |
| [MCI-5192](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5192) | ServiceNow issue management filter enhancement |
| [MCI-5194](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5194) | Added enhanced logging for trust store issues during Workbench setup wizard |
| [MCI-5199](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5199) | Add Workbench debug logging for inspecting HTTP(S) requests used by Issue Management Services |
| [MCI-5200](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5200) | Workbench 'Generic' issue management services works on initial startup without additional configuration |
| [MCI-5216](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5216) | Fixed `NullPointerException` in Workbench while performing ServiceNow issue lookup |
| [MCI-5234](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5234) | Enhanced Workbench ServiceNow integration to allow credential specification |
| [MCI-5250](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5250) | Workbench verifies project permissions at login for correctly displaying project names |
| [MCI-5307](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5307) | Refactored Git 'HTTPS' credentials store to be generic Git 'Secrets' store |
| [MCI-5308](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5308) | Updated User Profile REST API endpoint to permit upload of private key for Git commit signing |
| [MCI-5309](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5309) | Update commit code to sign Git commits when the responsible user has a Git signing key |
| [MCI-5311](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5311) | Added ability to upload Git signing key through Workbench UI |
| [MCI-5334](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5334) | Added Workbench option to specify Azure Project ID when configuring Azure Issue Management |
| [MCI-5339](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5339) | Workbench Setup now generates Git SSH Key which is compatible with Azure DevOps |
| [MCI-5368](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5368) | Fixed `config.yml` regression when upgrading Workbench |
| [MCI-5373](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5373) | Workbench Service failed to start as user specified in DM\_WORKBENCH\_USER variable |
| [MCI-5391](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5391) | Workbench failed to connect to Git over SSH on Azure cloud |
| [MCI-5400](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5400) | Workbench - Refreshing 'Configure DataStage Project' page produces error |
| [MCI-5441](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5441) | Workbench Attempting to edit a project that has been deleted in DataStage causes odd state behaviour |

### MettleCI Unit Test Harnesses

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5408](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5408) | Unit Test date column has precision. This should be stripped out during interception/unit testing |

### MettleCI Command Line Interface

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5369](https://datamigrators.atlassian.net/browse/MCI-5369) | New [MettleCI compliance command](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2504491009/Compliance+List-Tags+Command) to list rules and their tags |

# Upgrade Process

Customers performing an initial installation, or upgrading from a previous version of MettleCI, can follow the instructions included (or linked) from these pages:

*   [Installation and Configuration](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/415367258/Installation+and+Configuration)
    
    *   [Installing MettleCI Workbench](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/453902355/Installing+MettleCI+Workbench)
        
    *   [Installing MettleCI Unit Test Harness](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/454393879/Installing+MettleCI+Unit+Test+Harness)
        
    *   [Installing MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488898631/Installing+MettleCI+Command+Line+Interface)
        

# Known Issues

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5055](https://datamigrators.atlassian.net/browse/MCI-5055) | The integration with Microsoft Azure currently assumes that your Azure DevOps project uses an Azure DevOps-hosted Git repository. MettleCI does not currently support Azure DevOps projects using externally-linked GitHub repositories. This is a known issue from a previous release and is a priority fix for the next release. |

# Notes

For documentation please visit [http://docs.mettleci.io](http://docs.mettleci.io)