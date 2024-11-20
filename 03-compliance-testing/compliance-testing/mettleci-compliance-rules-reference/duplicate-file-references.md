# Duplicate File References

|     |     |
| --- | --- |
| **Rule name** | Duplicate File References |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Verifies that a file is only referenced once in a DataStage job (Sequential File, Complex Flat File and DataSet) |

# Description

Sometimes developers will copy and paste stages rather than adding a new stage from the palette. In doing so there is a risk that the developer may not update the reference to the filename property which which may result in incorrect processing being performed by the ETL job.

# Actions

Ensure that a file is only referenced once in a DataStage job.