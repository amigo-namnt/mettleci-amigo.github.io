# Adjacent Transformers

|     |     |
| --- | --- |
| **Rule name** | Adjacent Transformers |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Identified job designs with adjacent Transformer stages. |

# Description

Although powerful, transformers contain embedded logic that is not immediately obvious when looking at the canvas and reduces a developers ability to immediately understand a job's logic. Overuse of transformers when more ‘verbose’ stages could achieve the same outcome can result in greater maintenance overhead.

Adjacent transformers can be a symptom of a transformer that has become so complex that a developer has needed to split the embedded logic across two transformers. When this occurs, developers should consider if there is an alternative implementation strategy that could be implemented using multiple standard stages working in conjunction rather than performing all logic within one or more transformer stages

Alternatively, adjacent transformers can also be a symptom of defect fixes that are "tacked on" to an existing job rather than understanding the existing job logic and refactoring accordingly. Making job changes without continually refactoring the existing code will degrade job quality and increase maintenance over time.

# Actions

Adjust your job design so that there are no adjacent transformers. Consider combining adjacent Transformer stages if possible.