# Working with `git` and GitHub in Data Science

How to set up, configure, and work with `git` and GitHub in the practice of data science.

## What is `git`?

Git is a distributed version control system that tracks changes in any set of computer files, usually used for coordinating work among programmers who are collaboratively developing source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows. <sup>[Wikipedia](https://en.wikipedia.org/wiki/Git)</sup>

## What is GitHub?

GitHub is a developer platform that allows developers to create, store, manage and share their code. It uses Git software, providing the distributed version control of Git plus access control, bug tracking, software feature requests, task management, continuous integration, and wikis for every project. It currently hosts work by approximately 100M developers. <sup>[Wikipedia](https://en.wikipedia.org/wiki/GitHub)</sup>

## Git & GitHub in Data Science

Data aggregation, cleaning, pipelines and ML models all rely on software in order to operate. Responsible software management depends on well-managed code, versioning, prioritizing bugs, features, and user issues. Further, modern platforms and infrastructure tend to favor code-driven tests, builds, deployment, and management.

All of which is to say: Code is fundamental to our work, and it would be both risky and impractical to not use source control.

## Contents

- [**Setup**](docs/setup.md)
  - Install and set up `git`
  - Authenticate `git` to GitHub
  - Basic configuration
  - Troubleshooting
- [**Creating and managing a repository**](docs/creating-repositories.md)
  - Create a repository locally
  - Create a repository in GitHub
  - Adding or removing collaborators
- [**Source control basics**](docs/basics.md)
  - Diff
  - Status
  - Add
  - Commit
  - Push/Pull
  - Fetch
  - Log
- [**Branches, Forks, and Merges**](docs/forks-branches.md)
  - Branches
  - Forks
  - Fetch from Upstream
  - Merges and Pull Requests
- [**Issues**](04-github-issues.md)
- [**Advanced Git/GitHub Features**](docs/advanced.md)
  - Stash
  - Signing commits
  - Reset and Revert
  - Rebase
  - Cherry-pick
  - Renaming `origin`
  - Bonus
- [**GitHub Actions**](docs/github-actions.md)
  - About
  - Credentials & Secrets
  - Example 1 - Build software upon a push
  - Example 2 - Build and deploy a container
- [**Skills Check**](docs/skills.md)
