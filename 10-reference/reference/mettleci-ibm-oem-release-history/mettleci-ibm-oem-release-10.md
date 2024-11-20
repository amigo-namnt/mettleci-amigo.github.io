# MettleCI IBM OEM Release 1.0

# Package Summary

|     |     |
| --- | --- |
| **Package name** | MettleCI 1.0 |
| **Release Date (yyyy-mm-dd)** | 2021-03-23 |

## Package Contents

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Function** | **File** | **Timestamp** | **Size** | **Type** | **Notes** |
| Command Shell | `dm-mettleci-command-shell-1.1-162-dist.zip` WINDOWS<br><br>`dm-mettleci-command-shell-1.1-162.noarch.rpm` UNIX | 2021-02-24 09:48:55<br><br>2021-02-24 09:48:46 | 163.3 MB<br><br>159.3 MB | ZIP<br><br>RPM | These Command Shell distributions each include a full set of the latest versions of all MettleCI CLI plugins (commands). |
| Workbench | `dm-mettleci-workbench-1.0-1165-setup.exe` WINDOWS<br><br>`dm-mettleci-workbench-1.0-1165.noarch.rpm` UNIX | 2021-03-10 00:22:37<br><br>2021-03-10 00:22:24 | 57.1 MB<br><br>56.9 MB | EXE<br><br>RPM |     |
| Compliance Rules | `dm-compliance-rules-159m.zip` | 2021-03-10 17:17:00 | 357.4 kB | ZIP | A ready-to-use Git repository folder |
| Sample Build Pipelines | `mettleci-azure-template.zip`<br><br>`mettleci-gitlab-template.zip`<br><br>`mettleci-jenkins-template.zip` | 2020-10-30 12:30:17<br><br>2020-10-30 12:29:01<br><br>2020-10-30 12:29:45 | 21.0 kB<br><br>19.5 kB<br><br>20.2 kB | ZIP<br><br>ZIP<br><br>ZIP |     |
| Parallel Unit Test Harness | `dm-unittest-harness-1.0-319-setup.exe` WINDOWS<br><br>`dm-unittest-harness-1.0-319.noarch.rpm` UNIX | 2021-03-05 16:06:45<br><br>2021-03-05 16:06:38 | 13.8 MB<br><br>12.1 MB | EXE<br><br>RPM |     |
| Server Unit Test Harness | `dm-server-unit-test-harness-1.0-001.zip`  WINDOWS  UNIX | 2021-03-23 22:59:00 | 4 kB | ZIP | This provides a Server interface to the capabilities provided by the Parallel test harness which must also be installed to provide unit test functionality. |
| License | `license.txt`<br><br>`properties.txt` | 2021-03-10 00:18:00<br><br>2021-03-10 00:18:00 | 1 kB<br><br>98 Bytes | TXT<br><br>TXT | The license file, valid from 2021-03-10 to 2099-12-31<br><br>A human-readable file describing the constraints within the supplied license |

> [!WARNING]
> **Important notes about** `license.txt`
> *   This MettleCI Release 1.0 package is currently the only place that you will find a MettleCI license file
>     
> *   Since this initial release we have standardised on `mettleci.lic` as the name of the license file, which you will need to deploy to enable your MettleCI Workbench and MettleCI CLI instances. **Consequently you should rename** `license.txt` **to** `mettleci.lic` **after unpacking this distribution media.**

# Change Log

*   MettleCI Workbench
    
    *   Initial release
        
*   MettleCI Unit Test Harness
    
    *   Initial release
        
*   MettleCI Command Line Interface
    
    *   Initial release
        
*   MettleCI Compliance Rules Repository
    
    *   Initial release
        

# Notes

For documentation please visit [http://docs.mettleci.io](http://docs.mettleci.io)