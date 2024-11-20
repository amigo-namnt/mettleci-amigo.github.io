# Bamboo Incremental Deployment Task

You can use the Incremental DataStage Deployment task to deploy an entire directory of ISX files to an existing DataStage Project.  Functionally, this is the equivalent of deleting everything from the existing project, importing all ISX files, provisioning all QualityStage rules and compiling all Jobs, Sequence, Server Routines and BuildOps.  However, the task will minimize the deployment time by performing as few operations based on the content of the existing project.

## Using the Incremental Deployment Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Incremental DataStage Deployment task or click **Add Task** and then search 'DataStage' to easily locate the Incremental DataStage Deployment task type, in order to create a new task.
    
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
| **Project name** | DataStage Project containing assets to be exported |
| **Root ISX Directory** | Optional: Root directory containing ISX files to deploy<br><br>If no value is specified, the agents working directory will be used |
| **Max Threads** | The number of threads that should be used during compilation |
| **Parse compilation logs** |     |
| **Deploy Parameter Sets** | If checked, a directory containing parameter set value files will be deployed. |
| **Parameter Set Directory** | Required if the **Deploy Parameter Sets** option is checked. Specifies a directory of parameter set value files in Bitbucket. Usually `Parameter Sets` which actually means `/datastage/Parameter Sets`<br><br>The file format should match the format of files found on your DataStage Engine under `${DSHOME}../Projects/${Project Name}/ParameterSets` directory |

4.  Click **Save**
    

## Using the Incremental Deployment Task in a YAML pipeline

```
- mci-incremental-datastage-deployment:
    server: ${bamboo.ServerName}
    params-dir: config/Parameter Sets
    project-name: ${bamboo.ProjectName}
    dsclient: DataStage v11.7
    max-threads: '8'
    domain: ${bamboo.DomainName}
    location: datastage
    deploy-params: 'true'
    shared-credentials: *datastage_credentials
    description: Deploy DataStage project
```