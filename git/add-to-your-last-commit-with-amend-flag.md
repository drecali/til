# Add to your last commit with the `--amend` flag

## 🚨 WARNING: only do this if you didn't `push` your last commit 🚨

If you `committed` but didn't `push` yet, you can use the command below to add your staged changes to the last commit without changing the commit message:

```bash
$git commit --amend --no-edit
```

It's great if you forgot to include one small change in your last commit before `pushing`.

But be careful, if you already pushed your commit, you should avoid using `--amend` because it will change the commit history and you will need to `force push` to the remote repository.

I highly recommend the Atlassian guide in the references because it includes a lot more detail, examples, and illustrations.

## References

- [Atlassian: Git commit `--amend` and other methods of rewriting history](https://www.atlassian.com/git/tutorials/rewriting-history)
