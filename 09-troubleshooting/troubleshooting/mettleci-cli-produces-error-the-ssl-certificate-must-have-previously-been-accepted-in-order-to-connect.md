# MettleCI CLI produces error 'The SSL certificate must have previously been accepted in order to connect'

# Problem

In this example the following `mettleci datastage deploy` command…

```
C:\> mettleci datastage deploy ^
     -domain iis-server.mycorp.com:9446 -server iis-server.mycorp.com ^
     -project myproject_ci ^
     -username isadmin -password **** ^
     -assets C:/jenkins-agent/workspace/MettleCI/datastage/Jobs/MettleCI -project-cache C:/MettleCI/cache/iis-server/myproject_ci
```

…works well until it gets to the compilation step at which point each job produces this error:

```
 * Compile 'iis-server.ibm.demo/dstage1_ci/Jobs/MettleCI/mci_test_base_vlo1.pjb' - FAILED
      
      Initializing
      
      Failed to attach to the project.
      The SSL certificate must have previously been accepted in order to connect to server https://iis-server.ibm.demo:9446.

      Exit Status 1
```

# Solution

Surprisingly, the solution to `The SSL certificate must have previously been accepted in order to connect` is to [ensure you have accepted your SSL certificate](https://www.ibm.com/support/pages/certificate-warning-when-launching-datastage-client-tools-right-after-information-server-client-installation).

# In summary

Ensure your DataStage environment is properly installed, configured, and functional before using the MettleCI CLI. In particular ensure your `istool` and `dscc` commands behave correctly.