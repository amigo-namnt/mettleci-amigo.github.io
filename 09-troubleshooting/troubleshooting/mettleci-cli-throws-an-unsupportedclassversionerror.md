# MettleCI CLI throws an 'UnsupportedClassVersionError'

## Problem

When invoking the MettleCI command shell you receive the following error message:

```
C:\Users\Developer>mettleci.cmd
Exception in thread "main" java.lang.UnsupportedClassVersionError: JVMCFRE003 bad major version; class=com/datamigrators/mettle/shell/MainClass, offset=6
        at java.lang.ClassLoader.defineClassImpl(Native Method)
        at java.lang.ClassLoader.defineClass(ClassLoader.java:331)
        at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:155)
        etc.
```

… or you see this in the Workbench `mci.log` file:

```
Exception in thread "main" java.lang.UnsupportedClassVersionError: JVMCFRE003 bad major version; class=com/datamigrators/mettle/MettleApplication, offset=6
	at java.lang.ClassLoader.defineClassImpl(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:331)
	at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:155)
	at java.net.URLClassLoader.defineClass(URLClassLoader.java:714)
	etc.
```

## Solution

This error is unavoidably produced when you invoke the MettleCI Command Line, or attempt to start the Workbench service, in an environment which is not running Java v1.8 or greater. In particular, the MettleCI Command Line cannot work with the IBM-specific version of Java typically shipped with DataStage. To confirm this is the issue login to the relevant host as the `mciworkb` user and run `java -version` to verify the java version.

To resolve this error please ensure you follow the first step in the [Command Line installation guide](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488898631/Installing+the+MettleCI+Command+Shell) which requests you to [install a more recent version of Java](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/488800406/Prerequisite+Java+Installation).

## Related articles

*   Page:
    
    [DataStage Connector Migration Command](/wiki/spaces/MCIDOC/pages/410681364/DataStage+Connector+Migration+Command)
    
*   Page:
    
    [DataStage Capture Command](/wiki/spaces/MCIDOC/pages/2568650800/DataStage+Capture+Command)
    
*   Page:
    
    [UnitTest Generate Command](/wiki/spaces/MCIDOC/pages/2176647169/UnitTest+Generate+Command)
    
*   Page:
    
    [UnitTest Install-Server-Test-Harness Command](/wiki/spaces/MCIDOC/pages/2640740386/UnitTest+Install-Server-Test-Harness+Command)
    
*   Page:
    
    [MettleCI Command Line Reference](/wiki/spaces/MCIDOC/pages/458850547/MettleCI+Command+Line+Reference)