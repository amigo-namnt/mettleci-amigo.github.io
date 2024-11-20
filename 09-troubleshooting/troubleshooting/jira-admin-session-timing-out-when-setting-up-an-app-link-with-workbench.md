# Jira admin session timing out when setting up an App Link with Workbench

## Problem

While trying to set up a generic Application Link in Jira to allow MettleCI Workbench to look up Jira items, Jira might start forcing you to re-authenticate with Jira administrator credentials at every step. This can prevent the user from completing the integration process.

If you:

*   have more than one Atlassian application installed on the server that Jira is hosted on; and
    
*   the applications (including Jira) are using the same URL except for the port number to differentiate between them…
    

…then they might be interfering with each other’s session information, thereby causing this behaviour.

## Solution

The simplest solution is to modify each application’s *context path* which results in a more application-specific URL.

The following pages describe the steps for the Atlassian applications that are typically installed together when a MettleCI customer doesn’t have their own applications to fulfill the usual application life-cycle management (ALM) roles:

*   https://confluence.atlassian.com/jirakb/change-the-context-path-used-to-access-jira-server-225119408.html
    

*   https://confluence.atlassian.com/bitbucketserver/moving-bitbucket-server-to-a-different-context-path-776640153.html
    

*   https://confluence.atlassian.com/bamboo/changing-bamboo-s-root-context-path-396300360.html
    

> [!INFO]
> MettleCI can work with many different vendors' ALM tools, not just Atlassian’s suite.

## Related articles

*   Page:
    
    [Workbench produces 'Failed to initialize DATASTAGE\_ASB authentication' error on startup](/wiki/spaces/MCIDOC/pages/2461859849/Workbench+produces+Failed+to+initialize+DATASTAGE_ASB+authentication+error+on+startup)
    
*   Page:
    
    [Integrating Atlassian Jira with MettleCI Workbench](/wiki/spaces/MCIDOC/pages/1507328025/Integrating+Atlassian+Jira+with+MettleCI+Workbench)
    
*   Page:
    
    [Configuring Authentication between Workbench and Atlassian Bitbucket](/wiki/spaces/MCIDOC/pages/1056047306/Configuring+Authentication+between+Workbench+and+Atlassian+Bitbucket)
    
*   Page:
    
    [How does MettleCI Workbench integrate with Git?](/wiki/spaces/MCIDOC/pages/615546893/How+does+MettleCI+Workbench+integrate+with+Git)
    
*   Page:
    
    [How does MettleCI integrate with other tools?](/wiki/spaces/MCIDOC/pages/457408522/How+does+MettleCI+integrate+with+other+tools)