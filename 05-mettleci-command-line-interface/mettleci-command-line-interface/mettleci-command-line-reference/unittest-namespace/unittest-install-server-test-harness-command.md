# UnitTest Install-Server-Test-Harness Command

# Purpose

Install the components required to enable unit testing of Server Jobs for a specific DataStage project.

# Syntax

(function(){ var data = { "addon\_key":"render-Markdown", "uniqueKey":"render-Markdown\_\_markdown6954921724788086155", "key":"markdown", "moduleType":"dynamicContentMacros", "moduleLocation":"content", "cp":"/wiki", "general":"", "w":"", "h":"", "url":"https://d27i9fmzbobp10.cloudfront.net/render-markdown.html?pageId=2640707592&pageVersion=22&macroHash=f536b154-762c-4669-8188-5904df94f380&macroId=f536b154-762c-4669-8188-5904df94f380&outputType=email&highlightStyle=&highlight=&xdm\_e=https%3A%2F%2Fdatamigrators.atlassian.net&xdm\_c=channel-render-Markdown\_\_markdown6954921724788086155&cp=%2Fwiki&xdm\_deprecated\_addon\_key\_do\_not\_use=render-Markdown&lic=none&cv=1000.0.0-f660f55a6ec0", "structuredContext": "{\\"confluence\\":{\\"editor\\":{\\"version\\":\\"\\\\\\"v2\\\\\\"\\"},\\"macro\\":{\\"outputType\\":\\"email\\",\\"hash\\":\\"f536b154-762c-4669-8188-5904df94f380\\",\\"id\\":\\"f536b154-762c-4669-8188-5904df94f380\\"},\\"content\\":{\\"type\\":\\"page\\",\\"version\\":\\"22\\",\\"id\\":\\"2640707592\\"},\\"space\\":{\\"key\\":\\"MCIDOC\\",\\"id\\":\\"264011780\\"}},\\"url\\":{\\"displayUrl\\":\\"https://datamigrators.atlassian.net/wiki\\"}}", "contentClassifier":"content", "productCtx":"{\\"page.id\\":\\"2640707592\\",\\"macro.hash\\":\\"f536b154-762c-4669-8188-5904df94f380\\",\\"space.key\\":\\"MCIDOC\\",\\"page.type\\":\\"page\\",\\"content.version\\":\\"22\\",\\"page.title\\":\\"unittest install-server-test-harness command syntax\\",\\"macro.localId\\":\\"\\",\\"macro.body\\":\\"### Syntax : unittest install-server-test-harness \[options\]\\\\n### Description\\\\n\\\\n\* \*\*-server\*\*\\\\n\\\\n Engine Tier\\\\n\\\\n \*Required\*\\\\n\* \*\*-pro\\",\\": = | RAW | = :\\":null,\\"space.id\\":\\"264011780\\",\\"macro.truncated\\":\\"true\\",\\"content.type\\":\\"page\\",\\"output.type\\":\\"email\\",\\"page.version\\":\\"22\\",\\"macro.fragmentLocalId\\":\\"\\",\\"content.id\\":\\"2640707592\\",\\"macro.id\\":\\"f536b154-762c-4669-8188-5904df94f380\\",\\"editor.version\\":\\"\\\\\\"v2\\\\\\"\\"}", "timeZone":"UTC", "origin":"https://d27i9fmzbobp10.cloudfront.net", "hostOrigin":"https://datamigrators.atlassian.net", "sandbox":"allow-downloads allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-scripts allow-same-origin allow-top-navigation-by-user-activation allow-storage-access-by-user-activation", "apiMigrations": { "gdpr": true } } ; if(window.AP && window.AP.subCreate) { window.\_AP.appendConnectAddon(data); } else { require(\['ac/create'\], function(create){ create.appendConnectAddon(data); }); } // For Confluence App Analytics. This code works in conjunction with CFE's ConnectSupport.js. // Here, we add a listener to the initial HTML page that stores events if the ConnectSupport component // has not mounted yet. In CFE, we process the missed event data and disable this initial listener. const \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_ = 20; const connectAppAnalytics = "ecosystem.confluence.connect.analytics"; window.connectHost && window.connectHost.onIframeEstablished((eventData) => { if (!window.\_\_CONFLUENCE\_CONNECT\_SUPPORT\_LOADED\_\_) { let events = JSON.parse(window.localStorage.getItem(connectAppAnalytics)) || \[\]; if (events.length >= \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_) { events.shift(); } events.push(eventData); window.localStorage.setItem(connectAppAnalytics, JSON.stringify(events)); } }); }());

> [!WARNING]
> MettleCI CLI version 1.1-218 or above is needed in order to use this command

## Example

```
C:\> mettleci unittest install-server-test-harness ^
  -domain my-svcs.datamigrators.io:9443 ^
  -server my-engn.datamigrators.io ^
  -project dstage1 ^
  -username isadmin ^
  -password mypassword ^
  -trust

MettleCI Command Line (build 218)
(C) 2018-2022 Data Migrators Pty Ltd
Changing 'Command' logger level from INFO to INFO
Changing 'Shell' logger level from INFO to DEBUG
unittest install-server-test-harness (v1.0-536)
Writing and Compiling routine 'DSU.ExtractArgs'
Writing and Compiling routine 'DSU.STUB'
Cataloging routine 'DSU.ExtractArgs' as 'DSU.ExtractArgs'
Cataloging routine 'DSD_RUN.B' as 'DSD.RUN_ORIG'
Cataloging routine 'DSU.STUB' as 'DSD.RUN'
Server Unit Test Harness installed.
DSStageTypeUpdater ran successfully.


```