# MettleCI Command Line Reference

Refer to the [MettleCI Command Line Interface](../mettleci-command-line-interface/mettleci-cli-operating-modes.md) to understand how the interface works, and what each of the columns in the table below means.

Refer to the [https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/264110081](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/264110081) section for recommendations about how these can be used to support specific processes.

# Available Namespaces

*   [Compliance Namespace](./mettleci-command-line-reference/compliance-namespace.md)
*   [DataStage Namespace](./mettleci-command-line-reference/datastage-namespace.md)
*   [DSParams Namespace](./mettleci-command-line-reference/dsparams-namespace.md)
*   [ISX Namespace](./mettleci-command-line-reference/isx-namespace.md)
*   [Properties Namespace](./mettleci-command-line-reference/properties-namespace.md)
*   [Remote Namespace](./mettleci-command-line-reference/remote-namespace.md)
*   [UnitTest Namespace](./mettleci-command-line-reference/unittest-namespace.md)
*   [Workbench Namespace](./mettleci-command-line-reference/workbench-namespace.md)

# Available Commands

| Command Documentation | Namespace | Command | Plugin Name | Plugin File | Credentials | Windows Client |
| --- | --- | --- | --- | --- | --- | --- |
| [DataStage Capture Command](/wiki/spaces/MCIDOC/pages/2568650800/DataStage+Capture+Command) | datastage | capture | datastage | dm-dsdeploy-plugin.jar | IS/DS | \-  |
| [ISX Cat Command](/wiki/spaces/MCIDOC/pages/458784837/ISX+Cat+Command) | isx | cat | isx | dm-isxexport-plugin.jar | \-  | \-  |
| [DataStage Connector Migration Command](/wiki/spaces/MCIDOC/pages/410681364/DataStage+Connector+Migration+Command) | datastage | ccmt | datastage | dm-ccmigrate-plugin.jar | IS/DS | Y   |
| [DataStage Cleanup-Projects Command](/wiki/spaces/MCIDOC/pages/458424418/DataStage+Cleanup-Projects+Command) | datastage | cleanup-projects | datastage | dm-dsadmin-plugin.jar | IS/DS | \-  |
| [DataStage Compile Command](/wiki/spaces/MCIDOC/pages/410157081/DataStage+Compile+Command) | datastage | compile | datastage | dm-dscompile-plugin.jar | IS/DS | Y   |
| [Properties Config Command](/wiki/spaces/MCIDOC/pages/718962693/Properties+Config+Command) | properties | config | properties | dm-properties-config-plugin.jar | \-  | \-  |
| [DataStage Create-Project Command](/wiki/spaces/MCIDOC/pages/408420417/DataStage+Create-Project+Command) | datastage | create-project | datastage | dm-dsadmin-plugin.jar | IS/DS | \-  |
| [ISX Cut Command](/wiki/spaces/MCIDOC/pages/458817574/ISX+Cut+Command) | isx | cut | isx | dm-isxexport-plugin.jar | \-  | \-  |
| [DSParams Delete Command](/wiki/spaces/MCIDOC/pages/458556054/DSParams+Delete+Command) | dsparams | delete | dsparams | dm-dsadmin-plugin.jar | \-  | \-  |
| [DataStage Delete-Project Command](/wiki/spaces/MCIDOC/pages/458424387/DataStage+Delete-Project+Command) | datastage | delete-project | datastage | dm-dsadmin-plugin.jar | IS/DS | \-  |
| [DataStage Deploy Command](/wiki/spaces/MCIDOC/pages/423952410/DataStage+Deploy+Command) | datastage | deploy | datastage | dm-dsdeploy-plugin.jar | IS/DS | Y   |
| [DSParams Diff Command](/wiki/spaces/MCIDOC/pages/458785100/DSParams+Diff+Command) | dsparams | diff | dsparams | dm-dsadmin-plugin.jar | \-  | \-  |
| [Remote Download Command](/wiki/spaces/MCIDOC/pages/716636187/Remote+Download+Command) | remote | download | remote | dm-bamboo-sftp-plugin.jar | OS  | \-  |
| [DataStage Execute Command](/wiki/spaces/MCIDOC/pages/458817755/DataStage+Execute+Command) | datastage | execute | datastage | dm-dsexecute-plugin.jar | IS/DS | \-  |
| [Remote Execute Command](/wiki/spaces/MCIDOC/pages/784367633/Remote+Execute+Command) | remote | execute | remote | dm-bamboo-sftp-plugin.jar | OS  | \-  |
| [ISX Export Command](/wiki/spaces/MCIDOC/pages/409305099/ISX+Export+Command) | isx | export | isx | dm-isxexport-plugin.jar | IS/DS | Y   |
| [UnitTest Generate Command](/wiki/spaces/MCIDOC/pages/2176647169/UnitTest+Generate+Command) | unittest | generate | unittest | dm-dstest-plugin.jar | IS/DS | \-  |
| [ISX Import Command](/wiki/spaces/MCIDOC/pages/409894937/ISX+Import+Command) | isx | import | isx | dm-isximport-plugin.jar | IS/DS | Y   |
| [UnitTest Install-Server-Test-Harness Command](/wiki/spaces/MCIDOC/pages/2640740386/UnitTest+Install-Server-Test-Harness+Command) | unittest | install-server-test-harness | unittest | dm-dstest-plugin.jar | IS/DS | \-  |
| [Compliance List-Tags Command](/wiki/spaces/MCIDOC/pages/2504491009/Compliance+List-Tags+Command) | compliance | list-tags | compliance | dm-compliance-plugin.jar | \-  | \-  |
| [DSParams Merge Command](/wiki/spaces/MCIDOC/pages/458556064/DSParams+Merge+Command) | dsparams | merge | dsparams | dm-dsadmin-plugin.jar | \-  | \-  |
| [ISX Message-Handlers Command](/wiki/spaces/MCIDOC/pages/412286979/ISX+Message-Handlers+Command) | isx | message-handlers | isx | dm-dsmsgh-plugin.jar | \-  | \-  |
| [Compliance Query Command](/wiki/spaces/MCIDOC/pages/458556115/Compliance+Query+Command) | compliance | query | compliance | dm-compliance-plugin.jar | \-  | \-  |
| [Workbench Set-Branch Command](/wiki/spaces/MCIDOC/pages/2449047553/Workbench+Set-Branch+Command) | workbench | set-branch | workbench | dm-workbench-plugin.jar | IS/DS | \-  |
| [ISX Set-Params Command](/wiki/spaces/MCIDOC/pages/458850355/ISX+Set-Params+Command) | isx | set-params | isx | dm-isxexport-plugin.jar | \-  | \-  |
| [UnitTest Test Command](/wiki/spaces/MCIDOC/pages/718831617/UnitTest+Test+Command) | unittest | test | unittest | dm-dstest-plugin.jar | IS/DS | \-  |
| [Compliance Test Command](/wiki/spaces/MCIDOC/pages/408322069/Compliance+Test+Command) | compliance | test | compliance | dm-compliance-plugin.jar | \-  | \-  |
| [UnitTest Uninstall-Server-Test-Harness Command](/wiki/spaces/MCIDOC/pages/2640281639/UnitTest+Uninstall-Server-Test-Harness+Command) | unittest | uninstall-server-test-harness | unittest | dm-dstest-plugin.jar | IS/DS | \-  |
| [Remote Upload Command](/wiki/spaces/MCIDOC/pages/716603405/Remote+Upload+Command) | remote | upload | remote | dm-bamboo-sftp-plugin.jar | OS  | \-  |

> [!INFO]
> Some command invocations will require credentials. For more on credentials, see [Mettle CI User Accounts](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1109491875/MettleCI+-+User+Accounts).

## Types of credentials

|     |     |
| --- | --- |
| **Code** | **Meaning** |
| IS/DS | This command requires credentials of an IS user that has the DataStage Admin permission and is bound/mapped to a valid DataStage user |
| OS  | This command requires credentials of an Operating System user that has sufficient authority to ssh/scp and to write in the project and other project related directories and invoke scripts. |
| IGC | This command requires credentials of an IGC user (an IS user that has IGC user permissions) |
| JIRA | This command requires credentials of an Atlassian Jira user that has sufficient permission to create, view and delete issues and comments. |
| \-  | This command does not need any credentials |

# Windows-Only Commands

Note from the ‘Windows Client’ column of the command list above that the following MettleCI commands rely on functionality only available on the DataStage Client tier, and as such can only be executed on a Windows-based DataStage Client tier.

| Title | Namespace | Command | Credentials |
| --- | --- | --- | --- |
| [DataStage Compile Command](/wiki/spaces/MCIDOC/pages/410157081/DataStage+Compile+Command) | datastage | compile | IS/DS |
| [DataStage Connector Migration Command](/wiki/spaces/MCIDOC/pages/410681364/DataStage+Connector+Migration+Command) | datastage | ccmt | IS/DS |
| [DataStage Deploy Command](/wiki/spaces/MCIDOC/pages/423952410/DataStage+Deploy+Command) | datastage | deploy | IS/DS |
| [ISX Export Command](/wiki/spaces/MCIDOC/pages/409305099/ISX+Export+Command) | isx | export | IS/DS |
| [ISX Import Command](/wiki/spaces/MCIDOC/pages/409894937/ISX+Import+Command) | isx | import | IS/DS |