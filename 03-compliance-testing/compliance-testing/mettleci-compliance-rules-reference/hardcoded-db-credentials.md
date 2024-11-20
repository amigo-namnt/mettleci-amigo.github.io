# Hardcoded DB Credentials

|     |     |
| --- | --- |
| **Rule name** | Hardcoded DB Credentials |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Ensures that all Database Connectors and Stages must use variables for location and credentials |

# Description

Developers occasionally hard code database credentials into their jobs. These will cause job failures when deploying to a different project or server.

Note that a number of Stages have the password fields commented out. This is because there is no way of selecting the parameter through the UI, leaving the user to type a parameter name which is then encrypted. Because the ISX merely contains the encrypted string, the rule would always report a failure, even if the user has entered a valid parameter.

# Actions

Parameterise the identified hard-coded values.