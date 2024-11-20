# The `mettleci datastage create-project` command fails

# Symptom

The `mettleci datastage create-project` command ([documented here](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408420417/DataStage+Create-Project+Command)) fails inexplicably.

# Cause

Due to a known issue with the DataStage `dsadmin` command (which is required by `datastage create-project`) it is not possible to distinguish between...

*   a DataStage project that already exists, and
    
*   a DataStage project that doesn’t exist in the DataStage repository, but for which the associated filesystem directories do exist.
    

There may be some situations in which this causes the `create-project` command to fail.

# Solution

When faced with an inexplicable failure of this nature check to see if the project’s directory structure already exists on the filesystem. If so, and it’s safe to do so, remove the file structure and try again

* * *

# See also

*   [DataStage Create-Project Command](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/408420417/DataStage+Create-Project+Command)