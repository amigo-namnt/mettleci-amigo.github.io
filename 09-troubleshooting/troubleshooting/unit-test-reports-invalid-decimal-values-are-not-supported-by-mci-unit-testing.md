# Unit Test reports 'Invalid Decimal values are not supported by MCI Unit Testing'

# Problem

When running MettleCI Unit Testing you receive the message `Invalid Decimal values are not supported by MCI Unit Testing`.

# Cause

MettleCI’s Unit Test functionality relies on DataStage’s underlying Java integration capabilities. There are two types of data which will cause exceptions within DataStage’s Java Integration stage:

1.  **Invalid Decimals** which are data defined as decimal but which do not fulfill the definition of that format; and
    
2.  **Binary Zero Decimals** which are literal `0x00` (ASCII `null`) bytes in the memory space, which MettleCI attempts to interpret as '0.0' but *can* be considered valid in their as-supplied form by DataStage if the [fix\_zero](https://www.ibm.com/docs/en/iis/11.7?topic=listing-fix-zero) option is specified.
    

For Unit Testing to operate correctly it needs to be able to read (during Unit Test Interception) and write (during Unit Test Execution) both of these types of decimal values. Unfortunately, the Java Integration Stage is unable to do this for either type of invalid data.

MettleCI does implement a workaround to avoid the exception reported when **reading** one of these types of invalid decimal values. However, DataStage doesn’t provide a way for MettleCI to **write** Invalid Decimals, or to **read or write** Binary Zero Decimals. The situation at the time of writing is summarised in the following table.

| DataStage limitations on MettleCI support for invalid decimal data | **Read** | **Write** |
| --- | --- | --- |
| **Invalid Decimal** | ![(blue star)](https://datamigrators.atlassian.net/wiki/s/267366890/6452/f660f55a6ec0c72869a509786ad7dcc22cb92d15/_/images/icons/emoticons/72/2714.png) | ![(blue star)](https://datamigrators.atlassian.net/wiki/s/267366890/6452/f660f55a6ec0c72869a509786ad7dcc22cb92d15/_/images/icons/emoticons/72/2716.png) |
| **Binary Zero** | ![(blue star)](https://datamigrators.atlassian.net/wiki/s/267366890/6452/f660f55a6ec0c72869a509786ad7dcc22cb92d15/_/images/icons/emoticons/72/2716.png) | ![(blue star)](https://datamigrators.atlassian.net/wiki/s/267366890/6452/f660f55a6ec0c72869a509786ad7dcc22cb92d15/_/images/icons/emoticons/72/2716.png) |

In use, MettleCI captures the invalid decimals during Unit Test [Interception](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/437518414/Unit+Test+Data+Interception+-+Capturing+Existing+Test+Data?src=search). However, when a Unit Test is executed the MettleCI Unit Test Harness attempts to read those Unit Test data containing invalid decimals and generates an error message.

The benefits of this approach are:

1.  Invalid Decimals are likely to be rare and possibly unexpected, so capturing them allows users to capture all useful data and then either manually change the Invalid Decimal values or remove them entirely using the [Unit Test Data editor](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/466387402/Manually+Editing+Unit+Test+Data).
    
2.  Unit Testing remains able to produce a (failure) test result when the expected Job output does not contain Invalid Decimals but the actual output does. This is more user-friendly than aborting a Unit Test in which the Job produces unexpected Invalid Decimals
    
3.  When a user intercepts data and then attempts to run the resulting MettleCI unit test, the user is presented with an unambiguous message stating it isn’t supported. This will hopefully prevent unnecessary support requests
    

Unfortunately, Binary Zero decimals will still cause aborts but there isn’t anything MettleCI can do about that (including specific error message) for now.

# Solution

Edit the intercepted unit test data to remove the invalid values. You can do this by either replacing individual values with invalid values, or removing the rows containing invalid values entirely.