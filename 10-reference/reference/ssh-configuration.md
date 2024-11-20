# SSH Configuration

MettleCI and its associated systems make use of [SSH](https://en.wikipedia.org/wiki/Secure_Shell) (a form of [public key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography)) to provide secure communications channels between software components running on different hosts. This page provides an outline of the MettleCI-related components which use SSH, and a high-level view of how those components should be configured.

> [!INFO]
> This page assumes you are running MettleCI Workbench on a Unix-based host under a user called `mciworkb` ([link](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/455802915/Installing+or+Upgrading+Workbench+on+Unix#Pre-install-steps-if-operating-Workbench-with-a-non-default-user)).

# Files relevant to MettleCI

The misconfiguration of SSH-related files on the DataStage Engine on which you have MettleCI Workbench installed can give rise to various symptoms, most of which are characterised by the failure of one system to form a trusted connection with another. This page describes the SSH components relevant to MettleCI, and how those components should be configured for successful operation.

![](./attachments/MettleCI%20SSH%20Components.png)

# MettleCI CLI

MettleCI CLI commands most commonly execute on the MettleCI Agent Host ([described here](#)) and communicate with the DataStage Engine to perform build and deployment tasks. Those commands which communicate over SSH (most notably those from the [Remote Namespace](#) with the `privateKey` option) are dependent upon correct configuration of the SSH between these two hosts.

In the diagram above the MettleCI Agent Host ([described here](#)) stores a private key file (named `client.key` in the diagram above) for which the public key equivalent (e.g. `client.key.pub`) is stored inside the `~/.ssh/authorized_keys` file of the user account you are using to execute the MettleCI Workbench - typically `mciworkb`. This permits SSH connection between the MettleCI Agent Host and your DataStage Engine upon which the MettleCI Workbench is running.

## Directory `/mciworkb/.ssh`

The directory `/home/mciworkb/.ssh`should have the following properties:

*   user ownership of `mciworkb`
    
*   group ownership of `dstage`
    
*   permissions of `700` (`drwx------`)
    

For example:

```
$> ls -ld /home/mciworkb/.ssh
drwx------ 2 mciworkb dstage 144 Feb 16 14:26 .ssh
```

These properties can be established with the following commands:

```
$> chown mciworkb:dstage /home/mciworkb/.ssh      # Ownership
$> chmod 700 /home/mciworkb/.ssh                  # Permissions
```

## Files within `/mciworkb/.ssh`

The directory `/home/mciworkb/.ssh`should contain the file **authorized\_keys** which effectively controls inbound connections from other hosts. It contains the SSH public keys of hosts that are permitted to connect to your DataStage Engine using key-based authentication. This directory may also contain other files such as **known\_hosts** or **config** which are not required for successful MettleCI operations.

The `authorized_keys` file should have the following properties:

*   user ownership of `mciworkb`
    
*   group ownership of `dstage`.
    
*   permissions of `600` (`drw-------`)
    

This can be established with…

```
$> chown mciworkb:dstage /home/mciworkb/.ssh/authorized_keys      # Ownership
$> chmod 600 /home/mciworkb/.ssh/authorized_keys                  # Permissions
```

For example:

```
$> ls -ld /home/mciworkb/.ssh/authorized_keys
-rw------- 1 mciworkb dstage 1167 Feb 16 14:31 .ssh/authorized_keys
```

# Third Party Systems

SSH may also be involved in MettleCI Workbench’s communication with Work Item Management and Git platforms. In these cases you will use a SSH key pair hosted on the DataStage Engine to form this connection. Your DataStage Engine will store a private key file, an example of which (`workbench.key`) is created in the MettleCI directory (typically `/opt/dm/mci`) during MettleCI installation. The the public key equivalent (e.g. `workbench.key.pub`) is supplied to third party systems with which your DataStage engine needs to communicate - most commonly your Git and Work Item Management platforms. You can either use the key pair created for you by the MettleCI installation process (`workbench.key` / `workbench.key.pub`, which is a 521-bit [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) key) or create your own if your organisation or third party system have specified SSH key requirements. The process varies from tool to tool, so please see the relevant MettleCI documentation for tools relevant to you.

* * *

# See Also

*   [Adding public keys to GitHub](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2215084033/Adding+public+keys+to+GitHub)
    
*   [Configure MettleCI Workbench Authentication to Azure Git Repo](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/459178004/Configure+MettleCI+Workbench+Authentication+to+Azure+Git+Repo)
    
*   [Integrating Atlassian Jira with MettleCI Workbench](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1507328025/Integrating+Atlassian+Jira+with+MettleCI+Workbench)
    
*   [Configuring MettleCI Workbench SSH Authentication to GitLab](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/741376054/Configuring+MettleCI+Workbench+SSH+Authentication+to+GitLab)
    
*   [Using SSH Keys in MettleCI CI/CD Pipelines](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2377056265/Using+SSH+Keys+in+MettleCI+CI+CD+Pipelines)