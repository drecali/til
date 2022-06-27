# `[GitHub Actions]` - Conditionally run CI action if commit message has --flag

## User Story

- If a CI (continuous integration) action takes a long time, I want it to run only in specific user-defined situations.
- I don't want to trigger the action manually from the GitHub website. I want an easier way.
- I like how CLI tools use `--flags` to change their behavior.

## Solution

The action will automatically run if both conditions are met:

- The trigger for the action was detected.
- If the last commit message has a specific `--flag` defined by the user, much like CLI tools.

The steps to accomplish this are:

- Detect the trigger condition for the action
- Get the last commit message
- if the last commit message has the `--flag`, run the action.

## Real-world background info & caveats

This problem and solution were related to end-to-end tests, which usually take a relatively long time to run, because they're simulating actual user behavior. Against my wishes, the team wanted to severely limit how often we ran e2e tests. Though I wasn't again of the idea, we compromised on running e2e tests if the `--t` flag is present on the last commit message.

This action assumes that team members will always remember to add the `--t` flag to their commit message when they want to run the tests. In practice, we forgot to do this quite a bit, which defeated the purpose of regularly running e2e tests when they would be most useful. Ideally they should run regularly to catch bugs before they go to `production`.

```yaml
name: conditionally-run-e2e-tests-on-successful-deployment
on: [deployment] # any trigger you want if it's associated with a GitHub commit or pull that has a 'SHA'

# skipped some setup steps for this example

jobs:
  conditional-e2e-tests:

# skipped some setup steps for this job

    steps:
    - name: Get last commit message
        id: msg # use this to refer to the variable output from this step
        run: |
        MSG=$(git log --format=%B -n 1 ${{ github.event.deployment.sha }})
        echo "::set-output name=COMMIT_MESSAGE::${MSG}"
        echo "$MSG"

    - name: Run action if last commit msg has '--t' flag
        if: contains( steps.msg.outputs.COMMIT_MESSAGE, '--t') # referring to the COMMIT_MESSAGE variable output by the step with ID = `msg`.

        # actual action to run
```

For this line:

```bash
# 1️⃣ |--------- 2️⃣ ------------|--------------- 3️⃣ ---------------|
MSG=$(git log --format=%B -n 1 ${{ github.event.deployment.sha }})
```

Here is the equivalent JS pseudocode:

```js
//--- 1️⃣ --|--------- 2️⃣ -------|--- 3️⃣ ---|
const MSG = getGitCommitMessage(commitSha);
```

- 3️⃣ `${{ github.event.deployment.sha }}` - gets the `sha` value of the commit that triggered the deployment
- 2️⃣ `git log --format=%B -n 1 ${{ github.event.deployment.sha }}` - gets the commit message for the commit with the `sha` value determined in the previous step. See [`git log` docs](https://git-scm.com/docs/git-log) for more info.
- 1️⃣ `MSG=$()` - Sets the variable `MSG` equal to the value of the commit message from the previous step.

The line:

```bash
echo "::set-output name=COMMIT_MESSAGE::${MSG}"
```

[Sets a new output variable](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-an-output-parameter) for this step. The variable name is `COMMIT_MESSAGE` and its value is `$MSG` (the last commit message).

The `if` condition:

```dart
//- 🅰️ --|-------------- 🅱️ ---------------|- 🅾️ -|
contains( steps.msg.outputs.COMMIT_MESSAGE, '--t')
```

is equivalent to this JS pseudocode:

```js
/*
🅱️ |-- 🅰️ --| 🅾️ | */
s1.substring(s2);
```

- 🅱️ - `steps.msg.outputs.COMMIT_MESSAGE` gets the value of the `COMMIT_MESSAGE` [output variable](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#example-setting-a-value) of the `msg` step.
- `contains(s1, s2)` returns `true` if the string `s1` contains the substring `s2`. In this case, we check if the last commit message contains `--t`.
