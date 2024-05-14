---
layout: default
title: GitHub Actions
nav_order: 8
---

# GitHub Actions

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

> [**Learn More about GitHub Actions**](https://github.com/features/actions)

## Credentials & Secrets

GitHub Actions often require credentials in order to do some of their work. Consider, for example, a container that is built by an Action that needs to be pushed to Docker Hub. This push requires credentials in order to authenticate to Docker Hub.

For this reason, GitHub provides a secret management store where credentials, keys, and other confidential information can be kept within a GitHub repository, account, or organization for use by Actions but not visible to other users.

To access Secrets for a repository:

1. Go to the main page of the repository
2. Select "Settings"
3. On the lefthand navigation find "Secrets and Variables"
4. Select "Actions"
5. Create a new repository or organization secret. Each consists of a key-value pair similar to an `env` variable.


## Example 1 - Run a container against the repository contents with every push

This example passes the branch name and several other secrets into a container, which clones the repository branch and performs a build against the code.

Note it runs on pushes to `main` and `staging`, but also runs on a schedule at 8:00AM UTC each day.

> .github/workflows/build.yaml

```
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
```

## Example 2 - Build and push a container with all new tagged releases

This GitHub Action detects any tagged push (matching the format `*.*`, i.e. 1.4, 13.9, etc.) and performs a multi-architecture container build and push for both amd64 and arm64 platforms.

Note at the end the Action performs a "Remote Dispatch" where it updates an external repository to set a new value, which in turn triggers a deployment.

> .github/workflows/deploy.yaml

```
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
```