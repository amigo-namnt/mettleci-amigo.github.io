# MettleCI IBM OEM Release 1.1

*   [Package Summary](#package-summary)
*   [Package Contents](#package-contents)
*   [Change Log](#change-log)
    *   [New Features](#new-features)
        *   [New MettleCI Compliance Rules](#new-mettleci-compliance-rules)
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
| **Package name** | MettleCI 1.1 |
| **Release Date (yyyy-mm-dd)** | 2022-12-22 |

# Package Contents

> [!NOTE]
> This release also bundles **S2PX v.1.1**.
> See [this page](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2211414017/Server-to-Parallel+-+S2PX+Release+v1.1) for detailed release notes for S2PX.

This MettleCI v1.1 package contains a complete set of MettleCI and S2PX assets which give you everything you need to get up and running with these tools. You do **not** need to install any previous MettleCI or S2PX releases to use this package.

```
.
└── Software
    ├── CLI
    │   ├── dm-mettleci-command-shell-1.1-238-dist.zip
    │   └── dm-mettleci-command-shell-1.1-238.noarch.rpm
    ├── License
    │   ├── mettleci.lic
    │   └── properties.txt
    ├── Repositories
    │   ├── dm-compliance-rules-233.zip
    │   └── mettleci-repo-examples-27.zip
    ├── S2PX
    │   ├── dm-s2px-analysis-plugin-1.0-82.jar
    │   └── dm-s2px-conversion-plugin-1.0-570.jar
    ├── Unit Test Harnesses
    │   ├── dm-server-unit-test-harness-routine-1.1-391.zip
    │   ├── dm-unittest-harness-1.1-391-setup.exe
    │   └── dm-unittest-harness-1.1-391.noarch.rpm
    └── Workbench
        ├── dm-mettleci-workbench-1.0-1520-setup.exe
        └── dm-mettleci-workbench-1.0-1520.noarch.rpm
```

| **Function** | **File** | **Notes** |
| --- | --- | --- |
| Command Shell | `dm-mettleci-command-shell-1.1-238-dist.zip` WINDOWS<br><br>`dm-mettleci-command-shell-1.1-238.noarch.rpm` UNIX | These operating system-specific [MettleCI Command Shell](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2216886273/MettleCI+Command+Line+Interface) distributions each include a full set of the latest versions of all [MettleCI CLI plugins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2125725711/CLI+Plugins). |
| Compliance Rules | `dm-compliance-rules-233.zip` ALL PLATFORMS | A ready-to-deploy Git repository containing all the MettleCI sample [Compliance Rules](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2213085185/MettleCI+Compliance+Rules+Reference). |
| Template Git Repositories | `mettleci-repo-examples-27.zip` ALL PLATFORMS | Contains two example Git repositories:<br><br>*   `jenkins-mci-shared-libraries.zip` (ALL PLATFORMS) containing example [Jenkins Reusable Pipeline Components](#).<br>    <br>*   `mettleci-repo-template.zip` (ALL PLATFORMS) containing example CI/CD pipeline definitions for [GitHub](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741376173/GitHub), [GitLab](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741244932/GitLab), [Jenkins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/731709604/Jenkins), and [Microsoft Azure DevOps](#).<br>    <br><br>> [!NOTE]<br>> **Unsupported Examples**<br>> Note that despite being fully functional, these assets are supplied without warranty or support and are provided to serve as examples of how you can utilise the MettleCI Command Line Interface to construct your own build and deployment pipelines to meet your unique requirements. |
| License | `mettleci.lic` ALL PLATFORMS<br><br>`properties.txt` ALL PLATFORMS | The MettleCI license file (valid to the end of 2099) required to enable MettleCI functionality, along with a human-readable properties file describing the license constraints.<br><br>> [!NOTE]<br>> **Licence Update**<br>> If you download this MettleCI Release package v1.1 from IBM Passport Advantage (or a similar IBM site **excluding Fix Central**) then it includes a full IBM OEM MettleCI license file. From this release forward this license file will be named `mettleci.lic` which is the filename expected by MettleCI Workbench. Other than the name change the contents of the file are unaltered, so existing users of MettleCI do not need to replace their existing license file. |
| Server Unit Test Harness | `dm-server-unit-test-harness-routine-1.1-391.zip`  ALL PLATFORMS | The MettleCI Server Job Unit Test Harness for installation on your DataStage Engine. |
| Parallel Unit Test Harness | `dm-unittest-harness-1.1-391-setup.exe` WINDOWS<br><br>`dm-unittest-harness-1.1-391.noarch.rpm` UNIX | The MettleCI Parallel Job Unit Test Harness for installation on your Unix (`.rpm`) or Windows (`.exe`) DataStage Engine. |
| Workbench | `dm-mettleci-workbench-1.0-1520-setup.exe` WINDOWS<br><br>`dm-mettleci-workbench-1.0-1520.noarch.rpm` UNIX | The [MettleC Workbench Service](#). |
| S2PX | `dm-s2px-analysis-plugin-1.0-82.jar` ALL PLATFORMS<br><br>`dm-s2px-conversion-plugin-1.0-570.jar` ALL PLATFORMS | Two [MettleCI CLI Plugins](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2125725711/CLI+Plugins) which perform [pre-conversion analysis](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2080440325/Running+S2PX+Analysis) of a DSX containing Server Jobs and the [Server-to-Parallel conversion](https://datamigrators.atlassian.net/wiki/spaces/S2PX/pages/2080440348/Running+S2PX+Conversion) of an ISX containing Server Jobs. See [http://s2px.mettleci.io](http://s2px.mettleci.io/) for more details. |

# Change Log

## New Features

*   A significantly enhanced implementation of Unit Test Interception for Parallel Jobs using Sparse Lookups ([MCI-4992](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4992)).
    
    *   See documentation of the [Sparse Lookup ‘Replace’ method](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/534413695/Unit+Testing+Sparse+Lookup+Stages?src=search#Sparse-Lookup-Stage-('Replace'-method)).
        
*   Initial release of Azure pipeline examples.
    
*   Initial release of GitHub pipeline examples.
    
*   Initial release of GitLab pipeline examples.
    
*   Substantial overhaul of Jenkins Pipeline examples
    
    *   Introduction of reusable Groovy components (CCMT, Compile, Deploy, Unit Test) for use across multiple Jenkins pipelines
        
    *   Upgraded unified DevOps and Upgrade pipelines
        
    *   Two new multi-purpose pipelines: Build and Deploy
        
*   More new Compliance rules (details below)
    

### New MettleCI Compliance Rules

This release introduces nine new Compliance rules: (click the title of each for more details)

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-973](https://datamigrators.atlassian.net/browse/MCI-973) | [Oracle Connector Not Using Partition Read](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2356281345) |
| [MCI-1541](https://datamigrators.atlassian.net/browse/MCI-1541) | [Job Using Transformer Surrogate Key](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2352480257) |
| [MCI-2921](https://datamigrators.atlassian.net/browse/MCI-2921) | [Sequential File Read Using Same Partitioning](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2352742401/Sequential+File+Read+Using+Same+Partitioning) |
| [MCI-2948](https://datamigrators.atlassian.net/browse/MCI-2948) | [Transformer Uses Abort After Rows](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2351300609/Transformer+Uses+Abort+after+rows) |
| [MCI-3000](https://datamigrators.atlassian.net/browse/MCI-3000) | [DataSet Not Using Same Partition](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2351300693/Data+Sets+not+using+Same+partitioning+method) |
| [MCI-3565](https://datamigrators.atlassian.net/browse/MCI-3565) | [Join Partition vs Join Key](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2218721401/Join+Partition+vs+Join+Key) |
| [MCI-4517](https://datamigrators.atlassian.net/browse/MCI-4517) | [Date Format in Annotation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2365882369/Date+Format+in+Annotation) (template for seeking arbitrary text in a Job Annotation) |
| [MCI-4381](https://datamigrators.atlassian.net/browse/MCI-4381) | [Column Name Contains Unsupported Characters](#). |
| [MCI-4974](https://datamigrators.atlassian.net/browse/MCI-4974) | [Job Using Rnd() Function](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2351300651/Transformer+Uses+Rnd+Function) |

## Fixes

### MettleCI Foundations

These are cross-module fixes, often related to security enhancements or updates to [third party libraries](../../reference/mettleci-open-source-reference.md).

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-3832](https://datamigrators.atlassian.net/browse/MCI-3832) | XML specification allows the use of entities that can be external (Security issue) |
| [MCI-3831](https://datamigrators.atlassian.net/browse/MCI-3831) | X-Frame-Options header is not included in the HTTP response (CWE-16) |
| [MCI-5054](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-5054) | OWASP security vulnerabilities |

### MettleCI Workbench

> [!INFO]
> Starting from this release the MettleCI Workbench Setup Wizard no longer generates SHA-1 RSA keys (now [deprecated by GitHub](https://github.blog/2021-09-01-improving-git-protocol-security-github/)) but instead generates GitHub-supported ECDSA keys by default. See [MCI-4875](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4875) below.

A number of minor cosmetic issues were addressed, plus the following notable fixes and improvements:

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-1294](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-1294) | Standardise 'Loading' messages between the Workbench pages |
| [MCI-1297](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-1297) | Workbench toaster messages should be user-dismissible. |
| [MCI-2606](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-2606) | Update command line text when workbench `rpm` is installed. |
| [MCI-3008](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3008) | Requesting Unit Test Results for a job without a Unit Test should prompt a user to create one. |
| [MCI-3708](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3708) | Workbench to log the constraints/properties of the MettleCI license in use. |
| [MCI-3718](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3718) | Workbench Install - update docs to warn about file perms/owns. |
| [MCI-3798](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3798) | Uploading new file when file is empty should not produce a warning. |
| [MCI-3836](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3836) | Prevent the registration of a DS project that doesn't exist. |
| [MCI-3837](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3837) | Invalid CSV files should not be saved. |
| [MCI-3838](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3838) | Review token expiry time. |
| [MCI-3842](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3842) | Sensitive files should be read/write only by `mciworkb`. |
| [MCI-4203](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4203) | Installing Workbench Designer menus asks to confirm ‘v11.5’ installation on any platform. |
| [MCI-4251](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4251) | Prevent column data from overlapping in the Unit Test Results screen. |
| [MCI-4252](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4252) | Provide a read-only view of Workbench project settings to non-admin users. |
| [MCI-4301](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4301) | Update Workbench to default token session expiry to 1 hour. |
| [MCI-4405](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4405) | Workbench needs to provide to user enough info to configure Issue Management callback URL. |
| [MCI-4425](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4425) | Fresh MettleCI install can (unintentionally) present all pages with no registered project. |
| [MCI-4426](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4426) | Add ‘processing’ indication to Register Project page while validating supplied Git URL. |
| [MCI-4446](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4446) | Workbench Project Registration error validating GitLab SSH URI. |
| [MCI-4505](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4505) | Server Unit Tests should stub all passive stages. |
| [MCI-4513](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4513) | Can't successfully register an Azure DevOps project in MCI Workbench. |
| [MCI-4514](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4514) | Generated `workbench.key.pub` should have comment `mettleci@{hostname}` to distinguish keys in complex environments. |
| [MCI-4548](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4548) | Improve Case Search in Workbench. |
| [MCI-4575](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4575) | Document Workbench HTTPS configuration using an existing certificate rather than a new, self signed, certificate. |
| [MCI-4675](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4675) | Catch and display error when workbench fails to source a project list from DataStage. |
| [MCI-4734](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4734) | Workbench on Windows has an issue with `config.yml` setting `httpsCredentialsStore`. |
| [MCI-4772](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4772) | Workbench startup problems on RHEL8 systems. |
| [MCI-4794](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4794) | Enhance Workbench Setup Wizard to display or log error when failing during completion step. |
| [MCI-4841](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4841) | Enhance Workbench Windows Installer to allow silent mode. |
| [MCI-4874](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4874) | Remove reference to ‘Work Item Management Platform’ on Workbench Setup Wizard. |
| [MCI-4875](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4875) | SSH key generation performed by setup wizard must align with new GitHub requirements (ECDSA not RSA). |
| [MCI-4884](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4884) | Workbench (Windows) is not able to find `git-credentials-keystore-password` file from Setup Wizard generated `config.yml`. |
| [MCI-4886](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4886) | Don’t display a ‘ReadOnly’ message when creating a new test data file after opening a ‘ReadOnly’ file from a Unit Test Specification. |
| [MCI-4887](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4887) | Inconsistent use of license/licence in Workbench Setup Wizard summary screen. |
| [MCI-4889](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4889) | Workbench Setup Wizard’s 'ECDSA Key' page displays an RSA template. |
| [MCI-4923](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4923) | Fix `chkconfig` settings in Workbench `rpm` Service. |

### MettleCI Unit Test Harnesses

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-3904](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-3904) | Update to support new [S2PX](http://s2px.mettleci.io/) Asset Query which detects instances of custom DS Basic Routines in Transformers. |
| [MCI-4470](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4470) | Unit Test Harness occasionally aborts with ‘ds\_anyopen() - Slot1 1 already in use’ error |
| [MCI-4524](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4524) | Parallel Unit Test Spec, for Jobs with certain conditions, incorrectly fails validation |
| [MCI-4545](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4545) | Server Unit Test Interception crashes when intercepting input connected to Collector stages |
| [MCI-4842](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4842) | Enhance Unit Test Harness Windows Installer to allow silent mode |
| [MCI-4903](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4903),<br><br>[MCI-4904](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4904),<br><br>[MCI-4977](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4977) | Remodel some Unit Test underpinnings in preparation for forthcoming CP4D integration |
| [MCI-4992](https://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4992) | Implement Sparse Lookup interception for Parallel Unit Testing |

### MettleCI Command Line Interface

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-4686](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4686) | Handle leading space in front of namespace when invoking from MettleCI CLI interactive session. |
| [MCI-4805](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4805) | MettleCI command should permit user-specified Java options. |
| [MCI-4900](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4900) | MettleCLI (Windows) not able to handle password with `!` (since introduction of supporting `-Xms` & `-Xmx` options). |
| [MCI-4922](http://build.datamigrators.io/bamboo/project/jiraRedirect.action?jiraIssueKey=MCI-4922) | MCI CLI `config.properties` file should have default uncommented `license.file` entry should be the Windows version. |
| [MCI-4928](https://datamigrators.atlassian.net/browse/MCI-4928) | MettleCI CLI on Windows dropping arguments which include wildcard characters. |

# Upgrade Process

Customers performing an initial installation, or upgrading from a previous version of MettleCI, can follow the instructions included (or linked) from these pages:

*   [Installation and Configuration](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/415367258/Installation+and+Configuration)
    
    *   [Installing MettleCI Workbench](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/453902355/Installing+MettleCI+Workbench)
        
    *   [Installing MettleCI Unit Test Harness](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/454393879/Installing+MettleCI+Unit+Test+Harness)
        
    *   [Installing MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488898631/Installing+MettleCI+Command+Line+Interface)
        

# Known Issues

| **Issue Reference** | **Summary** |
| --- | --- |
| [MCI-5055](https://datamigrators.atlassian.net/browse/MCI-5055) | The integration with Microsoft Azure currently assumes that your Azure DevOps project uses an Azure DevOps-hosted Git repository. MettleCI does not currently support Azure DevOps projects using externally-linked GitHub repositories. This is a priority fix for the next release. |

# Notes

For documentation please visit [http://docs.mettleci.io](http://docs.mettleci.io)