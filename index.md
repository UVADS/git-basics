---
layout: default
title: Home
nav_order: 1
description: "Working with git and GitHub in Data Science."
permalink: /
last_modified_date: "2025-05-07 02:13AM"
---

# `git` in Data Science
{: .fs-9 }

Source Control Basics: How to set up, configure, and work with `git` and GitHub.
{: .fs-6 .fw-300 }

[Setting Up](docs/setup/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Basic Commands](docs/basics/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Advanced](docs/advanced/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Actions](docs/github-actions/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Check](docs/skills-check/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

---

<img src="https://uvads.github.io/git-basics/assets/images/git6963.jpg" style="float:right;max-width:40%;" />

## What is Source Control?

Source control, also known as "version control," is the process of tracking changes and versions of electronic files over time. This might include code, data, images, and other files. Good source control management tools allow users to see the entire history of changes to any specific file, or the evolution of an entire project. `git` is currently the most popular and feature-rich source control tool.

## What is `git`?

> Git is a distributed version control system that tracks changes in any set of computer files, usually used for coordinating work among programmers who are collaboratively developing source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows. <sup>[Wikipedia](https://en.wikipedia.org/wiki/Git)</sup>

## What is GitHub? <img src="https://raw.githubusercontent.com/UVADS/git-basics/refs/heads/main/_assets/images/octocat-24.png" />

> GitHub is a developer platform that allows developers to create, store, manage and share their code. It uses Git software, providing the distributed version control of Git plus access control, bug tracking, software feature requests, task management, continuous integration, and wikis for every project. It currently hosts work by approximately 100M developers. <sup>[Wikipedia](https://en.wikipedia.org/wiki/GitHub)</sup>

## Source Control in Data Science

Data aggregation, cleaning, pipelines and ML models all rely on software in order to operate. Responsible software management depends on well-managed code, versioning, prioritizing bugs, features, and user issues. Working at scale, modern platforms and infrastructure tend to require code-driven tests, builds, deployments, and management. Code can be used to define all the layers of effort across teams of engineers and data scientists.

Which is to say: Code is fundamental to our work, and it would be risky, inefficient, and impractical not to use source control.


## Contents

- [**Setup**](docs/setup/)
  - Install and set up `git`
  - Authenticate `git` to GitHub
  - Basic configuration
  - Troubleshooting authentication
  - Key rotation
- [**Creating and managing repositories**](docs/creating-repositories/)
  - Clone
  - Init
  - Fork
  - Delete
  - Managing collaborators
- [**Source control basics**](docs/basics/)
  - Diff
  - Status
  - Add
  - Commit
  - Push/Pull
  - Fetch
  - Log
- [**Branches, Forks, and Merges**](docs/forks-branches/)
  - Branches
  - Forks
  - Fetch from Upstream
  - Merges and Pull Requests
  - Partial Merges
- [**Advanced Git/GitHub Features**](docs/advanced/)
  - Tag
  - Stash
  - Signing commits
  - Resets and reverting
  - Rebase
  - Cherry-pick
  - Rename `origin`
  - Changing from SSH to Token Authentication
  - Alias Commands
  - `gh` - the GitHub CLI
  - Bonus - So You Think You Know Git
- [**Issues**](docs/issues/)
- [**GitHub Actions**](docs/github-actions/)
  - Use Cases for Data Science
  - Credentials & Secrets
  - Example 1 - Perform tests against your code
  - Example 2 - Run a container against the repository contents with every push
  - Example 3 - Build and push a container with all new tagged releases
- [**Skills Check**](docs/skills-check/)
