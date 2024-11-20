# MettleCI command 'workbench set-branch' command produces a credentials error

# Symptom

MettleCI command `workbench set-branch` ([documentation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2449047553/Workbench+Set-Branch+Command)) command produces the error `Credentials are required to access this resource`.

# Cause

This can be caused when the `config.yml` file has the following property set:

`userInactiveTimeout: 0`

Read more about this setting [here](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2093514784/Configuring+MettleCI+Workbench+to+increase+session+timeout).

> [!WARNING]
> Note that this FAQ refers to the MettleCI Workbench `config.yml` file and not the `config.properties` used to configure the MettleCI Command Line Interface.

# Solution

Either remove the`userInactiveTimeout` line completely or set it to a positive (non-zero) value.