# Error "can't create transaction lock" when installing MettleCI Workbench on Unix

# Symptom

You receive a `can't create transaction lock` error when attempting to install the Workbench on a Unix environment using `rpm`:

```
$> rpm -U dm-mettleci-workbench-1.0-1405.noarch.rpm
error: can't create transaction lock on /var/lib/rpm/.rpm.lock (Permission denied)
```

# Cause

You aren’t running the Workbench `rpm` installation as the `root` user, or as a user with `root` privileges.

# Solution

Run the Workbench `rpm` installation as the `root` user! ![(wink)](https://datamigrators.atlassian.net/wiki/s/267366890/6452/f660f55a6ec0c72869a509786ad7dcc22cb92d15/_/images/icons/emoticons/wink.png)