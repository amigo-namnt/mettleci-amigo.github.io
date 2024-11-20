# The MettleCI Bamboo Command Plugin Fails With java.lang.NoSuchMethodError

# Problem

When using the MettleCI CLI to generate Bamboo plans, the `mettleci deploy devops-pipeline` command fails with the following error:

```
Exception in thread "main" java.lang.RuntimeException: java.lang.NoSuchMethodError: org.yaml.snakeyaml.constructor.Constructor: method <init>()V not found
	at com.atlassian.bamboo.specs.util.IsolatedYamlizator.execute(IsolatedYamlizator.java:24)
	at com.atlassian.bamboo.specs.util.BambooSpecSerializer.dump(BambooSpecSerializer.java:19)
	at com.atlassian.bamboo.specs.util.BambooServer.publish(BambooServer.java:73)
	at com.datamigrators.mettle.bamboo.commands.DevOpsPipelineCommand.execute(DevOpsPipelineCommand.java:142)
	at com.datamigrators.mettle.shell.Shell.executeCommand(Shell.java:183)
	at com.datamigrators.mettle.shell.Shell.run(Shell.java:48)
	at com.datamigrators.mettle.shell.MainClass.main(MainClass.java:186)
Caused by: java.lang.NoSuchMethodError: org.yaml.snakeyaml.constructor.Constructor: method <init>()V not found
	at com.atlassian.bamboo.specs.util.WhitelistedYamlConstructor.<init>(WhitelistedYamlConstructor.java:31)
	at com.atlassian.bamboo.specs.util.Yamlizator.getYaml(Yamlizator.java:84)
	at com.atlassian.bamboo.specs.util.IsolatedYamlizator.lambda$static$0(IsolatedYamlizator.java:9)
	at com.atlassian.bamboo.specs.util.IsolatedExecutor$1.run(IsolatedExecutor.java:50)
```

# Cause

This issue is caused by incorrect versions of one or more of the following items in your MettleCI CLI installation:

*   SnakeYAML
    
*   dm-command-bamboo-plugin
    

# Solution

Check the versions in the table below and replace the incorrect version of …

*   SnakeYAML in the `lib` folder of your MettleCI CLI installation; or
    
*   dm-command-bamboo-plugin in the `plugins` folder of your MettleCI CLI installation.
    

| **Bamboo Version** | **SnakeYaml Version** | **MettleCI CommandLine Build** | **dm-command-bamboo-plugin Version** |
| --- | --- | --- | --- |
| 9.2.8 or later | 2.0 | 173 or above | 1.1-xx |
| 9.2.7 or earlier | 1.x | 173 or above | 1.0-90 |