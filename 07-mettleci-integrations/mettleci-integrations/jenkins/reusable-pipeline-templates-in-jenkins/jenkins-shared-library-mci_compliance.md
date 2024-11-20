# Jenkins Shared Library - mci_compliance

This Shared Library hosts a Custom Step which is an example implementation of the [Compliance step](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2222653459/MettleCI+Example+Pipeline+for+DevOps#Compliance-Test-Warnings) of a MettleCI Pipeline. It provides parameterised set of steps which…

*   Checks out the specified Compliance repository
    
*   Invokes the [MettleCI compliance test](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408322069/Compliance+Test+Command) command test your repository's DataStage assets against your Compliance rules
    
*   Publishes the generated [JUnit](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1754890299/JUnit+Test+Results) Compliance results back to your Jenkins Controller.
    

Here’s the pseudocode for the Shared Library:

```
def call(
    def COMPLIANCE_REPO_CREDENTIALS,
    def COMPLIANCE_REPO_URL,
    def RULESDIR,
    def TESTSUITENAME,
    def CONTINUEONFAIL
) {
    try {
        // Perform a 'git checkout' of a remote repository which is NOT the repository from which this pipeline code was sourced
        checkout COMPLIANCE_REPO_URL using COMPLIANCE_REPO_CREDENTIALS 

        // Executes the 'mettleci compliance test' command to test your repository's DataStage jobs against your Compliance rules.
        // Note that 'mettleci compliance test' is not the same as 'mettleci compliance query' - See the documentation for more details. 
        mettleci compliance test $RULESDIR $TESTSUITENAME

    }
    finally {                                                         // Whether the above is successfult or not...
        junit testResults "compliance_report_${TESTSUITENAME}.xml"    // Publish CCMT output as JUnit Test Results
            allowEmptyResults: true                                   // Don't fail the build on missing test result files or empty test results
            skipPublishingChecks: true                                // Don't automatically publish test results to Git
            skipMarkingBuildUnstable: (CONTINUEONFAIL)                // (Optionally) mark the build as successful,even if there are test failures reported
    }
}
```

Note that this Custom Step makes used of Jenkins' [JUnit plugin](https://www.jenkins.io/doc/pipeline/steps/junit/).