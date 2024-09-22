---
layout: default
title: Token Authentication for GitHub
nav_exclude: true
# nav_order: 2
last_modified_date: "2024-09-21 02:13AM"
---

# Working with Token Authentication to GitHub

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

This page explains in more depth how to configure `git` to use token authentication, and how to set up a `.git-credentials` file so that your PAT only needs to be stored in one location (and not within each repository's `.git/config` file. This is accomplished by configuring git to use the credential store (a hard-coded local file) instead of the credential cache (which keeps credentials in memory).

## 1. Configuring `git`

Add a credentials configuration to your environment

```
git config --global credential.helper 'store --file ~/.my-credentials'
```

This will insert the following stanza in your `~/.gitconfig` file:

```
[credential]
  helper = store --file ~/.git-credentials
```
    
## 2. Saving your credentials

Notice that configuration points to another file, `~/.git-credentials`. Populate (or add to) that file with the following command. This assumes you have two environment variables available: `$GITHUB_USER` and `$GITHUB_TOKEN`.

```
printf "protocol=https\nhost=github.com\nusername=$GITHUB_USER\npassword=$GITHUB_TOKEN" | git credential-store --file ~/.git-credentials store
```
    
If you cat out that file you will notice a single line for each provider. For GitHub, this will look something like:
    
```
https://USERNAME:PERSONAL_ACCESS_TOKEN@github.com
```

## 3. Using Tokens when cloning

Once the above changes are in place, you can now clone repositories by HTTPS address without inserting your GITHUB_TOKEN or any other value:

```
git clone https://github.com/ACCOUNT/REPO.git
```

> **NOTE:** Do not add or commit the `.git-credentials` file to a repository as it contains a sensitive token value, and
> therefore access to your GitHub account.
