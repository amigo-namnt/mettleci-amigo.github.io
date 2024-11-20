# Running Unit Test Interception produces an error 'Can not deserialize'

# Symptom

When running a DataStage job using MettleCI Unit Testing Interception mode you receive an error from the unit test harness that is `Can not deserialize` something. e.g.,

```
main_program: Skipping test spec '/opt/dm/mci/specs/DS_IIS_ADMIN/EnvironmentScouter/EnvironmentScouter.yaml', 
Can not deserialize instance of java.util.LinkedHashMap out of START_ARRAY token
 at [Source: java.io.FileInputStream@61ee5e4e; line: 10, column: 3] 
 (through reference chain: com.datamigrators.mettle.spec.TestSpecification["when"]->com.datamigrators.mettle.spec.JobExecution["parameters"])
```

# Cause

This is caused by a unit test specification specification with an invalid syntax. The following specification, for example, does not specify Job parameters correctly, and causes the error described above:

```
---
given:
- path: "es_queryEnv-ln_results.csv"
  stage: "es_queryEnv"
  link: "ln_results"
when:
  job: "EnvironmentScouter"
  controller:
  parameters:
  - APT_GRID_ENABLE
then:
- path: "sf_envReport-ln_toFile.csv"
  stage: "sf_envReport"
  link: "ln_toFile"
```

# Solution

Fix your test specification to use the correct syntax.