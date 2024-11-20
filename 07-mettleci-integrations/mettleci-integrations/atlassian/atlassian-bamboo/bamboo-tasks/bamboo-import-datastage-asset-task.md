# Bamboo Import DataStage Asset Task

You can use this task to import ISX files into an existing DataStage project.  Import can be performed using a specific ISX file, list of ISX files or entire directory containing ISX files.

## Using the Import DataStage Asset Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Import DataStage Asset task or click **Add Task** and then search 'DataStage' to easily locate the Import DataStage Asset task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Executable** | From the pulldown list, choose a DataStage [Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability). |
| **Domain** | Enter the Domain of the DataStage instance (Host name of the Services Tier). e.g. `${bamboo.Domain}` |
| **Server** | Enter the Server of the DataStage instance (Host name of the Engine Tier). e.g. `${bamboo.ServerName}` |
| **Username** | Enter the DataStage Username. e.g. `${bamboo.DataStageUsername}` |
| **Password** | Enter the DataStage Password |
| **Project name** | DataStage Project containing assets to be Imported |
| **Import Type** | Specify **Import File**, **File List**, or **Entire Directory**.  See below for import type specific options. |

4.  Click **Save**
    

The following sections detail the parameters required by each value of **Import Type**.

### **Import File**

|     |     |
| --- | --- |
| **Import Type** | Import File |
| **ISX File** | Enter the ISX File Name to be imported |
| **Delete all project assets not in import** | Check to delete any assets that exist in the DataStage project that do not exist in the import |

### **File List**

|     |     |
| --- | --- |
| **Import Type** | File List |
| **List file name** | File containing a list of ISX files to be imported, this list is relative to the Root ISX Directory |
| **Root ISX Directory** | Optional: Root directory containing ISX files<br><br>If not specified, the agent working directory is used |
| **Delete all project assets not in import** | Check to delete any assets that exist in the DataStage project that do not exist in the import directory |

### **Entire Directory**

|     |     |
| --- | --- |
| **Import Type** | Entire Directory |
| **Root ISX Directory** | Optional: Root directory containing ISX files<br><br>If not specified, the agent working directory is used |
| **Delete all project assets not in import** | Check to delete any assets that have not been included in this import |

## Using the Import DataStage Asset Task in a YAML pipeline

```
<TBC>
```