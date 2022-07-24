# Checkout a specific commit

If you need to go back in time to a very specific point in a repo's history, Git enables time travel very nicely with the `checkout` command. This is really useful for troubleshooting a specific working version of the app, or going back in time when a certain bug was present.

The `checkout` command changes all the contents of your local project directory to a specified state, like the most recent commit on a different branch, or a specific commit on any branch.

It's most frequently used to switch between different branches. In this case, we will change the local directory contents to a specific commit.

The syntax is simple:

```
git checkout <commitSha>
```

In case you didn't know what the `commitSha` is, it's an alphanumeric 'id' of the commit. It's 40 characters long. For example: `73f33074ada943eb5faf3cb3b5bc11059bda30a8`. One way to see it is with the `git log` command.

On GitHub you can see the first 7 characters, so `73f3307`. This is called the partial hash. The partial hash for a `git` command can be as short as 4 characters if it's distinct from other repo commits' partial hashes.

<img width="871" alt="image" src="https://user-images.githubusercontent.com/24983797/180633614-1d9ed640-79bc-4def-a6e8-00e13a966ea6.png">

The partial hash is enough for the `checkout` command. So you could do `git checkout 73f3307` to check out that specific commit.

## ⚠️ Caution!

Checking out a specific commit is is not like checking out a branch. If you want to make some changes in reference to that commit, it's best to create a new branch in reference to that commit, or else you may lose your progress. Here is an excellent explainer from [GitTower](https://www.git-tower.com/learn/git/faq/git-checkout-commits).

> The HEAD pointer in Git determines your current working revision (and thereby the files that are placed in your project's working directory). Normally, when checking out a branch, Git automatically moves the HEAD pointer along when you create new commits: you're automatically and always on the newest commit of the chosen branch.
>
> When you instead choose to check out a specific commit hash, Git will NOT do this for you. This means that when you make changes and commit them, these changes do NOT belong to any branch.
> The consequence is that these changes can easily get lost once you check out a different revision or branch: not being recorded in the context of a branch, you lack the possibility to access that state easily.
>
> To make a long story short: be very careful when checking out a specific commit instead of a branch (and make sure this is really what you want and need).

## Create a branch from a specific commit

To create a branch from a specific commit, use the `git branch` command.

```
git branch <branchName> [<commit-id>]
```

This creates a new branch, `branchName` whose head points to specified `commit-id`. For example, the following creates a develop branch from the specified commit hash.

```
git branch newBranch 73f33074ada943eb5faf3cb3b5bc11059bda30a8
```

This creates a new branch `newBranch` whose head points to commit `73f33074ada943eb5faf3cb3b5bc11059bda30a8`.

## References

- [TechieDelight - create branch from previous commit](https://www.techiedelight.com/create-branch-from-previous-commit-git/)
