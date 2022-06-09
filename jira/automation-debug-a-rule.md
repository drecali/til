# Debug an automation rule

1. Check the audit log
    * Sometimes errors can provide useful information.
1. Debugging smart values
    * Use the `Log` action
        * This adds the values to the audit log, but requires adding an additional component to the rule.
    * Use the `debug` function
        * Surrounding a smart action with `debug` processes the smart value as usual and also prints its value to the audit log as a `Debug message`.
        * Example: `{{#debug}}{{#=}}1 + 1{{/}}{{/}}` prints the following in the audit log:

            ```sh
            Debug message
            2
            ```

    * Make testing easy & clean
        * Copy the rule and disable the original before testing so there's a backup of the original rule.
        * Use the `Manual` trigger (Jira only) to execute a rule from an issue at any time. The `Scheduled` trigger is also useful for testing.
        * When testing an action that enters a value, use the smart value `{{now}}` to include the current time. This shows when the edit was made and if the value changed.

## Source

* Jira Docs for [Debug an automation rule](https://support.atlassian.com/cloud-automation/docs/debug-an-automation-rule/)
