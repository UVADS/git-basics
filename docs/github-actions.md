---
layout: default
title: 6 - GitHub Actions
nav_order: 8
last_modified_date: "2024-08-20 02:13AM"
---

# GitHub Actions
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>

GitHub Actions is a continuous integration and continuous delivery (CI/CD) service provided by GitHub. It allows developers to automate various tasks and workflows within their repositories. With GitHub Actions, you can define custom workflows using YAML files that specify the sequence of steps to be executed when certain events occur, such as code pushes, pull requests, or releases. 

These workflows can include tasks like:

- building code
- testing code / unit tests
- building containers
- deploying applications
- notifying team members about failures/errors
- triggering remote integrations / APIs

GitHub Actions helps streamline the development process by automating repetitive tasks, improving collaboration, and ensuring consistent and reliable code deployments.

GitHub Actions is highly customizable and integrates seamlessly with other GitHub features and third-party tools. It provides a wide range of pre-built actions and workflows in the GitHub Marketplace, making it easy for developers to adopt and extend existing configurations.

{: .success :}
> [**Learn More about GitHub Actions**](https://github.com/features/actions)

## Use Cases for Data Science

Data Scientists tend to build reusable scripts and components to be assembled in various pipelines. Such pipelines might ingest and clean data, or

Think of Actions as a programmable process to check for accuracy or errors, to build or stage software, to launch pipelines, etc. Actions may contain if/then logic, multiple simultaneous processes, they may reach out to external data sources, other git repositories, or APIs.

In the examples below, notice that the Action is defined in a YAML file. Multiple action definitions may exist for a single repository, and may be defined to run in parallel, or in a specific order.

We suggest adopting Actions first with simple use cases and then building toward longer and more complex workflows.


## Credentials & Secrets

GitHub Actions often require credentials in order to do some of their work. Consider, for example, a container that is built by an Action that needs to be pushed to Docker Hub. This push requires credentials in order to authenticate to Docker Hub.

For this reason, GitHub provides a secret management store where credentials, keys, and other confidential information can be kept within a GitHub repository, account, or organization for use by Actions but not visible to other users.

To access Secrets for a repository:

1. Go to the main page of the repository
2. Select "Settings"
3. On the lefthand navigation find "Secrets and Variables"
4. Select "Actions"
5. Create a new repository or organization secret. Each consists of a key-value pair similar to an `env` variable.


## Example 1 - Perform tests against your code

This GitHub Action tests your code for basic errors using [`pytest`](https://docs.pytest.org/en/stable/) against multiple versions of Python. This requires you write the appropriate test file(s) to demonstrate success/failure in your application.

In industry, it is **extremely common** to run production code through dozens or even hundreds of various tests before it is released. While Data Science does not generally impact production systems, it is to no one's advantage to release broken, buggy code in this setting.

> `.github/workflows/python-version-testing.yaml`

```
{% raw %}
name: Python Testing

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        # Test against multiple versions of Python
        python-version: ["3.9", "3.10", "3.11", "3.12"]

    steps:
      - uses: actions/checkout@v4
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
      # Install packages you need for the testing
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      # Finally run a test unit using pytest / ruff / tox, etc.
      - name: Test with pytest
        run: |
          pip install pytest pytest-cov
          pytest tests.py --doctest-modules --junitxml=junit/test-results.xml --cov=com --cov-report=xml --cov-report=html
{% endraw %}
```

{: .success }
Learn more about [**Building and Testing in Python**](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python) using GitHub Actions.


## Example 2 - Run a container against the repository contents with every push

This example passes the branch name and several other secrets into a container, which clones the repository branch and performs a build against the code.

{: .note }
Note this action runs on pushes to the `main` and `staging` branches, but also runs on a schedule at 8:00AM UTC each day.

> `.github/workflows/build.yaml`

```
{% raw %}
name: Build CI

on:
  push:
    branches:
    - 'main'
    - 'staging'
  schedule:
    - cron: '0 8 * * *'

jobs:
  Build:
    runs-on: ubuntu-latest
    steps:
    - uses: nelonoel/branch-name@v1
      env:
        ACTIONS_ALLOW_UNSECURE_COMMANDS: true
    - run: echo ${BRANCH_NAME}
    - name: Set ENV vars
      env:
        BUCKET_NAME: ${{ secrets.BUCKET_NAME }}
        BUCKET_NAME_STAGING: ${{ secrets.BUCKET_NAME_STAGING }}
        DISTRIBUTION_ID: ${{ secrets.DISTRIBUTION_ID }}
        STAGING_DISTRIBUTION_ID: ${{ secrets.STAGING_DISTRIBUTION_ID }}
        MAX_AGE: ${{ secrets.MAX_AGE }}
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      run: echo $BUCKET_NAME
    - name: Get HUGO container
      run: docker pull ghcr.io/uvarc/hugo-build:v2
    - name: Run HUGO container
      run: docker run -e BRANCH=$BRANCH_NAME -e DISTRIBUTION_ID=${{ secrets.DISTRIBUTION_ID }} -e BUCKET_NAME_STAGING=${{ secrets.BUCKET_NAME_STAGING }} -e STAGING_DISTRIBUTION_ID=${{ secrets.STAGING_DISTRIBUTION_ID }} -e AWS_ACCESS_KEY_ID=${{ secrets.AWS_ACCESS_KEY_ID }} -e AWS_SECRET_ACCESS_KEY=${{ secrets.AWS_SECRET_ACCESS_KEY }} -e MAX_AGE=${{ secrets.MAX_AGE}} ghcr.io/uvarc/hugo-build:v2 /root/build-site.sh uvarc/rc-website hugo-0.80.0-ext
{% endraw %}
```

## Example 3 - Build and push a container with all new tagged releases

This GitHub Action detects any tagged push (matching the format `*.*`, i.e. 1.4, 13.9, 989.14, etc.) and performs a multi-architecture container build and push for both amd64 and arm64 platforms.

{: .note }
Note at the end the Action performs a "Remote Dispatch" where it updates a separate repository with a new value, which in turn triggers a deployment from that repository.

> `.github/workflows/deploy.yaml`

```
{% raw %}
name: Container Build CICD

on:
  push:
    tags: ['*.*']

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: uvarc/id-generator
  SVC_NAME: idGenerator

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set ENV
        run: echo "IMAGE_TAG=${GITHUB_REF#refs/*/}" >> $GITHUB_ENV

      - name: Set up QEMU
        uses: docker/setup-qemu-action@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ secrets.GHCR_USERNAME }}
          password: ${{ secrets.GHCR_PAT }}

      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          platforms: linux/amd64,linux/arm64
          tags: ghcr.io/${{ env.IMAGE_NAME }}:${{ env.IMAGE_TAG }}
          labels: ${{ steps.meta.outputs.labels }}

      - name: Image digest
        run: echo ${{ steps.docker_build.outputs.digest }}

      # Update another repo so that Kubernetes deploys the new version.
      - name: Remote Dispatch
        run: |
          curl -X POST https://api.github.com/repos/uvarc/uvarc-services/dispatches \
            -H 'Accept: application/vnd.github.everest-preview+json' \
            -H "Authorization: token ${{ secrets.GHCR_PAT }}" \
            --data '{"event_type": "${{ env.IMAGE_NAME }} update to ${{ env.IMAGE_TAG }}", "client_payload": { "service": "${{ env.SVC_NAME }}", "version": "${{ env.IMAGE_TAG }}" }}'
{% endraw %}
```
