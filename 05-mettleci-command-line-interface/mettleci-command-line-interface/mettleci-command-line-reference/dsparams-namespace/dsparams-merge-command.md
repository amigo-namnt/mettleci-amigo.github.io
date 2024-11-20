# DSParams Merge Command

# Purpose

Creates a new DSParams file from an existing DSParams file and merging it with the provided diff file.

# Syntax

![](./attachments/image-20220816-095731.png)

(function(){ var data = { "addon\_key":"render-Markdown", "uniqueKey":"render-Markdown\_\_markdown8119755905155201385", "key":"markdown", "moduleType":"dynamicContentMacros", "moduleLocation":"content", "cp":"/wiki", "general":"", "w":"", "h":"", "url":"https://d27i9fmzbobp10.cloudfront.net/render-markdown.html?pageId=864845839&pageVersion=184&macroHash=5d0df640-54b0-40c5-b91d-48802802faed&macroId=5d0df640-54b0-40c5-b91d-48802802faed&outputType=email&highlightStyle=&highlight=&xdm\_e=https%3A%2F%2Fdatamigrators.atlassian.net&xdm\_c=channel-render-Markdown\_\_markdown8119755905155201385&cp=%2Fwiki&xdm\_deprecated\_addon\_key\_do\_not\_use=render-Markdown&lic=none&cv=1000.0.0-f660f55a6ec0", "structuredContext": "{\\"confluence\\":{\\"macro\\":{\\"outputType\\":\\"email\\",\\"hash\\":\\"5d0df640-54b0-40c5-b91d-48802802faed\\",\\"id\\":\\"5d0df640-54b0-40c5-b91d-48802802faed\\"},\\"content\\":{\\"type\\":\\"page\\",\\"version\\":\\"184\\",\\"id\\":\\"864845839\\"},\\"space\\":{\\"key\\":\\"MCIDOC\\",\\"id\\":\\"264011780\\"}},\\"url\\":{\\"displayUrl\\":\\"https://datamigrators.atlassian.net/wiki\\"}}", "contentClassifier":"content", "productCtx":"{\\"page.id\\":\\"864845839\\",\\"macro.hash\\":\\"5d0df640-54b0-40c5-b91d-48802802faed\\",\\"space.key\\":\\"MCIDOC\\",\\"page.type\\":\\"page\\",\\"content.version\\":\\"184\\",\\"page.title\\":\\"dsparams merge command syntax\\",\\"macro.localId\\":\\"\\",\\"macro.body\\":\\"### Syntax : dsparams merge \[options\]\\\\n### Description\\\\n\\\\n\* \*\*-before\*\*\\\\n\\\\n input DSParams - the \\\\\\"before\\\\\\" state\\\\n\\\\n \*Required\*\\\\n\* \*\*-d\\",\\": = | RAW | = :\\":null,\\"space.id\\":\\"264011780\\",\\"macro.truncated\\":\\"true\\",\\"content.type\\":\\"page\\",\\"output.type\\":\\"email\\",\\"page.version\\":\\"184\\",\\"macro.fragmentLocalId\\":\\"\\",\\"content.id\\":\\"864845839\\",\\"macro.id\\":\\"5d0df640-54b0-40c5-b91d-48802802faed\\"}", "timeZone":"UTC", "origin":"https://d27i9fmzbobp10.cloudfront.net", "hostOrigin":"https://datamigrators.atlassian.net", "sandbox":"allow-downloads allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-scripts allow-same-origin allow-top-navigation-by-user-activation allow-storage-access-by-user-activation", "apiMigrations": { "gdpr": true } } ; if(window.AP && window.AP.subCreate) { window.\_AP.appendConnectAddon(data); } else { require(\['ac/create'\], function(create){ create.appendConnectAddon(data); }); } // For Confluence App Analytics. This code works in conjunction with CFE's ConnectSupport.js. // Here, we add a listener to the initial HTML page that stores events if the ConnectSupport component // has not mounted yet. In CFE, we process the missed event data and disable this initial listener. const \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_ = 20; const connectAppAnalytics = "ecosystem.confluence.connect.analytics"; window.connectHost && window.connectHost.onIframeEstablished((eventData) => { if (!window.\_\_CONFLUENCE\_CONNECT\_SUPPORT\_LOADED\_\_) { let events = JSON.parse(window.localStorage.getItem(connectAppAnalytics)) || \[\]; if (events.length >= \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_) { events.shift(); } events.push(eventData); window.localStorage.setItem(connectAppAnalytics, JSON.stringify(events)); } }); }());

# Example

```
$> mettleci dsparams merge \
   -before .\DSParams \
   -diff .\DSParams_diff \
   -after .\DSParams_new 
   
MettleCI Command Line (build ${buildNumber})
(C) 2018-2020 Data Migrators Pty Ltd
Merging differences from .\DSParams_diff (-diff) into .\DSParams (-before), to create .\DSParams_new (-after)
Comparing section PROJECT...
Section present in -before. Adding entries...
JobAdminEnabled=0
…
Differences added
Comparing section EnvVarValues...
Section not present in -before. Adding entire section.
Merge complete. Writing merged DSParams to .\DSParams_new (-after)
```