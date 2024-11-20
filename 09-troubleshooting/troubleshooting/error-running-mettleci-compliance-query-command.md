# Error running 'mettleci compliance query' command

# Problem

You run a `mettleci compliance query -asset \folder -queries \something -report "\something\something.csv”` command and get an error similar to the following:

```
MettleCI Command Line (build 118)
(C) 2018-2021 Data Migrators Pty Ltd
[1/67] MyAssetName (SERVER_JOB)
Error processing query 'CCMigrateTool Stages'
com.datamigrators.mettle.compliance.exceptions.QueryExecutionException: javax.script.ScriptException: groovy.lang.MissingMethodException: No signature of method: com.tinkerpop.gremlin.groovy.GremlinGroovyPipeline.comply() is applicable for argument types: (CCMigrateTool_Stages$_run_closure1, CCMigrateTool_Stages$_run_closure2) values: [CCMigrateTool_Stages$_run_closure1@6b530eb9, CCMigrateTool_Stages$_run_closure2@328572f0]
Possible solutions: notify(), count(), cap(), count(), dump(), isEmpty()
	at com.datamigrators.mettle.compliance.gremlin.GremlinAssetQuery.execute(SourceFile:164)
	at com.datamigrators.mettle.compliance.service.AssetReportingService.a(SourceFile:141)
	at com.datamigrators.mettle.compliance.service.AssetReportingService.runReport(SourceFile:104)
	at com.datamigrators.mettle.compliance.commands.AssetQueryCommand.execute(SourceFile:85)
	at com.datamigrators.mettle.shell.Shell.executeCommand(Shell.java:170)
	at com.datamigrators.mettle.shell.Shell.run(Shell.java:45)
	at com.datamigrators.mettle.shell.MainClass.main(MainClass.java:162)
Caused by: javax.script.ScriptException: groovy.lang.MissingMethodException: No signature of method: com.tinkerpop.gremlin.groovy.GremlinGroovyPipeline.comply() is applicable for argument types: (CCMigrateTool_Stages$_run_closure1, CCMigrateTool_Stages$_run_closure2) values: [CCMigrateTool_Stages$_run_closure1@6b530eb9, CCMigrateTool_Stages$_run_closure2@328572f0]
Possible solutions: notify(), count(), cap(), count(), dump(), isEmpty()
	at org.codehaus.groovy.jsr223.GroovyScriptEngineImpl.eval(SourceFile:320)
	at org.codehaus.groovy.jsr223.GroovyCompiledScript.eval(SourceFile:71)
	at javax.script.CompiledScript.eval(CompiledScript.java:92)
	at com.datamigrators.mettle.compliance.gremlin.GremlinAssetQuery.execute(SourceFile:150)
	... 6 more
```

# Cause

The use of `query` instead of `test` in your command is the cause of the error you see.

See:

*   [compliance query](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/458556115/Compliance+Query+Command) command
    
*   [compliance test](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408322069/Compliance+Test+Command) command
    

# Solution

When running your compliance rules, ensure that you use the `compliance test` command and not `compliance query`.

E.g.:

```
$> mettleci compliance test /
   -asset \folder /
   -rules \compliance_rules_folder /
   -report "\folder\output.csv"
```