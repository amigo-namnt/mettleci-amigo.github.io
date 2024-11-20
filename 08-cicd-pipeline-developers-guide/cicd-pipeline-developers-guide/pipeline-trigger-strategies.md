# Pipeline Trigger Strategies

# Introduction

There are a number of different ways in which your CI/CD pipeline can be triggered. You should select the trigger strategy you employ carefully. MettleCI is typically demonstrated using the [Immediate build on commit (Polling Git)](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2240610366/Pipeline+Trigger+Strategies#Immediate-build-on-commit-(Polling-Git)) mechanism, bit some other strategies are briefly introduced here.

*   [Manual Triggers](#manual-triggers)
*   [Resource Triggers](#resource-triggers)
    *   [Immediate build on commit (Polling Git)](#immediate-build-on-commit-polling-git)
    *   [Build after Quiet Period](#build-after-quiet-period)
    *   [Build on Commit Message directive](#build-on-commit-message-directive)
*   [Webhook Triggers](#webhook-triggers)
    *   [Immediate build on commit (Git Webhook)](#immediate-build-on-commit-git-webhook)
*   [Schedule Triggers](#schedule-triggers)

> [!WARNING]
> Note that Data Migrators do not recommend adopting a trigger strategy which could result in the invocation of multiple pipelines concurrently, as this could lead to resource contention, particularly when multiple agents attempt to utilise DataStage-specific resources (such as command line utilities) on a single [MettleCI Agent Host](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1770520622/A+Summary+of+MettleCI+Components#MettleCI-Agent-Host).

# Manual Triggers

Most, if not all, build systems will enable you to trigger a build directly, using either its user interface or a programatic interface, commonly exposed through a command line or REST endpoint.

| **Pros** | **Cons** |
| --- | --- |
| *   Total control over the timing of pipeline<br>    <br>*   Run the pipeline when you want | *   No guarantee that a pipeline will get run for a commit<br>    <br>*   Unnecessarily delays Developer feedback on the accuracy of code changes<br>    <br>*   Allows the Git repository and build status to drift from one another<br>    <br>*   Undermines the principle of continuous integration testing |

# Resource Triggers

## Immediate build on commit (Polling Git)

In many cases you will want every commit to your Git repository to trigger a build.

| **Pros** | **Cons** |
| --- | --- |
| *   Ensure that the pipeline status always mirrors the quality of the contents of the Git repository | *   Can be difficult for Developers to co-ordinate separate commits which form a [changeset](https://git-scm.com/docs/gitglossary#Documentation/gitglossary.txt-aiddefchangesetachangeset), thereby leading to a number of potentially redundant pipeline invocations.<br>    <br>*   Poorly configured polling interval can create unnecessary network activity between your build system and Git repository. (Data Migrators' MettleCi demonstrations typically use a polling interval of 1 minute)<br>    <br>*   Some SaaS solutions may impose costs or limits related to the level of polling permitted |

## Build after Quiet Period

Commits often come in a burst, either because…

*   Developers sometimes forget to commit some important components of their solution, or
    
*   In the tranquility of waiting for their build tool to complete a CI test they realise a problem in the commit and want to quickly make follow-up changes, or
    
*   A single, cohesive body of work requires multiple commits, potentially from multiple Developers, and these will each trigger a separate build pipeline, with the early (incomplete) invocations failing due to missing dependencies which have yet to be committed.
    

A common way for the build server to accommodate this behaviour is configure it to wait for a burst of commits and pushes to finish before attempting a build. This can reduce the chance of a broken build, and it is also sometimes useful in reducing the average turn-around time for builds that take longer.

Most build servers are capable of waiting for a push burst to complete before triggering a new build. This feature is called a **Quiet Period** and normally permits the build project administrator the configure the preferred delay before initiating a build.

| **Pros** | **Cons** |
| --- | --- |
| *   Enables multiple commits/pushes to contribute to a single [changeset](https://git-scm.com/docs/gitglossary#Documentation/gitglossary.txt-aiddefchangesetachangeset) while triggers a build<br>    <br>*   Reduces the likelihood of triggering a build on incomplete an [changeset](https://git-scm.com/docs/gitglossary#Documentation/gitglossary.txt-aiddefchangesetachangeset) which is expected to fail. | *   Introduces a small, user configurable (but potentially unnecessary) delay in triggering a build for a single commit |

## Build on Commit Message directive

Some build systems provide capabilities (sometimes accessed through plugins) that enable Developers to trigger build pipelines only when a commit message contains a certain ‘trigger’ text. e.g.

`This is my commit message @build`

In this example the build pipeline will not normally run for every commit. but a relevant plugin in the build system will recognise and respond to the presence of the `@build` text and invoke your pipeline for you.

This approach has the same pros and cons as the ‘Manual’ approach detailed above.

We’ll leave the assessment of the merits of this approach, and the identification of any plugins which enable it in your build system, to the reader.

| **Pros** | **Cons** |
| --- | --- |
| *   Provides many of the benefits of the **Build after Quiet Period** strategy | *   Not (normally) natively supported by build systems, so…<br>    <br>*   Typically requires approval, installation, and configuration of a third-party plugin<br>    <br>*   Requires Developers to adhere to a manual process which, if ungoverned, still allows the Git repository and build status to drift from one another |

# Webhook Triggers

## Immediate build on commit (Git Webhook)

Git hooks are event-based triggers where the events are identified and responded to by the software managing your Git repository. When certain Git actions occur the software will look for any configured **hooks** (typically defined within files in the Git repository itself) to respond by triggering a scripted behaviour which typically makes a REST call to an associated third-party system or service. Some scripts run prior to an action taking place, which can be used to ensure code compliance to defined standards, for sanity checking, or to provision a testing environment. Other scripts run after an event, in order to deploy code, modify files, and so on.

| **Pros** | **Cons** |
| --- | --- |
| *   Webhooks allow your Git host to trigger build pipelines soon as a commit appears, without the latency introduced by polling.<br>    <br>*   Avoids the extra network noise caused by polling. | *   Precludes Developers from co-ordinating the separate commits forming a [changeset](https://git-scm.com/docs/gitglossary#Documentation/gitglossary.txt-aiddefchangesetachangeset), thereby leading to a number of redundant pipeline invocations |

> [!INFO]
> Note that sometimes Build after Quiet Period strategies can be combined with Webhook Triggers, reducing or eliminating the changeset challenge, but introducing additional delay, as with polling based Quiet Period strategies.

# Schedule Triggers

Some build systems also permit the triggering of pipelines on a schedule. This can be useful to trigger broader-scoped integration or performance tests which require larger volumes of data and take longer to complete. These are commonly scheduled overnight (while Developers are not actively using the environment) and can be used in conjunction with other trigger types described above to provide fast feedback on the quality of your solution.

| **Pros** | **Cons** |
| --- | --- |
| *   Useful for broad-scoped, slower integration tests with greater resource requirements | *   Not useful for same-day feedback commits |