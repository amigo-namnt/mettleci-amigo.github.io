# Handling Hanging Deployments

# Problem

On rare occasions, we see customers experience a “hung” deployment during the compilation phase due to something that’s locked up in DataStage. By default, the DataStage Client-side compilation tool, `dscc`, provides little-to-no information during execution so if it hangs the first you’ll know about it is when you observe the MettleCI-powered deployment as stuck. Bamboo’s log files can only echo what the running process returns and, in this, case, will simply show one or more Jobs has having compiled with no further entries.

Usually, the deployment simply succeeds when it is re-run but, for the curious among us, it’s frustrating not to know why `dscc` stalled.

However, there is a way to enable debug-level logging for the DataStage Client Tier. This allows you to capture details of what `dscc` was up to at the time of the hang and use that information as part of your root-causes analysis.

# Diagnostics

On the host of the Client Tier tools being used by your MettleCI solution, under `c:\users\<username>\ds_logs` directory there are usually some `dstage_wrapper_trace_xxx.log`files.

To start writing debug-level information to those files…

1.  Create a file on the client in `C:\IBM\InformationServer\ASBNode\conf\` called `NewRepos.debug.properties`.
    
2.  In the file add the following lines:
    
    ```
    # Logging level
    com.ibm.datastage.jlog.DSFileHandler.level=DEBUG
    
    # maximum number of log files, when exceeded least recently modified file will be overwritten
    com.ibm.datastage.jlog.DSFileHandler.count=20
    
    # log file names, {0} will be replaced with next file number
    com.ibm.datastage.jlog.DSFileHandler.pattern=${user.home}/ds_logs/dstage_wrapper_trace_{0}.log
    ```
    
3.  Inspect those files the next time you experience a hang.
    
4.  Be sure to do your housekeeping at least daily to ensure that the disk isn’t consumed by detailed log data.
    
5.  When you no longer need the extra information provided by the debug setting you can set `com.ibm.datastage.jlog.DSFileHandler.level=INFO`