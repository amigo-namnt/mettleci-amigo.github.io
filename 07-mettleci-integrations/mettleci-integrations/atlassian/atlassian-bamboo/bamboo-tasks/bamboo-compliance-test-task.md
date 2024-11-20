# Bamboo Compliance Test Task

MettleCI provides a function to evaluate a set of ISX files against user-defined compliance Rules.  The report that is produced by the compliance testing function provides details on success or failure of these tests.  In a CI/CD scenario, this information will determine whether to continue to the next step of the process.

The Bamboo implementation of the Compliance Test function provides additional functionality to the command line version:

*   Executes the Compliance Rules and generate the report file
    
*   Provides an additional option to select a specific set of ISX asset files instead of an entire directory
    
*   Assesses the contents of the report file and optionally halt the process in event of failure
    

* * *

## Using the Compliance Test InfoServer Asset Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing DataStage Admin task or click **Add Task** and then search for 'DataStage' to easily locate the DataStage Admin task type in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **description** | A description of the task, which is displayed in Bamboo. |
| **rules-location** | Directory containing Compliance Rule (`*.grm`) files. |
| **compliance-type** | The type of compliance test to run:<br><br>*   `ENTIRE_DIRECTORY` - Recursively compliance test all ISX files in a given directory<br>    <br>*   `FILE_LIST` - Selectively compliance test ISX files in a given directory based on a list |
| **Root ISX directory** | Root of a directory structure containing ISX files for compliance testing. |
| **compliance-list** | Path to file containing a list of ISX files to compliance test. ISX file names are expected to be relative to the Root ISX directory.<br><br>Only shown when Compliance Test type is ‘File List’. |
| **include-rule-tags** | See [compliance tagging](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2472050689/Compliance+Rule+Tags) |
| **exclude-rule-tags** | See [compliance tagging](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2472050689/Compliance+Rule+Tags) |
| **failOnTestFailure** | `'true'` to have the Bamboo build fail when at least one compliance test fails |

4.  Click **Save**
    

## Using the Compliance Test Task in a YAML pipeline

```
- mci-compliance-test:
    include-rule-tags: 'ci-fail'
    exclude-rule-tags: 'not-used'
    rules-location: rules
    compliance-list: build_deltas.txt
    compliance-type: COMPLIANCE_DIRECTORY
    failOnTestFailure: 'true'
    description: Perform static analysis - fatal rules
```