# Workbench throws 'OutOfMemoryError'

## Problem

If the Workbench server is constrained for resources, there is a possibility that Workbench will show errors in workbench log file `mci.log` soon after startup.

## Solution

The JAVA\_OPTS environment variable can be set to modify the resource usage of Java. More specifically, you can halve the Java Stack Size from 2MB to 1MB.

e.g. `$JAVA_OPTS=-Xss1024K`

## Related articles

*   Page:
    
    [Workbench produces 'Failed to initialize DATASTAGE\_ASB authentication' error on startup](/wiki/spaces/MCIDOC/pages/2461859849/Workbench+produces+Failed+to+initialize+DATASTAGE_ASB+authentication+error+on+startup)
    
*   Page:
    
    [Configuring Authentication between Workbench and Atlassian Bitbucket](/wiki/spaces/MCIDOC/pages/1056047306/Configuring+Authentication+between+Workbench+and+Atlassian+Bitbucket)
    
*   Page:
    
    [Which Bamboo license do I need if I want to use it with MettleCI?](/wiki/spaces/MCIDOC/pages/433717258/Which+Bamboo+license+do+I+need+if+I+want+to+use+it+with+MettleCI)
    
*   Page:
    
    [How does MettleCI Workbench integrate with Git?](/wiki/spaces/MCIDOC/pages/615546893/How+does+MettleCI+Workbench+integrate+with+Git)
    
*   Page:
    
    [MettleCI Git Support](/wiki/spaces/MCIDOC/pages/1933246550/MettleCI+Git+Support)