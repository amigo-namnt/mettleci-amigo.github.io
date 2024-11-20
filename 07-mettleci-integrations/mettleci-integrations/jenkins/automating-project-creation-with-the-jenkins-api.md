# Automating project creation with the Jenkins API

The MettleCI Jenkins DataStage repository and shared library repository templates require the specification of Jenkins nodes, environment variables, and credentials. Some DataStage organisations have multiple development teams working on multiple DataStage development projects, each of which would typically require a dedicated Git repository associated with a dedicated Jenkins project and all its attendant Jenkins artefacts. Creating all of these artefacts manually for a large number of DataStage delivery streams could be very onerous and error prone. A better solution might be to automate this process using the the [Jenkins Remote Access API](https://www.jenkins.io/doc/book/using/remote-access-api/) which provides calls that can minimise the effort of creating multiple Jenkins projects (“Jobs”), Nodes, and Credentials.

# Guides

*   [Prerequisites](#prerequisites)
*   [Generating the Jenkins Crumb](#generating-the-jenkins-crumb)
*   [Creating a Jenkins Node](#creating-a-jenkins-node)
*   [Creating a Jenkins Pipeline](#creating-a-jenkins-pipeline)
*   [Creating Jenkins Credentials](#creating-jenkins-credentials)

See [Authenticating scripted clients (jenkins.io)](https://www.jenkins.io/doc/book/system-administration/authenticating-scripted-clients/).

# Prerequisites

In order to successfully make calls to the Jenkins REST API you require…

*   a user with permissions to create pipelines, nodes and credentials,
    
*   an access token for that user, and
    
*   a session token, called a 'Jenkins Crumb'.
    

# Generating the Jenkins Crumb

The following request returns the Crumb Request Field and the Crumb itself:

```
$> wget -q --auth-no-challenge \
   --user <JENKINS_USER> --password <ACCESS_TOKEN> \
   --output-document - '<JENKINS_URL>:<JENKINS_PORT>/crumbIssuer/api/xml?xpath=concat(//crumbRequestField,":",//crumb)'
```

The response is in the format `<JENKINS_CRUMB_REQUEST_FIELD>:<JENKINS_CRUMB>`, for example:

```
Jenkins-Crumb:f4a44af38ffc911d34c1c331bf292c9d57c81b3e81761b503bde0a97544a60d8
```

# Creating a Jenkins Node

Jenkins provides a method for the creation of Nodes, including the environment variables required by the MettleCI pipeline and shared library.

#### JSON

```
{
  "name":"<NODE_NAME>",
  "nodeDescription":"<NODE_SESCRIPTION>",
  "numExecutors":"<NUM_EXECUTORS>",
  "remoteFS":"<REMOTE_ROOT_DIRECTORY>",
  "labelString":"<AGENT_LABELS>",
  "mode":"NORMAL",
  "":[
    "hudson.slaves.JNLPLauncher",
    "hudson.slaves.RetentionStrategy$Always"
  ],
  "launcher":{
    "stapler-class":"hudson.slaves.JNLPLauncher",
    "$class":"hudson.slaves.JNLPLauncher",
    "workDirSettings":{
      "disabled":false,
      "workDirPath":"",
      "internalDir":"remoting",
      "failIfWorkDirIsMissing":false
    },
    "webSocket":false,
    "tunnel":"",
    "vmargs":"",
    "oldCommand":""
  },
  "retentionStrategy":{
    "stapler-class":"hudson.slaves.RetentionStrategy$Always",
    "$class":"hudson.slaves.RetentionStrategy$Always"
  },
  "nodeProperties":{
    "stapler-class-bag":"true",
    "hudson-slaves-EnvironmentVariablesNodeProperty":{
      "env":[
        {
          "key":"AGENTMETTLECMD",
          "value":"<AGENT_METTLE_CMD>"
        },
        {
          "key":"AGENTMETTLEHOME",
          "value":"<AGENT_METTLE_HOME>"
        },
        {
          "key":"IISDOMAINNAME",
          "value":"<IIS_DOMAIN_NAME>"
        },
        {
          "key":"IISENGINENAME",
          "value":"<IIS_ENGINE_NAME>"
        },
        {
          "key":"IISUSERNAME",
          "value":"<IIS_USERNAME>"
        },
        {
          "key":"IISPASSWORD",
          "value":"<IIS_PASSWORD_CRED>"
        },
        {
          "key":"IISPROJECTTEMPLATEDIR",
          "value":"<DATASTAGE_PROJECT_TEMPLATE_DIR>"
        },
        {
          "key":"MCIUSERNAME",
          "value":"<MCI_USERNAME>"
        },
        {
          "key":"MCIPASSWORD",
          "value":"<MCI_PASSWORD_CRED>"
        },
        {
          "key":"ENGINEUNITTESTBASEDIR",
          "value":"ENGINE_UNITTEST_BASE_DIR>"
        }
      ]
    }
  },
  "type":"hudson.slaves.DumbSlave",
  "<JENKINS_CRUMB_REQUEST_FIELD>":"<JENKINS_CRUMB>"
}
```

This JSON requires a number of values to be provided:

*   `NODE_NAME`: name of the node
    
*   `NODE_SESCRIPTION`: node description
    
*   `NUM_EXECUTORS`: The number of concurrent tasks the agent related to this node can process
    
*   `REMOTE_ROOT_DIRECTORY`: The path to the agent installation
    
*   `AGENT_LABELS`: the labels that allow Jenkins to pick the appropriate Node/agent to perform specific tasks. For further information, refer to [Jenkins Agent Assignment](../jenkins/jenkins-build-agents/jenkins-agent-assignment.md).
    
*   Environment variables: Refer to [Jenkins Environment Variables](../jenkins/jenkins-environment-variables.md)
    
*   `JENKINS_CRUMB_REQUEST_FIELD`: the name of the Jenkins Crumb Request Field, usually “Jenkins-Crumb”
    
*   `JENKINS_CRUMB`: the value of the Jenkins Crumb.
    

This JSON is passed into the REST API call:

```
$> curl -L -s \
   -o /dev/null \
   -w "%{http_code}" \
   -u <JENKINS_USER>:<ACCESS_TOKEN> \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -H '<JENKINS_CRUMB_REQUEST_FIELD>:<JENKINS_CRUMB>' \
   -X POST \
   -d "json=<JSON_TEXT>" \
   '<JENKINS_URL>:<JENKINS_PORT>/computer/doCreateItem?name=<NODE_NAME>&type=hudson.slaves.DumbSlave'
```

# Creating a Jenkins Pipeline

The process to create a new Jenkins Pipeline requires the input in XML. Here is the XML configuration file for a default MettleCI pipeline:

#### XML

```
<flow-definition plugin="workflow-job@1186.v8def1a_5f3944">
	<actions>
		<org.jenkinsci.plugins.pipeline.modeldefinition.actions.DeclarativeJobAction plugin="pipeline-model-definition@2.2086.v12b_420f036e5"/>
		<org.jenkinsci.plugins.pipeline.modeldefinition.actions.DeclarativeJobPropertyTrackerAction plugin="pipeline-model-definition@2.2086.v12b_420f036e5">
			<jobProperties/>
			<triggers/>
			<parameters/>
			<options/>
		</org.jenkinsci.plugins.pipeline.modeldefinition.actions.DeclarativeJobPropertyTrackerAction>
	</actions>
	<description>PIPELINE_DESCRIPTION</description>
	<keepDependencies>false</keepDependencies>
	<properties>
		<hudson.plugins.jira.JiraProjectProperty plugin="jira@3.7.1"/>
		<org.jenkinsci.plugins.workflow.job.properties.DisableConcurrentBuildsJobProperty>
			<abortPrevious>false</abortPrevious>
		</org.jenkinsci.plugins.workflow.job.properties.DisableConcurrentBuildsJobProperty>
		<org.jenkinsci.plugins.workflow.job.properties.PipelineTriggersJobProperty>
			<triggers>
				<hudson.triggers.SCMTrigger>
					<spec>SCM_POLLING_SCHEDULE</spec>
					<ignorePostCommitHooks>false</ignorePostCommitHooks>
				</hudson.triggers.SCMTrigger>
			</triggers>
		</org.jenkinsci.plugins.workflow.job.properties.PipelineTriggersJobProperty>
	</properties>
	<definition class="org.jenkinsci.plugins.workflow.cps.CpsScmFlowDefinition" plugin="workflow-cps@2725.v7b_c717eb_12ce">
		<scm class="hudson.plugins.git.GitSCM" plugin="git@4.11.3">
			<configVersion>2</configVersion>
			<userRemoteConfigs>
				<hudson.plugins.git.UserRemoteConfig>
					<url>GIT_PROJECT_REPOSITORY_URL</url>
					<credentialsId>GIT_PROJECT_REPOSITORY_CRED</credentialsId>
				</hudson.plugins.git.UserRemoteConfig>
			</userRemoteConfigs>
			<branches>
				<hudson.plugins.git.BranchSpec>
					<name>*/master</name>
				</hudson.plugins.git.BranchSpec>
			</branches>
			<doGenerateSubmoduleConfigurations>false</doGenerateSubmoduleConfigurations>
			<submoduleCfg class="empty-list"/>
			<extensions/>
		</scm>
		<scriptPath>Jenkinsfile</scriptPath>
		<lightweight>true</lightweight>
	</definition>
	<triggers/>
	<disabled>false</disabled>
</flow-definition>
```

Relevant configuration information:

*   `<PIPELINE_NAME>`: Pipeline name. Used in the cURL call, not the XML configuration file
    
*   `PIPELINE_DESCRIPTION`: description for the pipeline
    
*   `SCM_POLLING_SCHEDULE`: sets the schedule for polling the source project repository, in CRON format. Data Migrators recommends using “\* \* \* \* \*”, which equates to polling once per minute.
    
*   `GIT_PROJECT_REPOSITORY_URL`: Source Git repository URL
    
*   `GIT_PROJECT_REPOSITORY_CRED:` Jenkins Credential containing login details for the source Git repository.
    

> [!NOTE]
> Note: The XML configuration file shown above is relevant for the selected options only (Git repository, SCM Polling, Pipeline Script from SCM). If different options are chosen, use the Jenkins GUI to create a template that matches the selected options:
> *   Open the Jenkins Dashboard and click New Item
>     
> *   Enter the name and select ‘Pipeline', then press OK.
>     
> *   Select the required options to suit your environment.
>     
> *   Press Save
>     
> *   Browse to `<JENKINS_URL>:<JENKINS_PORT>/job/<PIPELINE_NAME>/config.xml` and copy the returned XML.

Here is a cURL call to create the new Jenkins Pipeline:

```
$> curl -L -s \
   -o /dev/null -w "%{http_code}" \
   -H "Content-Type:text/xml" \
   -H '<JENKINS_CRUMB_REQUEST_FIELD>:<JENKINS_CRUMB>' \
   -X POST \
   -u '<JENKINS_USER>:<ACCESS_TOKEN>' \
   '<JENKINS_URL>:<JENKINS_PORT>/createItem?name=<PIPELINE_NAME>' \
   --data-binary @NewPipeline.xml
```

# Creating Jenkins Credentials

When setting up the Jenkins Nodes used by the MettleCI pipelines, there are two environment variables for storing passwords:

*   `IISPASSWORD`: the Information Server user password
    
*   `MCIPASSWORD` the MettleCI user password
    

Unlike the other environment variables which contain text, these 2 variables actually store the Id of the Jenkins Credential that contains the password. This means that if we are creating multiple Nodes relating to different Information Server instances, we need to create credentials to match.

#### JSON

```
{
	"": "0",
	"credentials": { 
		"scope": "GLOBAL", 
		"id": "<CREDENTIAL_ID>", 
		"secret": "<PASSWORD>", 
		"description": "<CREDENTIAL_DESCRIPTION>", 
		"$class": "org.jenkinsci.plugins.plaincredentials.impl.StringCredentialsImpl" 
	} 
}
```

`<CREDENTIAL_ID>` for the created credential is the referenced in either `<IIS_PASSWORD_CRED>` or `<MCI_PASSWORD_CRED>` of the Node creation JSON.

The cURL call to make is

```
$> curl -L -s \
   -o /dev/null -w "%{http_code}" \
   -u <JENKINS_USER>:<ACCESS_TOKEN> \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -H '<JENKINS_CRUMB_REQUEST_FIELD>:<JENKINS_CRUMB>' \
   -X POST \
   -d "json=<JSON_TEXT>" \
   '<JENKINS_URL>:<JENKINS_PORT>credentials/store/system/domain/_/createCredentials'
```