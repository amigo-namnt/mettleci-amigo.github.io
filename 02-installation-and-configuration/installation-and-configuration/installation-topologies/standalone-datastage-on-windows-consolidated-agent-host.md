# Standalone DataStage on Windows - Consolidated Agent Host

A Windows-only single-tier DataStage environment where…

*   The MettleCI Workstation is installed on your DataStage Engine tier, and
    
*   The MettleCI Agent is installed on your DataStage Engine tier.
    

**This topology may find some applications in POC or Demo environment, but is not recommended for real-world DataStage development.** ![](./attachments/Windows%20Topology%20Cosolidated%20Agent%20host.png)

# Notes

*   The Information Server environment (in this topology) has all tiers deployed on a single host. **This is not recommended as your DataStage Engine will have its licensed capacity reduced by the presence of other software components.**
    
*   The MettleCI Workbench Service runs (in this topology) on the Windows-based DataStage Engine tier. This is because this service requires a shared filesystem with the MettleCI Unit Test Harness which can only be installed on the Engine tier.
    
*   The MettleCI Agent host also shares the same host, and will have actions invoked by your selected CI/CD build tool via the installed CD/CD agent. The MettleCI CLI is used by the CI/CD Agent to automate build and deployment activities. The MettleCI CLI and Agent need to be installed on a Windows host co-resident with a DataStage Client tier in order to enable the automation of the DataStage job compilation process, which requires the use of a Windows-based Client tier.