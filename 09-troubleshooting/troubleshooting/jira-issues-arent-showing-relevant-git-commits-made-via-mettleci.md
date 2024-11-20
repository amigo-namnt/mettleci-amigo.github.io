# Jira issues aren't showing relevant Git commits made via MettleCI

# Problem

Git commits made by MettleCI are linked to one or more issues/stories in a work item management system.  In some cases, those links don't appear in Atlassian Jira items.

# Solution

There are a couple of potential fixes for this issue:

## Enable Smart Commits

One cause of this symptom be that Smart Commits had not been enabled in Jira. This will manifest as a Jira item that has recorded the checkin and subsequent build entries, but does not show the commit message as a comment against the Jira item. See the Atlassian [Enable Smart Commits](https://confluence.atlassian.com/adminjiracloud/enable-smart-commits-776830276.html) page for details on how to verify that smart commits are enabled.

Note: Even with Smart Commits enabled, if the email address against the commit cannot be matched to a Jira user, then the comment will still not be attached to the Jira item. There will be no indication of the error unless debug logging is enabled in Jira. See the Atlassian [Troubleshooting Smart Commit](https://confluence.atlassian.com/bitbucketserverkb/troubleshooting-smart-commit-860033511.html) page for further information on this and other potential Smart Commit issues.

## Jira Project Permissions

JIRA has a 'View Development Tools' project permission that needs to be granted. If that permission has not been granted, commit messages will still show on the Issue as comments, but commits and deployments won't be shown against the issue.  It's described on the Atlassian [Integrating with development tools](https://confluence.atlassian.com/adminjiraserver073/integrating-with-development-tools-867028207.html) page.

The View Permission section lists the user groups that can see the Development panel in a JIRA Software issue. The Development panel displays the Create Branch link and summary information for your development process, such as the number and status of the related commits, pull requests, reviews and builds. The visibility of the panel is controlled by the "View Development Tools" project permission.