# Date Format in Annotation

|     |     |
| --- | --- |
| **Rule name** | Date Format in Annotation |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | Yes |
| **Description** | Identify whether the a ‘Job Description’ annotation contains instances of particular arbitrary text. This example rule looks for dates. |

# Description

Identify whether the a ‘Job Description’ annotation contains instances of particular arbitrary text. You can modify this rule to get it to seek out any text your team wants to prevent passing compliance. This example rule looks for text matching the following date formats:

| **Format** | **Description** |
| --- | --- |
| `YYYY-MM-DD`<br><br>`YYYY/MM/DD`<br><br>`YYYY MM DD`<br><br>`YYYY-MMM-DD`<br><br>`YYYY/MMM/DD`<br><br>`YYYY MMM DD`<br><br>`YYYY-MMMM-DD`<br><br>`YYYY/MMMM/DD`<br><br>`YYYY MMMM DD` | YYYY-MM-DD format<br><br>with `/`, `-`, as delimited<br><br>Month format can be<br><br>`MM` , `MMM`, `MMMM` or `MON`<br><br>`MMM` and `MMMM` are Excel Syntax |
| `DD-MM-YYYY` | Similar to YYYY-MM-DD |
| `MM-DD-YYYY` | Similar to YYYY-MM-DD (common US date format) |

# Actions

Remove or alter the offending text.