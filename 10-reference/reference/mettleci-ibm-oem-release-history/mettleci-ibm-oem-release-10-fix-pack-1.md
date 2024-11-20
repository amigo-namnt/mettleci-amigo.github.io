# MettleCI IBM OEM Release 1.0 Fix Pack 1

# Package Summary

|     |     |
| --- | --- |
| **Package name** | MettleCI 1.0 fp1 |
| **Release Date (yyyy-mm-dd)** | 2021-10-13 |

# Package Contents

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Function** | **File** | **Timestamp** | **Size** | **Type** | **Notes** |
| Command Shell | `dm-mettleci-command-shell-1.1-179-dist.zip` WINDOWS<br><br>`dm-mettleci-command-shell-1.1-179.noarch.rpm` UNIX |     |     | ZIP<br><br>RPM | These Command Shell distributions each include a full set of the latest versions of all MettleCI CLI plugins (commands). |
| Workbench | `dm-mettleci-workbench-1.0-1348-setup.exe` WINDOWS<br><br>`dm-mettleci-workbench-1.0-1348.noarch.rpm` UNIX |     |     | EXE<br><br>RPM |     |
| Compliance Rules | `dm-compliance-rules-175m.zip` |     |     | ZIP | A ready-to-use Git repository folder |
| Sample Build Pipelines | `mettleci-azure-template.zip`<br><br>`mettleci-gitlab-template.zip`<br><br>`mettleci-jenkins-template.zip` |     |     | ZIP<br><br>ZIP<br><br>ZIP |     |
| Parallel Unit Test Harness | `dm-unittest-harness-1.0-343-setup.exe` WINDOWS<br><br>`dm-unittest-harness-1.0-343.noarch.rpm` UNIX |     |     | EXE<br><br>RPM |     |
| Server Unit Test Harness | `dm-server-unit-test-harness-1.0-343.zip`  WINDOWS  UNIX |     |     | ZIP | This provides a Server interface to the capabilities provided by the Parallel test harness which must also be installed to provide unit test functionality. |
| CP4D Integration | `workbench-icp4d-integration-1.0.zip` |     |     | TXT | MettleCI CP4D integration scripts |

> [!INFO]
> Note that to use this distribution you will need to source a MettleCI license file from the [MettleCI Release v1.0 package](../mettleci-ibm-oem-release-history/mettleci-ibm-oem-release-10.md).

All MettleCI v1.0 Fix Pack 1 package contents only include assets which are changed from those delivered in the initial v1.0 release and are supplied in this structure:

```
.
├── Documentation
│ └── MCIDOC.zip                                                  # Archive of
├── README.pdf                                                    # This document
└── Software
    └── Distribution
        ├── CLI                                                   # MettleCI Command Line Interface
        │   ├── dm-mettleci-command-shell-1.1-179-dist.zip        # Windows
        │   └── dm-mettleci-command-shell-1.1-179.noarch.rpm      # Unix/Linux
        ├── Git Repos
        │   └── dm-compliance-rules-175m.zip                      # Sample MettleCI Compliance Rules
        ├── Unit Test Harness
        │   ├── dm-server-unit-test-harness-routine-1.0-343.zip   # Server UTH - All platforms
        │   ├── dm-unittest-harness-1.0-343-setup.exe             # Parallel UTH - Windows
        │   └── dm-unittest-harness-1.0-343.noarch.rpm            # Parallel UTH - Unix/Linux
        └── Workbench
            ├── dm-mettleci-workbench-1.0-1348-setup.exe          # Workbench for Windows DS Engines
            └── dm-mettleci-workbench-1.0-1348.noarch.rpm         # Workbench for Unix/Linux DS Engines
            └── CP4D
                └── workbench-icp4d-integration-1.0.zip           # MettleCI CP4D integration scripts
```

# Upgrade Process

Customers performing an initial installation, or upgrading from a previous version of MettleCI licensed directly from Data Migrators can follow the instructions here:

*   MettleCI installation/upgrade on standalone (traditional) DataStage environments is described here: Installation and Configuration
    
*   MettleCI installation/upgrade on Cloud Pak for Data environments is described here: MettleCI for IBM Cloud Pak for Data
    

# Improvements and New Features

## MettleCI Compliance

*   General minor wording and documentation improvements across most rules.
    
*   New and significantly updated rules:
    

| **Compliance Rule** | **Asset Type** | **Type** | **Change Type** |
| --- | --- | --- | --- |
| DataStage Flow Designer Stages | PARALLEL | Update | Updated stage list to align with recent IBM announcements. |
| Database Row Limit | PARALLEL, SERVER | Update | Compliance error message now includes the configured limit value. |
| Default Values in Job Params | PARALLEL, SERVER | New | Ensures all job parameters have a default value. |
| Entire Partitioning on Non- Reference Link | PARALLEL | New | Ensures links with partitioning set to Entire are reference links for Lookup stages. |
| Job Activity with Hardcoded Parameter Values | SEQUENCE | Update | Refactored for improved compatibility and error handling. |
| Link Auto Partitioning set | PARALLEL | New | Reports links whose partitioning is set to ‘Auto’. |
| Link Partitioning Must Match Sort | PARALLEL | New | Ensures link partitioning keys match those of a link sort (so sort works as expected) |
| Log Column Values | PARALLEL, SERVER | New | Identify stages using ‘Log column values on first row error’ as they may expose sensitive information in the DataStage job log. |
| Sort Post Join Stage | PARALLEL, SERVER | New | Identifies potentially redundant sorting (a sort stage or link sort) situated immediately after a Join stage. |
| Stage Naming | PARALLEL | Update | Updated stage list to align with recent IBM announcements. |

## Cloud Pak for Data

*   This release includes a number of scripts (along with supporting documentation) which support the integration of MettleCI into versions of IBM Cloud Pak for Data [https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1512439920](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1512439920).
    

## MettleCI Workbench

*   MettleCI Workbench now supports associating different Work Item Management systems with each DataStage project ([MCI-3615](https://datamigrators.atlassian.net/browse/MCI-3615)) (documentation)
    
*   MettleCI Workbench now supports HTTPS connections to Git services ([MCI-3851](https://datamigrators.atlassian.net/browse/MCI-3851)) (documentation)
    
*   MettleCI Workbench now performs the Git Commit and Push using user-specific Git credentials rather than a generic application-wide SSH key ([MCI-3851](https://datamigrators.atlassian.net/browse/MCI-3851)) (documentation)
    
*   MettleCI Workbench works with Git systems which no longer use ‘Master’ as the term for their default branch ([MCI-4056](https://datamigrators.atlassian.net/browse/MCI-4056))
    
*   Improved SSL protocol negotiation to support recent changes to IBM's proprietary JVM extensions ([MCI-4116](https://datamigrators.atlassian.net/browse/MCI-4116))
    
*   Multiple minor UI and reliability fixes (detailed below)
    

# Fixes and Features

| **Reference** | **Component** | **Type** | **Description** |
| --- | --- | --- | --- |
| [MCI-3768](https://datamigrators.atlassian.net/browse/MCI-3768) | Workbench Setup Wizard | Technical Debt | Workbench Setup Wizard redundant Issue Management system selection removed |
| [MCI-3794](https://datamigrators.atlassian.net/browse/MCI-3794) | Workbench | Bug | Workbench column validation seems to have issues with ustrings and dates |
| [MCI-3797](https://datamigrators.atlassian.net/browse/MCI-3797) | Improvement |     | Workbench initial empty file display usability enhancements |
| [MCI-3809](https://datamigrators.atlassian.net/browse/MCI-3809)<br><br>[MCI-4033](https://datamigrators.atlassian.net/browse/MCI-4033)<br><br>[MCI-4035](https://datamigrators.atlassian.net/browse/MCI-4035) | Workbench Data Fabrication | Bug | Workbench Data Fabrication for date cannot update<br><br>Phone Number Data Fabrication not honouring the format<br><br>Date Fabrication throws exception when trying to modify date from text box (instead of date picker) |
| [MCI-3800](https://datamigrators.atlassian.net/browse/MCI-3800) | Workbench Installer | Bug | Corrected file permissions that are set in Workbench RPM installer |
| [MCI-3799](https://datamigrators.atlassian.net/browse/MCI-3799) | Workbench Installer | Bug | Fix Workbench RPM Installer on AIX |
| [MCI-3851](https://datamigrators.atlassian.net/browse/MCI-3851)<br><br>[MCI-3861](https://datamigrators.atlassian.net/browse/MCI-3861)<br><br>[MCI-3863](https://datamigrators.atlassian.net/browse/MCI-3863)<br><br>[MCI-3866](https://datamigrators.atlassian.net/browse/MCI-3866)<br><br>[MCI-3880](https://datamigrators.atlassian.net/browse/MCI-3880)<br><br>[MCI-3960](https://datamigrators.atlassian.net/browse/MCI-3960)<br><br>[MCI-3908](https://datamigrators.atlassian.net/browse/MCI-3908)<br><br>[MCI-3949](https://datamigrators.atlassian.net/browse/MCI-3949)<br><br>[MCI-3947](https://datamigrators.atlassian.net/browse/MCI-3947)<br><br>[MCI-3948](https://datamigrators.atlassian.net/browse/MCI-3948)<br><br>[MCI-3940](https://datamigrators.atlassian.net/browse/MCI-3940)<br><br>[MCI-3957](https://datamigrators.atlassian.net/browse/MCI-3957) | Workbench Git Integration | New feature | Add support for user-specific git credentials<br><br>Implement backend system to store users' git credentials<br><br>Implement config option to enable git via HTTPS<br><br>Update edit profile endpoint to accept git credentials<br><br>Add encryption key for git credentials to JWT<br><br>Git credentials use secrets directory<br><br>Implement front end for git credentials changes<br><br>User Friendly warnings when committing via https without credentials setup<br><br>Generate git credential keystore password<br><br>Handle commit/compliance when git password can't be decrypted<br><br>Execute commit and compliance using user git credentials<br><br>Modify the add/update project endpoints to not accept HTTPS URLs if git over HTTPS is disabled |
| [MCI-4027](https://datamigrators.atlassian.net/browse/MCI-4027) | Workbench Git Integration | Bug | Workbench Git Credentials - ssh commit fails when git username is null |
| [MCI-4055](https://datamigrators.atlassian.net/browse/MCI-4055) | Workbench Setup Wizard | Bug | Rerunning Setup Wizard leaves git-credentials in broken state |
| [MCI-4139](https://datamigrators.atlassian.net/browse/MCI-4139) | Workbench Installer | Bug | Remove redundant message from MettleCI Workbench Service banner message  <br>Workbench returns to home screen if no project has been registered |
| [MCI-3897](https://datamigrators.atlassian.net/browse/MCI-3897) | Workbench | Bug | Workbench returns to home screen if no project has been registered |
| [MCI-3879](https://datamigrators.atlassian.net/browse/MCI-3879) | Workbench Security | Technical Debt | Create log4j false-positive suppression XML and regenerate test report |
| [MCI-4054](https://datamigrators.atlassian.net/browse/MCI-4054) | Workbench Unit Testing | Bug | Unit Testing - “Incorrect column metadata” errors not appearing in test result |
| [MCI-3891](https://datamigrators.atlassian.net/browse/MCI-3891) |     | Bug | Various Xmeta queries fail for engine with non-default port |
| [MCI-3615](https://datamigrators.atlassian.net/browse/MCI-3615)<br><br>[MCI-3605](https://datamigrators.atlassian.net/browse/MCI-3605)<br><br>[MCI-3606](https://datamigrators.atlassian.net/browse/MCI-3606)<br><br>[MCI-3607](https://datamigrators.atlassian.net/browse/MCI-3607)<br><br>[MCI-3608](https://datamigrators.atlassian.net/browse/MCI-3608) | Workbench Work Item Management Integration | New feature | Add support for multiple concurrent Work Item Management systems<br><br>Notify customers of breaking change which comes with Workbench and the new Multi-WIM feature<br><br>Mystery customer test of Workbench upgrade with Multi- WIM enabled<br><br>Align Workbench upgrade documentation for Multi-WIM feature<br><br>Workbench with Multi-WIM enabled by default |
| [MCI-4116](https://datamigrators.atlassian.net/browse/MCI-4116) | Workbench | Bug | Fresh Workbench install produces cipher suite error on most very recent version of DataStage |
| [MCI-4023](https://datamigrators.atlassian.net/browse/MCI-4023) | Compliance | Bug | Handle a null\`XMLProperties\` object when running Compliance against a DataStage job with a new, unmodified Connector Stage. |
| [MCI-4201](https://datamigrators.atlassian.net/browse/MCI-4201) | Workbench | Bug | Identified and removed race condition in issue management page preventing project registration. |
| [MCI-4214](https://datamigrators.atlassian.net/browse/MCI-4214) | Workbench Unit Testing | Bug | Setting 24Hr time in Windows produces wrong date values in JUnit Test results. |