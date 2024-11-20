# Jenkins Shared Library - mci_deploy

This Shared Library hosts a Custom Step which is an example implementation of the [Deploy step](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2222653459/MettleCI+Example+Pipeline+for+DevOps#3.-Deploy-CI) of a MettleCI Pipeline.

Here’s the pseudocode for the Shared Library:

```
def call(
  	def PUBLISHCOMPILATIONRESULTS,
    def UPGRADE_DSPARAMS
) {
    try {
        mettleci datastage create-project     // Create DataStage Project
        
        if (UPGRADE_DSPARAMS == true) {
            mettleci remote download          // Fetch Template DSParams
            mkdir                             // Create artifacts dir
            mettleci dsparams merge           // Merge DSParams
        }

        mettleci properties config            // Substitute parameters in DataStage config
        mettleci remote upload                // Transfer DataStage config and filesystem assets
        mettleci remote execute               // Deploy DataStage config and file system assets
        mettleci datastage deploy             // Deploy DataStage project
                                              
        if (PUBLISHCOMPILATIONRESULTS) {
            // Publish JUnit test results
            junit testResults 'log/**/mettleci_compilation.xml'
        }
   }

    catch(e) {
        if (PUBLISHCOMPILATIONRESULTS) {
            // Publish JUnit test results
            junit testResults 'log/**/mettleci_compilation.xml'
        }
        throw e                               // Propagate error to donwstream error handling
    }
```

Note that this Custom Step makes used of Jenkins' [JUnit plugin](https://www.jenkins.io/doc/pipeline/steps/junit/).