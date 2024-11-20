# Azure pipeline error "You need the Git 'GenericContribute' permission"

# Symptom

Azure pipeline doesn't allow you to perform a Git Push and throws a message about requiring the 'GenericContribute' permission.

# Cause

The system account used to execute your Azure DevOps pipeline does not have the necessary permissions to perform the required actions on your Git repository.

# Solution

Take a look at the error message in your Azure DevOps pipeline log:

```
Starting: Tag Git commit
==============================================================================
Task         : Command line
Description  : Run a command line script using Bash on Linux and macOS and cmd.exe on Windows
Version      : 2.212.0
Author       : Microsoft Corporation
Help         : https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line
==============================================================================
Generating script.
========================== Starting Command Output ===========================
"C:\Windows\system32\cmd.exe" /D /E:ON /V:OFF /S /C "CALL "C:\azure-agent\_work\_temp\0fafce07-7341-4958-b308-bbf5a9745ab6.cmd""
remote: 001f# service=git-receive-pack
remote: 0000000000aaTF401027: You need the Git 'GenericContribute' permission to perform this action. Details: identity 'Build\cc2a152b-09d4-428e-ba27-5efec725bd87', scope 'repository'.
remote: TF401027: You need the Git 'GenericContribute' permission to perform this action. Details: identity 'Build\cc2a152b-09d4-428e-ba27-5efec725bd87', scope 'repository'.
fatal: unable to access 'https://dev.azure.com/mettleci/ADO-WWI/_git/ADO-WWI-117/': The requested URL returned error: 403
##[error]Cmd.exe exited with code '128'.
Finishing: Tag Git commit
```

1.  From the line containing the error message (`You need the Git 'GenericContribute' permission to perform this action`) extract the **build service identity** value after the `Build\` field - `cc2a152b-428e-09d4-ba27-5efec725bd87` in this case - and copy it to your keyboard buffer.
    
2.  Navigate to your Azure DevOps organization’s **Project Settings** and select the **Repositories** section.
    
3.  On the **Security** tab select the **User permissions** sub-tab.
    
4.  Paste your **build service identity** value into the field marked **Search for users or groups** and select the **Project Collection Build Service** which should be displayed in the drop down list of matches.
    
5.  Set the **Contribute**, **Create branch**, and **Create tag** permissions to **Allow**.
    
6.  This page does not have a ‘save’ function. Selecting permissions from the drop down lists grants them immediately.
    

![](./attachments/Web%20capture_28-8-2023_171042_dev.azure.com.jpeg)