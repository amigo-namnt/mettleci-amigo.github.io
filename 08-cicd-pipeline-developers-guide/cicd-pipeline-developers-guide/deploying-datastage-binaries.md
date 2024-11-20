# Deploying DataStage Binaries

# Introduction

Regardless of the technology you use to deploy your DataStage solutions (MettleCI or a less capable custom-crafted script-based approach) your software deployment process will contain these common steps:

1.  Get the code from source control
    
2.  Compile it (DataStage is a compiled visual language)
    
3.  Configure the software and deploy it to DataStage Project(s) in specific target environments
    

One decision you’ll need to make is whether you build your binaries once or do you build them on demand as part of each deployment.

The strategy to build as part of each deployment is illustrated the diagram below, where the code is fetched, compiled, and tested before each deployment. DataStage designs (the DataStage equivalent of source code) are deployed to target environment where they are compiled in-situ using the compiler on that environment. To ensure that the same code is used for each deployment the process needs to use the capabilities of a build system (like Bamboo or Jenkins, for example) to ensure it builds the binaries from the appropriate revision or tag each time.

![](./attachments/Multi-compile%20Deployment.png)

Some users operate in environments where organisational constraints mean that they do not have access to a DataStage compiler on their Production environments and can instead only deploy DataStage binaries from an artefact repository. This follows an approach more like the diagram below, where the build happens once, and the same set of binaries (the deployable artefacts) are reused when deploying to each environment.

![](./attachments/Single%20Binary%20Deployment.png)

While there can be an efficiency saving in building binaries once, the most common reason for wanting to adopt this approach is the perceived reduction in deployment risk. A build process isn't just a deterministic \`code in → binaries out’ function. The binaries produced don't just depend on the code going in, but also the libraries, compiler, O/S updates, and myriad other aspects that can differ between environments, and alter over time. Compiling your DataStage jobs on the destination environments as part of each deployment means you run the risk of differences creeping in to your Production deployment due to differences in your environmental configuration at compile time. Similarly, DataStage binaries compiled in one environment can be incompatible with other environments due to minor O/S or DataStage version differences.

An additional complicating factor is that of statically linked Shared Containers. It is important when deploying DataStage jobs to a target environments in which they are to be compiled to also deploy any Shared Containers referenced by that DataStage job. If not managed extremely carefully, it is possible to produce a binary of a DataStage job which cannot be produced from Git source control, as the DataStage job and its referenced shared container are misaligned. This is extremely dangerous from a configuration management and testing perspective.

MettleCI CLI’s capabilities can be used to implement both of the deployment scenarios ('binary only' or ‘compile on target’, described above) by using its different options.

# Deploying source and compiling in the target environment

Where possible, Data Migrators recommend that users employ the MettleCI CLI’s `datastage deploy` command to ensure the integrity of your import and compile process. This effectively performs an incremental `isx import` and `isx compile` in tandem. The source ISX files for Continuous Integration come from Git and, when successful, a Release is created using the source ISX files. All downstream environments use the same deployment process, the only difference being that source ISX files come from the release artefacts rather than Git:

![](./attachments/CI%20Pipeline%20Binaries%201.png)

# Building and deploying binaries

This process uses Release Artefacts comprising one or more ISX files which each contain a binary rather than source. Just like our existing process, the release needs to contain ISX binaries for the entire DataStage project but we use an Incremental Export process to reduce the time taken during Continuous Integration. Downstream environments are then deployed using an Incremental Import process which takes the ISX binaries for the entire project but only imports those which have changed since the last deployment. From a “logical” implementation process, the Incremental Export should be the same as performing a whole project binary export while the Incremental Import should be the equivalent of deleting the target project and then performing a full project import with binaries. Details of how incremental export/import should work are described later.

![](./attachments/Binary%20Deployment%202.png)

This process cannot use the MettleCI `datastage deploy` command as that command automatically performs a compilation in the target environment. In this scenario the `isx export` command enables you to include binaries in your exports (using the `-include-binaries` switch) so that the resulting file can be imported and executed on a compatible environment without requiring recompilation. The `isx import` can then be used to import the resulting binaries into one or more target environments without requiring that they are recompiled. Design information can be stripped from the files during the import process by using the import command’s `-exclude-designs` switch. Note that both of these processes are still incremental as they make use of a `-project-cache`. For example:

```
$> mettleci isx export 
   -domain test2-svcs.datamigrators.io:59445
   -username myuser -password mypassword 
   -server test2-engn.datamigrators.io -project myproject 
   -project-cache "C:\\dm\\mci\\cache\\hostname\\myproject"
   -include-binaries

$> mettleci isx import 
   -domain services.myorg.com:59445
   -username myuser -password mypassword
   -server engine.myorg.com -project myproject
   -project-cache "C:\\dm\\mci\\cache\\hostname\\myproject"
   -exclude-designs
```

# See also

*   [Repeatable DataStage Project Deployments - Deployment of job binaries](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1266843717/Repeatable+DataStage+Project+Deployments#Deployment-of-job-binaries)