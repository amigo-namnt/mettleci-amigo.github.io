# Bamboo DataStage Message Handlers Task

You can use the DataStage Message Handlers task to inject job level message handlers into ISX files that then will be imported into DataStage. Also see the documentation on the [DataStage Message Handlers CLI](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/412286979/ISX+Message-Handlers+Command).

## Using the Bambo DataStage Message Handlers task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing DataStage Message Handlers task or click **Add Task** and then search 'DataStage' to easily locate the DataStage Message Handlers task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Root ISX directory** | From the pulldown list, choose a DataStage [Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability). |
| **Root message handler directory** | Enter the Domain of the DataStage instance (Host name of the Services Tier) |

4.  Click **Save**
    

## Using the Bambo DataStage Message Handlers task in a YAML pipeline

```
<TBC>
```