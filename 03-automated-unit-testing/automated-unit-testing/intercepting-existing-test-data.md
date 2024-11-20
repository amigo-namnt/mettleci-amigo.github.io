# Intercepting Existing Test Data

> [!WARNING]
> Note that the unconstrained capture of unit test data can adversely affect the operation of your DataStage, making it inoperable in the worst case.
> For more information and mitigation strategies please see [Important MettleCI File System Considerations](../automated-unit-testing/managing-your-unit-test-data-volumes.md) .

Each DataStage developer will already have a set of test data that they use to verify their job's correct operation.  MettleCI enables you to capture that data (regardless of whatever technology is currently used to supply it) and encapsulate it into a commonly managed, well governed artefact which can travel with your job to repeatedly assert its consistent behaviour in any downstream environment.  This existing test data can be captured by MettleCI by running a job in 'Data Interception' mode.

Your browser does not support the HTML5 video element

This involves running your Job from either the DataStage Designer (thick client) or DataStage Flow Designer (browser-based client) with the reserved MettleCI Unit Test environment variable set to its 'Interception' value.  This causes MettleCI to 'sniff' the data flowing down the input and output links referenced in your unit test specification and record the data it sees into the unit test data file referenced against each link.  This permits the capture of structured and unstructured data from both batch and streaming data sources.  Note that the data that appears on your output links is also captured as the current definition of 'expected' output into the relevant output data files.

# High Volume Test Data

Capturing large volumes of test data will prevent those data from being interactively edited using MettleCI Workbench’s Unit Test Editor. In these circumstances you will be presented with a message of the form:

> *{data-file-name}*.csv is in ReadOnly mode. The data file is larger than is recommended for editing in workbench.

In this instance you can still edit the data file by exporting it to a CSV file (using the download button on the Unit Test Editor toolbar), editing it using your favourite local CSV editor, such as Microsoft Excel, and then re-importing it using the upload button.

![](./attachments/image-20210301-040612.png)

Also worth considering before using high volume test data is the impact on the filesystem. Here is a page with our recommendations on configuring your MettleCI installation to mitigate the potential impact of high volume test data on your filesystem:[Managing your Unit Test data volumes](../automated-unit-testing/managing-your-unit-test-data-volumes.md)

As well as this, you should consider the impact of high volumes of data on your git repository. If you have a cloud based git repository, there may be limits on the size of individual files you can commit, or on the total volume of data in the repository. On the other hand, most DataStage and MettleCI users have self-hosted git repositories. In this case, you may not have the same restrictions, but there will be performance impacts of storing high volumes of data in your repository. When you commit changes to git using Workbench, the repository must be cloned first, which will take longer the more data you have in the repository. The same is true for your CI/CD pipeline.

* * *

## Step By Step Guide

This process is identical to the [Execute Unit Test process](../automated-unit-testing/executing-a-unit-test.md), with the exception that you select the 'Interception' value for the Unit Testing parameter.  Note that running a job in interception mode replaces any existing data files that already exist.