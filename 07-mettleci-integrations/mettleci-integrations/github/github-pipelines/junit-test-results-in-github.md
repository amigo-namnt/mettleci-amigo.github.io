# JUnit Test Results in GitHub

GitHub Actions does not currently provide native support for parsing JUnit files and exposing them as GitHub Actions Annotations (i.e. signalling that workflows have generated warnings or failures.) To achieve this, you will need to rely on third party actions contributed by the GitHub community.

The sample GitHub workflows supplied with MettleCI utilise the [action-junit-report](https://github.com/mikepenz/action-junit-report) plugin, but you may prefer to use one of the [many others available](https://github.com/marketplace?query=JUnit) in its stead. Whichever you choose you should ensure that the action enables you to fail the workflow based on the presence of a failed test.