# `[Error]` - src refspec main does not match any. error: failed to push some refs to 'github.com...'

This Git error message is kind of confusing but the solution is quite simple.

```
error: src refspec main does not match any
error: failed to push some refs to 'github.com:gitAccountName/repoName.git'
```

It happened after creating a new repository and using the `git push -u origin main` command.

There can be other reasons for this, but the simplest one is that you were distracted while creating the new repository and tried to `push` without `commit`ing anything.

StackOverflow is great! [These answers](https://stackoverflow.com/questions/4181861/message-src-refspec-master-does-not-match-any-when-pushing-commits-in-git) show that a lot of people caused this error themselves by being distracted. The good news is the fix was super easy. Just make some changes to the repo, then `add` and `commit` 🚀

And try not to be so distracted next time 🤣
