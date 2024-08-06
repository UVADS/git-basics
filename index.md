---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# `git` and GitHub in Data Science
{: .fs-9 }

How to set up, configure, and work with `git` and GitHub.
{: .fs-6 .fw-300 }

[Get started now](docs/setup/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

---

## What is `git`?

> Git is a distributed version control system that tracks changes in any set of computer files, usually used for coordinating work among programmers who are collaboratively developing source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows. <sup>[Wikipedia](https://en.wikipedia.org/wiki/Git)</sup>

## What is GitHub?

> GitHub is a developer platform that allows developers to create, store, manage and share their code. It uses Git software, providing the distributed version control of Git plus access control, bug tracking, software feature requests, task management, continuous integration, and wikis for every project. It currently hosts work by approximately 100M developers. <sup>[Wikipedia](https://en.wikipedia.org/wiki/GitHub)</sup>

## Source Control in Data Science

Data aggregation, cleaning, pipelines and ML models all rely on software in order to operate. Responsible software management depends on well-managed code, versioning, prioritizing bugs, features, and user issues. Further, modern platforms and infrastructure tend to favor code-driven tests, builds, deployment, and management.

Which is to say: Code is fundamental to our work, and it would be risky, inefficient, and impractical not to use source control.

## Contents

- [**Setup**](docs/setup/)
  - Install and set up `git`
  - Authenticate `git` to GitHub
  - Basic configuration
- [**Creating and managing a repository**](docs/creating-repositories/)
  - Create a repository locally
  - Create a repository in GitHub
  - Add or remove collaborators
- [**Source control basics**](docs/git-basics/)
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
- [**Issues**](docs/github-issues/)
- [**Advanced Git/GitHub Features**](docs/git-advanced/)
  - Stash
  - Signing commits
  - Reset and Revert
  - Rebase
  - Cherry-pick
  - Renaming `origin`
  - Bonus
- [**GitHub Actions**](docs/github-actions/)
  - About
  - Credentials & Secrets
  - Example 1 - Build software upon a push
  - Example 2 - Build and deploy a container
