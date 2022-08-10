# `[CI]` - Always upload videos and screenshots

Cypress records videos by default when using the `run` command, regardless of test pass or fail status.

People may be tempted to upload the videos only in case of failure. Why waste space for video that's not necessary?

I think there's still a lot of value in videos of successful runs. I can think of 4 main benefits right now:

- Provides a baseline to illustrate correct app behavior.
- Can compare app behavior/performance before and after a larger change.
- Can be used later to confirm assumptions that a successful test run means the app looked and behaved perfectly and did not have other aberrations in behavior, UI, or data.
- Can capture other changes in behavior, UI, or data that don't affect test outcome, but may be relevant to another investigation. A Cypress test run video is like a time capsule. A quick reference of the state of the app at that point in time. In some cases it can be quicker (especially for less technical people) to download the video than to checkout a specific commit, run it locally, and reproduce the relevant state/behavior.

Thankfully, Cypress test videos are not that large and storage space is relatively cheap. For an fairly comprehensive test run of about 6 minutes, the videos are 68MB. Given the negligible cost, I think it's best to keep videos.

Here's one way to upload artifacts in GitHub Actions regardless of test outcome. It uses this [action](https://github.com/actions/upload-artifact).

```yml
- name: Upload Cypress artifacts 💾
  uses: actions/upload-artifact@v2
  ## The condition below may seem overly aggressive, but is necessary to cover all types of Cypress step failures (Cypress tests are the previous step)
  if: steps.tests.outcome == 'success' || steps.tests.outcome == 'failure' || failure()
  with:
    # I think this is the most useful human-readable name for the artifacts file.
    # The sort nicely alphabetically in the file system, which makes it easier to find them and track which run produced them.
    # artifacts_WORKFLOW_NAME#RUN-ATTEMPT_OUTCOME
    # artifacts_workflow-name#557-1_success
    # artifacts_workflow-name#793-2_failure
    name: artifacts_${{ steps.github-context.outputs.WORKFLOW_NAME }}#${{ steps.github-context.outputs.RUN_NUMBER }}-${{ steps.github-context.outputs.RUN_ATTEMPT }}_${{ steps.tests.outcome }}
    path: |
      cypress/screenshots/
      cypress/videos/
```

## References

- Cypress Docs re: [artifacts](https://docs.cypress.io/guides/guides/screenshots-and-videos)
