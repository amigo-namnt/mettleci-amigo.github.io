# The Problem With Message Handlers

> [!INFO]
> This page is an opinion on DataStage solution design practices and doesn’t affect MettleCI support for the functionality discussed.

There are two types of Message Handlers in DataStage.

1.  **Project Level Message Handlers:** These are installed in an application directory per Engine and and aren't supported by MettleCI so should be migrated manually.
    
2.  **Job Level Message Handlers:** There is MettleCI functionality to support their deployment only.  While MettleCI deploys Job Level Message Handler files from a Project's Git repository, it doesn't offer native check-in and deletion functions for them so they must be managed via command line Git.
    

The following observations about Message Handlers, based on Data Migrators' decades of field experience, suggest DataStage developers and architects should reconsider their use.

## Message Handlers are not DataStage assets

Message Handlers are not an asset of DataStage. IBM documentation notes that they cannot be managed the same way as jobs, sequences, parameter set definitions, etc., are managed. They cannot be placed in an ISX export of their own, they have to be associated with a Job.

> [!WARNING]
> According to [https://www.ibm.com/support/knowledgecenter/en/SSZJPZ\_11.5.0/com.ibm.swg.im.iis.ds.deploy.help.doc/topics/usingismanager.html](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.5.0/com.ibm.swg.im.iis.ds.deploy.help.doc/topics/usingismanager.html)
> "You can use the IBM® InfoSphere® Information Server Manager (the deployment tool) to move, deploy, and control your IBM InfoSphere DataStage® and QualityStage® assets."
> However, message handlers cannot be managed individually using the IS Manager or `istool` command line tool.

MettleCI can’t handle them in the conventional way for the reasons above. Project-Level Message Handlers can’t be handled at all, while special provisions must be made for Job-Level Message Handlers. Refer to [this page](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2687074305/Deploying+Message+Handlers+with+Bamboo) to understand the complicated manual process that is required to obtain and on-board Job-Level Message Handlers as you apply devops to your DataStage solution. These considerations mean extra work during all migrations and deployments.

## Message Handlers may disguise poor development practices

High-performing DataStage development teams rightly view message handlers as something that risks disguising poor coding or Job design decisions. They are most often found in organizations that mandate that Jobs should run without warnings but with little else to encourage their developers to remediate the root cause. Under this design standard, Jobs are often set to Abort (e.g. via an After Routine) if they generate warning messages. Unfortunately, this often leads to developers - especially those under pressure - applying Message Handlers to quickly get compliant and move on.

## Message Handlers are subject to regression

As previously highlighted, the very nature of IBM’s tools for managing Job Level Message Handlers in Information Server means any automation solution for them will be at risk of permanent regression with future IBM Fix Packs and Releases. Since they are not “assets”, they may be regarded as “second class citizens” when breaking changes are introduced.

## Conclusion

In view of the above drawbacks, it’s recommended that organizations reconsider the wisdom of using Message Handlers and, instead, focus on refactoring Jobs to eliminate (or at least minimise) warnings or errors. MettleCI features like Unit Testing and Compliance are a great way to increase the safety and speed of such refactoring efforts for developers. In conjunction, Job Schedulers can be reconfigured to be able to allow Warnings in exceptional circumstances. In this way, development standards improve but in the unlikely situation that there is no alternative, Job Warnings can be applied consciously, instead of by default.