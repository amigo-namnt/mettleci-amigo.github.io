# Column Name Contains Unsupported Characters

|     |     |
| --- | --- |
| **Rule name** | Column Name Contains Unsupported Characters |
| **Parallel Job** | \-  |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Identifies stage columns with names using characters not supported by the Parallel Engine. |

# Description

This rule identifies columns within stages of Server Jobs (and Server Shared Containers) which are named using characters which are not supported by the Parallel Engine.

# Actions

Rename the column(s) to avoid the use of unsupported characters.