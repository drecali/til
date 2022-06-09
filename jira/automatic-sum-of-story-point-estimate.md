# Automation - Update `Story point estimate` of parent task when subtask field changes

## User story

* The `Story point estimate` field for a task with subtasks should equal the sum of its subtasks' values for the same field.
* When I change the `Story point estimate` value of a subtask, the same field of the parent task should update so it still equals the sum of the subtask `Story point estimate` fields.
* Ideally, each `story`'s `Story point estimate` value should also be a sum of the same field of its `tasks`, but this seems more complicated because of a [limitation](https://support.atlassian.com/cloud-automation/docs/jira-smart-values-issues/#:~:text=accesses%20the%20details%20of%20a%20subtask's%20parent%20issue.%20can%20only%20be%20used%20when%20the%20active%20issue%20is%20a%20subtask%2C%20and%20can't%20be%20used%20to%20access%20a%20standard%20issue's%20parent%20issue.) of Jira's smart values for issues and because in this project, `tasks/issues` are not `children` of a `story`. They are just `related to` it. Maybe it's better if they have a parent-child relationship, but I'm not sure how many levels this can span.

> `{{issue.parent}}` - Accesses the details of a subtask's parent issue. **Can only be used when the active issue is a subtask, and can't be used to access a standard issue's parent issue.**

## Solution

I made an automation with the following logic (pseudocode):

```js
const targetField = 'Story point estimate'

if (changedValueForField(targetField) && changedFieldBelongsTo(Subtask)) {
    const parent = getParentOf(Subtask)
    parent.setFieldValue(targetField, sumOf(parent.subtasks.targetField))
}
```

### Notes

My project was a `team-managed project` but the [tutorial](https://www.atlassian.com/software/jira/automation-template-library/sum-up-story-points) used `company-managed Jira`, so the name of the fields were different. From relevant [docs](https://support.atlassian.com/cloud-automation/docs/jira-smart-values-issues/#:~:text=%7B%7Bissue.Story%20Points%20estimate%7D%7D%20%2D%20Returns%20the%20issue%27s%20story%20point%20estimate%20(team%2Dmanaged%20Jira%20Software%20Cloud%20only).):

> `{{Story Points}}` - Returns the story points for the issue (**company-managed Jira Software**)
>
> `{{Story point estimate}}` - Returns the story points for the issue (**team-managed Jira Software**)

Here are the changes required to make the tutorial code work in my case:

| Change | Jira Tutorial ❌ | Working Solution ✅ |
| -- | :--: | :--: |
| field watched | `Story Points` | `Story point estimate` |
| issue type monitored | `Sub-task` | `하위 작업` (Sub-task in Korean) |
| field to edit | Select `Story Points` from dropdown | `More options => JSON = {"fields":{"Story point estimate": {{issue.subtasks.Story point estimate.sum}}}}` |

* This [tutorial](https://www.atlassian.com/software/jira/automation-template-library/sum-up-story-points) from the Atlassian template library was helpful, but required some changes to work for my unique situation. Here is an [interactive rule](https://www.atlassian.com/software/jira/automation-template-library/rules#/rule/1381500) from the tutorial.
* Only single-project automations are possible on the Standard version of Jira. The Premium version allows global and multi-project automations. ([Details](https://www.atlassian.com/software/jira/premium))

### Docs

* These [docs](https://www.atlassian.com/software/jira/guides/expand-jira/automation) on Jira Automation cover the basics and link to more useful details.
* [Docs](https://support.atlassian.com/cloud-automation/docs/advanced-field-editing-using-json) for advanced field editing using JSON.
