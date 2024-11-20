# UnitTest Test Command

# Purpose

Run one or more MettleCI Unit Tests against one or more DataStage jobs.

The `-reports` option is used to specify the directory into which the JUnit XML files produced by this command will be placed. Each job tested will produce a separate XML file named after the Job (e.g. Job `MY_JOB_ABC` will produce a JUnit file named `MY_JOB_ABC.xml`)

The `-ignore-test-failures` option will prevent a failing Unit Test from being interpreted as a command failure by your build system, and consequently halting your CI/CD pipeline.

See [Repeatable DataStage Project Deployments](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1266843717/Repeatable+DataStage+Project+Deployments) for more details on how the `-project-cache` parameter is used to implement **incremental tests**. For more information on using the `-project-cache` parameter see our [detailed explanation](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/1356890161/MettleCI+CLI+and+the+project-cache+directory).

# Syntax

(function(){ var data = { "addon\_key":"render-Markdown", "uniqueKey":"render-Markdown\_\_markdown4002247216311731142", "key":"markdown", "moduleType":"dynamicContentMacros", "moduleLocation":"content", "cp":"/wiki", "general":"", "w":"", "h":"", "url":"https://d27i9fmzbobp10.cloudfront.net/render-markdown.html?pageId=864845852&pageVersion=186&macroHash=4b74998e-fe34-480d-ac85-fe6fe2f70507&macroId=4b74998e-fe34-480d-ac85-fe6fe2f70507&outputType=email&highlightStyle=&highlight=&xdm\_e=https%3A%2F%2Fdatamigrators.atlassian.net&xdm\_c=channel-render-Markdown\_\_markdown4002247216311731142&cp=%2Fwiki&xdm\_deprecated\_addon\_key\_do\_not\_use=render-Markdown&lic=none&cv=1000.0.0-f660f55a6ec0", "structuredContext": "{\\"confluence\\":{\\"macro\\":{\\"outputType\\":\\"email\\",\\"hash\\":\\"4b74998e-fe34-480d-ac85-fe6fe2f70507\\",\\"id\\":\\"4b74998e-fe34-480d-ac85-fe6fe2f70507\\"},\\"content\\":{\\"type\\":\\"page\\",\\"version\\":\\"186\\",\\"id\\":\\"864845852\\"},\\"space\\":{\\"key\\":\\"MCIDOC\\",\\"id\\":\\"264011780\\"}},\\"url\\":{\\"displayUrl\\":\\"https://datamigrators.atlassian.net/wiki\\"}}", "contentClassifier":"content", "productCtx":"{\\"page.id\\":\\"864845852\\",\\"macro.hash\\":\\"4b74998e-fe34-480d-ac85-fe6fe2f70507\\",\\"space.key\\":\\"MCIDOC\\",\\"page.type\\":\\"page\\",\\"content.version\\":\\"186\\",\\"page.title\\":\\"unittest test command syntax\\",\\"macro.localId\\":\\"\\",\\"macro.body\\":\\"### Syntax : unittest test \[options\]\\\\n### Description\\\\n\\\\n\* \*\*-domain\*\*\\\\n\\\\n Services Tier\\\\n\\\\n \*Required\*\\\\n\* \*\*-server\*\*\\\\n\\\\n Engine Tier\\\\n\\",\\": = | RAW | = :\\":null,\\"space.id\\":\\"264011780\\",\\"macro.truncated\\":\\"true\\",\\"content.type\\":\\"page\\",\\"output.type\\":\\"email\\",\\"page.version\\":\\"186\\",\\"macro.fragmentLocalId\\":\\"\\",\\"content.id\\":\\"864845852\\",\\"macro.id\\":\\"4b74998e-fe34-480d-ac85-fe6fe2f70507\\"}", "timeZone":"UTC", "origin":"https://d27i9fmzbobp10.cloudfront.net", "hostOrigin":"https://datamigrators.atlassian.net", "sandbox":"allow-downloads allow-forms allow-modals allow-popups allow-popups-to-escape-sandbox allow-scripts allow-same-origin allow-top-navigation-by-user-activation allow-storage-access-by-user-activation", "apiMigrations": { "gdpr": true } } ; if(window.AP && window.AP.subCreate) { window.\_AP.appendConnectAddon(data); } else { require(\['ac/create'\], function(create){ create.appendConnectAddon(data); }); } // For Confluence App Analytics. This code works in conjunction with CFE's ConnectSupport.js. // Here, we add a listener to the initial HTML page that stores events if the ConnectSupport component // has not mounted yet. In CFE, we process the missed event data and disable this initial listener. const \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_ = 20; const connectAppAnalytics = "ecosystem.confluence.connect.analytics"; window.connectHost && window.connectHost.onIframeEstablished((eventData) => { if (!window.\_\_CONFLUENCE\_CONNECT\_SUPPORT\_LOADED\_\_) { let events = JSON.parse(window.localStorage.getItem(connectAppAnalytics)) || \[\]; if (events.length >= \_\_MAX\_EVENT\_ARRAY\_SIZE\_\_) { events.shift(); } events.push(eventData); window.localStorage.setItem(connectAppAnalytics, JSON.stringify(events)); } }); }());

# Example

```
C:\> mettleci unittest test ^
    -domain test1-svcs.datamigrators.io:59445 ^
    -server test1-engn.datamigrators.io ^
    -username isadmin ^
    -password my_password ^
    -project my_project ^
    -specs unittest ^
    -reports unittest_reports ^
    -project-cache "C:\MettleCI\cache\test1-engn.datamigrators.io\my_project"
MettleCI Command Line (build 128)
(C) 2018-2022 Data Migrators Pty Ltd
Loading Unit Test Specifications from 'unittest'
Reading test1-engn.datamigrators.io/my_project
Attempting to identify changes with 1 working threads.
Inspecting DataStage assets for changes...
 * Check test1-engn.datamigrators.io/my_project/Jobs/Transform/TR_ORDERS.pjb - COMPLETED
Change identification complete
Executing Tests with 4 concurrent jobs...
 * Test TR_ORDERS/TR_ORDERS - SKIPPED
Updating incremental state...
Attempting to identify last change with 1 working threads.
Inspecting DataStage assets for last change...
 * Check test1-engn.datamigrators.io/my_project/Jobs/Transform/TR_ORDERS.pjb - COMPLETED
Last change identification complete
Test execution completed successfully.

C:\>
```