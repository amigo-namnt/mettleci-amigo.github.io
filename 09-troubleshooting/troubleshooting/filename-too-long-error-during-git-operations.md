# Filename too Long error during Git operations

## Problem

Filename too long error occurring when running Git commands over a repository or branch that has fully-qualified file paths (including a build tool’s working directory) over 260 characters in length.

For example (from Atlassian Bamboo):

```
Merge command error: com.atlassian.bamboo.repository.RepositoryException: DDM-CCI0-3: Checkout to revision 
6e71c27c4d11665f589d1d01d88711fc4b9ae29a has failed.command ['C:\Program Files\Git\cmd\git.exe' checkout -f 
develop] failed with code 1. Working directory was [D:\MettleCI\AppData\Bamboo\xml-data\build-dir\serverSide
\DDM-CCI0-3\mergeWorkspace]., stderr: Branch 'develop' set up to track remote branch 'develop' from 'origin'.
error: unable to create file datastage/Jobs/CCIS_GENERAL/MAIN/020_EXTRACTS/080_ASSESSMENT_ANSWER/080_ACAP/CACO_
ASSESSMENT/CG_ACAP_ACAPCareCo_Assessment_Answer_030_Filter_AssessmentAnswer_Into_ACAPCareCo_Templates_NEW.isx:
Filename too long
```

## Solution

The change in Windows and Git behaviour detailed below will allow paths up to 4096 characters long.

> [!INFO]
> ### NOTE
> From [Microsoft](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=registry)…
> "Starting in Windows 10, version 1607, (and Windows 2016 Server) MAX\_PATH limitations have been removed from common Win32 file and directory functions. However, you must opt-in to the new behaviour."

Here's how to enable Windows long file paths in the Windows registry:

### The Easy Way

1.  The easy way is to use `regedit.exe` to modify the registry key which enables or disables the new long path behaviour. To enable long path behaviour set the following registry key:
    
    ```
    HKLM\SYSTEM\CurrentControlSet\Control\FileSystem LongPathsEnabled (Type: REG_DWORD) = 1
    ```
    

### The Longer Way

1.  Open Group Policy Editor by typing the following command in a Windows command window.
    
    ```
    gpedit.msc
    ```
    
2.  Navigate to the following directory: **Local Computer Policy → Computer Configuration → Administrative Templates → System → Filesystem**
    
3.  Double-click the **Enable NTFS long paths** option.
    
4.  Choose **Enabled**
    
5.  Click **Apply** and **OK**
    

### Final Step: Update the Git Configuration

1.  Enable long paths on the Git client installed on your Bamboo Host (this will be automatically added to your git config files):
    
    ```
    git config --system core.longpaths true
    ```