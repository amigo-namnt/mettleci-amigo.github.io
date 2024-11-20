# Remote Execute Command

# Purpose

Execute a specified script on a target host.

> [!WARNING]
> Note that the `-privateKey` parameter is the name of a private key file accessible your `mettleci remote execute` command. If used as part of a CI/CD pipeline then the build agent process running the command will need access to the specified private key file.

# Syntax

See the examples below.

(function(){ var data = { "addon\_key":"render-Markdown", "uniqueKey":"render-Markdown\_\_markdown4370102241523933112", "key":"markdown", "moduleType":"dynamicContentMacros", "moduleLocation":"content", "cp":"/wiki", "general":"", "w":"", "h":"", "url":"https://d27i9fmzbobp10.cloudfront.net/render-markdown.html?pageId=864944158&pageVersion=187&macroHash=c340c437-ed62-44ca-85eb-6a5ffd94ea24&macroId=c340c437-ed62-44ca-85eb-6a5ffd94ea24&outputType=email&highlightStyle=&highlight=&xdm\_e=https%3A%2F%2Fdatamigrators.atlassian.net&xdm\_c=channel-render-Markdown\_\_markdown4370102241523933112&cp=%2Fwiki&xdm\_deprecated\_addon\_key\_do\_not\_use=render-Markdown&lic=none&cv=1000.0.0-f660f55a6ec0", "structuredContext": "{\\"confluence\\":{\\"macro\\":{\\"outputType\\":\\"email\\",\\"hash\\":\\"c340c437-ed62-44ca-85eb-6a5ffd94ea24\\",\\"id\\":\\"c340c437-ed62-44ca-85eb-6a5ffd94ea24\\"},\\"content\\":{\\"type\\":\\"page\\",\\"version\\":\\"187\\",\\"id\\":\\"864944158\\"},\\"space\\":{\\"key\\":\\"MCIDOC\\",\\"id\\":\\"264011780\\"}},\\"url\\":{\\"displayUrl\\":\\"https://datamigrators.atlassian.net/wiki\\"}}", "contentClassifier":"content", "productCtx":"{\\"page.id\\":\\"864944158\\",\\"macro.hash\\":\\"c340c437-ed62-44ca-85eb-6a5ffd94ea24\\",\\"space.key\\":\\"MCIDOC\\",\\"page.type\\":\\"page\\",\\"content.version\\":\\"187\\",\\"page.title\\":\\"remote execute command syntax\\",\\"macro.localId\\":\\"\\",\\"macro.body\\":\\"### Syntax : remote execute \[options\]\\\\n### Description\\\\n\\\\n\* \*\*-script\*\*\\\\n\\\\n Local script to execute on remote server\\\\n\\\\n \*Required\*\\\\n\*\\",\\": = | RAW | = :\\":null,\\"space.id\\":\\"264011780\\",\\"macro.truncated\\":\\"true\\",\\"content.type\\":\\"page\\",\\"output.type\\":\\"email\\",\\"page.version\\":\\"187\\",\\"macro.fragmentLocalId\\":\\"\\",\\"content.id\\":\\"864944158\\",\\"macro.id\\":\\"c340c437-ed62-44ca-85eb-6a5ffd94ea24\\"}", "timeZone":"UTC", "origin":"https://d27i9fmzbobp10.cloudfront.net", "hostOrigin":"https://datamigrators.atlassian.net", "sandbox":"allow-downloads allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-scripts allow-same-origin allow-top-navigation-by-user-activation allow-storage-access-by-user-activation", "apiMigrations": { "gdpr": true } } ; if(window.AP && window.AP.subCreate) { window.\_AP.appendConnectAddon(data); } else { require(\['ac/create'\], function(create){ create.appendConnectAddon(data); }); } // For Confluence App Analytics. This code works in conjunction with CFE's ConnectSupport.js. // Here, we add a listener to the initial HTML page that stores events if the ConnectSupport component // has not mounted yet. In CFE, we process the missed event data and disable this initial listener. const \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_ = 20; const connectAppAnalytics = "ecosystem.confluence.connect.analytics"; window.connectHost && window.connectHost.onIframeEstablished((eventData) => { if (!window.\_\_CONFLUENCE\_CONNECT\_SUPPORT\_LOADED\_\_) { let events = JSON.parse(window.localStorage.getItem(connectAppAnalytics)) || \[\]; if (events.length >= \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_) { events.shift(); } events.push(eventData); window.localStorage.setItem(connectAppAnalytics, JSON.stringify(events)); } }); }());

# Examples

```
$> mettleci remote execute \
   -host my-engine.my-org.com \
   -username myusername \
   -password mypassword \
   -script "config/deploy.sh"
MettleCI Command Line (build 128)
(C) 2018-2022 Data Migrators Pty Ltd
Connecting to my-engine.my-org.com on port 22

Status code = 0 
exit code = 0
$>
```

# See Also

*   Page:
    
    [MettleCI CLI produces error 'Incorrectly typed data found for annotation element'](/wiki/spaces/MCIDOC/pages/2524413953/MettleCI+CLI+produces+error+Incorrectly+typed+data+found+for+annotation+element)
    
*   Page:
    
    [MettleCI command 'workbench set-branch' command produces a credentials error](/wiki/spaces/MCIDOC/pages/2501476353/MettleCI+command+workbench+set-branch+command+produces+a+credentials+error)
    
*   Page:
    
    [SSH Configuration](/wiki/spaces/MCIDOC/pages/2396487711/SSH+Configuration)
    
*   Page:
    
    [MettleCI CLI produces 'Failed to connect to host' error](/wiki/spaces/MCIDOC/pages/2396487681/MettleCI+CLI+produces+Failed+to+connect+to+host+error)
    
*   Page:
    
    [Build Pipeline SFTP operations fail due to DataStage Engine name](/wiki/spaces/MCIDOC/pages/2169307137/Build+Pipeline+SFTP+operations+fail+due+to+DataStage+Engine+name)