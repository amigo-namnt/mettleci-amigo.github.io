# MettleCI DataStage Transmuters

This MettleCI capability takes a specified set of input ISX files and modifies them based on instructions provided in a supplied Recipe file. This feature is available from the MettleCI command line.

# Command

From the [MettleCI Command Line](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408354840/MettleCI+CLI+Operating+Modes), run the `asset-transformer transform` command, supplying values for these parameters:

*   **isx:** path to an ISX archive or directory containing archives
    
*   **user:** DataStage user to credit changes to
    
*   **transforms:** path to a YAML-format Recipe file describing the changes to perform
    

# Example

Assume the following:

*   `getmsg.isx` contains a Parallel Routine definition containing the target `filepath` string we wish to replce
    
*   `u915264` is the valid DataStage user that we wish to credit for the last save in the routine definition
    
*   Recipe file `changeLibFileInfo.yml` contains:
    
    ```
    - transform: SearchAndReplace
      xpath: /[contains(name(),'DSRoutineSDO')]/@modulePath
      searchString: /usr/local/dstage/[A-Za-z0-9_]/Routine/([A-Za-z0-9_]*).o
      replaceString: /usr/local/dstage/cplusplus/routines/$1.so
    ```
    

Executing the following command from a command prompt…

```
$> mettleci asset-transformer transform
  -isx C:\Users\u915264\transmuter\getmsg.isx 
  -user u915264  
  -transforms changeStaticLibToDynamicLibFilename.yml
```

…will result in this output:

```
C:\Users\u915264\transmuter>mettleci asset-transformer transform -isx C:\Users\u915264\transmuter\getmsg.isx -user u915264 -transforms changeStaticLibToDynamicLibFilename.yml
MettleCI Command Line (build 118)
(C) 2018-2020 Data Migrators Pty Ltd
----------------------------------
ISX File: C:\Users\u915264\transmuter\getmsg.isx
----------------------------------
Applying 'SearchAndReplace' transform to asset 'getmsg'
Replaced '/usr/local/dstage/TPODS/Routine/get_msg_code.o' with '/usr/local/dstage/cplusplus/routines/get_msg_code.so'
C:\Users\u915264\transmuter>
```

Notes:

*   The example uses a single ISX but any valid filepath (a directory, a wildcard expression, etc) can be used and all ISX files found that way will be processed
    
*   In this example the message shows the target and replacement strings. Other transforms will produce different, transform-specific output.
    

## See also

*   [Transmuter Transform Functions](./mettleci-datastage-transmuters/transmuter-transform-functions.md)
*   [Transmuter Recipes](./mettleci-datastage-transmuters/transmuter-recipes.md)