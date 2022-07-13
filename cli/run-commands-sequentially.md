# Run commands sequentially

## User Story

- If I run CLI command `A`, I want to run command `B` immediately when `A` finishes.
- `B` should not start running before `A` finishes.
- Time is money, so the terminal should not sit idle. `B` should run ASAP after `A` finishes.

## Solution: the `&&` operator

Much like in JavaScript, `&&` in `bash` is the 'logical AND' operator. It only executes the right side after the left side evaluates as `true`.

```bash
$ true && echo "This will be output"
This will be output

$ false && echo "This will not be output"
$
```

## A practical use case

This sequence of commands is so common that many devs make an alias for it. The alias includes the `&&` operator.

1. `npm install` runs. This can take a while if you have lots of dependencies or are installing a large package with lots of dependencies.
2. After `npm install` (finally) finishes, `npm start` runs.

```sh
npm install && npm start
```

## References

- This excellent [concise](https://stackoverflow.com/a/4510738/10117759) StackOverflow answer.
- This awesome [very detailed](https://stackoverflow.com/a/30508672/10117759) StackOverflow answer.
