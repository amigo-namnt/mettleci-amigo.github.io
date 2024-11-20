# Bamboo SFTP Upload Task

You can use the SFTP Upload task to transfer files and directories from the local working directory to a remote SFTP server.

## Using the SFTP Upload Task user interface

1.  Navigate to the **Tasks** configuration tab for the job (this will be the default job if creating a new plan).
    
2.  Click the name of an existing SFTP Download task or click **Add Task** and then search 'SFTP' to easily locate the SFTP Upload task type, in order to create a new task.
    
3.  Complete the following settings:
    

|     |     |
| --- | --- |
| **Task Description** | A description of the task, which is displayed in Bamboo. |
| **Disable this task** | Check, or clear, to selectively run this task. |
| **Host** | The hostname or IP address of the remote server to which the files will be copied. |
| **Authentication Type** | **Username and Password** - Enter username and password to use when connecting to remote host. |
| **SSH Private Key** - Browse to the SSH private key with which to authenticate with the remote host.  A passphrase for the key can be supplied if required. |
| **Local Directory** | The path to the upload source directory (relative to the Bamboo working directory). |
| **Include Pattern** | A comma separated list of files to be uploaded relative to the local directory path.  You can use Ant-style [pattern matching](https://confluence.atlassian.com/bamboo0600/pattern-matching-reference-894742650.html) to include multiple files, such as `**/target/*.jar`. |
| **Remote Directory** | The path to the upload destination directory on the remote server |
| **Verify remote host fingerprint on connect** | Enter the host fingerprint to be verified.  See [below](https://datamigrators.atlassian.net/wiki/pages/resumedraft.action?draftId=499056670#BambooSFTPUploadTask-fingerprint) for more details. |
| **Port** | The port number of the remote host that is used for the SSH connection. The default value is 22. |

4.  Click **Save**
    

## Determining the host fingerprint

You can determine the fingerprint for a host by running the following command:

```
ssh-keygen -l -F <HOSTNAME>
```

The fingerprint is included in the response.

```
$> ssh-keygen -l -F some.domain.name.com
# Host some.domain.name.com found: line 20 type RSA
2048 b9:81:c6:9f:4f:fc:9a:32:32:7c:8e:12:6c:9a:77:df some.domain.name.com (RSA)
     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

In the example above, `b9:81:c6:9f:4f:fc:9a:32:32:7c:8e:12:6c:9a:77:df` is the fingerprint.

## Use the SFTP Upload Task in a YAML pipeline

```
- mci-sftp-upload:
    destination-dir: ${bamboo.buildResultKey}-${bamboo.EnvironmentID}
    transfer-pattern: filesystem/**/*,config/*
    port: '22'
    host: ${bamboo.ServerName}
    username: ${bamboo.ServerUsername}
    shared-credentials: *ssh_credentials
    description: Transfer DataStage config and file system assets
```