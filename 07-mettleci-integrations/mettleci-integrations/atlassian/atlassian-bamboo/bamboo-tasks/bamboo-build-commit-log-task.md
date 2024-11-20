# Bamboo Build Commit Log Task

You can use the Build Commit Log task to build a list of files that have changed in a given repository since the last successful build and save them to a log file.

## Using the Build Commit Log Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing Build Commit Log task or click **Add Task** and then search 'Commit' to easily locate the Build Commit Log task type, in order to create a new task.
    
3.  Complete the following settings:
    

| **Task Description** | A description of the task, which is displayed in Bamboo. |
| --- | --- |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Repository Name** | Enter the Repository Name to search for Delta Commits |
| **Build commit changes file** | Enter the Filename to store the list of Delta Commits |
| **Append to existing file?** | Check to append to an existing commit log |

4.  Click **Save**
    

## Using the Build Commit Log Task in a YAML pipeline

```
- mci-build-commit-log:
    repository: default
    log: build_deltas.txt
    description: Calculate project changes
```