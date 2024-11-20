# Bamboo Compile DataStage Project Task

You can use the Compile DataStage Project task to compile all Jobs, Sequences, Server Routines and/or QualityStage Rulesets within a DataStage project.  Compilation results can optionally be added to the build result as test results.

## Using the Compile DataStage Project Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Compile DataStage Project task or click **Add Task** and then search 'DataStage' to easily locate the Compile DataStage Project task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Executable** | From the pulldown list, choose a DataStage [Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability). |
| **Domain** | Enter the Domain of the DataStage instance (Host Name of the Services Tier). e.g. `${bamboo.Domain}` |
| **Server** | Enter the Server of the DataStage instance (Host Name of the Engine Tier). e.g. `${bamboo.ServerName}` |
| **Username** | Enter the DataStage Username. e.g. `${bamboo.DataStageUsername}` |
| **Password** | Enter the DataStage Password |
| **Project name** | DataStage Project containing assets to be compiled |
| **Max Compile Threads** | How many jobs to compile concurrently. |
| **Parse compilation logs** | If checked, compilation logs are parsed and added as test results. The build will fail if no compilation logs are found. |
| **Skip compiled job** | Check to skip any jobs which are already compiled. |
| **Include server routines** | Check, or clear, to selectively compile server routines. |
| **Provision QualityStage Rulesets** | Check to include QualityStage rule provisioning as part of compilation |

4.  Click **Save**
    

## Using the Compile DataStage Project Task in a YAML pipeline

```
<TBC>
```