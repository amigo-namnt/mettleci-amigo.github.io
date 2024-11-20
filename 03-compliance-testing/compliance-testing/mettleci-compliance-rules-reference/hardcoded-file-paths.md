# Hardcoded File Paths

|     |     |
| --- | --- |
| **Rule name** | Hardcoded File Paths |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Ensures that all File Stages must use variables for determining paths |

# Description

Developers occasionally hard code file paths while debugging or developing. These will cause job failures when deploying to a different project or server. This problem is usually solved by using a project specific variable to define the base path for file based stages such as datasets. This compliance rule will identify hard coded file paths by checking that the pathname includes at least one predefined path parameter.

The predefined path parameters and the stages for which they can be used with can be customised by modifying the **pathParameters** variable.

# Actions

Parameterise the identified hard-coded file paths.