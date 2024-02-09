# Git Basics

This page covers the most essential commands when tracking your code using `git` and GitHub.

1. `git status`
1. `git add`
2. `git commit`
3. `git push`
4. `git pull`

## Status

Running the `git status` command at any point will tell you what untracked files are in your project directory,
or whether you have added changes that need committing, or whether you need to push.

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