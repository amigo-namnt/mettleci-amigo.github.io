# Database Row Limit

|     |     |
| --- | --- |
| **Rule name** | Database Row Limit |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | Yes |
| **Description** | Identifies Connectors Stages with a configured Database Row Limit |

# Description

Row limits set on the Database stages are options developers might use during development and unit testing to allow faster development. Leaving these options set may have unintended consequences should the job be deployed into test and production environments.

# Actions

Remove the configured row limit.