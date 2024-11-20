# UnitTest Uninstall-Server-Test-Harness Command

## Purpose

Uninstall the Server unit testing components for a specific DataStage project.

# Syntax

(function(){ var data = { "addon\_key":"render-Markdown", "uniqueKey":"render-Markdown\_\_markdown6392502158318722335", "key":"markdown", "moduleType":"dynamicContentMacros", "moduleLocation":"content", "cp":"/wiki", "general":"", "w":"", "h":"", "url":"https://d27i9fmzbobp10.cloudfront.net/render-markdown.html?pageId=2640314409&pageVersion=22&macroHash=921b03ea-f40b-4564-a69f-bf6f47652ced&macroId=921b03ea-f40b-4564-a69f-bf6f47652ced&outputType=email&highlightStyle=&highlight=&xdm\_e=https%3A%2F%2Fdatamigrators.atlassian.net&xdm\_c=channel-render-Markdown\_\_markdown6392502158318722335&cp=%2Fwiki&xdm\_deprecated\_addon\_key\_do\_not\_use=render-Markdown&lic=none&cv=1000.0.0-f660f55a6ec0", "structuredContext": "{\\"confluence\\":{\\"editor\\":{\\"version\\":\\"\\\\\\"v2\\\\\\"\\"},\\"macro\\":{\\"outputType\\":\\"email\\",\\"hash\\":\\"921b03ea-f40b-4564-a69f-bf6f47652ced\\",\\"id\\":\\"921b03ea-f40b-4564-a69f-bf6f47652ced\\"},\\"content\\":{\\"type\\":\\"page\\",\\"version\\":\\"22\\",\\"id\\":\\"2640314409\\"},\\"space\\":{\\"key\\":\\"MCIDOC\\",\\"id\\":\\"264011780\\"}},\\"url\\":{\\"displayUrl\\":\\"https://datamigrators.atlassian.net/wiki\\"}}", "contentClassifier":"content", "productCtx":"{\\"page.id\\":\\"2640314409\\",\\"macro.hash\\":\\"921b03ea-f40b-4564-a69f-bf6f47652ced\\",\\"space.key\\":\\"MCIDOC\\",\\"page.type\\":\\"page\\",\\"content.version\\":\\"22\\",\\"page.title\\":\\"unittest uninstall-server-test-harness command syntax\\",\\"macro.localId\\":\\"\\",\\"macro.body\\":\\"### Syntax : unittest uninstall-server-test-harness \[options\]\\\\n### Description\\\\n\\\\n\* \*\*-domain\*\*\\\\n\\\\n Services Tier (including port)\\\\n\\\\n\\",\\": = | RAW | = :\\":null,\\"space.id\\":\\"264011780\\",\\"macro.truncated\\":\\"true\\",\\"content.type\\":\\"page\\",\\"output.type\\":\\"email\\",\\"page.version\\":\\"22\\",\\"macro.fragmentLocalId\\":\\"\\",\\"content.id\\":\\"2640314409\\",\\"macro.id\\":\\"921b03ea-f40b-4564-a69f-bf6f47652ced\\",\\"editor.version\\":\\"\\\\\\"v2\\\\\\"\\"}", "timeZone":"UTC", "origin":"https://d27i9fmzbobp10.cloudfront.net", "hostOrigin":"https://datamigrators.atlassian.net", "sandbox":"allow-downloads allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-scripts allow-same-origin allow-top-navigation-by-user-activation allow-storage-access-by-user-activation", "apiMigrations": { "gdpr": true } } ; if(window.AP && window.AP.subCreate) { window.\_AP.appendConnectAddon(data); } else { require(\['ac/create'\], function(create){ create.appendConnectAddon(data); }); } // For Confluence App Analytics. This code works in conjunction with CFE's ConnectSupport.js. // Here, we add a listener to the initial HTML page that stores events if the ConnectSupport component // has not mounted yet. In CFE, we process the missed event data and disable this initial listener. const \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_ = 20; const connectAppAnalytics = "ecosystem.confluence.connect.analytics"; window.connectHost && window.connectHost.onIframeEstablished((eventData) => { if (!window.\_\_CONFLUENCE\_CONNECT\_SUPPORT\_LOADED\_\_) { let events = JSON.parse(window.localStorage.getItem(connectAppAnalytics)) || \[\]; if (events.length >= \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_) { events.shift(); } events.push(eventData); window.localStorage.setItem(connectAppAnalytics, JSON.stringify(events)); } }); }());

> [!WARNING]
> NOTE: The username argument expects an Engine tier OS (Information Server) user, not a DataStage user. e.g: `dsadm`.

## Example

```
C:\> mettleci unittest uninstall-server-test-harness ^
  -domain services.datamigrators.io:9443 ^
  -server engine.datamigrators.io ^
  -project dstage1 ^
  -username isadmin ^
  -password password
  
MettleCI Command Line (build 199)
(C) 2018-2022 Data Migrators Pty Ltd
Changing 'Command' logger level from INFO to INFO
Changing 'Shell' logger level from INFO to DEBUG
unittest uninstall-server-test-harness (v1.0-SNAPSHOT)
Decataloging program 'DSD.RUN'
Cataloging routine 'DSD_RUN.B' as 'DSD.RUN'
Decataloging program 'DSU.ExtractArgs'
Decataloging program 'DSD.RUN_ORIG'
Deleting routine 'DSU.ExtractArgs'
Deleting routine 'DSU.STUB'
Uninstall complete.
C:\>
```