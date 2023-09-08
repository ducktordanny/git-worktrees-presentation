# Git Worktrees Presentation

> Get to know git worktree: What is it? What to use it for? Why is it great?

## Introduction, and the problem

See the [link](https://ducktordanny.github.io/git-worktrees-presentation/) in the About section of the GitHub repo.

## Demo

1. Clone bare repository:

```sh
git clone --bare git@github.com:ducktordanny/git-worktrees-presentation.git
cd git-worktrees-presentation.git
```

2. Because we fetch the bare repo, check:

```sh
git config --get remote.origin.fetch
```

If this does not return anything, or it doesn't return "+refs/heads/*:refs/remotes/origin/*", then:

```sh
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
```

Why is this needed? Well git clone --bare does two things:

- it makes a bare repository that has no work-tree and does no initial checkout
- it changes the default fetch refspec from +refs/heads/*:refs/remotes/origin/* to +refs/heads/*:refs/heads/*

So we have to set it manually. Otherwise, fetch and pull might not work when you want to access new changes.

3. Create working trees

E.g.:

```sh
git worktree add feature-1
git worktree add review-stuff
git worktree add random
```

Then it will create the "feature-1", "review-stuff" and "random" folders, each having its own repo files, and we can easily just cd into them and out of them.

- Navigate inside "feature-1", start to implement your feature.
- While there is something that you have to check in another branch for your coworker, just leave everything as it is and `cd` into the "random" folder, and then checkout the needed branch from there.
- After you finished, just `cd` back and continue.
