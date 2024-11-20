# Transmuter Recipes

Transmuter ‘Recipes’ are files which define an ordered combination of Transmuter Functions which work together to deliver a useful transformation for your DataStage assets.

| **Name** | **Config File** | **Description** |
| --- | --- | --- |
| Change prefetch memory | `recipes/change_prefetchmemory.yaml` | Change the prefetch memory setting for an ORAOCI9 stage to 102,400,000  <br>Demonstrates use of the **InsertAttribute** transform. |
| Add unit test parameter | `recipes/add_unittest_parameter.yaml` | Add the `$DM_ENABLE_UNIT_TESTING` parameter to all jobs in the target folder structure  <br>Demonstrates use of the **InsertJobParameter** transform. |
| Remove unit test parameter | `recipes/remove_unittest_parameter.yaml` | Remove the `$DM_ENABLE_UNIT_TESTING` parameter from jobs in the target folder structure that have it  <br>Demonstrates use of the **RemoveJobParameter** transform. |
| Change library path and file type | `recipes/changeLibFileInfo.yaml` | Search the modulePath attribute (of parallel routine definitions, typically) for a given pattern, and replace it with a different directory path, keeping the base name of the file but changing the extension from `.o` to `.so`. This changes a statically linked routine to dynamic, helping ensure coherence of routine definitions and routine implementations.  <br>Demonstrates use of the **SearchAndReplace** transform. |
| Fix ODBC SQL placeholder issue | `recipes/fix_odbc_sql_parameter_issue.yaml` | This recipe fixes an issue where the following warning is displayed when migrating an ODBC stage using CCMT:<br><br>> **\[WARN\] WARNING: The number of placeholders in the UPDATE statement does not match the number of key flow variables so placeholder substitution will not occur.**<br><br>Demonstrates use of the **RemoveElement** transform.<br><br>> [!INFO]<br>> **NOTE:** This warning can occur due to a genuine bug in the job in which case this recipe will not fix it. This is a fix for a specific, unusual scenario (described in the YAML file). |

# Example YAML file

This file essentially defines an ordered set of `transform` behaviours, each describing the name of a [transform function](../mettleci-datastage-transmuters/transmuter-transform-functions.md) and other properties required by that transform. e.g.:

```
 - transform: AppendToAttribute
   xpath: //contains_JobObject[@stageType]/@name
   appendString: _I_AM_STAGE

 - transform: PrependToAttribute
   xpath: //contains_JobObject[@stageType]/@name
   prependString: MY_NAME_IS_
```

Note that this file has more than one transform. Each transform is performed sequentially, so for any given ISX the first one will be applied to each DataStage object within that ISX before the second one is applied.