# Debug Row Limit

|     |     |
| --- | --- |
| **Rule name** | Debug Row Limit |
| **Parallel Job** | Yes |
| **Server Job** | \-  |
| **Job Sequence** | \-  |
| **Description** | Identifies row limits in debug stages (Peek, Sample, Tail) |

# Description

Debug stages are options developers might use during development to enable debugging and testing. Leaving these options set may have unintended consequences should the job be deployed into test and production environments.

# Actions

Remove either the Debug Row Limit setting, or remove the Stage within which it is set.