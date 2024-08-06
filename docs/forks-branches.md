---
layout: default
title: 3 - Forks & Branches
nav_order: 5
---
# Branches Forks & Merges

Git enables software developers to copy an existing codebase and work with the copy alongside the original, without one interfering with the other. 

- The easiest way to copy your entire project code and work with it is called a ["Branch"](#branches).
- The method for copying someone else's project in order to work with is called a ["Fork"](#forks).
- Bringing your changes back into either your project or someone else's is called a ["Merge"](#merges--pull-requests). This function is called a "Pull Request" in GitHub.

## Branches

The default branch of most repositories is called `main`. Many developers do their everyday work adding and committing to the `main` branch. But what if you would like to experiment with a new library, or test out new functionality without disrupting the functionality of the original code? This is what a branch is for.

A new branch is a complete copy of your code that can have an independent life from the branch it was copied from. 

To create a new branch (based on a copy of the branch you are currently using)
```
git branch development
```
To work with the new branch:
```
git checkout development
```
To list all your branches, and indicate which you are currently on (denoted by the `*`)
```
$ git branch
  dev
* main
```

Branches generally end up in one of two possible states:

- The idea / experiment / feature / test that motivated creating the branch in the first place is abandoned and the branch can be deleted. Perhaps the test was unsatisfactory in some way, or impossible to deliver, or otherwise deemed unsuccessful. See [how to delete a branch](#deleting-a-branch) below.
- The new functionality of the branch is considered successful, and you want to fold the new code into the original branch. See [merges & pull requests](merges--pull-requests) below.

### Deleting a branch

To delete a branch:
```
git branch -d <branch-name>
```

## Forks

<img style="width:600px;align:left;" src="https://uvads.github.io/git-basics/assets/images/fork-clone-upstream.png">

A fork is a copy of someone else's repository. This is usually because you do not have access to push changes to the repository, or because the organization that controls it requires all changes come through forks and pull requests.

When you fork a repository, a complete copy is made in your own account (or Organization) in GitHub. This gives you complete control to clone and work with the code freely. You own the forked copy, so you can make additions, new functionality, and commit+push to your own fork.

To create and work with a fork of a repository:

1. Go to the project's page in GitHub that you want to fork.
2. In the upper-right corner of the page, select the "Fork" button.
3. You will be asked where you want the fork to exist, and if you want to rename it.
4. Once copied, you can [clone](01-creating-repositories.md#clone) the repo to your local computer.
5. Make changes, then `git add`, `git commit` and `git push` to your fork.

## Upstream

Repotories that are linked with GitHub already have a remote configuration generally called "origin". This is a reference to the external hosted version of a repository, i.e. the destination when you `git push` or the source when you `git pull`.

To see your remote settings for a specific repository, use the verbose output of the `git remote` command:
```
$ git remote -v

origin  git@github.com:UVADS/git-basics.git (fetch)
origin  git@github.com:UVADS/git-basics.git (push)
```
In this example, `origin` is configured for both pulling and pushing.

## Merges / Pull Requests
