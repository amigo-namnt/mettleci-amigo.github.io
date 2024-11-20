# Bamboo DataStage Admin Task

MettleCI APIs can be used to greatly simplify a variety of DataStage administration tasks within your CI/CD pipelines:

*   Creating DataStage Projects
    
*   Deleting DataStage Project
    
*   Cleaning up DataStage Projects - i.e. delete multiple projects based on regular a regular expression
    

## Using the DataStage Admin Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing DataStage Admin task or click **Add Task** and then search 'DataStage' to easily locate the DataStage Admin task type, in order to create a new task.
    
3.  Complete the following common settings:
    

| **Task Description** | A description of the task, which is displayed in Bamboo. |
| --- | --- |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Executable** | From the dropdown list, choose a specified DataStage [Capability](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/116525745/Bamboo+DataStage+Capability). |
| **Domain** | Enter the Domain of the DataStage instance (Host Name of the Services Tier). e.g. `${bamboo.Domain}` |
| **Server** | Enter the Server of the DataStage instance (Host Name of the Engine Tier). e.g. `${bamboo.ServerName}` |
| **Username** | Enter the DataStage Username. e.g. `${bamboo.DataStageUsername}` |
| **Password** | Enter the DataStage Password |
| **DataStage Admin Type** | **Create Project**, **Delete Project** or **Cleanup Projects**.  See below for type specific settings |

4.  Provide the remaining details to the Task as determined by your selected 'DataStage Admin Type'.  See the sections below for more details. 
    
5.  Click **Save**
    

### **Create Project settings**

Provide the following details:

|     |     |
| --- | --- |
| **DataStage Admin Type** | Create Project |
| **Project name** | Name of the DataStage project to be created. e.g. `${bamboo.ProjectName}` |
| **Use default project location?** | If checked, project files are created in the standard path under the default Projects directory on the Engine tier. If unchecked, enter the custom **Project Location** below. |
| **Project Location** | Enter the custom DataStage project directory |
| **Copy roles from another project?** | Check to copy roles from another project. If checked, enter a **Roles Project name** below. |
| **Roles project name** | Enter the name of the DataStage project from which to copy roles |

### **Delete Project settings**

Provide the following details:

|     |     |
| --- | --- |
| **DataStage Admin Type** | Delete Project |
| **Project name** | Name of DataStage project to be delete. e.g. `${bamboo.ProjectName}` |

### **Cleanup Projects** **settings**

Provide the following details:

|     |     |
| --- | --- |
| **DataStage Admin Type** | Cleanup Projects |
| **Project pattern (regex)** | Search pattern for existing projects, sorted in [natural order](https://en.wikipedia.org/wiki/Natural_sort_order) |
| **Number of projects to retain** | Number of projects to retain. Projects at the top of the sorted list are deleted first.   <br>For example, if the project pattern results in the following sorted project list:<br><br>*   project1<br>    <br>*   project2<br>    <br>*   project11<br>    <br>*   zzProject3<br>    <br>*   zzProject4<br>    <br><br>A setting of 3 will result in the following actions:<br><br>*   project1 - **DELETED**<br>    <br>*   project2 - **DELETED**<br>    <br>*   project11 - Retained<br>    <br>*   zzProject3 - Retained<br>    <br>*   zzProject4 - Retained |

## Use in a Bamboo YAML pipeline

```
- mci-datastage-admin:
    server: ${bamboo.ServerName}
    default-location: 'true'
    admin-type: CREATE_PROJECT
    project-name: ${bamboo.ProjectName}
    dsclient: DataStage v11.7
    domain: ${bamboo.DomainName}
    shared-credentials: *datastage_credentials
    description: Create Datastage Project
```