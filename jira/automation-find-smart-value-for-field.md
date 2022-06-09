# Automation: Find smart value for a field

Jira uses smart values to access and manipulate Jira data. Here's how to inspect an actual issue and see its data structure with **all** of the fields.

Simply visit the following URL to see a JSON representation of your issue:

`https://<yourinstanceurl>/rest/api/2/issue/<issuekey>?expand=names`

Smart Fields in Jira use the following syntax: `{{smartField}}`.

> To test what a smart value returns, use the Manual trigger with Log action. The result displays in the audit log.

## Source

* Jira Docs: [Find the smart Value for a field](https://support.atlassian.com/cloud-automation/docs/find-the-smart-value-for-a-field/)
