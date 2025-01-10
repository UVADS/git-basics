---
layout: default
title: SSH Authentication for GitHub
nav_exclude: true
# nav_order: 2
last_modified_date: "2024-09-25 02:13AM"
---

# Setting up SSH Authentication for GitHub
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>


This page explains in more depth how to configure `git` to use SSH authentication, and how to clone repositories
using that method.

## 0. Create an SSH Keypair

For users who were using the `cache` credential helper for `git` before switching to the `store`
credential helper, you may need to erase your cache.

In either the Mac OSX terminal (using the `bash` shell), WSL on Windows, or any distro of Linux,
run this command to generate your keys:

```
ssh-keygen
```

## 1. Check the permissions

Your keys will typically be generated and placed in a hidden directory within your home directory named `.ssh`.
Permissions for this directory and the keypair are usually set automatically. But if you get permission errors,
check and verify.

The `~/.ssh` directory should have `700` permissions:

```
chmod 700 ~/.ssh
```

The private key, usually named something like `id_rsa` should have `600` permissions:

```
chmod 600 ~/.ssh/id_rsa
```

The public key, usually ending in `.pub` should have 644 permissions:

```
chmod 644 ~/.ssh/id_rsa.pub
```
    
## 2. Share your public key with GitHub

Cat out the public key and copy its contents to your clipboard:

```
cat ~/.ssh/id_rsa.pub
```
    
Go to your SSH key settings page in GitHub [https://github.com/settings/ssh](https://github.com/settings/ssh).
    
1. Press the "New SSH Key" button.
2. Give your key a name.
3. Keep the "Authentication Key" setting selected.
4. Paste the contents of your public key into the "key" field.
5. Click the "Add SSH Key" button to save and exit.

> NOTE: Only distribute your PUBLIC key to GitHub, never your private key. Keep the private key confidential and do not distribute to anyone else.

## 3. Use SSH keys when cloning

Once the above changes are in place, you can now clone repositories by SSH address, which will look something 
like this:

```
git clone git@github.com:ACCOUNT/REPO.git
```

If you have an existing repository that was cloned with your `$GITHUB_TOKEN` inserted into the URL, or cloned
using SSH, and you would like to update or switch it, you can set the repository URL with this command:
local clone with this command:

```
# Set to use HTTPS
git remote set-url origin https://github.com/ACCOUNT/REPO.git

# Set to use SSH
git remote set-url origin git@github.com:ACCOUNT/REPO.git
```

## Watch how to set up SSH Keys

[![Using SSH keys with GitHub](https://i.ytimg.com/vi/rajlGZ3w4OU/maxresdefault.jpg)](https://www.youtube.com/watch?v=rajlGZ3w4OU)
