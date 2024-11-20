# Remote Download Command

# Purpose

This command transfers files from a target host to the host where the command is being executed. This is typically used to download files from a DataStage Engine to a [MettleCI Agent Host](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1770520622/A+Summary+of+MettleCI+Components#MettleCI-Agent-Host) as part of a MettleCI-enabled build pipeline. This command…

*   uses the [SFTP protocol](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol),
    
*   authenticates using either a username/password or SSH Private Key, and
    
*   uses [ANT File Patterns](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/2310307841/Ant+File+Patterns)
    

Note that all directories matched by transfer patterns are created in the `-destination` folder.

> [!WARNING]
> Note that the `-privateKey` parameter is the name of a private key file accessible your `mettleci remote execute` command. If used as part of a CI/CD pipeline then the build agent process running the command will need access to the specified private key file.

# Syntax

See the examples below.

(function(){ var data = { "addon\_key":"render-Markdown", "uniqueKey":"render-Markdown\_\_markdown6198361741114129611", "key":"markdown", "moduleType":"dynamicContentMacros", "moduleLocation":"content", "cp":"/wiki", "general":"", "w":"", "h":"", "url":"https://d27i9fmzbobp10.cloudfront.net/render-markdown.html?pageId=864976933&pageVersion=187&macroHash=b2e4f7ac-2747-4d7e-8520-95c8dcf9de97&macroId=b2e4f7ac-2747-4d7e-8520-95c8dcf9de97&outputType=email&highlightStyle=&highlight=&xdm\_e=https%3A%2F%2Fdatamigrators.atlassian.net&xdm\_c=channel-render-Markdown\_\_markdown6198361741114129611&cp=%2Fwiki&xdm\_deprecated\_addon\_key\_do\_not\_use=render-Markdown&lic=none&cv=1000.0.0-f660f55a6ec0", "structuredContext": "{\\"confluence\\":{\\"macro\\":{\\"outputType\\":\\"email\\",\\"hash\\":\\"b2e4f7ac-2747-4d7e-8520-95c8dcf9de97\\",\\"id\\":\\"b2e4f7ac-2747-4d7e-8520-95c8dcf9de97\\"},\\"content\\":{\\"type\\":\\"page\\",\\"version\\":\\"187\\",\\"id\\":\\"864976933\\"},\\"space\\":{\\"key\\":\\"MCIDOC\\",\\"id\\":\\"264011780\\"}},\\"url\\":{\\"displayUrl\\":\\"https://datamigrators.atlassian.net/wiki\\"}}", "contentClassifier":"content", "productCtx":"{\\"page.id\\":\\"864976933\\",\\"macro.hash\\":\\"b2e4f7ac-2747-4d7e-8520-95c8dcf9de97\\",\\"space.key\\":\\"MCIDOC\\",\\"page.type\\":\\"page\\",\\"content.version\\":\\"187\\",\\"page.title\\":\\"remote download command syntax\\",\\"macro.localId\\":\\"\\",\\"macro.body\\":\\"### Syntax : remote download \[options\]\\\\n### Description\\\\n\\\\n\* \*\*-source\*\*\\\\n\\\\n Directory to be transferred from\\\\n\\\\n \*Required\*\\\\n\* \*\*-des\\",\\": = | RAW | = :\\":null,\\"space.id\\":\\"264011780\\",\\"macro.truncated\\":\\"true\\",\\"content.type\\":\\"page\\",\\"output.type\\":\\"email\\",\\"page.version\\":\\"187\\",\\"macro.fragmentLocalId\\":\\"\\",\\"content.id\\":\\"864976933\\",\\"macro.id\\":\\"b2e4f7ac-2747-4d7e-8520-95c8dcf9de97\\"}", "timeZone":"UTC", "origin":"https://d27i9fmzbobp10.cloudfront.net", "hostOrigin":"https://datamigrators.atlassian.net", "sandbox":"allow-downloads allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-scripts allow-same-origin allow-top-navigation-by-user-activation allow-storage-access-by-user-activation", "apiMigrations": { "gdpr": true } } ; if(window.AP && window.AP.subCreate) { window.\_AP.appendConnectAddon(data); } else { require(\['ac/create'\], function(create){ create.appendConnectAddon(data); }); } // For Confluence App Analytics. This code works in conjunction with CFE's ConnectSupport.js. // Here, we add a listener to the initial HTML page that stores events if the ConnectSupport component // has not mounted yet. In CFE, we process the missed event data and disable this initial listener. const \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_ = 20; const connectAppAnalytics = "ecosystem.confluence.connect.analytics"; window.connectHost && window.connectHost.onIframeEstablished((eventData) => { if (!window.\_\_CONFLUENCE\_CONNECT\_SUPPORT\_LOADED\_\_) { let events = JSON.parse(window.localStorage.getItem(connectAppAnalytics)) || \[\]; if (events.length >= \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_) { events.shift(); } events.push(eventData); window.localStorage.setItem(connectAppAnalytics, JSON.stringify(events)); } }); }());

# Examples

```
$> mettleci remote download \
    -host my-engine.my-org.com \
    -username mci-user \ 
    -privateKey ~/.ssh/MyPrivateKey.pem \
    -source /source-dir \
    -destination /target-dir \ 
    -transferPattern DSParams

MettleCI Command Line (build 128)
(C) 2018-2022 Data Migrators Pty Ltd
Connecting to my-engine.my-org.com on port 22
Downloading 'DSParams' from remote directory '/source-dir' to local directory '/target-dir':
  DSParams - SUCCESS
Done. 1 file transferred.
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