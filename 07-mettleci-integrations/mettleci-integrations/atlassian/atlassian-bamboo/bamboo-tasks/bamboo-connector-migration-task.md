# Bamboo Connector Migration Task

The MettleCI Connector Migration Tool plugin is used to automate the changing of Jobs to use Connector Stages instead of the deprecated Plug-in and Operator Stages. It uses the IBM-supplied Connector Migration Tool (AKA 'CCMT') which is provided as part of the installation media for each new version of DataStage. MettleCI provides an intelligent wrapper around the Connector Migration Tool to identify and upgrade the relevant jobs, also reporting issues that cannot be resolved by the Connector Migration Tool itself. You can use the Execute Connector Migration Tool task to invoke the Connector Migration Tool and log its output to the Bamboo log.

## Configuring the Connector Migration Source Code Checkout Task

1.  Navigate to the **Artefacts** configuration tab for your job and add a new definition for InfoServer Assets:
    

| **Name** | **Location** | **Copy pattern** | **Operations** |
| --- | --- | --- | --- |
| InfoServer Assets | datastage | `**/*` | Share |

2.  Create two Bamboo Tasks in the following order:
    
    1.  Source Code Checkout
        
    2.  Execute Connector Migration Tool
        
3.  Configure each task as described below
    

> [!INFO]
> Note that you may add additional tasks in between **Source Code Checkout** and **Execute Connector Migration Tool**, however **Source Code Checkout** must always come before **Execute Connector Migration Tool***.*

## Using the Source Code Checkout Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Export DataStage Asset task or click **Add Task** and then search 'DataStage' to easily locate the Export DataStage Asset task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task description** | Description of the Bamboo task |
| **Disable this task** | If checked, this task will be disabled |
| **Repository** | The name of the repository |
| **Checkout Directory** | Alternate sub-directory to which the code will be checked out. It is recommended that you leave this option empty. |
| **Force Clean Build** | Removed the source directory and check it out again prior to each build. It is recommended that you check this option. |

4.  Click **Save**
    

## Using the Execute Connector Migration Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Export DataStage Asset task or click **Add Task** and then search 'DataStage' to easily locate the Export DataStage Asset task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task description** | Description of the Bamboo task |
| **Disable this task** | If checked, this task will be disabled |
| **Executable** | The name of the DataStage client capability to be used by this task<br><br>###### *At least one DataStage client capability needs to be defined* |
| **Domain** | The URL *<domain name>:<port number>* of the IBM Information Server Services tier. It is recommended you use the value `${bamboo.Domain}`. |
| **Server** | The URL<domain name> of the IBM Information Server Engine tier. It is recommended you use the value `${bamboo.ServerName}`. |
| **Username** | The username used to connect to IBM Information server. It is recommended you use the value `${bamboo.DatastageName}`. |
| **Password** | The password for the username specified above (if you check the *Change password* box). It is recommended you use the value `${bamboo.DatastagePassword}`. |
| **Project Name** | The name of the IBM Information Server DataStage project containing the job or sequence to execute |
| **Optional parameters** | Optional parameters<br><br>*   `-R` to run the process in ‘preview’ mode (i.e. List the jobs that require Connector Migration, but do not modify the jobs) |
| **Unique CCMigrate Log Filename** | Unique log file name. It is recommended you use the value `${bamboo.buildKey}.log`. |
| **Root ISX Directory** | It must match the InfoServer Assets location specified in Artifacts tab |
| **Max Threads** | Number of threads used to identify **before** and **after** status. If you don’t have a reason to choose otherwise it is recommended you use the value `8`. |
| **Fail plan when compile error** | *   **True**: Build plan will fail when it encounters a compilation error<br>    <br>*   **False(default)**: Build plan will pass, even if there are compilation errors |

4.  Click **Save**
    

> [!WARNING]
> ## Remote Agent Workaround
> Atlassian Bamboo Remote Agents running on Windows (**before** Bamboo v6.10) exhibit a problem for which you may need to implement a workaround [documented here](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/458457095/Bamboo+Agent+produces+chcp+or+-107374+errors).

## Using the Source Code Checkout Task in a YAML pipeline

```
<TBC>
```

## Using the Execute Connector Migration Task in a YAML pipeline

```
<TBC> 
```