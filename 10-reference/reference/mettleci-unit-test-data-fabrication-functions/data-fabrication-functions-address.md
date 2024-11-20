# Data Fabrication Functions - Address

| **Module** | **Fabricator** | **Description** | **Parameters** | **Notes** |
| --- | --- | --- | --- | --- |
| address | city | Generates a random localized city name. The format string can contain any method provided by the MettleCI data fabrication library wrapped in `{{}}`, e.g. `{{name.firstName}}` in order to build the city name.<br><br>If no format string is provided one of the following is randomly used:<br><br>*   `{{address.cityPrefix}} {{name.firstName}}{{address.citySuffix}}`<br>    <br>*   `{{address.cityPrefix}} {{name.firstName}}`<br>    <br>*   `{{name.firstName}}{{address.citySuffix}}`<br>    <br>*   `{{name.lastName}}{{address.citySuffix}}` | **format** string |     |
| address | cityPrefix | Return a random localized city prefix | \-  |     |
| address | citySuffix | Return a random localized city suffix | \-  |     |
| address | country | Return a random country name | \-  |     |
| address | countryCode | Return a random ISO country code | \-  |     |
| address | county | Return a random county name | \-  |     |
| address | latitude | Return a random latitude | **max** double default is 90<br><br>**min** double default is -90<br><br>**precision** number default is 4 | *The function parameters are currently disabled and will be made available in a forthcoming release.* |
| address | longitude | Return a random longitude | **max** double default is 90<br><br>**min** double default is -90<br><br>**precision** number default is 4 | *The function parameters are currently disabled and will be made available in a forthcoming release.* |
| address | secondaryAddress | Return a secondary address | \-  |     |
| address | state | Return a state | **useAbbr** boolean | *This function parameter is deprecated and will be removed in a forthcoming release. Please use the stateAbbr function instead.* |
| address | stateAbbr | Return a state abbreviation | \-  |     |
| address | streetAddress | Returns a random localized street address | **useFullAddress** boolean |     |
| address | streetName | Returns a random localized street name | \-  |     |
| address | streetPrefix | Returns a random street prefix | \-  |     |
| address | streetSuffix | Returns a random street suffix | \-  |     |
| address | zipCode | Returns a random localized zip or postal code | \-  |     |
| address | direction | Return a direction | **useAbbr** boolean defaults to false | *This function is currently disabled and will be made available in a forthcoming release.* |
| address | cardinalDirection | Return a cardinal direction | \-  | *This function is currently disabled and will be made available in a forthcoming release.* |
| address | ordinalDirectiopn | Return a direction . | **useAbbr** boolean defaults to false | *This function is currently disabled and will be made available in a forthcoming release.* |