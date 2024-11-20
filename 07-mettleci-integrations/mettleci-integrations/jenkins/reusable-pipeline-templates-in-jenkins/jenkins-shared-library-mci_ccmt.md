# Jenkins Shared Library - mci_ccmt

This Shared Library hosts a Custom Step which is an example implementation of the [CCMT step](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2178875414/MettleCI+Example+Pipeline+for+Upgrades#CCMT-Upgrade-of-Target) of a MettleCI Pipeline. It provides parameterised wrapper around the [mettleci datastage ccmt](#) command.

Here’s the pseudocode for the Shared Library:

```
def call(
    def PUBLISHCOMPILATIONRESULTS,
    def UPGRADEORACLEVARIANT = false,
    def UPGRADEDORACLEVERSION = "11"
) {
    def variantParams = "{CCMT parameters required when using Oracle}"

    try {
         mettleci datastage ccmt ${variantParams}    // Run CCMT to Upgrade Stages

        if (PUBLISHCOMPILATIONRESULTS) {
            // Publish CCMT output as JUnit Test Results when successful
            junit testResults 'log/**/mettleci_compilation.xml'
        }
    }
    catch(e) {
        if (PUBLISHCOMPILATIONRESULTS) {
            // Publish CCMT output as JUnit Test Results in the event of an error
            // See Jenkins JUnit plugin documentation.
            junit testResults 'log/ccmt/**/mettleci_compilation.xml'
                allowEmptyResults: true,              // Don't fail the build on missing test result files or empty test results
                skipPublishingChecks: true            // Don't automatically publish test results to Git
        }
        throw e                                       // Propagate error for downstream error handling
    }
}
```

Note that this Custom Step makes used of Jenkins' [JUnit plugin](https://www.jenkins.io/doc/pipeline/steps/junit/).