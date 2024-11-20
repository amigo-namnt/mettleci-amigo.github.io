# Bamboo Properties Configuration Task

You can use the Properties Configuration Task in Bamboo Jobs to replace specially formatted text placeholders in DataStage configuration files (e.g. `DSParams`) with environment-specific values as part of the MettleCI-automated deployment process. The replacement values can be taken from Plan Variables (e.g. `${bamboo.buildResultKey}`) and `/` or MettleCI Override files.

Placeholders are written in the following format: `${PlanVariableNameOrOverrideFileReference}`

## Using the Properties Configuration Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Properties Configuration Task or click **Add Task** and then search 'Properties Configuration' to easily locate the Properties Configuration Task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Base Directory** | Optional: A relative path from the working directory to the root directory of configuration file(s). This path will be the root of file patterns. If not specified, the agent working directory will be used. |
| **File Patterns** | Relative paths to different configuration files from the base directory (wild card is acceptable). Each line is one pattern.  Examples could include … <br><br>```<br>*.apt<br>DSParams<br>Parameter Sets/*/*<br>``` |
| **Override File** | ***Optional:*** A relative path from the working directory to a Java properties file containing variable values to be used during substitution. |
| **Output Directory** | ***Optional:*** A relative path from working directory to write all filled configuration files to (all relative path from the base directory will be preserved. If output directory is the same as base directory, all original configuration files will be replaced.  If not specified, the agent working directory will be used. |

4.  Click **Save**
    

## Using the Properties Configuration Task in a YAML pipeline

```
- mci-properties-configuration:
    baseDir: datastage
    filePatterns: |-
      *.apt
      DSParams
      Parameter Sets/*/*
    outputDir: config
    overrideFile: var.${bamboo.EnvironmentID}
    description: Substitute parameters in DataStage configuration file
```