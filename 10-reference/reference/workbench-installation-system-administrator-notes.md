# Workbench Installation - System Administrator Notes

# What’s installed where?

> [!INFO]
> This section is purely informational, and requires no action

## \*NIX Hosts

When executed, the MettleCI **Workbench** RPM package installer performs the following actions:

*   Creates a MettleCI service user account if it doesn’t already exist. By default, this user is called `mciworkb` and is a member of the group DataStage is configured to use (commonly`dstage`, the group that the owning ID `dsadmin`has as primary group). An alternative MettleCI user and group can be specified. but the MettleCI user must be in the DataStage group, whatever it is called.
    
*   Creates the MettleCI home directory (default `/opt/dm/mci`), owned by the MettleCI service user, with the following contents:
    
    ```
    $> ls -al /opt/dm/mci/
    total 52292
    -r-xr----- 1 root         dstage     1766 Oct  7 11:11 dm-mettleci-workbench
    -rwxrwxr-x 1 mciworkb     dstage 53531885 Oct  7 11:11 mettle-ui-1.0-449.jar
    drwxrwxr-x 2 mciworkb     dstage        6 Oct  7 11:11 reports
    drwxrwxr-x 2 mciworkb     dstage        6 Oct  7 11:11 specs
    -rwx------ 1 mciworkb     dstage     1675 Oct  7 11:11 workbench_rsa
    -rwxr-xr-x 1 mciworkb     dstage      414 Oct  7 11:11 workbench_rsa.pub
    ```
    
*   Copies the workbench jar file (mettle-ui-x.x-x.jar) to the MettleCI home
    
*   Creates an SSH key pair for Git integration as `workbench_rsa.pub` (public key) and `workbench_rsa` (private) in the MettleCI home
    
*   Changes permissions on the private Git SSH key to 700
    
*   Creates a `SysVinit` service for the workbench
    

Running the MettleCI Workbench setup wizard has the following effect:

*   Creates a `config.yml` file in the MettleCI Home directory
    
*   When Jira issue management is selected, creates Jira App Link Private Key as `jira_privatekey.pcks8` in the MettleCI home