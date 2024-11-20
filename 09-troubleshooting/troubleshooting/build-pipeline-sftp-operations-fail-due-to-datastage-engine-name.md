# Build Pipeline SFTP operations fail due to DataStage Engine name

# Symptom

While running pipeline you receive a ‘Server not found’ or other similar error when performing an SFTP-related commands such as those available in the `mettleci` [remote namespace](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2262794241/Remote+Namespace).

# Cause

Causes can vary, but some network configuration and operating system combinations may permit connecting to DataStage using a capitalised hostname while simultaneously prohibiting SFTP operations using the same capitalised hostname.

This issue has been encountered by customers who have a DNS/proxy server configuration which prevents the use of uppercase hostnames in uppercase.

# Solution

Other than working with your network management team to better understand the cause of your issue you can dynamically manipulating the capitalisation of your hostnames from within your build pipeline definition. Using the capabilities of the Windows Command Shell (used by your build agent on your MettleCI Agent Host) capabilities to manipulate the capitalisation of your environment variables.

```
C:\Users\Administrator>set "str=The Quick Brown Fox"

C:\Users\Administrator>echo %str%
The Quick Brown Fox

C:\Users\Administrator>powershell "\"%str%\".toUpper()
THE QUICK BROWN FOX

C:\Users\Administrator>powershell "\"%str%\".toLower()
the quick brown fox
```