# Row Count Unit Testing

Be aware that a row count test is a superficial check of the number of rows produced by a job, and should not be considered a real (or particularly valuable) Unit Test. That being said, there are times when a row count check can be useful - particularly when it’s difficult to curate a manageable value of test data.

The MettleCI unit testing feature allows you to thoroughly check that your jobs produce the expected outputs, given a specific set of inputs. If you don’t yet have some or all of your test data ready for a job, you can run a unit test in row count only mode for some or all outputs. This means that, instead of testing that the job output exactly matches what was expected, the unit test harness will only test that the number of rows output by the job matches the number of rows that were expected.

This is not a substitute for thorough unit testing, but is a tool that can be used to gain some extra confidence while you are getting on top of your test data management and into a position where you can run full unit tests on your jobs.

# Enabling Row Count Testing

To enable row count testing for a job, you must add the property, `checkRowCountOnly`, to the links in the `then` section of your test specification. The property applies to the link, so you must add it to each link, in the `then` section, individually.

## Test Spec Example 1

In the following example, there are two output links in the test specification, both of which have the `checkRowCountOnly` property set to `true`. This means that when the test is run, both output links will only be testing to check that the row count matches the expected count.

```
...
then:
  - stage: Output
    link: Write1
    path: Output-Write1.csv
    checkRowCountOnly: true
  - stage: Output
    link: Write2
    path: Output-Write2.csv
    checkRowCountOnly: true
```

## Test Spec Example 2

In this example, there are two output links in the test specification, only one of which has the `checkRowCountOnly` property set to `true`. This means that when the test is run, one link will be tested to check that the row count matches the expected count, and the other will be tested to check that the data output on that link exactly matches the expected data.

```
...
then:
  - stage: Output
    link: Write1
    path: Output-Write1.csv
    checkRowCountOnly: true
  - stage: Output
    link: Write2
    path: Output-Write2.csv
```

# Setting the Expected Row Count

When running a normal unit test, you define CSV files with the expected data for each output link referenced in the `then` section of your test specification. When running a row count unit test, you define an expected CSV in the same way, however when the test is run, it will only validate that the job outputs the same number of rows as you have defined in your expected CSV file.

# Row Count Test Report

The report for a row count unit test takes the form of a CSV diff, just like a regular unit test. The diff will have one column, labelled “Row Count”, and one row with the count. This is an example of what the report will look like in Workbench if the counts are different (i.e. the test failed):

![](./attachments/Screen%20Shot%202021-03-10%20at%205.34.25%20pm.png)