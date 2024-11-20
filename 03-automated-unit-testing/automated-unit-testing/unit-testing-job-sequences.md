# Unit Testing Job Sequences

The parameter which sets a job's Unit Test execution mode to either 'Interception' or 'Testing' is an environment variable which can be added to individual Jobs or to Job Sequences.  When applied to a Job Sequence (and propagated to the jobs within that sequence) this enables you to run an entire batch of Jobs in Interception mode, capturing all jobs' inputs and outputs as an integrated set of MettleCI Unit Tests, or in Testing mode, where you can replay that set of Unit Tests for each Job in turn.

MettleCI’s Unit Test capability deliberately avoids treating a Job Sequence as a testing unit, meaning that it does not support injecting test data into the inputs of the first Job(s) in a Sequence and testing the outputs of the last Job(s). While it has been common practice for some DataStage developers to ‘unit test' multiple Jobs as a single test event using one or more Job Sequences (prior to handing them over for some form of batch-level testing) this, in effect, forms an **integration test**. By strictly defining the scope of a unit test as a single DataStage Job MettleCI reduces the risk and additional root-cause analysis effort required to address test failures that arise during the execution of multiple Jobs.

# A Pragmatic Approach

Notwithstanding the caution expressed above, it is possible to hand-craft a set of unit test specifications which support the testing of multiple sequenced Jobs:

You can create MettleCI Unit Test Specifications which effectively inject test data into the Jobs as the beginning of the Job Sequence an test the data being produced at the output of the Job Sequence. For example, given a simple sequence of three interdependent DataStage Jobs…

![](./attachments/Job%20Sequence%20UT.png)

… you could test this sequence using Test Specifications which look like this:

| **Parallel Job 1** | **Parallel Job 2** | **Parallel Job 3** |
| --- | --- | --- |
| ```<br>given:<br>  # Inject test data<br>  - stage: Sequential_File_0<br>    link: Link_1<br>    path: Sequential_File_0.csv<br>when:<br>  # Test conditions<br>then:<br>  # No outputs tested<br>  # Allow normal output operation to support downstream jobs<br>``` | No MettleCI Test Specification is required for this Job as it runs normally during a unit test, with no runtime intervention from MettleCI. | ```<br>given:<br>  # No input data injected<br>  # Allow normal input operation to read from upstream job<br>when:<br>  # Test conditions<br>then:<br>  # Compare output<br>  - stage: ODBC_1<br>    link: Link_2<br>    path: ODBC_1.csv<br>``` |

…and which would effectively look like this at runtime:

![](./attachments/Job%20Sequence%20Unit%20Test%20Process.png)