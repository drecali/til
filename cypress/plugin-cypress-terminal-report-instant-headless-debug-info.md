# `[Plugin]` - `cypress-terminal-report` for instant headless debug info

## Background 

A test spec is a file with multiple tests. Sometimes they can contain a lot of tests and can take a few minutes to complete. 

Unfortunately, if a test fails, Cypress does not output any information about the failure while the spec is running. If the first test in the spec failed, you won't know anything about the failure unless you wait for the spec to finish. If you cancel the run before that, you won't get any feedback in the terminal 😢

In my opinion, that's a bad developer experience. Sometimes the failure has a simple cause and debugging can begin while the spec is running in the background. There's no use wasting that time. It's best to strike while the iron is hot.

## User Story

- When a test fails, I want to know ASAP so I can start debugging immediately.

## Solution

A dev with that exact problem created [`cypress-terminal-report`](https://github.com/archfz/cypress-terminal-report). As soon as the failed test finishes, it outputs the failed test's entire log to the terminal, and it's nicely formatted.

It has a bunch of options to customize the behavior. It can even output all the logs for all the tests, but that may be overkill.

It's a great plugin and easy to set up. It's great for CI or local runs! What are you waiting for?

| Before | After |
|--|--|
| <img width="827" alt="image" src="https://user-images.githubusercontent.com/24983797/180014273-4ab96254-3be1-47f7-af61-a749bcb5c3b1.png"> | <img width="827" alt="image" src="https://user-images.githubusercontent.com/24983797/180014347-92da2b73-eb92-472b-a1c0-e92b2d535b90.png">
 |

