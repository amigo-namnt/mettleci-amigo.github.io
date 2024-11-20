# MettleCI Unit Test execution throws 'java.lang.OutOfMemoryError: Java heap space' exception

If you receive an ‘Out of Memory’ error when running a MettleCI Unit Test then your test data is unable to fit into the memory allocated by the underlying MettleCI Unit Test operator. Options available are:

*   Curate your test data too reduce its volume (recommended), or
    
*   Use a `cluster` key specification to reduce your test’s memory footprint.