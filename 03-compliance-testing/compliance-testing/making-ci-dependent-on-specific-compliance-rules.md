# Making CI dependent on specific Compliance Rules

This page describes how you can specify the Compliance Rules that, if triggered by the presence of certain (undesirable) coding patterns in your DataStage assets, will cause the Continuous Integration build to fail. This will mean that the version of code present in Git at the time won’t be promote-able to downstream environments until those particular Compliance Rule-detected issues are addressed.

Here’s a pseudo-code example of a Compliance rule with a set of `@tag` annotations (described [here](../compliance-testing/compliance-rule-tags.md)):

```
package datamigrators

# Rule tags (effectively user-defined, free-form attributes)
@Tag("security")            # Is a potential security vulnerability
@Tag("portability")         # Is a issues with assets' portability between dev, test, and prod environments
@Tag("maintainability")     # Is a potential maintainability issue
@Tag("CorpDataWarehouse")   # Is specific to the 'CorpDataWarehouse' team
@Tag("fail-ci")             # Is mandatory and so should fail continuous integration if breached

# Rule definition
<blah blah blah>
```

A subset of our Compliance rules (including the one above) us a specific tag value to identify those rules which are mandatory for CI success; these rules are considered of utmost importance, and may enforce constraints related to security, or portability across environments, for example. We can choose any value we wish for this identifying tag, however the tag we use in the rule must correspond with the tag referenced in the part of your CI pipeline which calls the `mettleci compliance test` command.

> [!NOTE]
> Build systems used to orchestrate CI/CD processes do not (for the most part) support the concept of a test ‘warning’. The ‘warnings’ configured in the example pipelines shipped with MettleCI are simply there to allow a subset of compliance rules to fail without causing your entire CI process to fail.

# Specify which tags will cause a Continuous Integration run to fail

For example, you’ll see that the rule above defines a tag with the value `fail-ci`. In most environments the Continuous Integration pipeline will be configured to call the `mettleci compliance test` command twice:

1.  **Warning breaches**: The first call will be to determine which of your DataStage assets trigger those Compliance rules which **do not** have the `fail-ci` tag. This call will produce relevant output to your build system’s logs, but **will not** be configured to cause your build to abort.
    
2.  **Fatal breaches:** The second call will be to determine which of your DataStage assets trigger those Compliance rules which **do** have the `fail-ci` tag (i.e. a mutually exclusive set of rules from the first call). This call will again produce relevant output to your build system’s logs, but in this case it **will** be configured to cause your build to abort.
    

Again, the actual tag you choose to identify rules can be any value, as long as the tag in your rules and the tag used in your CI pipelines is the same value.

## Practical examples

Here are some example calls to [Compliance Test Command](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408322069/Compliance+Test+Command) for each of the use cases described above.

Rules which only generate warnings would be identified as those rules **not** using the `fail-ci` tag and would be invoked using the `ignore-test-failures` option to prevent the pipeline from failing. e.g.

```
# Invoke a Compliance tests for NON-FATAL rules
# Note that this call uses the 'ignore-test-failures' option

$> mettleci compliance test
  -rules compliance_rules
  -assets datastage
  -report compliance_report_warn.xml
  -project-cache ./project-cache      # Uses incremental testing to optimise Compliance performance.
  -exclude-tag 'fail-ci'              # Exclude the set of rules which should cause CI to abort
  -junit                              # Produce JUnit output so CI build system can manage test results
  -test-suite compliance_warnings     # Optional. Label these JUnit outputs as part of a 'compliance_warnings' test suite. 
  -ignore-test-failures               # Make this call succeed regardless of whether any rules fail!
```

Rules which abort the pipeline would be identified using the `fail-ci` tag and invoked **without** the `ignore-test-failures` option. e.g.

```
# Invoke a Compliance test for FATAL rules
# Note that this call OMITS the 'ignore-test-failures' option

$> mettleci compliance test
  -rules compliance_rules
  -assets datastage
  -report compliance_report_warn.xml
  -project-cache ./project-cache      # Uses incremental testing to optimise Compliance performance.
  -include-tag 'fail-ci'              # Use ONLY the set of rules which should cause CI to abort
  -junit                              # Produce JUnit output so CI build system can manage test results
  -test-suite compliance_failures     # Optional. Label these JUnit outputs as part of a 'compliance_failures' test suite. 
```

## Use within a CI pipeline

In the context of a CI pipeline these calls would look like this example from Jenkins…

Firstly, let’s take a look the pseudocode of a reusable pipeline component in `mci_compliance.groovy`:

```
def call(
    def COMPLIANCE_REPO_CREDENTIALS,
    def COMPLIANCE_REPO_URL,
    def RULESDIR,
    def TESTSUITENAME,
    def INCLUDETAGS,
    def EXCLUDETAGS,
    def CONTINUEONFAIL
)
try {
    bat label: "Compliance Test - ${TESTSUITENAME}",
        script: """
            %AGENTMETTLECMD% compliance test ^
                -rules compliance\\${RULESDIR} ^
                -assets datastage ^
                -report \"compliance_report_${TESTSUITENAME}.xml\" ^
                -project-cache \"%AGENTMETTLEHOME%\\cache\\%IISENGINENAME%\\%DATASTAGE_PROJECT%\"
                -include-tag \"${INCLUDETAGS}\" ^                 
                -exclude-tag \"${EXCLUDETAGS}\" ^
                -junit -test-suite \"${TESTSUITENAME}\" ^
                ${((CONTINUEONFAIL as boolean) == true)? '-ignore-test-failures':''}  ^
            """
}
```

This reusable component, which acts as a wrapper for the `mettleci compliance test` command, takes a number of parameters, including values which will be used as operands for the `-include-tag` and `-exclude-tag` options.

In the main Jenkins pipeline definition we make two calls to the reusable compliance component, using appropriate settings for the `include-tags`, `exclude-tags`, and `ignore-test-failures` options:

```
steps {
  // Warning
  mci_compliance(
      env.COMPLIANCE_REPO_CREDENTIALS,
      env.COMPLIANCE_REPO_URL,
      "DEVOPS-WARN",
      "Warnings",
      "",                   // Include everything...
      "fail-ci",            // ...then exclude rules tagged 'fail-ci'
      true                  // Ignore test failures
  )   
  // Fatal
  mci_compliance(
      env.COMPLIANCE_REPO_CREDENTIALS,
      env.COMPLIANCE_REPO_URL,
      "DEVOPS-FAIL",
      "Errors",
      "fail-ci",            # Include only rules tagged 'fail-ci'...
      "",                   # ... then exclude nothing
      false                 # DO NOT ignore test failures
  )
}
```

See [MettleCI System Integrations](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/733675552/MettleCI+Integrations) for more details of CI configuration.