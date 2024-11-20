# Enabling debug logging for MettleCI CLI

The MettleCI Command Line Interface has a debugging mode which is enabled by inserting entries in the `config.properties` configuration file in the root directory of your CLI installation (e.g., `/opt/dm/mci/cli` UNIX or `C:\MettleCI\cli` WINDOWS)

Enable debugging by updating the file to include the following lines:

```
# Setting the log level for a specific logger takes the format:
#     logger.[LOG_NAME]=[LOG_LEVEL]

logger.com.datamigrators.mettle.process.CommandRunner=DEBUG
logger.com.datamigrators.mettle.dsadmin.commands.DSParamsMergeCommand=DEBUG
```

These entries will cause any `mettleci` command to create a file `log/stdout.log` file in the current directory from which the CLI command was invoked. This will typically be under your CLI installation directory (in the case of manually executed `mettleci` commands) or in a different directory when invoked by pipeline agents running CLI commands under the direction of a build pipeline. You may be asked to provide this file when raising a MettleCI support request.

## Available Debug Loggers

| **Logger** | **Enhanced Logging Provided** |
| --- | --- |
| `logger.com.datamigrators.mettle.process.CommandRunner` | Logs the external calls made to DataStage APIs |
| `logger.com.datamigrators.mettle.dsadmin.commands.DSParamsMergeCommand` | Logs details of differences (sections and entries) calculated by the DSParams Merge Command |
| `logger.com.datamigrators.mettle.dsadmin.commands.DSParamsDiffCommand` | Logs sections and entries merged by the DSParams Diff Command |