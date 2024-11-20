# MettleCI IBM OEM Release 1.3

*   [Package Summary](#package-summary)
*   [Package Contents](#package-contents)
*   [Change Log](#change-log)
    *   [Significant New Features](#significant-new-features)
    *   [New MettleCI Compliance Rules and Capabilities](#new-mettleci-compliance-rules-and-capabilities)
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
| **Package name** | MettleCI v1.3.0 Multiplatform English |
| **Release Date (yyyy-mm-dd)** | 2024-09-05 |
| **IBM Part Number** | M0M6LEN |

# Package Contents

> [!NOTE]
> This release also bundles **S2PX v.1.3**.
> See [this page](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2828927128/Server-to-Parallel+-+S2PX+Release+v1.3) for detailed release notes for S2PX.

This MettleCI v1.3 package contains a complete set of MettleCI and S2PX assets which give you everything you need to get up and running with these tools. You do **not** need to install any previous MettleCI or S2PX releases to use this package.

```
.
└── Software
    ├── CLI
    │   ├── dm-mettleci-command-shell-1.1-287-dist.zip
    │   └── dm-mettleci-command-shell-1.1-287.noarch.rpm
    ├── License
    │   ├── mettleci.lic
    │   └── properties.txt
    ├── Repositories
    │   ├── dm-compliance-rules-304.zip
    │   └── mettleci-repo-template-90.zip
    ├── S2PX
    │   ├── dm-s2px-analysis-plugin-1.0-158.jar
    │   └── dm-s2px-conversion-plugin-1.0-726.jar
    ├── Unit Test Harness
    │   ├── dm-unittest-harness-1.3-527-setup.exe
    │   └── dm-unittest-harness-1.3-527.noarch.rpm
    └── Workbench
        ├── dm-mettleci-workbench-1.3-1775-setup.exe
        └── dm-mettleci-workbench-1.3-1775.noarch.rpm

```

| **Function** | **File** | **Notes** |
| --- | --- | --- |
| Command Shell | `dm-mettleci-command-shell-1.1-287-dist.zip` WINDOWS<br><br>`dm-mettleci-command-shell-1.1-287.noarch.rpm` UNIX | These operating system-specific [MettleCI Command Shell](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2216886273/MettleCI+Command+Line+Interface) distributions each include a full set of the latest versions of all [MettleCI CLI plugins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2125725711/CLI+Plugins). |
| Compliance Rules | `dm-compliance-rules-304.zip` ALL PLATFORMS | A ready-to-deploy Git repository containing all the MettleCI sample [Compliance Rules](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2213085185/MettleCI+Compliance+Rules+Reference). |
| Template Git Repositories | `mettleci-repo-examples-90.zip` ALL PLATFORMS | Contains two example Git repositories:<br><br>*   `jenkins-mci-shared-libraries.zip` (ALL PLATFORMS) containing example [Jenkins Reusable Pipeline Components](#).<br>    <br>*   `mettleci-repo-template.zip` (ALL PLATFORMS) containing example CI/CD pipeline definitions for…<br>    <br>    *   [Atlassian Bamboo](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2106425347/Atlassian+Bamboo)<br>        <br>    *   [GitHub](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741376173/GitHub)<br>        <br>    *   [GitLab](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741244932/GitLab)<br>        <br>    *   [Jenkins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/731709604/Jenkins)<br>        <br>    *   [Microsoft Azure DevOps](#).<br>        <br><br>> [!NOTE]<br>> **Unsupported Examples**<br>> Note that despite being fully tested with their respective CI/CD software, these assets are supplied without warranty or support and are provided to serve as examples of how you can use the MettleCI Command Line Interface to construct your own build and deployment pipelines to meet your unique requirements. |
| License | `mettleci.lic` ALL PLATFORMS<br><br>`properties.txt` ALL PLATFORMS | The MettleCI license file (valid to the end of 2099) required to enable MettleCI functionality, along with a human-readable properties file describing the license constraints.<br><br>> [!NOTE]<br>> **Licence Update**<br>> If you download this MettleCI Release package from IBM Passport Advantage (or a similar IBM site **excluding Fix Central**) then it includes a full IBM OEM MettleCI license file. |
| Parallel Unit Test Harness | `dm-unittest-harness-1.3-527-setup.exe` WINDOWS<br><br>`dm-unittest-harness-1.3-527.noarch.rpm` UNIX | The MettleCI [Parallel Job Unit Test Harness for installation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/455868494/Installing+or+Upgrading+the+Parallel+Job+Unit+Test+Harness+on+Unix) on your Unix (`.rpm`) or Windows (`.exe`) DataStage Engine. |
| Workbench | `dm-mettleci-workbench-1.3-1775-setup.exe` WINDOWS<br><br>`dm-mettleci-workbench-1.3-1775.noarch.rpm` UNIX | The [MettleCI Workbench Service](#). |
| S2PX | `dm-s2px-analysis-plugin-1.0-158.jar` ALL PLATFORMS<br><br>`dm-s2px-conversion-plugin-1.0-726.jar` ALL PLATFORMS | Two [MettleCI CLI Plugins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2125725711/CLI+Plugins) which perform [pre-conversion analysis](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2080440325/Running+S2PX+Analysis) of a DSX containing Server Jobs and the [Server-to-Parallel conversion](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2080440348/Running+S2PX+Conversion) of an ISX containing Server Jobs. See [http://s2px.mettleci.io](http://s2px.mettleci.io/) for more details. |

# Change Log

## Significant New Features

*   Expansion of [Compliance tagging](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2472050689/Compliance+Rule+Tags) to include new Compliance tagging-aware commands and example tags for all rules
    
*   Automation of the install/uninstall of the Server Unit Test Harness using two new MettleCI commands ([install](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2640740386/UnitTest+Install-Server-Test-Harness+Command) and [uninstall](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2640281639/UnitTest+Uninstall-Server-Test-Harness+Command))
    
    *   … and consequent removal of the now-redundant `dm-server-unit-test-harness-routine-1.3-xxx.zip` package
        
*   Introduction of example pipelines using Atlassian Bamboo Specs (YAML-based pipeline definitions)
    
    *   … and consequent removal of the now-redundant `mettleci deploy devops-pipeline` command
        
*   Support for using external Git repositories (e.g. GitHub) in Azure DevOps projects
    
*   A variety of minor bug fixes and improvements
    
*   More new Compliance rules (detailed below) targeted at customers planning to migrate their DataStage solutions to Cloud Pak
    
*   Significant changes to the underpinnings of MettleCI to prepare for a forthcoming release which will feature…
    
    *   Replacement of the existing Workbench application with a new application using IBM’s Carbon UI framework
        
    *   Native integration of MettleCI functionality into the Cloud Pak DataStage NextGen interface 
        

## New MettleCI Compliance Rules and Capabilities

This release introduces a number of new Compliance rules and deprecates a number of now-redundant rules. Details of all rules shipped are below. Rules not described below remain unaltered from the previous release.

| **Capability** | **Description** |
| --- | --- |
| `Job Using Custom Function.*.grm` ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863300609](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863300609)) | **✨ New Rules**<br><br>Detect various features and functions of Classic DataStage Jobs which will require manual remediation to migrate to CP4D because those features and functions were not currently supported by the relevant Cloud Pak DataStage offering at the time of this MettleCI v1.3 release.<br><br>> [!INFO]<br>> Given the frequent release cadence of CP4D, customers are advised to verify the content of these rules against the version of CP4D that they are using. Customers can, of course, update the contents of these rules themselves, as they see fit. |
| `DataStage SaaS Unsupported Stages.*.grm` ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863333469](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863333469)) |
| `Using DB2 Sequence to Generate SK.*.grm` ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863300655](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863300655)) |
| `Job Using ODBC Connector.*.grm` ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863300701](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863300701)) |
| `Jobs With Before and After Routine.*.grm` ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863333423](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863333423)) |
| `Asset using Java Integration Stage.*.grm` ([https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863333377](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2863333377)) |
| All rules | Extended all rules with tag annotations so that they are grouped for easier filtering by [relevant MettleCI commands](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2262990849/Compliance+Namespace). A set of default tags is supplied and can be listed with the `mettleci compliance list-tags` ([documentation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2504491009/Compliance+List-Tags+Command)) command. |
| Cloud Pak upgrade tags | Added the following tags to relevant compliance rules to assist customers planning their migration to DataStage NextGen on Cloud Pak for Data:<br><br>*   `saas-unsupported` tag - Identifying features and functions not currently supported in CP4D DataStage SaaS in any circumstances<br>    <br>*   `saas-anywhere` tag - Identifying features and functions only currently supported in CP4D DataStage SaaS when using the ‘Anywhere’ remote engine capability<br>    <br>*   `saas-warning` - Identifying features and functions not supported in CP4D DataStage SaaS when certain settings are selected<br>    <br><br>> [!INFO]<br>> Given the frequent release cadence of CP4D, customers are advised to verify the content of these tags against the version of CP4D that they are using. Customers can, of course, update the contents of these rules themselves, as they see fit. |

## Fixes

> [!INFO]
> Note that **MCI-*****NNNN*** issue reference links are only accessible to authenticated users.

### MettleCI Foundations

These are cross-module fixes, often related to security enhancements or updates to [third party libraries](../../reference/mettleci-open-source-reference.md).

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5503](https://datamigrators.atlassian.net/browse/MCI-5503) | Security - Resolve CRITICAL CVE on Apache SSH library |

### MettleCI Workbench

In addition to a number of tweaks, enhancements, and optimisations to the Workbench implementation, the following notable fixes and improvements were introduced:

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5055](https://datamigrators.atlassian.net/browse/MCI-5055) | **Enhancement** - Known issue from last release. MettleCI Workbench integration with Microsoft Azure no longer assumes that the Azure DevOps project being used for work item tracking is the same project used to host your Git repository. MettleCI Workbench now supports Azure DevOps projects using externally linked Git repositories, including GitHub. |
| [MCI-5268](https://datamigrators.atlassian.net/browse/MCI-5268), [MCI-5523](https://datamigrators.atlassian.net/browse/MCI-5523) | **Enhancement** - Preparing Workbench service for future release of full Java 11-compatibility |
| [MCI-5668](https://datamigrators.atlassian.net/browse/MCI-5668) | **Security** - Resolve SnakeYAML CVE in Workbench |
| [MCI-5730](https://datamigrators.atlassian.net/browse/MCI-5730) | **Enhancement** - Preparing Workbench user authentication for future upgrade to IBM Carbon user interface framework |
| [MCI-5859](https://datamigrators.atlassian.net/browse/MCI-5859) | **Bug** - Workbench unit test data entered with a leading apostrophe is not being filtered out during save process |
| [MCI-5909](https://datamigrators.atlassian.net/browse/MCI-5909) | **Enhancement** - Preparing Workbench work item lookup for future upgrade to IBM Carbon user interface framework |
| [MCI-6006](https://datamigrators.atlassian.net/browse/MCI-6006) | **Regression** - Workbench unit test data table unable to save data when values are numeric |
| [MCI-6013](https://datamigrators.atlassian.net/browse/MCI-6013) | **Bug** - Command `mettleci workbench set-branch` returned HTTP 415 "unsupported media type" error |

### MettleCI Unit Test Harnesses

| **Issue Reference** | **Summary** |
| --- | --- |
| Numerous | Enhancements to unit test underpinnings to prepare for future Java 11 compatibility |
| Numerous | Enhancements to unit test underpinnings to prepare for future release of Cloud Pak for Data native MettleCI unit testing capability |

### MettleCI Command Line Interface

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5619](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5619) | Update Bamboo tasks to accept Shared Credential name from YAML spec |
| [MCI-5609](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5609) | Generate fingerprint from ISX Export(s) |

# Upgrade Process

Customers performing an initial installation, or upgrading from a previous version of MettleCI, can follow the instructions included (or linked) from these pages:

*   [Installation and Configuration](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/415367258/Installation+and+Configuration)
    
    *   [Installing MettleCI Workbench](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/453902355/Installing+MettleCI+Workbench)
        
    *   [Installing MettleCI Unit Test Harness](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/454393879/Installing+MettleCI+Unit+Test+Harness)
        
    *   [Installing MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488898631/Installing+MettleCI+Command+Line+Interface)
        

# Known Issues

| **Issue Reference** | **Summary** |
| --- | --- |
|     | None. |

# Notes

For documentation please visit [http://docs.mettleci.io](http://docs.mettleci.io)