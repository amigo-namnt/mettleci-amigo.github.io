# MettleCI CLI produces error of the form 'Cannot run program "XXX"'

# Problem

When executing a MettleCI CLI command you receive a message of the following form:

```
Exception in thread "main" java.lang.RuntimeException:
Cannot run program "/opt/IBM/InformationServer/Server/DSEngine/bin/istool.sh": error=2, No such file or directory
or
Cannot run program "dsadmin": error=2, No such file or directory
or
Cannot run program "dsjob.exe": the system cannot find the file specified
```

# Solution

Your Client Tier does not have an accessible or correctly functioning IBM-supplied `istool.sh`, `dsadmin`, or `dsjob.,exe` command. Try verifying your access to, and the correct behaviour of, the relevant IBM commands before retrying the MettleCI CLI command.

Ensure you…

*   Are you able to successfully execute the specified command with the user account, and in the same environment, that you’re using to execute your MettleCI command.
    
*   Are running your command in an environment that supports its underlying requirements. Notably, ensure that MettleCI commands which must be run on a Windows-based DataStage Client Tier are … run it on a Client Tier.