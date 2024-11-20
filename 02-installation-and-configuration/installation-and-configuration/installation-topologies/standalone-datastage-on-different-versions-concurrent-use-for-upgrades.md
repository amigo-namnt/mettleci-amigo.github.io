# Standalone DataStage on Different Versions - Concurrent use for upgrades

This topology describes an environment featuring two DataStage platforms:

1.  A traditional standalone DataStage environment on v11.5.0 (for example) referred to below as the **Legacy DataStage** environment, and
    
2.  A traditional standalone DataStage environment on v11.7.1 (for example) referred to below as the **Target DataStage** environment
    

Each environment has its own dedicated MettleCI Agent running on a dedicated Windows host.

This topology is ideal for customers using MettleCI to upgrade between different versions of Standalone DataStage. Customers upgrading to Cloud Pak for Data should refer to [https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1656815621](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1656815621).

![](./attachments/Version%20Upgrade%20Topology%202.png)

# Connections

1.  Developer’s DataStage Designer Client to Legacy DataStage platform (using DataStage Multi-Client Manager, desktop virtualisation, or equivalent)
    
2.  Legacy Workbench service to Work Item Management (Work Item lookup on Workbench Commit page)
    
3.  Legacy Workbench service to Git (Compliance Clone, DataStage Commit/Push)
    
4.  Legacy build pipeline invokes MettleCI CLI activity on the Legacy build system agent
    
5.  Legacy build system agent uses MettleCI CLI to perform CI/CD operations on Legacy DataStage Development environment
    
6.  Legacy build system agent uses MettleCI CLI to perform CI/CD operations on Legacy non-development DataStage environments (e.g. QA, PROD)
    
7.  Developer’s DataStage Designer Client to Target DataStage platform (using DataStage Multi-Client Manager, desktop virtualisation, or equivalent)
    
8.  Target Workbench service to Work Item Management (Work Item lookup on Workbench Commit page)
    
9.  Target DataStage Workbench service to Git (Compliance Clone, DataStage Commit/Push)
    
10.  Target build pipeline invokes MettleCI CLI activity on the Target build system agent
    
11.  Target build system agent uses MettleCI CLI to perform CI/CD operations on Target DataStage Development environment
    
12.  Target build system agent uses MettleCI CLI to perform CI/CD operations on Target non-development Target DataStage environments (e.g. QA, PROD)