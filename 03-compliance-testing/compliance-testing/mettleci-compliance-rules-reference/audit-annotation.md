# Audit Annotation

|     |     |
| --- | --- |
| **Rule name** | Audit Annotation |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | Yes |
| **Description** | Identifies where sensitive information may potentially be present in DataStage Job and Sequence Annotations |

# Description

This rule looks for the following signatures in all annotations:

1.  The name of a DataStage hostname, as well as instances
    

2\. Instances of the words `hostname`, `password`, `organisation` (UK-EN spelling) or `organization` (US-EN spelling).

Note that it is impossible to use regular expressions to detect a password, hostname, or organisation, but assuming one of these words is found the likelihood of the actual sensitive information being present is high.

Like all MettleCI Compliance Rules, this rule is an example intended for you to adapt to suit your needs.

# Actions

Remove the sensitive information from your Job or Sequence annotation.