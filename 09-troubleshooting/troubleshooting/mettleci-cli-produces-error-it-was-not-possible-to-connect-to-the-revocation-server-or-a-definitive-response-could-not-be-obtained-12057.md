# MettleCI CLI produces error 'It was not possible to connect to the revocation server or a definitive response could not be obtained. [12057]'

## Symptom

Running a MettleCI CLI command (typically on a Windows client being used as a build agent) works well until it attempts to connect to a DataStage Engine or Service tier and then produces a 12057 error of the following form:

```
simple	21-Jan-2024 20:49:39	Compiling DataStage jobs...
error	21-Jan-2024 20:52:34	 * Compile 'WBIUTV/CI_Utvikling/Jobs/GZC GZD - Gml arkitektur/GZC/GZC0501/MicroFocusJCLSekvensGZC0501.qjb' - FAILED
error	21-Jan-2024 20:52:34	      
error	21-Jan-2024 20:52:34	      Initializing
error	21-Jan-2024 20:52:34	      
error	21-Jan-2024 20:52:34	      Failed to attach to the project.
error	21-Jan-2024 20:52:34	      It was not possible to connect to the revocation server or a definitive response could not be obtained. [12057]
error	21-Jan-2024 20:52:34	
error	21-Jan-2024 20:52:34	      Exit Status 1
```

This error can occur while executing any CLI command that uses DataStage tooling or commands to connect to the Services or Engine tier over SSH, the above is just one example.

The `dscc` and/or `istool` command can be used to help debug this and isolate the error. Connect to the Agent Host machine (the one where your build agent (e.g. Jenkins Agent, ADO Agent, Gitlab runner, or Bamboo Remote Agent) is running), open a Command Prompt, then try to use `istool` to export an ISX of a job you saw a failure for, and/or try to use `dscc` to compile one of the jobs you observed failing. You must do this in the project that was failing, using the same userid and credentials your build agent uses, or it is not an accurate test. Capture the full log of this test for further analysis. If either or both commands fail the same way from the command line, you have ruled out MettleCI, as this isn’t a MettleCI issue. The error is being reported by `istool` or `dscc` and simply captured by MettleCI logging. If both `istool` and `dscc` succeed in an identical environment when the CLI fails, then contact MettleCI support.

## Cause

SSL certificates are supposed to have a definite time to be valid, but there is a mechanism to revoke them early. Contacting the revocation server (which then asserts that the presented certificate is not revoked, and is still valid) is part of establishing an SSL connection, most likely between `dscc` or `istool` and the Services Tier. The revocation server that is relevant to the Services Tier might be part of your own network infrastructure (if you issue your own SSL certificates) or it might be external (if not).

If the revocation server can’t be reached because of network issues or the server isn’t functioning correctly, then you will see errors about contacting the revocation server and DataStage client tool connection refusals. We’ve experienced this at other customer sites. This situation is *entirely* dependent on **where** the relevant `dscc` or `istool` command is being executed and by **which account**. These types of errors can be intermittent and difficult to reproduce, but if you are not replicating the environment (which machine and which account) exactly, you will make problem determination more difficult.

## Resolution

Correct the issue preventing the revocation server from being reached. The details of how to do this are client and environment specific, and it is not possible to exhaustively enumerate all possible causes. But, here are some thought starters to aid you:

*   If when you were reproducing/narrowing the error, one command worked but the other did not, check for policy or configuration changes, since some tools use java mechanisms and others use windows mechanisms.
    
*   If the issue is intermittent, it is possible that one server of a pool is misconfigured and sometimes the connection gets through (it works if any other server is chosen randomly, which may be very opaque to you).
    

You may want to consult with your network or security team, there are many different components that may contribute to the unreachability issue, and they may be better equipped to examine all of them for possible issues.