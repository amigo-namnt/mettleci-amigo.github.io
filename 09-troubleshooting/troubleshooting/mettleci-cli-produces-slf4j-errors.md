# MettleCI CLI produces SLF4J errors

# Problem

With some MettleCI command line options you may receive some messages that look like errors preceded by `SLF4J:`.

```
c:\Jenkins\Builds\workspace\wwi_jenkins_ds117>C:\dm\mci\cli\mettleci.cmd remote execute -host demo4-engn.datamigrators.io -username **** -password **** -script "config\cleanup.sh"
MettleCI Command Line. Build 96
(C)2019 Data Migrators Pty Ltd
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
Connecting to demo4-engn.datamigrators.io on port 22
exit code = 0
```

# Solution

Despite their somewhat alarming wording these messages are innocuous logging messages from one of the open source Java modules used within MettleCI and can be safely ignored. A future release of MettleCI will suppress these messages.

> [!INFO]
> **UPDATE**
> This symptom was removed in Command Shell release `1.1-174`.