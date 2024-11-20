# Jenkins Shared Library - mci_unittest

This Shared Library hosts a Custom Step which is an example implementation of the [Unit Test step](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2222653459/MettleCI+Example+Pipeline+for+DevOps#Unit-Test) of a MettleCI Pipeline.

Here’s the pseudocode for the Shared Library:

```
def call(
    def ENVIRONMENTNAME
) {
    mettleci properties config                              // Configure Properties
    mettleci remote execute "config/cleanup_unittest.sh"    // Cleanup results of previous unit tests
    mettleci remote upload                                  // Unit test specifications and data
    mkdir                                                   // Create unit test report dir

	try {
        mettleci unittest test                              // Run Unit Tests
    }

    finally {                                               // Whether the above is successfult or not...
        mettleci remote download                            // Download unit test reports
        if (exists 'unittest-reports/**/*.xml') {
            junit testResults 'unittest-reports/**/*.xml'   // Publish Unit Test results
        }
    }
}
```

Note that this Custom Step makes used of Jenkins' [JUnit plugin](https://www.jenkins.io/doc/pipeline/steps/junit/).