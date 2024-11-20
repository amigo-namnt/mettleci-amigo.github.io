# Encrypted DB Passwords

|     |     |
| --- | --- |
| **Rule name** | Encrypted DB Passwords |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Ensures that all Connectors and Stages must use encrypted Passwords |

# Description

Unencrypted passwords are a security risk and should be avoided. This rule is somewhat complex because there are a few factors to consider:

*   Some Stages have their passwords as clear text
    
*   Some are encrypted and the value is always stored as encrypted, so we can't tell whether they are hardcoded or using parameters.
    
*   Connector password fields are encrypted, but store parameter names as clear text. The parameter itself may or may not be encrypted.
    

The one caveat on this rule is that the ISX stores Parameter Sets separately to jobs, so if a Password field refers to a parameter inside a Parameter Set, that parameter may be unencrypted and we won't know.

# Actions

Ensure all passwords as stored in encrypted fields.