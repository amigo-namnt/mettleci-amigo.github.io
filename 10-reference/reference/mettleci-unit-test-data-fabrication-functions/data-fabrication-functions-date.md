# Data Fabrication Functions - Date

| **Module** | **Fabricator** | **Description** | **Parameters** | **Notes** |
| --- | --- | --- | --- | --- |
| date | between | Random date between two supplied dates | **from** (date**,** default is empty)<br><br>**to** (date**,** default is empty | If either parameter is empty the function generates an error message. |
| date | future | Generates a random future date X years from Y date, where X and Y are parameters. | **years** (number**,** default is 1)<br><br>**refDate** (date**,** default is today) |     |
| date | month | A random month name | **abbr** (boolean**,** default is false)<br><br>**context** (boolean**,** default is false) |     |
| date | past | Generates a random past date X years from Y date, where X and Y are parameters. | **years** (number**,** default is 1)<br><br>**refDate** (date**,** default is today) |     |
| date | recent | Generates a random past date a specified number of days from the current date. | **days** (number**,** default is 1) |     |
| date | weekday | A random weekday name | **abbr** (boolean**,** default is true)<br><br>**context** (boolean, default is true) |     |