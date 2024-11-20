# Shared Container image previews not available in Atlassian Bitbucket

# Environment

Standalone (non-Cloud Pak) DataStage installation, Atlassian Bitbucket.

# Problem

When committing a a Shared Container to a Git repository which supports DataStage image previews (currently limited to Atlassian Bitbucket) no images of the Shared Container’s design are created. It works fine for Jobs and Sequences, but not for Shared Containers.

# Reason

The underlying IBM components upon which MettleCI relies to generate those previews do not support generating previews of Shared Containers.

# Solution

There are currently no workarounds for this issue.

* * *

# See also

*   [Installing the MettleCI Job Visualisation Plugin for Atlassian Bitbucket](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/733675614/Installing+the+MettleCI+Job+Visualisation+Plugin+for+Atlassian+Bitbucket)