# The MettleCI Bamboo Command Plugin Fails With java.lang.ClassNotFoundException

## Problem

When using the MettleCI CLI to generate Bamboo plans, the `mettleci deploy devops-pipeline` command fails with the following error:

```
Exception in thread "main" java.util.ServiceConfigurationError: com.bmsquire.plugin.api.Plugin: Provider com.datamigrators.mettle.bamboo.commands.DevOpsPipelineCommand could not be instantiated
	at java.util.ServiceLoader.fail(ServiceLoader.java:232)
	at java.util.ServiceLoader.access$100(ServiceLoader.java:185)
	at java.util.ServiceLoader$LazyIterator.nextService(ServiceLoader.java:384)
	at java.util.ServiceLoader$LazyIterator.next(ServiceLoader.java:404)
	at java.util.ServiceLoader$1.next(ServiceLoader.java:480)
	at com.datamigrators.mettle.shell.plugin.PluginManager.loadCommands(PluginManager.java:81)
	at com.datamigrators.mettle.shell.plugin.PluginManager.addPluginsFromDirs(PluginManager.java:63)
	at com.datamigrators.mettle.shell.MainClass.main(MainClass.java:76)
Caused by: java.lang.NoClassDefFoundError: com/atlassian/bamboo/specs/api/builders/RootEntityPropertiesBuilder
	at java.lang.Class.getDeclaredConstructors0(Native Method)
	at java.lang.Class.privateGetDeclaredConstructors(Class.java:2671)
	at java.lang.Class.getConstructor0(Class.java:3075)
	at java.lang.Class.newInstance(Class.java:412)
	at java.util.ServiceLoader$LazyIterator.nextService(ServiceLoader.java:380)
	... 5 more
Caused by: java.lang.ClassNotFoundException: com.atlassian.bamboo.specs.api.builders.RootEntityPropertiesBuilder
	at java.net.URLClassLoader.findClass(URLClassLoader.java:387)
	at com.datamigrators.mettle.shell.plugin.IsolatedClassLoader.loadClass(IsolatedClassLoader.java:48)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:351)
	... 10 more

```

## Cause

This issue is caused by one of the following:

*   The `bamboo-specs` and `bamboo-specs-api` libraries are missing from MettleCI CLI’s `lib` folder
    
*   The version of `bamboo-specs` and / or `bamboo-specs-api` in MettleCI CLI’s `lib` folder is incorrect for the version of Bamboo you are working with.
    

Solutions

1.  Identify the version of Bamboo you are using. The `bamboo-specs` and `bamboo-specs-api` must match the version of bamboo you are using
    
2.  Follow the instructions in [the Prerequisites section of this page](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/556302364/Generating+MettleCI+Bamboo+Plans#Prerequisites) to download and install the required version of `bamboo-specs` and `bamboo-specs-api` .
    

> [!NOTE]
> MettleCI Command needs to be build 173 or above in order to use dm-command-bamboo-plugin