# Database Connector does not Auto-Generate SQL

|     |     |
| --- | --- |
| **Rule name** | Database Connector does not Auto-Generate SQL |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Ensures a Database Connector uses Auto Generated SQL |

# Description

DataStage permits you to automatically generate the SQL statements required to read from and write to data sources.

Alternatively, you can manually specify the SQL statements that read from and write to data sources. User-specified SQL may contain certain DBMS-vendor-specific constructs that cannot be parsed correctly in job lineage analysis, preventing the correct determination of the relationships between Connector stages and their data sources/targets.

The use of custom SQL may also prohibit the portability of jobs between different vendors' databases when performing an upgrade.

# Actions

Set the Connector stage’s ‘Auto-generate SQL’ option to true.