# DB2 with No Non Recovery Load

|     |     |
| --- | --- |
| **Rule name** | DB2 with No Non Recovery Load |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Identify Db2 Stages using bulk load with Non Recovery Load set to No |

# Description

This rule warns developers using Db2 bulk load with **Non Recovery Load** set to **No** which could require the restoration of the Db2 database if it crashes during the execution.

# Actions

User dependent.