# MettleCI CLI warns "'ds.client.path' not configured, assuming DataStage client is available on system PATH"

# Problem

Your MettleCI Command Line does not have an explicit route to the underlying `istool` command required to perform the requested operation. In this case it will simply call `istool` and assume it can be found on the configured system path.

# Solution

Follow the instructions under [Add DataStage Client Engine path to MettleCI Command Line config](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488833077/Installing+MettleCI+CLI+on+Windows#Add-DataStage-Client%2FEngine-path-to-MettleCI-Command-Line-config).