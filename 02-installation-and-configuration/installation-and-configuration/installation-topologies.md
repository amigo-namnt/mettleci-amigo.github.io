# Installation Topologies

These pages summarise some (but not all) possible MettleCI deployment topologies.

## [A Summary of MettleCI Components](./installation-topologies/a-summary-of-mettleci-components.md)

A summary of all of the components referenced in [MettleCI Topology diagrams](./installation-topologies.md).

## [MettleCI Components for Upgrades to DataStage to v11.7.X](./installation-topologies/mettleci-components-for-upgrades-to-datastage-to-v117x.md)

When upgrading to the latest non-Cloud Pak version of DataStage you’ll wonder which MettleCI tools and assets need to be upgraded, replaced, or reconfigured, and which can be safely left in place. This page outlines the technical aspects of re-configuration and will deliberately omit the important project management aspects of handling a cutover between old and new DataStage environments.

## [MettleCI for DataStage Failover Configurations](./installation-topologies/mettleci-for-datastage-failover-configurations.md)

When deploying MettleCI to DataStage environments configured for failover you will need to ensure that your MettleCI Agent Host is included in the replication set, and that it uses shared storage so that its disk image is retained in an unaltered state during a failover event.

Your ALM (Application Lifecycle Management) platform - Git, Work Item Management, and Build tools - may also be replicated to support failover, although for simplicity this has been omitted from this diagram.

## [Standalone DataStage on Different Versions - Concurrent use for upgrades](./installation-topologies/standalone-datastage-on-different-versions-concurrent-use-for-upgrades.md)

A hybrid environment featuring two DataStage platforms:

1.  A traditional standalone DataStage environment on v11.5.0 (for example), and
    
2.  A traditional standalone DataStage environment on v11.7.1 (for example)
    

Each environment has its own dedicated MettleCI Agent running on a dedicated Windows host.

This topology is ideal for customers using MettleCI to upgrade between different versions of Standalone DataStage.

## [Standalone DataStage on Unix - Dedicated Agent Host](./installation-topologies/standalone-datastage-on-unix-dedicated-agent-host.md)

A Unix-based multi-tier DataStage environment where…

*   The MettleCI Workstation is installed on your DataStage Engine tier, and
    
*   The MettleCI Agent is installed on a dedicated Windows host
    

## [Standalone DataStage on Windows - Consolidated Agent Host](./installation-topologies/standalone-datastage-on-windows-consolidated-agent-host.md)

A Windows-only single-tier DataStage environment where…

*   The MettleCI Workstation is installed on your DataStage Engine tier, and
    
*   The MettleCI Agent is installed on your DataStage Engine tier.
    

**This topology may find some applications in POC or Demo environment, but is not recommended for real-world DataStage development.**

## [Standalone DataStage on Windows - Dedicated Agent Host](./installation-topologies/standalone-datastage-on-windows-dedicated-agent-host.md)

A Windows-only multi-tier DataStage environment where…

*   The MettleCI Agent is installed
    
*   The MettleCI Workstation is installed on your Windows-based DataStage Engine tier, and
    
*   The MettleCI Agent is installed on a separate, dedicated Windows host
    

## [The Mettle Agent Host](./installation-topologies/the-mettle-agent-host.md)

The MettleCI Agent Host is a dedicated Microsoft Windows host which is used to run three major components:

*   A [DataStage Client tier](https://www.ibm.com/docs/en/iis/11.7?topic=components-client-tier),
    

## [Using Multiple MettleCI Agents](./installation-topologies/using-multiple-mettleci-agents.md)

Many customers cannot use a single MettleCI Agent Host to communicate with multiple DataStage environments due to organizational security policies.

This page describes how multiple MettleCI Agents Host can be configured when you need to segregate agent access by DataStage environment or network zone.

## [Virtual Desktop Example Topology](./installation-topologies/virtual-desktop-example-topology.md)

An example topology for an environment using the following technologies:

*   Citrix desktop virtualisation
    
*   Atlassian Bitbucket Git repository
    
*   Atlassian Jira work item management platform
    
*   Jenkins build tool