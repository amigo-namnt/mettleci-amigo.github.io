# Deprecated Stages

|     |     |
| --- | --- |
| **Rule name** | Deprecated Stages |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Identify deprecated stages and suggests the recommended alternative |

# Description

From time to time, older Stage Types are updated/replaced. While the older Stage Types will continue to function, it is recommended to use the newer replacement Stage Types

### HOW TO USE

*   If you are running v11.7 or higher, don't comment out any rules
    
*   If you are running v11.5, comment out all the v11.7 rules
    
*   If you are running v11.3, comment out all the v11.5 and v11.7 rules
    
*   If you are running v9.1, comment out all the v11.5 and v11.7 rules
    
*   If you are running v8.7, comment out all the v9.1, v11.5 and v11.7 rules
    
*   If you are running v8.5, comment out all the v8.7, v9.1, v11.5 and v11.7 rules
    
*   If you are running below v8.5, comment out all the rules, but upgrade your environment soon. Seriously.
    

# Actions

Redesign your Job to avoid the use of deprecated stages.