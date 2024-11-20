# Custom Stages

|     |     |
| --- | --- |
| **Rule name** | Custom Stages |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | This rule detects the use of Custom stages in Parallel Jobs |

# Description

Custom stages you have built may work in your current version of DataStage, but may not work for newer versions. This rule raises awareness of the use of custom stages enabling you to plan ahead when performing project upgrades.

# Usage

*   Object **builtinStages** holds all the built-in stages, and the version in which it was made available
    
*   Object **builtinStagesOnly** holds built-in stages that only present in those stages
    

# Actions

Prioritise the testing of your Custom Stage(s) in your proposed environment.