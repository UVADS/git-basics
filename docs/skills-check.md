---
layout: default
title: 7 - Skills Check
nav_order: 9
last_modified_date: "2025-05-06 02:13AM"
---

# Skills Check
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>

Test your grasp of git and GitHub by using the following checks. Each level assumes a grasp of all
previous levels. How far can you get?

## Novice

1. Create a `git` repository in GitHub. [[Review]](../creating-repositories/#creating-new-repositories)
2. Create a `git` repository using the command-line. [[Review]](../creating-repositories/#init)
3. Set up SSH key authentication to GitHub [[Review]](../ssh-authentication/)
4. Clone a GitHub repository to your local computer. [[Review]](../creating-repositories/#clone)
5. Perform simple `git add` / `commit` / `push` / `pull` operations. [[Review]](../basics/)
6. Display `git` status at any time in your repository. [[Review]](../basics/#status)

## Advanced Beginner

1. List the branches in your local repository. [[Review]](../forks-branches/#branches)
2. Create and switch to a new branch in your local repository. [[Review]](../forks-branches/#creating-a-branch)
3. Make changes then add/commit/push the new branch back to GitHub. [[Review]](../basics/)
4. Merge a branch into `main`. [[Review]](../forks-branches/#merge)
5. Delete a local branch. [[Review]](../forks-branches/#deleting-a-branch)
6. Display the `git log` for your repository. [[Review]](../basics/#log)
7. Use `git diff` to inspect changes made to a file. [[Review]](../basics/#diff)

## Competent

1. Fork a repository that you do not own. [[Review]](../forks-branches/#forks)
2. Clone the fork you just created. [[Review]](../creating-repositories/#clone)
3. Configure an `upstream` remote so that you can synchronize your fork with any changes in the original repo. [[Review]](../forks-branches/#upstream)
4. Fetch and merge from `upstream`. [[Review]](../basics/#fetch)
5. Be familiar with how to smooth out a simple (1 file) MERGE conflict. [[Review]](../forks-branches/#merge-conflicts-aka-merge-hell)
6. Know how to pull in a file from another branch into your current branch. [[Review]](../forks-branches/#partial-merges)

## Proficient

1. Use `git stash` properly to save state without committing. [[Review]](../advanced/#stash)
2. Restore a stash to resume working. [[Review]](../advanced/#viewing-recovering-or-applying-a-stash)
3. Tag a commit and push it to GitHub. [[Review]](../advanced/#tag)
4. List all tags for a repository. [[Review]](../advanced/#tag)
5. Move the repository back one commit. [[Review]](../advanced/#resets-and-reverting)
5. Change the name of a repository in GitHub and manually update the address in `.git/config`. [[Review]](../creating-repositories/#renaming-repositories)
6. Submit a Pull Request so that your changes can be merged upstream into the original repository. [[Review]](../forks-branches/#pull-requests)

## Expert

1. Create a `git alias` by editing `~/.gitconfig` [[Review]](../advanced/#alias-commands)
2. Set up a GitHub Action to automatically build or test your software. [[Review]](../github-actions/)
3. Customize this Action so that it only runs on a specific branch, or only if it contains a tag. [[Review]](../github-actions/#example-3---build-and-push-a-container-with-all-new-tagged-releases)
4. Work with repository or GitHub Organization secrets to pass sensitive information into Actions. [[Review]](../github-actions/#credentials--secrets)
4. Understand the difference between `rebase`, `reset`, and `revert`. [[Review]](../advanced/#resets-and-reverting)
5. Create a `release` in GitHub. [[Review]](../advanced/#releases)
6. Set up Actions to respond to Issue types in GitHub.
7. Understand `submodule` in `git`. [[Learn More]](https://github.blog/open-source/git/working-with-submodules/)

## Jedi

No Instructions Given - you're on your own!

1. Install the `gh` CLI and open or close an Issue with it.
2. Create a GitHub Action that relies on a "remote dispatch" call to another repository.
3. Write a script that both creates a repository in GH and clones it to your local machine.
4. Use the [GitHub API](https://docs.github.com/en/rest) to grant access to another user for one of your repositories.
5. Create a GitHub Pages site and publish your own GH site. (Hint: this site runs that way!)
6. Create a Pull Request template for a repo, which asks for specific information from anyone submitting a PR.
