# Some MettleCI Command Line options are being ignored on Windows

# Problem

When you run a multi-line `mettleci` command on Microsoft Windows using the caret (`^`) line continuation character it appears that processing of the command line options seems to stop at some point in the command.

For example:

```
# This input...
C:\> mettleci compliance test ^
  -assets datastage ^
  -report out.xml ^
  -rules rules ^
  -junit ^ 
  -test-suite warnings ^
  -ignore-test-failures ^
  -project-cache .

# ...executes the following command:
C:\> mettleci compliance test ^  -assets datastage ^  -report out.xml ^  -rules rules ^ -junit
MettleCI Command Line (build 128)
(C) 2018-2022 Data Migrators Pty Ltd
rules configuration discovered
new rule discovered - 'Adjacent Transformers' (PARALLEL_JOB)
new rule discovered - 'Adjacent Transformers' (SERVER_JOB)
<etc.>
```

When you look at your output it seems that command line options after the `-junit` option (`-test-suite warnings`, `-ignore-test-failures`, and `-project-cache`) have all been ignored.

# Cause

**In the command submitted above the** `-junit` **line has a space following the caret!**

When using the caret (`^`) line continuation character in a Windows command shell script you must be careful to avoid adding a trailing space after the caret as this will cause command parsing to stop at that point. The caret causes the Windows Command Shell to effectively ignore the following character, which is normally a newline. If the character following a caret is a space then the space is ignored and the following newline is processed as normal, meaning the command is effectively ended at that point.

# Solution

Remove any trailing spaces after line continuation carets.