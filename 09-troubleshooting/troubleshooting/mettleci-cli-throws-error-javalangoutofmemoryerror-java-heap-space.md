# MettleCI CLI throws error 'java.lang.OutOfMemoryError: Java heap space'

## Problem

Various commands in the MettleCI CLI are throwing a `java.lang.OutOfMemoryError: Java heap space` error.

## Solution

> [!INFO]
> If you are using MettleCI CLI versions between `139` and `145` then ensure you upgrade to `146` or later.

Increase the Java Heap Size by passing the `-Xms` & `-Xmx` value while running the CLI

> [!NOTE]
> Default maximum heap size set by `MettleCI CLI` is 512m

### Unix/Linux

```
$ export JAVA_OPTIONS="-Xms32m -Xmx1024m"
$ ./mettleci datastage execute 
                  -domain svcs.host:9443 
                  -server engn.host 
                  -username isadmin 
                  -password *****
                  -project dstage1
                  -jobname myfirstjob
```

### Windows

```
C:\mci\cli> set JAVA_OPTIONS=-Xms32m -Xmx1024m
C:\mci\cli> mettleci datastage execute 
                  -domain svcs.host:9443 
                  -server engn.host 
                  -username isadmin 
                  -password *****
                  -project dstage1
                  -jobname myfirstjob
```

# Solution for MettleCI CLI version 138 or earlier

If you are using are using `MettleCI CLI` version `1.0-138 or below`, you will need to edit the `mettleci` or `mettleci.cmd` file

Search for

```
JAVA_OPTIONS=-Xms32m -Xmx512m
```

and increase the `-Xmx` value

```
JAVA_OPTIONS=-Xms32m -Xmx1024m
```