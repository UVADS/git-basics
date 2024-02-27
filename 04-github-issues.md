# GitHub Issues

From GitHub:

> GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.

For data science developers, GitHub Actions offer important ways to trigger workflow steps based on actions that happen in your repository.

Some examples of useful GitHub Actions:

- Automated unit testing
- Container builds and pushes
- Security checks
- Softare builds/compiling
- Deployment of content
- Remote API triggers/notifications

## Basic Concepts

1. Workflows
2. Events
3. Jobs
4. Actions
5. Runners

## How do I set up a GitHub Action?

GitHub Actions use a YAML file to define a workflow according to GitHub's standard schema. This YAML file for a repository is stored within `.github/workflows/` for that repository.

You can author more than one workflow. Each consists of a separate YAML file with its own workflow definition.

