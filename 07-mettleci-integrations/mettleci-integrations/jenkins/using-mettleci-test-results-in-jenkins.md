# Using MettleCI Test Results in Jenkins

MettleCI can generate [JUnit-formatted test results](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1754890299/JUnit+Test+Results) for the following MettleCI Pipeline operations:

*   Page:
    
    [Compliance Test Command](/wiki/spaces/MCIDOC/pages/408322069/Compliance+Test+Command)
    
*   Page:
    
    [DataStage Compile Command](/wiki/spaces/MCIDOC/pages/410157081/DataStage+Compile+Command)
    
*   Page:
    
    [DataStage Connector Migration Command](/wiki/spaces/MCIDOC/pages/410681364/DataStage+Connector+Migration+Command)
    
*   Page:
    
    [DataStage Deploy Command](/wiki/spaces/MCIDOC/pages/423952410/DataStage+Deploy+Command)
    
*   Page:
    
    [DataStage Execute Command](/wiki/spaces/MCIDOC/pages/458817755/DataStage+Execute+Command)
    
*   Page:
    
    [UnitTest Test Command](/wiki/spaces/MCIDOC/pages/718831617/UnitTest+Test+Command)
    

Each command details the name of the JUnit XML file generated, or provides an option for you to specify the output filename. Jenkins has [basic support for reporting or acting on the contents of these files](https://www.jenkins.io/doc/pipeline/tour/tests-and-artifacts/) without employing [JUnit plugins](https://plugins.jenkins.io/ui/search?query=junit).

# Automatically Creating or Updating Work Items from JUnit Test Results

Jenkins does not provide a Work Item Management facility but it is likely that you could easily use your MettleCI jUnit XML test results to automatically maintain relevant Work Items in an associated Work Item Management system. This might necessitate adding a Pipeline step which parsed your jUnit output file and used the API of you Work Item Management system to create and/or update relevant Work Items as appropriate. See your Work Item Management system’s documentation for more guidance.