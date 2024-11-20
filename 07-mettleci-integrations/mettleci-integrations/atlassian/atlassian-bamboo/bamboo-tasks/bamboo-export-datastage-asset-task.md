# Bamboo Export DataStage Asset Task

You can use the Export DataStage Asset task to export one or more DataStage assets as individual ISX files in a folder structure matching the project.  The assets to be exported can be specified by name, list or entire project.

## Using the Export DataStage Asset Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Export DataStage Asset task or click **Add Task** and then search 'DataStage' to easily locate the Export DataStage Asset task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Executable** | From the pulldown list, choose a DataStage [Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability). |
| **Domain** | Enter the Domain of the DataStage instance (Host Name of the Services Tier). e.g. `${bamboo.Domain}` |
| **Server** | Enter the Server of the DataStage instance (Host Name of the Engine Tier). e.g. `${bamboo.ServerName}` |
| **Username** | Enter the DataStage Username. e.g. `${bamboo.DataStageUsername}` |
| **Password** | Enter the DataStage Password |
| **Project name** | DataStage Project containing assets to be exported |
| **Export Type** | Select **Asset Name**, **Asset List** or **Entire Project**.  See below for type specific options |

4.  Provide the remaining details to the Task as determined by your selected 'Export Type'.  See the sections below for more details. 
    
5.  Click **Save**
    

The following sections detail the parameters required by each value of **Export Type**.

### **Asset Name**

Provide the following details:

|     |     |
| --- | --- |
| **Export Type** | Asset Name |
| **Asset name** | Comma separated list of asset names to be exported |
| **Delete ISX when asset not in project** | Use this option to apply project deletions or moves between categories to an existing directory of assets.  Rules used by this option are as follows:<br><br>*   If ISX file exists and the asset has been deleted in the project, then the existing ISX file will be deleted.<br>    <br>*   If ISX file exists and the asset has moved categories in the project, then the existing ISX file will be deleted before re-exporting. |
| **Include binaries** | Check to include binary files containing the compiled assets |
| **Include previews** | Check to allow the ISX to be viewed using the MettleCI ISX preview plugin for Bitbucket. |
| **Export location** | The directory in which the export file should be generated |

### **Asset List**

 Provide the following details:

|     |     |
| --- | --- |
| **Export Type** | Asset List |
| **List file name** | File containing a list of assets to be exported |
| **Include Binaries** | Check to include binary files containing the compiled assets |
| **Include previews** | Check to allow the ISX to be viewed using the MettleCI ISX preview plugin for Bitbucket. |
| **Export location** | The directory in which the export file should be generated |

### **Entire Project**

Provide the following details:

|     |     |
| --- | --- |
| **Export Type** | Entire Project |
| **Include Binaries** | Check to include binary files containing the compiled assets |
| **Include previews** | Check to allow the ISX to be viewed using the MettleCI ISX preview plugin for Bitbucket. |
| **Export location** | The directory in which the export file should be generated |

## Using the Export DataStage Asset Task in a YAML pipeline

```
<TBC>
```