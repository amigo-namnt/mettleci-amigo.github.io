# Command timed out waiting to complete

# Problem

Your CI/CD pipeline produces a timeout error of the following form:

```
17-Jan-2022 12:30:56	Status code = 0 
17-Jan-2022 12:34:02	Failed to read assets from DataStage repository
17-Jan-2022 12:34:02	com.datamigrators.mettle.exception.ReadAssetRepositoryException: 
17-Jan-2022 12:34:02	Command timed out waiting to complete
17-Jan-2022 12:34:02	        at com.datamigrators.mettle.infoserver.asset.DatastageProject.a(SourceFile:226)
17-Jan-2022 12:34:02	        at com.datamigrators.mettle.infoserver.asset.DatastageProject.readAssets(SourceFile:109)
17-Jan-2022 12:34:02	        at com.datamigrators.mettle.services.deploy.IncrementalDeploymentService.<init>(SourceFile:48)
17-Jan-2022 12:34:02	        at com.datamigrators.mettle.incremental.deploy.task.DSIncrementalDeploymentTask.execute(SourceFile:139)
etc.
```

# Diagnosis

MettleCI’s timeouts are designed to catch hanging processes before they cause instability to your CI/CD pipelines. Many processes have a timeout which is hard coded (such as 3 minutes for the process in the example above) which is not simply measured from the start of a command to the end. Instead it actively monitors the output from `istool` and only triggers a timeout if there is no `istool` output for 3 minutes.

This exception indicates that `istool` is not reliably working as expected. We suggest investigating what might be causing this. Possible places to start this investigation are…

### Validate that CPU/Memory contention wasn’t an issue on the server that hosts your Agent when the timeout occurred.

Running multiple heavy builds (eg. multi-threaded compiles) at the same time could severely starve an `istool` of resources and trigger a timeout.

### Validate that CPU/Memory contention wasn’t an issue on the InfoServer Services Tier when the timeout occurred.

`istool` relies on activities on the Services Tier. If the server side processes that are triggered by `istool` become severely starved on compute resources, then `istool` could hang.

### Check InfoServer Services Tier logs for errors that occurred at the time of the timeout

Errors on the services tier can sometimes kill the server side `istool` process without aborting the client side processes leading to an `istool` hang

### Perform XMETA database maintenance

Server side `istool` processes trigger a lot of queries to the XMETA database. These can run slow or even fail to complete if basic database maintenance hasn’t been performed. The required maintenance will vary from DBMS to DBMS, so its best to discuss with your DBA. But as an example, Oracle would normally needs Database Statistics to be updated on a regular basis.

### IBM’s Suggestions for Tuning

1.  Disable in Information Governance Catalog (IGC) the capture of lineage for those objects for which lineage is not required. See [https://www.ibm.com/support/knowledgecenter/SSZJPZ\_11.7.0/com.ibm.swg.im.iis.mdwb.doc/topics/t\_configAssetsForBusinessLineage.html](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.7.0/com.ibm.swg.im.iis.mdwb.doc/topics/t_configAssetsForBusinessLineage.html).
    
2.  Improve performance of DB2 XMETA (RUNSTATS and REORG on tables). See [https://www.ibm.com/support/pages/node/607015](https://www.ibm.com/support/pages/node/607015).
    
3.  Increase WAS heap size. See [https://www.ibm.com/docs/en/iis/11.5?topic=catalog-computing-allocating-memory-information-governance](https://www.ibm.com/docs/en/iis/11.5?topic=catalog-computing-allocating-memory-information-governance).
    
4.  Manage operational metadata. If you only need operational metadata from the last thirty days remove metadata older than thirty days using `istool`. See [https://www.ibm.com/docs/en/iis/11.7?topic=assets-workbench-purgeomd](https://www.ibm.com/docs/en/iis/11.7?topic=assets-workbench-purgeomd).
    

# Conclusion

This list of *possible* causes is not exhaustive, and is only provided to provide starting points for your own investigation of the issue.