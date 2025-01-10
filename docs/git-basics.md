---
layout: default
title: 2 - Git Basics
nav_order: 4
last_modified_date: "2024-08-20 02:13AM"
---

# Git Basics
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>


This page covers the most essential commands when tracking your code using `git` and GitHub.

## Diff

Git was designed to track changes made to files and their location within a project. `git diff` is one of the best ways to see how things have actually changed. `git diff` is a function that takes two input data sets and outputs the changes between them.

For example, imagine that you have cleaned up your code a bit, added some new functionality, and inserted more comments inline. But you step away from your desk (or go to sleep or it's suddenly the weekend) and you need a reminder of what changes have been made to file before you add and commit it? `git diff` can tell you.

A command like this:
```
git diff filename.py
```
will show you a detailed inventory of inserted lines (which start with `+` and are highlighted in blue), deleted lines (which start with `-` and are highlighted in red) for the entire file.

Or if you need to compare the structure of two directories:
```
git diff dir1 dir2
```

Or if you need to compare the changes between two commits:
```
git diff 6a63 d726
```

Or if you need to compare the last commit with the current state (before commits):
```
git diff a0ea0 .
```


## Status

Running the `git status` command at any point will tell you what untracked files are in your project directory, or whether you have added changes that need committing, or whether you need to push.

For example, the command below shows that a file has been modified but not yet staged for commit:
```
$ git status

On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   02-git-basics.md

no changes added to commit (use "git add" and/or "git commit -a")
```


## Add

The `git add` command stages your file(s) to be committed. Instead of thinking of "add" as simply adding new files
or changes, think of "add" as adding your changes (new files, edited files, deleted files) to `git` for tracking.

You can specify individual files to be staged for commit:
```
git add README.md
git add my_script.py
git add one_script.py config.json requirements.txt
```

Or you can add everything recursively within the current directory:
```
git add .
```

Extending the example from above, here is the output from `git add .`:
```
$ git add .

On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   02-git-basics.md
```


## Commit

The most important action in `git` is the **commit**. Commits are permanent, irrevocable transactions that snapshot
an entire codebase at a specific moment in time. Remember that the idea of source control is that users can always see
the history of all changes to any file within a project, over time. Even users who are new to an existing project can look
back into the entire history of commits for a repository.

To commit your staged (added) changes, use the `git commit` command with the `-m "Message..."` flag. Every commit requires 
a meaningful, plainspoken message describing the commit.

```
git commit -m "Added new numpy parameter for verbose logging"
```

### How often should I commit my changes?

As a general rule, commit every time you make an important change - whether that is an addition, modification, or deletion. If you are cleaning up syntax or comments across several files, that could be folded into a single commit. But the addition of a new method or class probably counts as a big enough change to be its own commit.

The point is to avoid a single, end-of-the-day commit with 50 unrelated changes. If your commit represents changes made in one file (for example) it is possible to check out a previous version of that file in case you would like to roll back. More about that is in the advanced topics page.

### Writing good commit messages

The practice of writing quality commit messages is important even for the solo developer. How else can you or a teammate
easily pinpoint important changes to a file or entire project? It is important to remember not to err on the side of either (a) overly-brief or repetitive comments, or (b) overly-long narrative commentary that will never be read.

> Getting in the habit of creating quality commit messages makes using and collaborating with Git a lot easier. As a general rule, your messages should start with a single line that’s no more than about 50 characters and that describes the changeset concisely, followed by a blank line, followed by a more detailed explanation. The Git project requires that the more detailed explanation include your motivation for the change and contrast its implementation with previous behavior — this is a good guideline to follow. Write your commit message in the imperative: "Fix bug" and not "Fixed bug" or "Fixes bug." <sup>[git-scm.com](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)</sup>

## Push / Pull

The actions above have all happened on the local workstation, without really interacting with a remote origin such as GitHub. Pushing and Pulling are the steps to synchronize your local changes with the remote origin.

### `git push`

To push your local changes "up" to GitHub issue this command:
```
git push origin main
```

The use of `origin` in this command is a reference to a remote git endpoint (i.e. a hosted service such as GitHub, Bitbucket, etc.) and `main` is the branch you want to push. Note that `origin` can actually be renamed, though it's become the common moniker for any hosted git service.

### `git pull`

To pull the most recent version of the repository from GitHub to your local computer, use the same syntax with the `pull` command:
```
git pull origin main
```
Where `origin` is a reference to the remote endpoint and `main` is the name of the branch you want to synchronize.

### How often should I push or pull?

For solo developers who are not working in a team/collaboration, one or two pushes per day should be fine. While GitHub is not a backup service per se, it is always wise to have an external copy of your important work offsite. Hard drives die, and data can get corrupted.

For collaboration settings, a good rule of thumb for how frequently to `git push` is to push every time an important change to the code has been made. And you should `git pull` at the start of each day of work, and before you begin working on a new or file you have not touched earlier in the day.

Ultimately, good team communication matters the most in this environment.

### Why doesn't `git` synchronize automatically like Dropbox?

Since changes to code happen over time and require effort to get to a working state, the `git` model depends upon developers having their own sense for when code is ready to be committed and added to source control. Put another way, you don't want half-completed code shipping into the rest of your project.

## Fetch

The `git fetch` command downloads the latest changes from a remote repository, but it doesn't merge those changes into your local working directory. This means that you can see what changes have been made to the remote repository without having to merge them into your own work.

Fetch is a relatively "harmless" command since it does not modify or delete anything. You can never fetch too often, and the advantage is that it lets you see all remote changes before you commit or merge.

How is `fetch` different from `pull`? Pulling updates the HEAD of your repository with the changes from the remote repository. So it both pulls down new data/changes but also integrates them with your copy of the repository. 

> **What does HEAD mean?** `HEAD` is the name for the current version of the repository, the most recent commit. Notice in the section below, the top-most (i.e. most recent) commit will also be aliased as `HEAD`.

## Log

Since `git` was built to track changes, returning a log of all commits is simple. The default output is verbose and each entry takes several lines:

```
$ git log
commit 6a6357bd9f27663e093ef8b08ed8a1cff6d3685d (HEAD -> main, origin/main, origin/HEAD)
Author: Data Student <mst3k@virginia.edu>
Date:   Wed Feb 28 10:01:24 2024 -0500

    Extending the advanced page

commit 1c552497f2b80100a0256d2b9bfd36895acca260
Author: Data Student <mst3k@virginia.edu>
Date:   Tue Feb 27 10:23:34 2024 -0500

    Typos abound. Adding second new section.

commit 7c271f203df3a9eaab9e2cb6081a4ebda029dfdb
Author: Data Student <mst3k@virginia.edu>
Date:   Tue Feb 27 10:22:13 2024 -0500

    Clearer sections in the TOC.
```

Notice that at least four data points are returned for each commit:

- The commit SHA or hash identifier
- The commit author and email
- The commit date and time
- The commit message


{: .note }
When referencing other commits you do not need to use the entire hash. Usually the first 4-5 characters are enough, so long as they can be differentiated from any other commits. Notice in the log output below even git itself truncates commit hashes to six characters.

The git log can be displayed and manipulated. One useful flag is `--online`:
```
$ git log --oneline
6a6357b (HEAD -> main, origin/main, origin/HEAD) Extending the advanced page
1c55249 Typos abound. Adding second new section.
7c271f2 Clearer sectioning in the TOC.
9200074 Tracking - more content and adding 4-5-6 pages
8c0e746 Update 03-forks-branches.md
c98492b Width of image
dd1ea8e Update 03-forks-branches.md
b835f2f Adding image and upstream
dc97b96 TOC on page 3
```

Even more informative, you can log with a graph output, showing commits across all branches:

```
$ git log --oneline --graph --decorate --all
* 9bccb364 (origin/staging) Updated ANSYS docs and scripts
| *   66027815 (HEAD -> main, origin/main, origin/HEAD) Merge pull request #506 from uvarc/staging
| |\  
| |/  
|/|   
* | 0832e6ee timestamp message
* | ad6834d7 lammps slurm
* | 1f8beb43 lammps cpu and gpu
* | 6c7137d3 Changed Gurobi page to reflect latest version
| *   cfaf53cc Merge pull request #505 from uvarc/staging
| |\  
| |/  
|/|   
* | 9663a4be Pushing changes to people
| *   60d037e2 Merge pull request #504 from uvarc/staging
| |\  
| |/  
|/|   
* | 79c0c50e status page update and timestamps
```
