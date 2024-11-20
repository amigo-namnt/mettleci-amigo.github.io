# Database tables references are fully qualified

|     |     |
| --- | --- |
| **Rule name** | Database table references are fully qualified |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Identifies where database table references are fully-qualified |

# Description

Database table references can sometimes cause problems when migrating from Development to downstream QA and Production environments as they will likely be communicating with different databases to those used in Development. Those databases may well have different configurations to those against which the Job was developed, and there may arise some confusion about which schemas or other database objects are being referenced by the Job. Fully qualified database table references (of the form `database.schema.table`)

# Actions

Ensure all database object references used by your Job are not-fully qualified (e.g., not of the form `{database}.{schema}.{tablename}`)