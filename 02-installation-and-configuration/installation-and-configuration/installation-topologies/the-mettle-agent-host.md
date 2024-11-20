# The Mettle Agent Host

![](./attachments/MettleCI%20Agent%20Host%20Explainer.png)

The MettleCI Agent Host is a dedicated Microsoft Windows host which is used to run three major components:

*   A [DataStage Client tier](https://www.ibm.com/docs/en/iis/11.7?topic=components-client-tier),
    
*   A [MettleCI Command Line Interface](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2216886273/MettleCI+Command+Line+Interface), and
    
*   A CI/CD agent/runner for your chosen CI/CD build platform (e.g. [Jenkins Agent](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2246770695/Jenkins+Build+Agents), Azure Agent, Bamboo Agent, GitLab Runner, GitHub Runner, etc.)
    

The MettleCI Agent Host operating system **must** be Microsoft Windows because the compilation of traditional (i.e., non-Cloud Pak) DataStage jobs can only be performed by tools available within the DataStage client. IBM only supplies these DataStage client tools for Windows.