# Development Model Options & Recommendations

# Introduction

Although DataStage source artifacts (such as jobs, routines and rule sets) have a compilation or provisioning process, there are technical constraints within Information Server which can result in unexpected results when treating compiled output as deployable artifacts from a Configuration Management perspective. Therefore, all DataStage source artifacts will be committed and managed in the source control system and the process that Information Server refers to as compilation or provisioning will be considered a standard step of deploying source artifacts to a managed environment.

DataStage jobs make up the vast majority of all source artifacts that represent MettleCI based projects.  These source artifacts can be represented in two possible formats:

1.  **ISX** – Supports all Information Server asset types and is the format used by MettleCI.  Compressed XML (binary) based format. 
    
2.  **DSX** – Older Information Server format that only supports a subset of all Information Server asset types.  Text based format, not supported by MettleCI. 
    

While the DSX format might be considered “human readable”, both DSX and ISX formats represent DataStage jobs as an acyclic graph with complex relationships and extensive metadata properties.  This complexity means that although DSX files are text and are readable, it is impossible for a human to open them in a text editor and *fully* *understand* the DataStage asset that they represent.

Additionally, DataStage does not provide a method to merge two DSX or ISX files making it near impossible to reliably perform a merge.  Therefore all DataStage source artifacts should be considered as binary files within the context of the source control management system.  Unfortunately, binary files cannot be merged which makes any development model that uses a high degree branching a merging (ie. Gitflow) inappropriate.

> [!INFO]
> Instinctively, developers will make a large number of changes across multiple jobs and only check-in when they are completely happy with all changes.  Unfortunately, this behavior results in large, infrequent check-ins which will:
> *   Increase cycle time
>     
> *   Slow down feedback
>     
> *   Introduce variability in CI/CD pipelines flow
>     
> *   Increase risk and overheads
> Developers should consider breaking up their changes so they can be checked in and deployed (possibly to production) without any negative impacts.  Eg. Instead of adding a new transform and load as a single check-in, add and check-in the transform and then add and check-in load.
> There are well known development practices that can make this a viable approach even the most complex ETL changes:
> *   Feature Toggles - Use job parameters to turn on/off new functionality at runtime
>     
> *   Branch by Abstraction - Provide one or more implementations of the same job and use job sequences or batch schedulers to decide which version to run at run time.

# Trunk Based Model

Under a [trunk based development model](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1414234192/Trunk+Based+Development) developers make changes directly to the master branch.  Developers make changes in a development DataStage project and commit them directly to "master" branch. The Continuous Integration tool (Jenkins, Bamboo, etc.) will detect changes on the "master" branch and deploy them to a  DataStage Continuous Integration project where the quality of all source artifacts can be verified.

The following diagram depicts the basic trunk based development model.  The horizontal line represents a branch within the source control management system and the circles shows commits being added in chronological order (left being earlier commits, right being later).    

### Version Control

![](./attachments/Branching%20model%20-%20Standard.png)

### Continuous Delivery Pipeline

![](./attachments/Trunk%20Pipeline.png)

**Positives**

*   Easy to understand
    
*   Master branch always reflects the latest version of code ready for Continuous Integration
    
*   Merge conflicts can never occur
    
*   Continuous Integration occurs after every change
    
*   Supports fast release cadence and continuous deployment activities
    

**Negatives**

*   Not clear when code has passed Continuous Integration
    
*   A fast release cadence is required as "hot fixes" cannot be deployed independently of normal development activities
    
*   Trunk based development practices such as Feature Toggles and Branch by Abstraction increase the learning curve for new developers
    

# Trunk + Development Model

> [!INFO]
> ### NOTE
> This is the **recommended branching strategy** for teams first starting with MettleCI. Once the team is comfortable with this approach, it can be expanded easily to include support for emergency fixes, if required.

This is a variation of the trunk based development model where there are two active branches, "develop" and "master".  Developers make changes in a development DataStage project and commit them to the "develop" branch. The Continuous Integration tool will detect detect changes on the "develop" branch and deploy them to a  DataStage Continuous Integration project where the quality of all source artifacts can be verified.  If no problems are detected during Continuous Integration, the Continuous Integration tool will automatically merge the changes from the Development branch to the Master branch.

### Version Control

![](./attachments/Branching%20model%20-%20Trunk.png)

### Continuous Delivery Pipeline

![](./attachments/Trunk%20and%20development%20Pipeline.png)

This process ensures the following constraints are met:

*   Commits are only made to the Develop branch
    
*   Merges only ever occur from Develop to Master branch
    
*   The Master branch is never directly modified
    

Because Develop and Master branches can never be modified concurrently, Git is able to perform what is known as a *fast-forward* merge.  Merges of this type don’t actually perform any merging and instead results in the Master branch being updated to be exactly the same as the Develop branch.  This avoids the issues and risks related to merging DataStage source artefacts that were described earlier in this documentation.

Depending on the amount of change occurring during development, Continuous Integration can be merging changes to Master branch multiple times throughout a single day.  At any given point, a release (v1.0 and v2.0 in the diagram) can be created from the Master branch.   Once a release has been created, an automated deployment to one or more managed environments can be triggered.

**Positives**

*   Easy to understand
    
*   Development branch reflects the latest code ready for Continuous Integration
    
*   Master branch reflects the latest code that has passed Continuous Integration
    
*   Merge conflicts can never occur
    
*   Continuous Integration occurs after every change
    
*   Supports fast release cadence and continuous deployment activities
    

**Negatives**

*   A fast release cadence is required as "hot fixes" cannot be deployed independently of normal development activities
    
*   Trunk based development practices such as Feature Toggles and Branch by Abstraction increase the learning curve for new developers
    

# Trunk + Emergency Fixes

Emergency fixes should be managed by creating a new branch from the latest production release on the Master branch. Developers can continue to work in the development DataStage project as described in the previous section or emergency fixes can be developed in the Hotfix DataStage project.  The DataStage Hotfix project is updated whenever a release goes live and changes are committed to the currently active Hotfix branch.

### Version Control

![](./attachments/Branching%20model.png)

### Continuous Delivery Pipeline

![](./attachments/Hotfix%20Deployment%20Pipeline.png)

However, unlike the trunk based scenarios described in the previous sections, changes on Hotfix branches should not be automatically merged back to master.  Doing so could introduce merge conflicts or regression depending on how the merge of ISX files is handled.  Instead the following options are available to ensure changes implemented as hotfixes and deployed to production are not lost when a new version from Master is deployed.

*   **Perform a git merge with the “--ff-only” switch**.  Git will attempt to perform a *fast-forward* merge which avoids the issues and risks related to merging DataStage source artefacts that were described earlier in this documentation.   This will not always be possible, so an alternative approach will need to be chosen when the merge fails.  Never attempt to force or drop the “--ff-only” switch.
    
*   **Use Test Driven Development and raise issue with test case**.  If a *fast-forward* merge is not possible, then there must be active development on the Develop branch.  Instead of attempting to replicate the hotfix on the Development branch, which is extremely error prone, a new issue should be created in the development backlog which outlines the problem identified in Production along with relevant test cases for verifying it has been resolved.  No new versions (other than hotfixes) should be released until all issues raised as a result of a hotfix have been resolved.  This is an application of Test Driven Development (TDD).
    

Unlike traditional hot fix branching strategies, we have deliberately chosen to use a single eternal Hotfix branch.  This has been done to reduce the number of manual configuration changes required within your Continuous Integration and MettleCI Workbench tools after every major release.  A merge from the Master to Hotfix branch is performed after every major release using a merge strategy of "theirs", this results in the Hotfix branch being *exactly* the same as the revision being merged from master.

**Positives**

*   Development branch reflects the latest code ready for Continuous Integration
    
*   Master branch reflects the latest code that has passed Continuous Integration
    
*   Emergency fixes can be deployed independent of major releases
    
*   Continuous Integration can be run on both the development and hot fix branches
    
*   Major releases can be deployed on a slower release cadence
    

**Negatives**

*   Changes in hot fix branches have to be manually moved to the develop branch to prevent regression when the next release is deployed.
    
*   Hot fixes can only be developed for a single release at a time
    
*   Trunk based development practices such as Feature Toggles and Branch by Abstraction increase the learning curb for new developers.
    

# Independent Feature Branches

> [!WARNING]
> ### Warning
> Due to the risk of cause merge conflicts due to parallel development, this is not a recommended development model.  In our experience working with a diverse range of clients both large and small, managing partially complete or experimental features through feature toggles or branch by abstraction avoids the need to rely on isolated branches while mitigating merge conflict risks which are unique to DataStage.
> Recommended reading:
> *   [Jez Humble - CI/CD and Feature Branches](https://continuousdelivery.com/2011/07/on-dvcs-continuous-integration-and-feature-branches/)
>     
> *   [Martin Fowler - Feature Branches](https://martinfowler.com/bliki/FeatureBranch.html)
>     
> *   [General Information - Trunk Based Development](https://trunkbaseddevelopment.com/)
> It should also be noted that a peer reviewed, 5 year research program conducted by Dr Nichole Forsgren, Jez Humble and Gene Kim produced empirical evidence that showed that **long lived branches** (those that remained active for longer than 1 day) was a **key indicator for reduced development performance.**  The full findings and statistical reasoning can be found in the book [Accelerate](https://www.amazon.com.au/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339).
> Only use this approach if you are sure that Parallel development is required and you can guarantee that parallel development streams are 100% independent.

In this development model, no changes are made directly to the master branch.  Instead, development occurs on independent "feature" branches which are created from the master branch.  For each actively developed feature branch, there exists an equivalent DataStage development and CI projects.  Developers make changes in the DataStage development project for the relevant feature and use MettleCI to commit changes to the matching feature branch. 

When a feature is deemed to be "complete", the branch is merged into master, the DataStage Project is removed and the Git branch made inactive. As noted in the warning above, if the same job is independently modified in two feature branches, then a merge conflict will occur and developers will need to use the DataStage designer to manually merge changes. Depending on the complexity of the conflicting changes, this manual merge process can take a lot of time, effort and is high risk.

![](./attachments/Branching%20Model%20-%20Parallel.png)

Whenever a feature branch is merged into the Master branch, Continuous Integration will verify this fully integrated set of source assets.  Changes merged to master should also be merged to each feature branch.  While this can be easily performed using Git, MettleCI does not currently provide tools to deploy these changes to the development projects of each active feature.   However, if feature changes are 100% independent, it could be reasonable to suggest that synchronizing the DataStage project is not necessary.

**Positives**

*   Features are completely isolated
    
*   Continuous Integration on each feature branch can verify quality as changes are made
    
*   The master branch always reflects a build which is ready for deployment
    

**Negatives**

*   Integration only occurs after a feature branch is merged and defers discovery
    
*   Merge conflicts are a risk that can only be mitigated through manual governance
    
*   Increased complexity
    
*   Results in large numbers of DataStage projects, each need to be provisioned at time of branch creation
    
*   No tooling (currently) available to sync DataStage feature projects after master → feature branch merge.