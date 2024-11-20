# Automated Unit Testing

# Introduction

MettleCI enables you to rapidly (in most cases, automatically) create re-usable Unit Tests for your DataStage Jobs, feed them with data and run them. The focus of MettleCI Unit Testing is create and publish, to Git, a set of artefacts (test specifications and associated test data) that embody a definition of (used to demonstrate) your job's correct functional behaviour.  These artefacts can be propagated to downstream environments where they can be used to verify your job's consistent behaviour on DataStage platforms which may not have the same configuration, connectivity, or even DataStage version as the project in which the original job was developed.  

The Unit being tested by MettleCI's Unit Test capability is an individual DataStage job.  Unit testing is not intended to replace performance testing, nor does it support connecting to source or target databases to validate SQL queries.  Broader-scoped testing activities (typically involving database interaction) is the role of MettleCI's ***End-to-End tests*** which are created, managed, and executed separately to Unit Tests. 

## Sections

*   [Unit Test Fundamentals](./automated-unit-testing/unit-test-fundamentals.md)
*   [Creating a Unit Test](./automated-unit-testing/creating-a-unit-test.md)
*   [Unit Test Specification Format](./automated-unit-testing/unit-test-specification-format.md)
*   [Intercepting Existing Test Data](./automated-unit-testing/intercepting-existing-test-data.md)
*   [Managing your Unit Test data volumes](./automated-unit-testing/managing-your-unit-test-data-volumes.md)
*   [Manually Editing Unit Test Data](./automated-unit-testing/manually-editing-unit-test-data.md)
*   [Capturing a Baseline Test Result](./automated-unit-testing/capturing-a-baseline-test-result.md)
*   [Executing a Unit Test](./automated-unit-testing/executing-a-unit-test.md)
*   [Row Count Unit Testing](./automated-unit-testing/row-count-unit-testing.md)
*   [Unit Testing Job Sequences](./automated-unit-testing/unit-testing-job-sequences.md)

## Test Data

Test data can be derived using a number of methods, each of which may be used in combination with one another:

1.  Entered manually into the Excel-like test data file tables in MettleCI Workbench
    
2.  Provided as CSV file which are imported into the relevant test data file using MettleCI Workbench
    
3.  Fabricated using MettleCI Workbench's Data Fabrication capabilities (illustrated in the diagram above)
    
4.  Captured from your existing unit test data sources using MettleCI's Data Interception capabilities (see below)
    

To create Unit Tests for your jobs you'll need to [Install the MettleCI Workbench](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/453902355/Installing+MettleCI+Workbench).

To intercept test data and run Unit Tests you'll need to [Install the Unit Testing Harness](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/454393879/Installing+MettleCI+Unit+Test+Harness).

* * *

## Related FAQ Pages

*   Page:
    
    [Can data from the production environment be used for unit testing?](/wiki/spaces/MCIDOC/pages/445907004/Can+data+from+the+production+environment+be+used+for+unit+testing)
    
*   Page:
    
    [Can we unit test a sequence of Jobs?](/wiki/spaces/MCIDOC/pages/469631035/Can+we+unit+test+a+sequence+of+Jobs)
    
*   Page:
    
    [Do we need to modify our jobs to be compatible with MettleCI?](/wiki/spaces/MCIDOC/pages/449740827/Do+we+need+to+modify+our+jobs+to+be+compatible+with+MettleCI)
    
*   Page:
    
    [Does the MettleCI Unit Test job parameter need to be removed from a job before promoting it to a Production environment?](/wiki/spaces/MCIDOC/pages/416252086/Does+the+MettleCI+Unit+Test+job+parameter+need+to+be+removed+from+a+job+before+promoting+it+to+a+Production+environment)
    
*   Page:
    
    [How are our existing test data inputs and outputs captured?](/wiki/spaces/MCIDOC/pages/416120980/How+are+our+existing+test+data+inputs+and+outputs+captured)
    
*   Page:
    
    [How does Unit Testing work with RCP and/or schema files?](/wiki/spaces/MCIDOC/pages/457474124/How+does+Unit+Testing+work+with+RCP+and+or+schema+files)
    
*   Page:
    
    [How set configure default credential mapping when user registry sharing is enabled](/wiki/spaces/MCIDOC/pages/2352578583/How+set+configure+default+credential+mapping+when+user+registry+sharing+is+enabled)
    
*   Page:
    
    [Is the unit testing function dependent upon the design of our jobs? Are there any restrictions?](/wiki/spaces/MCIDOC/pages/450003012/Is+the+unit+testing+function+dependent+upon+the+design+of+our+jobs+Are+there+any+restrictions)
    
*   Page:
    
    [What skills are required to use MettleCI on daily basis?](/wiki/spaces/MCIDOC/pages/396919043/What+skills+are+required+to+use+MettleCI+on+daily+basis)
    
*   Page:
    
    [Why don't Before/After job routine failures cause a Unit Test failure?](/wiki/spaces/MCIDOC/pages/2546434049/Why+don+t+Before+After+job+routine+failures+cause+a+Unit+Test+failure)
    
*   Page:
    
    [Will MettleCI have access to our company's private data?](/wiki/spaces/MCIDOC/pages/457867277/Will+MettleCI+have+access+to+our+company+s+private+data)