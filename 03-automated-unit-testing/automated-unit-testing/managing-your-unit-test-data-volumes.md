# Managing your Unit Test data volumes

Each MettleCI Unit test for a DataStage Job comprises…

*   a YAML specification file, typically located under the `{MettleCI-Home-Directory}/specs/{projectname}/{jobname}/` directory of your development DataStage Engine, and
    
*   a set of data files for each of the inputs and outputs of your Job, located under the same directory as your Job specification.
    

You will also see a test output directory, typically located under the `{MettleCI-Home-Directory}/reports/{projectname}/{jobname}/` directory of your development Engine which contains the results of a unit test, including [diffs](https://en.wikipedia.org/wiki/Diff) between the expected and actual data produced by the job.

It’s tempting to think that you could just run a DataStage Job (configured to run using MettleCI’s [Unit Test Interception](../automated-unit-testing/intercepting-existing-test-data.md) mode) against a full-volume data source and capture all input and output rows as a comprehensive Unit Test, however there are good reasons (described below) why this approach is not feasible.

## Disk Footprint

**DataStage Engine:** As Unit Test data are stored on disk as flat, uncompressed delimited files they will occupy a significant disk footprint. Running multiple jobs in interception mode could result in a Unit Test disk footprint as big as (or even bigger than) the size of the entire database from which you intercept your data! MettleCI does not manage your disk space for you, so you run the risk of filling up your DataStage Engine tier’s disk which will cause your DataStage instance to stop responding to requests.

**Git:** Those data files will also need to be committed to Git if you want to use them for unit testing as part of a CI build process. In this case the use of unconstrained Unit Test data will then present the same disk footprint challenges to your Git host, with a similar effect on your Git service.

> [!INFO]
> **Store Unit Test data on a separate volume**
> To further mitigate the potential risks caused by high unit test data volumes it is recommend that you locate the `specs` and `reports` directories on a volume separate to that serving your DataStage software. Having these directories on a separate volume will prevent other parts of your DataStage engine being impacted if the disk is filled with large unit test files. Your DataStage instance will continue running normally, and MettleCI Workbench will even continue functioning (albeit with some features no longer working).
> This configuration isn’t absolutely required, but is a safe, precautionary configuration for your MettleCI installation.

## Memory Limits

The MettleCI output comparison performed when a Unit Test is executed is not order-dependent (it’s effectively a [Set Intersection](https://en.wikipedia.org/wiki/Set_(mathematics)#Intersections) comparison), meaning …

*   the order of your actual job output could be different to the order of rows in your test CSV file (representing your job’s expected output), and
    
*   the order of your actual jobs output could vary between job executions
    

Despite these situations your test would still pass as long as every output row was present and identical to the rows in each CSV file representing ‘expected output’. To achieve this comparison the Unit Test harness loads all expected output values (from the CSV files associate with your Unit Test’s output links) into memory and compares them to the rows appearing on your job’s relevant output link(s) at runtime. This means that the constraining factor on the number of rows that can be compared is the memory made available to the comparison process, and Unit Test files which exceed that threshold [will fail](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/634617857/Unit+Test+fails+due+to+exceeded+memory+threshold). While there are some available [options to mitigate this](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/634617857/Unit+Test+fails+due+to+exceeded+memory+threshold), the number of rows that can be compared using this technique will always have an upper limit.

# Why doesn’t MettleCI allow us to minimize test data by taking the first *N* rows from each input?

It would be easy to introduce a limiting capability which simply filtered input data to the first *N* rows (where *N* is an arbitrarily small value), but what effect would that have on your job’s behaviour, and outputs?

The majority of useful DataStage jobs involve filtering data based on one of more logical conditions, or joining sets of data on one or more input key values. Simply taking the first *N* rows of each input and expecting them to satisfy the (sometimes complex) filtering and/or join conditions in a typical DataStage job is to literally engage in [lottery mathematics](https://en.wikipedia.org/wiki/Lottery_mathematics). As the difference between the number of potential input rows and the actual number of arbitrarily-filtered input rows increases, so the probability of a useful output being generated by your DataStage job shrinks quickly towards zero.

Imagine a lottery where you (the primary input link) randomly selected 6 numbers (primary keys) from a pool of 100 possible numbers (representing all available source keys). Now imagine your neighbour (representing the secondary input link) does the same. What’s the probability that you and your neighbour have chosen the same 6 numbers (i.e. the keys will join successfully)? Now add a few zeros onto these example numbers and the problem becomes obvious. The only way to guarantee that your job produces any output at all is to carefully curate your test data to ensure you’re supplying data that meets your job’s functional requirements, and that will ensure your job’s functionality is tested.

The good news is that you only need to create the minimum number of test rows necessary to test all the functionality of your job. For even complex jobs this can often be achieved with a very small number of carefully crafted input data rows. Joins only require a single matching row on each input. Filtering conditions often only require two Unit Test rows: one row that passes the filter, and one that doesn’t. This is a sound approach to Unit Test data.

# Your options

## Create some real test data

It is strongly recommended that you restrict the size of your unit test data files to be as small as possible, while still providing enough complexity and coverage to allow you to test the logic of your DataStage jobs.

## Use cluster keys

You can mitigate the effect of Unit Test memory limitations by defining a [Cluster Key for your Unit Test](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/644546565/High+Volume+Unit+Tests). This will partition your data on the specified key and share the burden of test comparison across multiple parallel processes.

## Simplify your test

If you don’t need the sophistication of a MettleCI Unit Test then consider simply configuring your test as a [Row Count test](../automated-unit-testing/row-count-unit-testing.md).