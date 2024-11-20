# Definition of a Unit Test

A unit test is a way of testing a unit - the smallest piece of code that can be logically isolated in a system. In most programming languages, that is a function, a subroutine, a method or property. The isolated part of the definition is important. In his book “Working Effectively with Legacy Code”, author Michael Feathers state that such tests are not unit tests when they rely on external system:

> If it talks to the database, it talks across the network, it touches the file system, it requires system configuration, or it can't be run at the same time as any other test.

Due to the nature of DataStage development, it is not normally possible to logically isolate ETL logic in a way that adheres to this definition. As a result, unit testing has come to mean something different to every DataStage development team and sometimes even individual developers within the same team.

With the use of MettleCI Unit Testing, transformation logic within DataStage jobs can be isolated from external systems and tested in an automated and repeatable fashion.

## Characteristics of a good unit test

1.  **Fast**. It is not uncommon for mature projects to have thousands of unit tests. Unit tests should take very little time to run. Milliseconds.
    
2.  **Isolated**. Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.
    
3.  **Repeatable**. Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.
    
4.  **Self-Checking**. The test should be able to automatically detect if it passed or failed without any human interaction.
    
5.  **Timely**. A unit test should not take a disproportionately long time to write compared to the code being tested. If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.