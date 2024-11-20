# Bamboo Agent produces chcp or -107374 errors

## Problem

Atlassian Bamboo Remote Agents running on Windows (**before** Bamboo v6.10) may produce a couple of errors:

*   'chcp' is not recognized as an internal or external command, operable program or batch file.
    
*   the Return Code -1073741515
    

If you encounter these symptoms you may need to implement the workaround described below. This Bamboo defect is [documented here](https://confluence.atlassian.com/bamkb/bamboo-or-remote-agent-does-not-pick-up-the-path-environment-variable-correctly-when-running-as-a-windows-service-323982768.html) and the status of the Atlassian fix is [described here](https://jira.atlassian.com/browse/BAM-16205?_ga=2.64634735.17192666.1547599188-2066070865.1384855247).

> [!INFO]
> If you need to run the MettleCI `dm-ccmigrate-plugin` via a Remote agent you will need to use the following workaround

## Solution

Follow these steps to work around this Bamboo bug:

1.  Configure Bamboo Remote Agent to run as an application user (via Windows Services)
    
2.  Add the following 2 paths to the application user path (**not** the system path!)
    
    *   `%SystemRoot%\system32`
        
    *   `<DataStage Client Installation Path>\ASBNode\apps\proxy\cpp\vc60\MT_dll\bin`
        

![](./attachments/ccmigrate-path.png)

> [!INFO]
> If another, similar error code appears (e.g. -1073741819) we recommend you copy the value of the system `PATH` environment variable and append it to the local user `PATH` environment variable that is configured to run the Bamboo remote agent service.

## Related articles

*   Page:
    
    [Which Bamboo license do I need if I want to use it with MettleCI?](/wiki/spaces/MCIDOC/pages/433717258/Which+Bamboo+license+do+I+need+if+I+want+to+use+it+with+MettleCI)
    
*   Page:
    
    [How does MettleCI integrate with other tools?](/wiki/spaces/MCIDOC/pages/457408522/How+does+MettleCI+integrate+with+other+tools)
    
*   Page:
    
    [Bamboo Compliance Test Task](/wiki/spaces/MCIDOC/pages/408322090/Bamboo+Compliance+Test+Task)
    
*   Page:
    
    [Bamboo DataStage Message Handlers Task](/wiki/spaces/MCIDOC/pages/412155905/Bamboo+DataStage+Message+Handlers+Task)
    
*   Page:
    
    [Bamboo DataStage Admin Task](/wiki/spaces/MCIDOC/pages/408387649/Bamboo+DataStage+Admin+Task)