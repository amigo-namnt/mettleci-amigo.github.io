# Unexpected DataStage error occurred - Unhandled exception Type=Segmentation error

# Problem

While running the MettleCI Workbench Setup Wizard on a Unix based OS, the following error is displayed while verifying DataStage credentials:

```
Unexpected DataStage Error Occured. Please contact the Administrator. Additional Details : 
Unhandled exception Type=Segmentation error 
<...snip...>
Module=/opt/freeware/openjdk/jdk8u265-b01/jre/lib/ppc64/server/libjvm.so 
<...snip...>
```

> [!INFO]
> The path indicated by **Module=** may vary between installations and platform but it is important to note that this is a related to the OpenJDK, not the IBM JDK packaged with DataStage.

# Cause

For certain platforms and configurations of `$LD_LIBRARY_PATH`/`$LIBPATH`, OpenJDK shared libraries can be incorrectly loaded while running DataStage clients via MettleCI Workbench.

# Solution

As a work around for this behavior, create a file called `setupEnv.sh` in the root of `/opt/dm/mci`, add the following environment variable definition to this file and ensure it is owned by `mciworb` with permissions `-rwxr-xr-x`:

```
export JAVA_OPTS=-Dcom.datamigrators.mettle.process.CommandRunner.libpath=$LD_LIBRARY_PATH
OR for AIX:
export JAVA_OPTS=-Dcom.datamigrators.mettle.process.CommandRunner.libpath=$LIBPATH
```

Once `/opt/dm/mci/setupEnv.sh` has been created, restart MettleCI Workbench:

```
# restart the workbench service
sudo service dm-mettleci-workbench stop
sudo service dm-mettleci-workbench start
```