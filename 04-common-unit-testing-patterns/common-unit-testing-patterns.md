# Common Unit Testing Patterns

Most DataStage jobs can be tested via MettleCI’s Unit Testing function simply by replacing input and output stages. However, some job designs - while commonplace - will necessitate a more advanced Unit Testing configuration. The sections below outline MettleCI Unit Test Spec patterns that best match these job designs.

*   [Unit Testing Stages with Rejects](./common-unit-testing-patterns/unit-testing-stages-with-rejects.md)
*   [Unit Testing Stored Procedure Stages](./common-unit-testing-patterns/unit-testing-stored-procedure-stages.md)
*   [Unit Testing Surrogate Key Generator Stages](./common-unit-testing-patterns/unit-testing-surrogate-key-generator-stages.md)
*   [Unit Testing Sparse Lookup Stages](./common-unit-testing-patterns/unit-testing-sparse-lookup-stages.md)
*   [Unit Testing Jobs with current date calculations](./common-unit-testing-patterns/unit-testing-jobs-with-current-date-calculations.md)
*   [High Volume Unit Tests](./common-unit-testing-patterns/high-volume-unit-tests.md)
*   [Creating and Running Multiple Unit Tests for a Single Job](./common-unit-testing-patterns/creating-and-running-multiple-unit-tests-for-a-single-job.md)
*   [Unit Tests featuring Local and Shared Containers](./common-unit-testing-patterns/unit-tests-featuring-local-and-shared-containers.md)