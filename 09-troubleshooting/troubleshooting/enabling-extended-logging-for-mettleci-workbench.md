# Enabling extended logging for MettleCI Workbench

> [!WARNING]
> Workbench’s log file already captures a high volume of information by default so to minimise over-consumption of storage, use extended logging only for as long as necessary to log relevant events .

You can set MettleCI Workbench to log more verbose diagnostic information (e.g. the specific DataStage client CLI commands it ran during Job check-in) in two ways:

## Semi-permanent Method

You can add a line to your MettleCI `config.yml`. This file is typically located at `/dm/mci/config.yml` UNIX or `C:\dm\mci\config.yml` WINDOWS.

To **enable** verbose logging…

1.  add the following lines (#3 and #4) within the `logging:` section in your `config.yml` file:
    
    ```
    logging:
      ...<snip>...
      loggers:
        com.datamigrators.mettle.process.CommandRunner: DEBUG
      ...<snip>...
    ```
    
2.  Restart your Workbench service for extended logging to begin.
    

To **disable** extended logging simply remove the lines above from your `config.yml` file and restart your Workbench service again.

## Temporary Method

You can use the following command to send a REST call to the Workbench to increase the logging level for the current session without changing your `config.yml`:

```
curl -X POST -d "logger=com.datamigrators.mettle.process.CommandRunner&level=DEBUG" http://your-engine.your-domain.com:8081/tasks/log-level
```

This increases the Workbench logging level **until** the Workbench service is next **restarted**, at which point the log reverts the settings defined in `config.yaml`.