# Failing to Read Assets from the DataStage Repository

## Problem

If you are using the DataStage Bamboo capability ([https://datamigrators.atlassian.net/wiki/spaces/AET/pages/291700836](https://datamigrators.atlassian.net/wiki/spaces/AET/pages/291700836)) then under the hood MettleCI will interact with DataStage through SSH ([What is SSH?](https://en.wikipedia.org/wiki/Secure_Shell)).  To configure this communication to work properly you must take some preparatory steps.

## Solution

Follow carefully the steps described by IBM in their document [Storing certificates for client applications](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.3.0/com.ibm.swg.im.iis.found.admin.common.doc/topics/cert_truststore.html).  This should adequately solve any outstanding issues with the DataStage bamboo capability.

> [!INFO]
> Be attentive to the paragraph that mentions "**For command line utilities"**.  We recommend using [istool export](https://www.ibm.com/support/knowledgecenter/en/search/istool%20export?scope=SSZJPZ_11.5.0) to test if this communication is working properly without harming your environment.

## Related articles

##### Filter by label

There are no items with the selected labels at this time.