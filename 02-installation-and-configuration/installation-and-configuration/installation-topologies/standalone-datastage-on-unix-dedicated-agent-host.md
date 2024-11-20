# Standalone DataStage on Unix - Dedicated Agent Host

A Unix-based multi-tier DataStage environment where…

*   The MettleCI Workstation is installed on your DataStage Engine tier, and
    
*   The MettleCI Agent is installed on a dedicated Windows host
    

![](./attachments/DataStage%20on%20Unix%20Separate%20Agent.png)

# Notes

*   The Information Server environment can be deployed using a 1-tier, 2-tier, or 3-tier architecture. Common best practise places the Engine tier on a dedicated host, and the Services and Repository tiers together on a separate host.
    
*   The MettleCI Workbench Service runs (in this topology) on a Unix-based DataStage Engine tier. This is because this service requires a shared filesystem with the MettleCI Unit Test Harness which can only be installed on the Engine tier.
    
*   The MettleCI Agent host is a dedicated host reserved exclusively for use by your selected CI/CD build tool via the installed CD/CD agent. The MettleCI CLI is used by the CI/CD Agent to automate build and deployment activities. The MettleCI CLI and Agent need to be installed on a Windows host co-resident with a DataStage Client tier in order to enable the automation of the DataStage job compilation process, which requires the use of a Windows-based Client tier.