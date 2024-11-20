# Command shell Error: Unable to access jarfile

# Symptom

When executing any command using the MettleCI command shell, the process crashes with the following error:

`Error: Unable to access jarfile demo/dm-mettleci-command-shell-1.1/bin/command-shell-1.1-174.jar`

# Cause

The Command Shell installation path includes whitespace (anywhere in the path).

# Solution

The Command Shell must be installed in a location where the full absolute path includes no whitespace.