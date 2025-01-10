---
layout: default
title: Token Authentication for GitHub
nav_exclude: true
# nav_order: 2
last_modified_date: "2024-09-23 02:13AM"
---

# Setting up Token Authentication for GitHub
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>


This page explains in more depth how to configure `git` to use token authentication, and how to set up a `.git-credentials` file so that your PAT only needs to be stored in one location (and not within each repository's `.git/config` file. This is accomplished by configuring git to use the credential store (a hard-coded local file) instead of the credential cache (which keeps credentials in memory).

> Pre-requisite: Create a GitHub [**Personal Access Token (PAT)**](https://github.com/settings/tokens).

## 0. Clear Existing Cached Credentials

For users who were using the `cache` credential helper for `git` before switching to the `store`
credential helper, you may need to erase your cache.

For MacOSX users, enter the following three lines, then hit return twice:

```
git credential-osxkeychain erase
host=github.com
protocol=https


```

For Windows users, open the Windows **Credential Manager** control panel, then select Windows Credentials
and remove any entries for GitHub.


## 1. Configure `git` credential helper store

Add a credentials configuration to your environment

```
git config --global credential.helper 'store --file ~/.git-credentials'
```

This will insert the following stanza in your `~/.gitconfig` file:

```
[credential]
  helper = store --file ~/.git-credentials
```
    
## 2. Store your credentials

Notice that configuration points to another file, `~/.git-credentials`. Populate (or add to) that file with the following command. This assumes you have two environment variables available: `$GITHUB_USER` and `$GITHUB_TOKEN`.

```
export GITHUB_USER="myuser"
export GITHUB_TOKEN="gph_TtOoKkEeNn12345"
printf "protocol=https\nhost=github.com\nusername=$GITHUB_USER\npassword=$GITHUB_TOKEN" | git credential-store --file ~/.git-credentials store
```
    
If you cat out that file you will notice a single line for each provider. For GitHub, this will look something like:
    
```
https://USERNAME:PERSONAL_ACCESS_TOKEN@github.com
```

## 3. Use Tokens when cloning

Once the above changes are in place, you can now clone repositories by HTTPS address without inserting your GITHUB_TOKEN or any other value:

```
git clone https://github.com/ACCOUNT/REPO.git
```

If you have an existing repository that was cloned with your `$GITHUB_TOKEN` inserted into the URL, or cloned
using SSH, and you would like to update it, copy the HTTPS URL again from your repository and update your
local clone with this command:

```
git remote set-url origin https://github.com/ACCOUNT/REPO.git
```

> **NOTE:** Never add or commit the `.git-credentials` file to a repository as it contains a sensitive token value, and
> therefore access to your GitHub account.

## Watch how to set up a PAT

[![Using a Personal Access Token with GitHub](https://i.ytimg.com/vi/C4R2mMx6C-k/maxresdefault.jpg)](https://www.youtube.com/embed/C4R2mMx6C-k?si=UPknm4ygzhenNrRN)
