---
layout: default
title: 5 - AI Tooling in Git
nav_order: 7
last_modified_date: "2026-10-07 11:13AM"
---

# AI Tooling in Git
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>


## AI Tools - Claude Code / Codex, etc.

AI coding agents such as **Claude Code** and **OpenAI Codex** run in your terminal, inside your project folder. They can read your files and run the same `git` commands you would. You describe what you want in plain language, and the agent works out the commands, runs them, and reports back.

This doesn't replace knowing `git`. The agent will usually show you each command before it runs, and you should understand what you're approving. Think of it as a fast assistant that still needs a supervisor.

{: .warning }
Agents ask for permission before running commands. Read the command before approving it, especially anything with `reset --hard`, `push --force`, `clean`, or `branch -D`. These can permanently delete work.

### 1. Everyday Commands: Add, Commit, Push

The most common use is the routine add / commit / push cycle. The agent can look at what changed, write a sensible commit message, and push.

Example prompts:

- *"What files have I changed since my last commit?"*
- *"Commit my changes to `analysis.py` with a clear message and push."*
- *"Stage everything except the `data/` folder and commit it."*
- *"Write a commit message that describes these changes."*

Behind the scenes the agent runs commands such as `git status`, `git diff`, `git add`, `git commit`, and `git push`. Ask it to show you the diff before committing if you want to check its work.

{: .note }
A good habit is to ask the agent to commit only the files it changed for a given task, rather than `git add .`. This keeps unrelated files, such as notebooks with output or local data, out of your commits.

### 2. Working with Branches

Agents are useful for creating, switching, and cleaning up branches, and for explaining how branches relate to each other.

Example prompts:

- *"Create a new branch called `feature-cleaning` and switch to it."*
- *"What branches exist, and which ones have already been merged into `main`?"*
- *"How far behind `main` is my current branch?"*
- *"Merge `main` into my branch so it's up to date."*
- *"Delete local branches that have already been merged."*

You can also ask questions you would otherwise search for, such as *"What's the difference between merging and rebasing my branch?"* The agent can answer using your actual repository as the example.

### 3. Going Back in Time: Reset, Revert, Restore

Undoing changes is where `git` confuses people most, and where an agent helps the most. Describe the outcome you want, and let the agent pick the right command.

Example prompts:

- *"Undo my last commit but keep the changes in my files."* (`git reset --soft HEAD~1`)
- *"Throw away my uncommitted changes to `model.py`."* (`git restore model.py`)
- *"I already pushed a bad commit. Undo it safely without rewriting history."* (`git revert`)
- *"Show me what `config.yml` looked like three commits ago."*
- *"Restore `notebook.ipynb` to how it was on Monday."*

The agent should know the key rule: **if a commit has already been pushed and others may have pulled it, use `revert`, not `reset`.** If you aren't sure, ask it: *"Is this safe to do on a branch I've already pushed?"*

{: .warning }
`git reset --hard` and `git restore` permanently discard uncommitted work. Before approving them, ask the agent to list exactly what will be lost.

### 4. Resolving Merge Conflicts

A merge conflict happens when two branches change the same lines. Git stops and marks the conflicting sections in the file with `<<<<<<<`, `=======`, and `>>>>>>>`. An agent can read both versions, explain the difference, and propose a combined result.

Example prompts:

- *"I have a merge conflict. Explain what each side changed."*
- *"Resolve the conflict in `train.py`, keeping the new function from my branch and the updated imports from `main`."*
- *"Show me your proposed resolution before you save it."*
- *"Finish the merge once the conflicts are resolved."*

The agent can only guess at intent, so review its resolution. It's often best to ask for an explanation first and decide yourself which changes to keep. After resolving, have it run your tests (if you have them) before completing the merge.

### 5. Watching GitHub Actions Builds and Tests

If your repository uses [**GitHub Actions**](../github-actions/), an agent can check build, test, and deployment results for you, using the GitHub CLI (`gh`) or the GitHub MCP described below. This saves switching to the browser and digging through long logs.

Example prompts:

- *"Did the build for my last push pass?"*
- *"Why did the last Actions run fail?"*
- *"Watch the current run and tell me when it finishes."*
- *"Re-run the failed job."*

When a run fails, the agent can read the log, find the actual error among hundreds of lines, and often suggest or make the fix. It also tells the difference between a problem in your code and a temporary problem on GitHub's side, where simply re-running is the right answer.

{: .note }
To use the `gh` CLI, install it from [cli.github.com](https://cli.github.com/) and sign in once with `gh auth login`.


## GitHub MCP

**MCP** (Model Context Protocol) is a standard way to connect AI agents to outside services. The **GitHub MCP server** gives an agent direct access to GitHub itself: issues, pull requests, repositories, code search, and more. Plain `git` only knows about your local files and commits. The MCP lets the agent work with everything that lives on GitHub's website.

### Setting It Up

GitHub hosts an official MCP server. To connect it to Claude Code, create a [**personal access token**](../token-authentication/) and run:

```
claude mcp add --transport http github https://api.githubcopilot.com/mcp/ \
  -H "Authorization: Bearer YOUR_GITHUB_TOKEN"
```

Other agents, such as Codex, Cursor, and VS Code, have similar settings. See GitHub's setup guide linked at the bottom of this page.

{: .warning }
Your token grants the agent the same access you have. Give it only the permissions it needs, and never commit it to a repository.

### Working with Issues

[**Issues**](../issues/) track bugs, tasks, and ideas. With the MCP, the agent can read and manage them for you.

Example prompts:

- *"List the open issues in this repo labeled `bug`."*
- *"Summarize issue #42 and its comments."*
- *"Create an issue describing the error we just found, with steps to reproduce it."*
- *"Fix issue #42, then comment on the issue explaining what changed."*
- *"Close issues that were fixed by last week's commits."*

The last two are where an agent is most useful: it can read the issue, change the code, and update the issue in one go.

### Working with Pull Requests

Pull requests are how changes get reviewed and merged on GitHub. The agent can handle most of the routine steps.

Example prompts:

- *"Open a pull request from my branch into `main` with a summary of the changes."*
- *"What pull requests are waiting for my review?"*
- *"Review PR #17 and point out any bugs or unclear code."*
- *"Summarize the review comments on my PR and address them."*
- *"Are the checks passing on PR #17?"*
- *"Merge PR #17 if all checks have passed."*

Agent reviews are a helpful first pass, but they don't replace a review from a teammate who knows the project.

### Other Things the MCP Does Well

- **Searching code across GitHub**: *"Find examples of how other repos use `pandas.merge_asof`."*
- **Exploring a repo without cloning it**: *"Explain how the data loading works in `uvads/some-repo`."*
- **Reading files from another repo or branch**: *"Show me the `requirements.txt` in the `dev` branch."*
- **Creating repositories and branches**: *"Create a new private repo called `thesis-analysis`."*
- **Forking**: *"Fork this repo into my account."*
- **Checking history**: *"List the last 10 commits on `main` and who made them."*

### MCP or `gh` CLI?

Both let an agent work with GitHub, and many tasks can be done either way. The MCP gives the agent purpose-built tools for GitHub and works even in agents that can't run terminal commands. The `gh` CLI is often faster to set up if you already use it, and it's especially good for Actions logs. Using both is fine.

{: .success :}
[**GitHub MCP Server setup guide**](https://github.com/github/github-mcp-server)

{: .success :}
[**Claude Code documentation**](https://docs.claude.com/en/docs/claude-code/overview)
