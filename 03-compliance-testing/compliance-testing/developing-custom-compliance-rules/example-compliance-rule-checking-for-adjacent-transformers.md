# Example Compliance Rule - Checking for Adjacent Transformers

*   [Step 1. Prepare for Development and Testing](#step-1-prepare-for-development-and-testing)
*   [Step 2. Inspect graph model to identify Transformer Stages](#step-2-inspect-graph-model-to-identify-transformer-stages)
*   [Step 3. Develop and Debug Compliance Rule](#step-3-develop-and-debug-compliance-rule)

In this example, let's examine the following job, called **LD\_INV\_ACCOUNT\_INVGROUPS\_ADJ\_TX**:

![](./attachments/Screen%20Shot%202019-01-09%20at%202.43.01%20pm.png)

Although powerful, transformers contain embedded logic that is not immediately obvious when looking at the canvas and reduces a developer's ability to immediately understand a job's logic.  
Overuse of transformers when more "verbose" stages could achieve the same outcome can result in greater maintenance overhead.

Adjacent transformers can be a symptom of a transformer that has become so complex that a developer has needed to split the embedded logic across two transformers.  
When this occurs, developers should consider if there is an alternative implementation strategy that could be implemented instead using multiple standard stages.

Alternatively, adjacent transformers can also be a symptom of defect fixes that are "tacked on" to an existing job, rather than understanding the existing job logic and refactoring accordingly.  
Making job changes without continually refactoring the existing code will degrade job quality and increase maintenance over time.

From inspecting the job, it is apparent that **txRICheck** and **txAudit** are adjacent Transformers, and the scenario we wish to discover.

The Compliance Rule we are looking to develop needs to:

*   Identify the list of Transformer Stages in graph vertices
    
*   For each Stage in that list:
    
    *   Traverse to the adjacent downstream Stage
        
    *   Determine whether that Stage is also a Transformer, and if so return a result of Fail
        
*   If there are no adjacent Transformer stages, the rule Passes by default
    

* * *

# Step 1. Prepare for Development and Testing

Before we can start developing, we want to ensure our development tools are setup and ready for debugging.  This documentation will be using an export of the example job shown above but you can follow along using an ISX export of any parallel job containing adjacent transformers.

1.  Set up the development tool as per the instructions in [Compliance Rule Development](../developing-custom-compliance-rules/compliance-rule-development.md).
    
2.  Create a directory called **assets** under the **command-shell** directory. Copy the **LD\_INV\_ACCOUNT\_INVGROUPS\_ADJ\_TX.ISX** file into this directory.
    
3.  Create a directory called **rules** under the **command-shell** directory.
    

* * *

# Step 2. Inspect graph model to identify Transformer Stages

The rule we are building requires the identification of all Transformer Stages in the compliance graph.  Using the `debug.pjb.grm` rule described in [Compliance Rule Development](../developing-custom-compliance-rules/compliance-rule-development.md), we will dump the graph to a human readable format and use it to determine how we can identify the Transformer Stage we are looking for.  

1.  Add `debug.pjb.grm` to the **rules** directory in order to dump the graph model in JSON format.
    
2.  Execute the debug rule over the ISX file using the [mettleci compliance test](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408322069/Compliance+Test+Command) command:
    
    ```
    $> mettleci compliance test -assets assets -report Report.xml -rules rules
    ```
    
    A **.json** file for each compliance tested job will be created in the root of the **command-shell directory**.
    
3.  Use your preferred JSON formatter/beautifier to convert the output json to a human readable format.  The [command line](https://stedolan.github.io/jq/) or [web](https://jqplay.org/) versions of jq could be used to achieve this, see [Compliance Rule Development](../developing-custom-compliance-rules/compliance-rule-development.md) for more details.
    
4.  Looking at the JSON graph, you will see that it has two distinct sections: **vertices** and **edges**.  Find a vertex with a **stageName** matching a transformer in the job, eg. txRICheck:
    
    ```
    {
      "mode": "NORMAL",
      "vertices": [
    ... SNIP ....
        {
          "MaxLoopIterations": "0",
          "StageVarsMinimised": "0",
          "ValidationStatus": "0",
          "stageName": "txRICheck",
          "stageType": "CTransformerStage",
          "type": "stage",
          "BlockSize": "0",
          "LoopVarsMaximised": "0",
          "_id": "50",
          "_type": "vertex"
        }
    ... SNIP ...
      ],
      "edges": [
    ... SNIP ...
      ]
    }
    ```
    
5.  Notice the following attributes:
    
    *   **\_type** indicates this is a graph **vertex** and not an edge
        
    *   **type** is a **stage** vertex
        
    *   **stageType** is set to **CTransformerStage**
        
6.  Find one or more additional Transformer stages and verify that the **stageType** field is consistently set as **CTransformerStage**
    

* * *

# Step 3. Develop and Debug Compliance Rule

Lets use our knowledge of the graph model to create a compliance rule that will fail when two adjacent transformers are identified

1.  Create a new file called `Adjacent Transformers.pjb.grm` in the rules directory.  Since we are using the `.pjb.grm` extension, this rule will only be executed for Parallel jobs in the asset directory.  A similar rule could be developed for server jobs using `.sjb.grm` but the **stageType** property for server jobs would need to be confirmed.
    
2.  Start by adding the following code to find all transformer stages and dump them to a file for debugging
    
    ```
    item.graph.V.stage.has('stageType', 'CTransformerStage').debug("${item.name}_transformers.dump")
    ```
    
    This is a codified version of what we discovered in step 2.  `item.graph.v` finds all graph vertices (\_type = "vertex"), `.stage` filters non-stage vertices (type = "stage") and `.has('stageType', 'CTransformerStage')` retains only the Transformer stages (stageType = "CTransformerStage").  
    Finally, `.debug("${item.name}_transformeres.dumo")` will dump all matching vertices to a human readable file called **<job name>\_transformers.dump** in the root of the **command-shell** directory.
    
3.  Run compliance test and inspect the output dump file.  Verify that it includes all transformers in the job.
    
    ```
    compliance test -assets assets -report Report.xml -rules rules
    ```
    
    ![](./attachments/Screen%20Shot%202019-01-10%20at%201.43.51%20pm.png)
    
      
    Be aware that you will see additional output if the \``` debug.pjb.grm` `` rule h
    
4.  as not been removed from the rules directory or you have multiple job exports in the assets directory.
    
5.  For each Stage in that list, traverse to the adjacent downstream Stage by adding `.out.stage` to our rule. 
    
    ```
    item.graph.V
       .stage.has('stageType', 'CTransformerStage').debug("${item.name}_transformers.dump").out
       .stage.debug("${item.name}_adjacent.dump")
    ```
    
    Notice that we have broken the rule across multiple lines to make it easier to read and added an additional `.debug`() pipe for debugging
    
6.  Run compliance test again and verify the **<job name>\_adjacent.dump** file contains all stages adjacent to transformers
    
    ```
    compliance test -assets assets -report Report.xml -rules rules
    ```
    
7.  Filter out all adjacent stages which are not transformers by adding `.has('stageType', 'CTransformerStage')` ([Gremlin documentation](https://tinkerpop.apache.org/docs/current/reference/#has-step))
    
    ```
    item.graph.V
       .stage.has('stageType', 'CTransformerStage').debug("${item.name}_transformers.dump").out
       .stage.has('stageType', 'CTransformerStage').debug("${item.name}_adjacent.dump")
    ```
    
8.  Run compliance again and verify the **<job name>\_adjacent.dump** file now only contains transformers which are adjacent to transformers
    
9.  Add a `dedup()` ([Gremlin documentation](https://tinkerpop.apache.org/docs/current/reference/#dedup-step)) pipe to remove multiple instances and only emit a single instance of this traversal.
    
    ```
    item.graph.V
       .stage.has('stageType', 'CTransformerStage').debug("${item.name}_transformers.dump").out
       .stage.has('stageType', 'CTransformerStage').debug("${item.name}_adjacent.dump").dedup()
    ```
    
10.  We need our compliance test to fail any time adjacent transformers are found, so add a \``` .comply()` `` pipe with a user friendly message
    
    ```
    item.graph.V
       .stage.has('stageType', 'CTransformerStage').debug("${item.name}_transformers.dump")
       .out.stage.has('stageType', 'CTransformerStage').debug("${item.name}_adjacent.dump").dedup()
       .comply{"Transformer '${it.stageName}' is adjacent to another transformer."}
    ```
    
    Notice the `${it.stageName}` variable in the `.comply()` message, this will be replaced with the **stageName** field of the graph objects processed by `.comply()`. In this case, we are processing the adjacent transformer Stage Vertices.
    
11.  Run compliance again and inspect the content of `Report.xml`.  The XML report should show one `Result` entry for each combination of job and rule processed.  Assuming there is only one ISX in the assets directory and the debug.pjb.grm rule has been removed, you should see output like this:
    
    ![](./attachments/Screen%20Shot%202019-01-10%20at%201.45.36%20pm.png)
    
    Notice that our rule has failed with message indicating which transformers are adjacent to another transformer
    
12.  Remove all `.debug()` pipes and your rule is ready for production use
    
    ```
    item.graph.V
       .stage.has('stageType', 'CTransformerStage').out
       .stage.has('stageType', 'CTransformerStage').dedup()
       .comply{"Transformer '${it.stageName}' is adjacent to another transformer."}
    ```