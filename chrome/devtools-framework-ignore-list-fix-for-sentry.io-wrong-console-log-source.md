# `[DevTools]` - Framework Ignore List - Fix for Sentry.io wrong console log source

## Background

Messages in the Chrome console always show their `source`: the exact file and line of code that triggered the message is shown on the right side of the console panel (for LTR languages at least). The format is `filename.extension:line#`

![image](https://user-images.githubusercontent.com/24983797/177786463-2335c89d-f689-4427-9126-6590556c6b97.png)

If you're investigating something, you may log a few different messages to the console. It's nice not having to also include information about the message `source`. It's easy to take that basic feature for granted.

Until you install [Sentry.io](https://sentry.io). 😅

Sentry is a very useful tool that captures all errors and user behavior, network logs, console logs, etc. It's great for troubleshooting.

Except it eats your `console.log` statements and poops them out of its own `source` file. That's right: you've lost access that basic feature you took for granted. Now you won't know the true `source` of any of your messages. Here's an example below. The `console.log()` actually came from `saga.ts:25` but is being misreported as coming from `instrument.ts:124`. This is a Sentry file with the path `http://localhost:3000/node_modules/@sentry/instrument.ts`.

![old](https://user-images.githubusercontent.com/24983797/177777426-f3ece7b6-e96f-4599-a42c-3c4988f50290.png)

## Authorized solution from Sentry

> ❗️ [Click Here](#a-slightly-better-idea) for a solution that seems more elegant.

The solution recommended in the [Sentry docs](https://docs.sentry.io/platforms/javascript/guides/react/troubleshooting/#instrumentjs-line-numbers-for-console-log-statements) is to add `/@sentry/` to Chrome's `Framework Ignore List`.

> If `instrument.js` displays in your console while debugging, add Sentry to your framework [blackboxing\*](#questions) settings like: `/@sentry/` so Chrome ignores the SDK stackframes when debugging.

## Instructions

1. Open Dev Tools. If you're messing around with Sentry you should already know how. If not, see my [keyboard shortcuts](keyboard-shortcuts-high-roi.md#:~:text=W-,Open%20dev%20tools,-%E2%8C%98) for Mac and Windows.
1. Open the Dev Tool Settings.

   ![image](https://user-images.githubusercontent.com/24983797/177766992-a1b11391-2250-49af-9509-92787e111924.png)

1. Select the `Ignore List` option.

   ![image](https://user-images.githubusercontent.com/24983797/177768325-eb3823f3-7c04-49c8-b7b7-aca4c16dcb88.png)

1. Click the <kbd>Add pattern...</kbd>

   ![image](https://user-images.githubusercontent.com/24983797/177768864-4adbcdfe-7cff-47a2-b100-c8a46e7d944a.png)

1. Add `/@sentry/` **OR** the wrong Sentry `source` filename listed in the console. In my case that was `instrument.ts`.
1. Celebrate that Sentry decided to allow you to get your precious console message `source`info back 🎉

   ![new](https://user-images.githubusercontent.com/24983797/177777528-d5eee7a3-d101-482a-a454-e2f63958764c.png)

## Questions

Since I'm new to Sentry and the `Ignore List` feature, I don't know if this fix has any caveats. It came from Sentry's docs so it should be legit. But the docs page it came from is using the old term `Blackboxing` instead of `Ignore List`. Their link to the Chrome Dev Docs is broken but has a [cached version](https://web.archive.org/web/20150322015741/https://developer.chrome.com/devtools/docs/blackboxing) from 2015, thanks to the Wayback Machine. I could only find this `Ignore List` [stub](https://developer.chrome.com/docs/devtools/javascript/ignore-chrome-extension-scripts/) on the Chrome Devs Docs.

## The Downside

```bash
# This solution has to be manually implemented on each browser of each machine used for development 😥
```

The solution seems like a blunt instrument. It may cause you to miss **all** Sentry console messages even if they're important.

## A slightly better idea?

According to this GitHub issue [comment](https://github.com/getsentry/sentry-react-native/issues/794#issuecomment-672280790), adding `instrument.ts` to the `Ignore List` also works. I prefer this method because it seems like a more targeted approach than ignoring the **entire** Sentry framework.

Still, it seems like a bit of a hack because I'm not familiar with `instrument.ts`, its role, and any caveats. It does seem like it would have fewer downsides than a blanket block of the entire framework but unfortunately, I don't have time to investigate now, so 🤷‍♂️

## Next Steps?

In the `sentry-react-native` repo issue [#794](https://github.com/getsentry/sentry-react-native/issues/794) suggests other options that might work, but those could be specific to the React Native version.
