# Bamboo Execute DataStage Job Task

You can use the Execute DataStage Job task to execute a DataStage job or sequence. 

## Using the Execute DataStage Job Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Execute DataStage Job task or click **Add Task** and then search 'DataStage' to easily locate the Execute DataStage Job task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Executable** | From the pulldown list, choose a DataStage [Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability). |
| **Domain** | The Domain of the DataStage instance (host name of the Services Tier). e.g. `${bamboo.Domain}` |
| **Server** | The Server of the DataStage instance (host name of the Engine Tier). e.g. `${bamboo.ServerName}` |
| **Username** | The DataStage user's username. e.g. `${bamboo.DataStageUsername}` |
| **Password** | The DataStage user’s password |
| **Project name** | The name of the DataStage Project containing assets to be executed |
| **Job/Sequence Name** | The name of the Job or Job Sequence to be executed |
| **Run Mode** | Choose **NORMAL**, **RESET**, **RESTART** or **VALIDATE** |
| **Use Property File for Optional Parameters** | Check this option if parameters should come from a file rather than configuring them in the Bamboo plan |
| **Optional Parameters** | Use this multi-line text box to enter job parameters as key value pairs (e.g. `DBPassword=tiger`)<br><br>Alternatively, if the **Use Property File for Optional Parameters** property is set you can enter the name of a file containing parameters as key value pairs. |

4.  Click **Save**
    

## Using the Execute DataStage Job Task is a YAML pipeline

```
<TBC>
```