# Updating DataStage Stops the MettleCI Unit Test Harness Working for Parallel Jobs

# Problem

You ran a DataStage patch installer and now the Parallel Unit Test harness does not work.

# Cause

The IBM update installer may destroy [the osh symbolic link](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1465778187/How+the+Parallel+Unit+Test+Harness+Integrates+with+DataStage) created by MettleCI.

# Solution

There are two ways to address this, one using a reinstall with the **force** option, and one that manually fixes the required symbolic link:

## Reinstall

The fix procedure with the least opportunity to cause damage is to…

1.  verify that `osh` is not a symlink,
    
2.  backup and remove `osh-ibm` and `osh-dm`, and
    
3.  reinstall MettleCI Unit Test Harness using the force option (if installing the same version). Consult your O/S-specific documentation on how to force the installation of an `rpm` package. On many systems using `rpm` it will be `-replacepkgs`
    

This procedure ensures you only perform destructive operations to `osh-dm` (which is easily replaceable) and `osh-ibm` which is the renamed version of `osh` which was overwritten by the DataStage patch install process.

There is a risk if one inadvertently attempts this procedure when `osh` is actually a symlink, thereby deleting the only copy of osh. However, this is lower risk than deleting `osh-ibm` and recreating the symlink manually.

## Manually fixing the file

If you want to manually fix the Parallel execution infrastructure on a Unix-based system you can manually restore the affected files as follows: (as user `dstage`)

```
$> mv osh-ibm osh-ibm.bad
$> mv osh osh-ibm
$> ln -s osh-dm osh
```

This will restore harness operation.

## See also

*   [How the Parallel Unit Test Harness Integrates with DataStage](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1465778187/How+the+Parallel+Unit+Test+Harness+Integrates+with+DataStage)
    
*   [How do I safely update a DataStage Installation in which the MettleCI Unit test harness has been Installed?](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1457750170/How+do+we+safely+update+DataStage+where+the+MettleCI+Unit+Test+Harness+has+been+Installed)